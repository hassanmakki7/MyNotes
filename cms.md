# Exceptional Bug in 5 minutes at @intigriti


**About myself:**  
My Name is Md Mahfujur Rahman, and my username is [mahfujwhh](https://twitter.com/mahfujwhh) . I am a Bug bounty Hunter.

**lets’s start**

**Today I will discuss about a Execptional bug which is I got just 5 minutes at** [**@intigriti**](http://twitter.com/intigriti)**.**

Our target is suppose target.com. I start enumeration subdomain and start Fuzzing main domain target.com, Then I collect all of subdomain and collect Urls using waybackurls.Then I run the urls in nuclei.

I visit my target site and open wapplyzer extension and i can see in this site used drupal cms.

![](https://miro.medium.com/v2/resize:fit:547/1*WxZtvn8oT-GP25Jv2GTR-A.png)

In this sccreenshot you can see CMS is drupal

**What is Drupal used for?**

Drupal is a free, Open Source content management system (CMS) to build and maintain websites, online directories, e-commerce stores, intranets and other types of digital content. It can be used by individuals or groups of users and is a useful CMS for developers, marketers and agencies.

Sometimes ago, I run nuclei with my all urls which i found waybackurls. When I visit nuclei and scrool down it show me info and provide me a endpoint :

**/core/install.php**

previously I found this type of endpoint many times but when I open the endpoint I see the drupal or wordpress is installed like this:

![](https://miro.medium.com/v2/resize:fit:700/1*nPKgLecDfyJskfSWOr1HRw.png)

when drupal is installed alredy

But in this case, Surprisely I see that Drupal is not installed here. The page look like-

![](https://miro.medium.com/v2/resize:fit:700/1*0VamzqMHXVrKYD3SV6tc_Q.png)

when drupal is not installed

After finding this I reported it at intrigriti and then they take the vulnerbility as **expectional**.

![](https://miro.medium.com/v2/resize:fit:700/1*6fBakmc-uHv9rAnuWBkI5Q.png)

**Why this simple issue is Expectional??**  
In this site Drupal is not installed and I can insatll Drupal and Takeover the site easily. After I configure and installed Drupal I can logged in as **Administrator**. Right!

**If I logged in as administrator and I can able to upload reverse-shell and The result is RCE.**

That’s why this issue is **Exectional**

**you can follow me:**  
[https://twitter.com/mahfujwhh](https://twitter.com/mahfujwhh)  
[https://www.linkedin.com/in/mahfujwhh/](https://www.linkedin.com/in/mahfujwhh/)

[https://buymeacoffee.com/mahfujwhh6](https://buymeacoffee.com/mahfujwhh6)

Thanks

