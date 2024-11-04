```
  sudomy -d domain.com -dP -eP -rS -cF -pS -tO -gW --httpx --dnsprobe  -aI webanalyze --slack -sS
```

```
./sudomy -d ngesec.id -dP -eP -rS -cF -pS -tO -gW --httpx --dnsprobe --graph  -aI webanalyze --slack -sS
```


1111aaaa@@@@AAAA

```
./sudomy -d bugcrowd.com -dP -eP -rS -cF -pS -tO -gW --httpx --dnsprobe  -aI webanalyze -sS
```

# collect ips from ASN 


whois -h whois.radb.net -- '-i origin AS1449' | grep -Eo "([0-9.]+){4}/[0-9]+" | uniq | mapcidr -silent | httpx


In the first step of this command, it obtains the information of the ASN’s owner and extracts the CIDRs from the `whois` command output using the `grep` command. It then removes any duplicates and passes the result to [Mapcidr](https://github.com/projectdiscovery/mapcidr) for mapping and IP conversion. The final step in the pipeline is to perform service discovery using `httpx`. You can also specify ports for `httpx`.

The easiest way to do this flow is to use Shodan with this search query:

```
asn:AS123
```

It follows almost the same flow for us, but the CLI method is much more complete because it’s possible that a service has gone live for a new IP and Shodan hasn’t yet found it (hasn’t yet sent a request to it).






Starting content discovery using [ffuf](https://github.com/ffuf/ffuf), a directory such as `/administrator/login/index.php` was found, which provided the administrator login panel. How the web directory was structured provided the idea to perform content discovery **after** the web directory `/administrator/`. As the web application was using PHP, the following **ffuf** command was used along with [raft-small-words.txt](https://github.com/danielmiessler/SecLists/blob/master/Discovery/Web-Content/raft-small-words.txt) wordlist:

- `ffuf -c -ac -w raft-small-words.txt -u https://sub.domain.ca/administrator/FUZZ -e php`


# shodan 

shodan domain -D pypal.com -S
 gzip -d *.gz 
jq -cs '.[0]' paypal.com.json
jq -cs '.[1]' paypal.com.json
jq -cs .'[3]' paypal.com-hosts.json 
jq -cs .'[3]' paypal.com-hosts.json | jq -r
jq -r '.domains' paypal.com-hosts.json
jq -r '.hostnames' paypal.com-hosts.json
jq -r '.ip_str' paypal.com-hosts.json
jq -r '.ip_str' paypal.com-hosts.json | httpx -title -port 443,80,8080,8000 | nuclie
shodan search org:\"paypal\" --fields ip_str,port,http,title
shodan search org:\"paypal\" \!port:80,443  --fields ip_str,port,http,title
shodan search org:\"paypal\" \!port:80,443  --fields ip_str,port | awk '{print $1,$2}' | tr " " ":"
shodan search org:\"paypal\" \!port:80,443  --fields ip_str,port | awk '{print $1,$2}' | tr " " ":" |nuclie

 shodan search org:\"paypal\" \!port:80,443  --fields ip_str,port | awk '{print $1,$2}' | tr " " ":" | httpx
 shodan search ssl:paypal.com   --fields ip_str,port | awk '{print $1,$2}' | tr " " ":" |httpx
 shodan search asn:AS1449 --fields hostnames | tr ";" "\n" | sort -u | domainparser | sort -u
censys search hackerone.com | grep "ip" | egrep -v "description" | cut -d ":" -f2 | tr -d \"\,
uncover -q "hackerone.com" -e censys,fofa,shodan,shodan-idb | httpx