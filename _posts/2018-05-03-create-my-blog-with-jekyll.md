---
layout: post
title: "Jekyll Build Static Blog"
date: 2018-05-03 13:27:00
categories: jekyll
tags: jekyll RubyGems
mathjax: true
---

* content
{:toc}

From the first blog I applied from Baidu in 2008, 10 years have passed. I cannot adapt to the Baidu space v2.0, so I move my articles to the CSDN. In this period, I had tried the WordPress, but it is very complicated to apply for space and verify it. And now I find a good solution in Github Pages: [https://643435675.github.io/2015/02/15/create-my-blog-with-jekyll/](https://643435675.github.io/2015/02/15/create-my-blog-with-jekyll/)

This website is built from his template, Thank you very much for HyG! Here are some introductions from this website.

## Build

Follow the tutorial of jekyll on the website:[http://jekyllrb.com/](http://jekyllrb.com/)




### install Ruby

Ruby download：[https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/)

set the environment variation(path), and test it like:

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue0e393vj20cu00t748.jpg)

### install RubyGems

RubyGems download: [http://rubygems.org/pages/download](http://rubygems.org/pages/download) rubygems-2.4.5.zip   

cd to RubyGems dirctory:   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue1l2yscj20gk02amxj.jpg)

install:

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue1w8eqnj20bx00hglg.jpg)  

### using RubyGems install Jekyll

install:

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue2g2p3uj207x00ft8j.jpg)

finish: 

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue32drwhj20hv09xq5m.jpg)

### Blog

create a new workspace: jekyllWorkspace

cd to jekyllWorkspace   

```c++
jekyll new jekyllWorkspace      
```

![](http://ww3.sinaimg.cn/large/7011d6cfjw1f2ue3lt31nj20cj02nt8u.jpg)

file structure：   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue3ujsybj20ek06wabh.jpg)

cd to the blog dirctory, run the server   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue47y9lgj20ao00f0sl.jpg)

watch to check the file changes, when you change the files do not need to restart the jekyll

instal yajl-ruby and rouge:  

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue4v42koj20g505bdgy.jpg)

look the http://localhost:4000/ in the browse:  

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue56ckwoj20je0eumz3.jpg)

detal page:  

![](http://ww2.sinaimg.cn/large/7011d6cfjw1f2ue5f3j9cj20je0gyq7a.jpg)

{% if page.comments %}
<div id="disqus_thread"></div>
    <script type="text/javascript">
        /* * * CONFIGURATION VARIABLES: EDIT BEFORE PASTING INTO YOUR WEBPAGE * * */
        var disqus_shortname = 'perfectlyrandom'; // required: replace example with your forum shortname
        // var disqus_developer = 1; // Comment out when the site is live
        var disqus_identifier = "{{ page.url }}";

        /* * * DON'T EDIT BELOW THIS LINE * * */
        (function() {
            var dsq = document.createElement('script'); dsq.type = 'text/javascript'; dsq.async = true;
            dsq.src = '//' + disqus_shortname + '.disqus.com/embed.js';
            (document.getElementsByTagName('head')[0] || document.getElementsByTagName('body')[0]).appendChild(dsq);
        })();
    </script>
    <noscript>Please enable JavaScript to view the <a href="http://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
    <a href="http://disqus.com" class="dsq-brlink">comments powered by <span class="logo-disqus">Disqus</span></a>
{% endif %}