
## List

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Reconnaissance/Google%20Dorks.md#list)

- inurl:example.com intitle:"index of"
- inurl:example.com intitle:"index of /" "*key.pem"
- inurl:example.com ext:log
- inurl:example.com intitle:"index of" ext:sql|xls|xml|json|csv
- inurl:example.com "MYSQL_ROOT_PASSWORD:" ext:env OR ext:yml -git
- inurl:example.com intitle:"index of" "config.db"
- inurl:example.com allintext:"API_SECRET*" ext:env | ext:yml
- inurl:example.com intext:admin ext:sql inurl:admin
- inurl:example.com allintext:username,password filetype:log site:example.com "-----BEGIN RSA PRIVATE KEY-----" - inurl:id_rsa
- site:codepad.co "keyword"
- site:scribd.com "keyword"
- site:npmjs.com "keyword"
- site:npm-runkit.com "keyword"
- site:libraries.io "keyword"
- site:ycombinator.io "keyword"
- site:coggle.it "keyword"
- site:papaly.com "keyword"
- site:google.com "keyword"
- site:trello.com "keyword"
- site:prezi.com "keyword"
- site:jsdelivr.net "keyword"
- site:codepen.io "keyword"
- site:codeshare.io "keyword"
- site:sharecode.io "keyword"
- site:pastebin.com "keyword"
- site:repl.it "keyword"
- site:productforums.google.com "keyword"
- site:gitter.im "keyword"
- site:bitbucket.org "keyword"
- site:*atlassian.net "keyword"
- inurl:gitlab "keyword"
- inurl:github "keyword"

