---
layout: post
title: You're up and running!
---


{% highlight python %}
def anti_vowel(text):
	text = text.lower()
	vowels = ['a','e','i','o','u']
	return ''.join([x for x in text if x not in vowels])
{% endhighlight %}


<div>
    <a href="https://plot.ly/~RafehQazi/14/" target="_blank" title="" style="display: block; text-align: center;"><img src="https://plot.ly/~RafehQazi/14.png" alt="" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="RafehQazi:14"  src="https://plot.ly/embed.js" async></script>
</div>



Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository . HEYYOOOOO. Yup did that. (shown below)

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub. 

rafeh01
