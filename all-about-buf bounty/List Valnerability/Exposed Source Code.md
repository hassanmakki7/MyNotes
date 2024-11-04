
## Introduction

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Exposed%20Source%20Code.md#introduction)

Source code intended to be kept server-side can sometimes end up being disclosed to users. Such code may contain sensitive information such as database passwords and secret keys, which may help malicious users formulate attacks against the application.

## Where to find

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Exposed%20Source%20Code.md#where-to-find)

`-`

## How to exploit

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Exposed%20Source%20Code.md#how-to-exploit)

1. Exposed Git folder

```
https://site.com/.git
```

[![GIT folder](https://camo.githubusercontent.com/834fd16c5579a2b14d518067908c1ab54ddc0e63424dc5951149175c02933b62/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d77545a4f75554c61714e772f586c6949396a53307733492f41414141414141414154412f565a787337564c355043593846646e6f4b61456a5336415770636a6f4a7a344d67434c63424741735948512f73313630302f312e706e67)](https://camo.githubusercontent.com/834fd16c5579a2b14d518067908c1ab54ddc0e63424dc5951149175c02933b62/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d77545a4f75554c61714e772f586c6949396a53307733492f41414141414141414154412f565a787337564c355043593846646e6f4b61456a5336415770636a6f4a7a344d67434c63424741735948512f73313630302f312e706e67)

Tools to dump .git

- [https://github.com/arthaud/git-dumper](https://github.com/arthaud/git-dumper)

2. Exposed Subversion folder

```
https://site.com/.svn
```

[![SVN folder](https://camo.githubusercontent.com/734e9c824eb1cdfcf7920945656a02e882b5e191acf8ddc13a3ad04ee50b21d4/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d3562435f4568465368676b2f586c694a71697738704a492f41414141414141414154492f3248687258304561334d77513630417832747a4e70724e76756c676750725a4141434c63424741735948512f73313630302f312e706e67)](https://camo.githubusercontent.com/734e9c824eb1cdfcf7920945656a02e882b5e191acf8ddc13a3ad04ee50b21d4/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d3562435f4568465368676b2f586c694a71697738704a492f41414141414141414154492f3248687258304561334d77513630417832747a4e70724e76756c676750725a4141434c63424741735948512f73313630302f312e706e67)

Tools to dump .svn

- [https://github.com/anantshri/svn-extractor](https://github.com/anantshri/svn-extractor)

3. Exposed Mercurial folder

```
https://site.com/.hg
```

[![HG folder](https://camo.githubusercontent.com/4a9de31110a9379fa29f120c1216221605d9cdca5a97e8dc77b10429bf6ddb92/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d344661715565546c76346b2f586c694b48424f70676d492f41414141414141414154512f734c6477687653462d4a676e30574635502d506f754c70367554654855414f5741434c63424741735948512f73313630302f312e706e67)](https://camo.githubusercontent.com/4a9de31110a9379fa29f120c1216221605d9cdca5a97e8dc77b10429bf6ddb92/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d344661715565546c76346b2f586c694b48424f70676d492f41414141414141414154512f734c6477687653462d4a676e30574635502d506f754c70367554654855414f5741434c63424741735948512f73313630302f312e706e67)

Tools to dump .hg

- [https://github.com/arthaud/hg-dumper](https://github.com/arthaud/hg-dumper)

4. Exposed Bazaar folder

```
http://target.com/.bzr
```

[![BZR folder](https://camo.githubusercontent.com/6f8c0b4ee2d4d7d6d085e99bde0f25506fd7137d1404237dc19d65ba68839269/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d3637574f5f6b4c5f6942382f586c694b6c316a676741492f41414141414141414154632f6d57427737696771303545644b52334a5a6d6258594e344c716a70424f72455367434c63424741735948512f73313630302f312e706e67)](https://camo.githubusercontent.com/6f8c0b4ee2d4d7d6d085e99bde0f25506fd7137d1404237dc19d65ba68839269/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d3637574f5f6b4c5f6942382f586c694b6c316a676741492f41414141414141414154632f6d57427737696771303545644b52334a5a6d6258594e344c716a70424f72455367434c63424741735948512f73313630302f312e706e67)

Tools to dump .bzr

- [https://github.com/shpik-kr/bzr_dumper](https://github.com/shpik-kr/bzr_dumper)

5. Exposed Darcs folder

```
http://target.com/_darcs
```

Tools to dump _darcs (Not found)

6. Exposed Bitkeeper folder

```
http://target.com/Bitkeeper
```

Tools to dump BitKeeper (Not found)

## Reference

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Exposed%20Source%20Code.md#reference)

- [NakanoSec (my own post)](https://www.nakanosec.com/2020/02/exposed-source-code-pada-website.html)


