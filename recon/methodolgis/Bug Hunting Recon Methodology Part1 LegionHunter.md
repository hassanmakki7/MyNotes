
Welcome fellow hackers and security enthusiasts! I’m Abhirup Konwar, known in the bug hunting space as [_LegionHunter_](https://youtube.com/@legionhunter)

This is Part 1 of the live bug hunting youtube [series](https://www.youtube.com/playlist?list=PLqOQy6wxttBhnTjURDZU-WKnW-NmuBk-P) , hope you will enjoy this detailed article.

# **Recursive Subdomain Enumeration🔍🔍**

subfinder -d domain.com -all -recursive > subs_domain.com.txt

- `-d domain.com`: Specifies the target domain.
- `-all`: Uses all available sources for subdomain discovery. Subfinder integrates with multiple data sources such as ThreatCrowd, VirusTotal, Censys, etc., and using `-all` ensures you're casting a wide net.
- `-recursive`: Allows recursive subdomain discovery. This digs deeper into subdomains and checks for more subdomains within the already found subdomains.

# **Filtering live hosts with httpx🚨**

cat subs_domain.com.txt | httpx -td -title -sc -ip > httpx_domain.com.txt  
cat httpx_domain.com.txt | awk '{print $1}' > live_subs_domain.com.txt

- `-td`: Technology Detection
- `-title`: Extracts the HTML `<title>` from the response for each subdomain. This is useful for identifying what services might be running on each host.
- `-sc`: Prints the HTTP status code, making it easy to spot potential points of interest like 200 (OK) or 403 (Forbidden).
- `-ip`: Displays the IP address for each subdomain.

# **Nuclei Automated Live Subdomains Spray (with rate limit)🔨**

nuclei -l live_subs_domain.com.txt -rl 10 -bs 2 -c 2 -as -silent -s critical,high,medium

- `-l live_subs_domain.com.txt`: Specifies the input file containing the live subdomains.
- `-rl 10`: Limits the rate of requests to 10 per second. This is essential to avoid overwhelming the target server, which could lead to rate-limiting or even being blocked.
- `-bs 2`: maximum number of hosts to be analyzed in parallel per template(default is 25)
- `-c 2`: maximum number of templates to be executed in parallel (default is 25)
- `-as`: Automatic web scan using wappalyzer technology detection to tags mapping
- `-silent`: Removes extra output from the terminal, leaving only critical information.
- `-s critical,high,medium`: Tells Nuclei to scan only for critical, high, and medium severity vulnerabilities, which helps you focus on the most important findings

These nuclei options are important as it helps to rate limit the number of requests thrown to the server at every second, which will help upto some extent to prevent from getting blocked easily and unresponsive target skipped problems of nuclei.

# **Finding WAF (web application firewall)👮‍♂️**

cat httpx_domain.com.txt | grep 403

One quick way to identify the presence of Web Application Firewalls (WAFs) is to look for subdomains returning a `403 Forbidden` status code. WAFs are often configured to block unauthorized access, and spotting multiple `403` responses can indicate that a WAF is protecting the target.

Some of the common WAFs used by reputed companies are

Amazon Cloudfront  
Cloudflare  
Imperva  
Akamai kona site defender  
F5 Advanced WAF  
Barracuda Web Application Firewall  
Fortinet FortiWeb  
Microsoft Azure Web Application Firewall  
Radware AppWall  
Sucuri WAF

# **Subdomains without WAF✅**

After identifying live subdomains and their corresponding WAFs, the next step is to filter out subdomains that aren’t protected by a Web Application Firewall (WAF). This helps focus on potentially weaker targets.

cat httpx_domain.com.txt | grep -v -i -E 'cloudfront|imperva|cloudflare' > nowaf_subs_domain.com.txt

# **Visit All Non-WAF Subdomains Manually**

Next, you can visit these subdomains manually to look for interesting responses. For example, a `403 Forbidden` response may suggest the existence of restricted areas or resources that could be valuable to investigate further. In some cases, you might encounter endpoints where you have a strong suspicion of what could be hidden behind the restriction, making them prime targets for deeper exploration

cat nowaf_subs_domain.com.txt | grep 403 | awk '{print $1}'

To streamline this process, I recommend using a browser extension like [**Open Multiple URLs**](https://chromewebstore.google.com/detail/open-multiple-urls/oifijhaokejakekmnjmphonojcfkpbbh?hl=en&pli=1), which lets you open several subdomains simultaneously in different tabs for quicker manual investigation.

# **Prepare the List of 403 Subdomains for Fuzzing**

Once you’ve identified subdomains returning a `403 Forbidden` response, prepare them for further fuzzing. Fuzzing can help uncover hidden files, directories, or misconfigurations.

cat nowaf_subs_domain.com.txt | grep 403 | awk '{print $1}' > 403_subs_domain.com.txt

# **403 Fuzzing🔍**

When you encounter a `403 Forbidden` response, it usually means that access to a specific resource or endpoint is restricted. While it might seem like a dead end at first, this restriction can actually signal that valuable information is being protected—whether it's sensitive files, hidden directories, or misconfigured security rules.Here’s why fuzzing these `403 Forbidden` subdomains is crucial.

_Default Wordlist Fuzzing_

dirsearch -u https://sub.domain.com -x 403,404,500,400,502,503,429 --random-agent

_Extension based Fuzzing_

dirsearch -u https://sub.domain.com -e xml,json,sql,db,log,yml,yaml,bak,txt,tar.gz,zip -x 403,404,500,400,502,503,429 --random-agent

One of the good wordlists resource is below.

[

## Index of /data/

### automated/ 28-Jul-2024 13:04 - kiterunner/ 28-Apr-2023 13:14 - manual/ 28-Apr-2023 13:14 - technologies/ 28-May-2024…

wordlists-cdn.assetnote.io







](https://wordlists-cdn.assetnote.io/data/?source=post_page-----975b7bbe3231--------------------------------)

![](https://miro.medium.com/v2/resize:fit:700/1*IDnCMhYRTMZZPBrwvHeWfw.png)

# **Finding Public Exploits💣**

After identifying potential vulnerabilities in a specific subdomain, the next step is to search for public exploits that could be leveraged. For example, if you discover a vulnerable version of Apache Tomcat, use Google dorks to search for exploit proof-of-concept (PoC) scripts:

apache tomcat 9.0.82 exploit poc site:github.com

Would suggest to watch the complete video why we are searching for apache tomcat exploits here!

# **Chatgpt exploit assistance🤖**

![](https://miro.medium.com/v2/resize:fit:700/1*t3iwtMPai85Dfdtc6PVw0w.png)

# **Finding Appropriate Wordlists📗**

When fuzzing specific services like Apache Tomcat, using targeted wordlists can significantly improve your chances of finding hidden vulnerabilities. You can search for wordlists specific to the server you’re targeting, such as Apache Tomcat, with the following commands:

sudo apt install seclists  
cd /usr/share/seclists/Discovery/Web-Content  
ls | grep -i apache

To see how many entries are in a specific wordlist, run:

cat ApacheTomcat.fuzz.txt | wc -l

# **Apache Tomcat Fuzzing🐱**

Once you’ve found the appropriate wordlist, use it to fuzz the Apache Tomcat server for hidden files, misconfigurations, or vulnerable endpoints:

dirsearch -u https://sub2.sub1.domain.com -x 403,404,500,400,502,503,429 -w /usr/share/seclists/Discovery/Web-Content/ApacheTomcat.fuzz.txt

# **Extension Based Fuzzing**

Fuzzing for different file extensions can help uncover sensitive files like backups, configuration files, or database dumps. Use dirsearch for this purpose as well:

dirsearch -u https://sub2.sub1.domain.com -x 403,404,500,400,502,503,429 -e xml,json,sql,db,log,yml,yaml,bak,txt,tar.gz,zip -w /usr/share/seclists/Discovery/Web-Content/ApacheTomcat.fuzz.txt

# **Finding Hidden Database Files💎**

Another valuable source of information is hidden database files. You can search for wordlists that specifically target database file extensions using Google dorks or community-sourced wordlists.

![](https://miro.medium.com/v2/resize:fit:700/1*FRsomGYxG80qzw6NitsKYQ.png)

mkdir db_wordlists  
cd db_wordlists  
wget https://raw.githubusercontent.com/dkcyberz/Harpy/refs/heads/main/Hidden/database.txt

dirsearch -u https://sub2.sub1.domain.com -x 403,404,500,400,502,503,429 -e xml,json,sql,db,log,yml,yaml,bak,txt,tar.gz,zip -w /path/to/wordlists/database.txt

This is just the beginning! Stay tuned for **Part 2**, where I’ll dive deeper into recon techniques and live demonstrations. Make sure to follow my YouTube channel, where I’ll be posting walkthroughs and live bug hunting sessions to help you level up your skills.

# ☕ Enjoyed this article?

If you find any bugs using my articles and videos and found it to be helpful to you, I would greatly appreciate your support! Your contributions enable me to continue sharing detailed knowledge and improving my work in cybersecurity.

[

## Abhirup Konwar

### If you find any bugs using my articles and videos and found it to be helpful to you, I would greatly appreciate your…

buymeacoffee.com



](https://buymeacoffee.com/legionhunter?source=post_page-----975b7bbe3231--------------------------------)

