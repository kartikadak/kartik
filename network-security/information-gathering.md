# Information Gathering

The Information gathering phase is focused on two essential aspects of all targets: 

1. Business
2. Infrastructure.

The Business side of information gathering deals with collecting information regarding the type of business, its stakeholders, assets, products, services, employees and generally non-technical information.

 The organization will probably operate its business purpose through an Infrastructure such as networks, systems, domains, IP addresses and so on.

![](../.gitbook/assets/image%20%282%29.png)

The information gathering can be classified in two main disciplines:

1. Passive
2. Active

Passive or OSINT \(Open Source INTelligence\) information gathering is gathering as much information about our target \(network, system...\) without exposing our presence. In this phase we not only try to gather information such as web presence, partners, financial info, and physical plants but also, infrastructure related information using publicly available resources \(accessible by anyone\).

Active information gathering techniques interact directly with the target system. In this phase, we will gather information about ports, services, running systems, net blocks and so on. In general, active techniques can reveal the investigation to the organization through IDS or servers logs so caution should be taken to prevent this.

![](../.gitbook/assets/image%20%2882%29.png)

**Search engines**

![](../.gitbook/assets/image%20%2888%29.png)

Web Presence

In this phase, you will learn a great deal more about your target including:

* What they do
* What is their business purpose
* Physical and logical locations
* Employees and departments
* Email and contact information
* Alternative web sites and sub-domains
* Press releases, news, comments, opinions

Jot down all the information in you mind mapping tool

![](../.gitbook/assets/image%20%2883%29.png)

-&gt; Next step is to use Google dorks

![](../.gitbook/assets/image%20%2885%29.png)

![](../.gitbook/assets/image%20%2880%29.png)

For more details

* [https://support.google.com/websearch/answer/136861?hl=e](https://support.google.com/websearch/answer/136861?hl=e)
* [www.googleguide.com/advanced\_operators\_reference.html](http://www.googleguide.com/advanced_operators_reference.html)
* [http://pdf.textfiles.com/security/googlehackers.pdf](http://pdf.textfiles.com/security/googlehackers.pdf) 
* [https://www.exploit-db.com/google-hacking-database/](https://www.exploit-db.com/google-hacking-database/)

You can also change search engines to get more information.

![](../.gitbook/assets/image%20%2887%29.png)

**Partners and third parties**

Other useful information that you can gather about the company are mergers and acquisitions, partnerships, third parties... With these you can deduce what type of technologies and systems they use internally. You can take advantage of this information in later phases of the pen test. You can also use it to perform a more effective social engineering attack with a higher chance of success.

![](../.gitbook/assets/image%20%2889%29.png)

From these web pages, you can gather information such as the technology stack the organization uses \(hardware and software\), tools, systems and so on

**Job Posting**

This might not seem like harmful information however, an investigator can deduce internal hierarchies, vacancies, projects, responsibilities, weak departments, financed projects, technology implementations and more.

![](../.gitbook/assets/image%20%2878%29.png)

![](../.gitbook/assets/image%20%2884%29.png)

**Financial**

More useful information can be acquired from financial details about the organization. For example, you can easily find out if the organization:

* is going to invest in a specific technology 
* might be subject to a possible merge with another organization
* has critical assets and business services

We can use CrunchBase, inc.com, google finance, yahoo finance to view the information.

**Harvesting**

In this phase, we unpack methods for gathering company documents such as charts \(detailing the corporate structure\), database files, diagrams, papers, documentation, spreadsheets and so on. ****Moreover, this is the right time to begin harvesting emails, accounts \(Twitter, Facebook, etc.\), names, roles and more.

It is important to know that when a document is created, it automatically stores information \(metadata\) like who created it, date and time of creation, software used, computer name and so on. If we are able to retrieve documents online and inspect the underlying metadata, we can extract useful information.

You can use theharvester to hunt these information.

**Cached and archival sites**

Since information on the web changes so quickly, sometimes seeking an older version of a site could prove useful to our cause. Consider a job post. If the organization deletes it from the website, you will “lose” that information; if you could see the web page, before the update, you could harvest that information. Turns out this is entirely possible through cache and archival technology.

![](../.gitbook/assets/image%20%2881%29.png)

You can also use google dork such as cache:URL

Social Media

In this particular phase, social media is useful in the following ways: • Learn about corporate culture, hierarchies, business processes, technologies, applications. • To build a network map of people \(relationships\). • Select the most appropriate target for a social engineering attack.

![](../.gitbook/assets/image%20%2879%29.png)

Why is building a network of people important? Social engineering \(among the other things\) is the art of exploiting trust relationships. If your target is Bob and you know that Bob trusts Adam therefore, you can get to Bob through Adam. Figuring out this trust relationship is an important part of the information gathering process.

![](../.gitbook/assets/image%20%2890%29.png)

![](../.gitbook/assets/image%20%2891%29.png)





