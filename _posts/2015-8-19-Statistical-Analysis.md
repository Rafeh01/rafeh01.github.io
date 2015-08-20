---
layout: post
title: Split Test Analysis
---

<h4>Problem: A/B Test. Testing an online forum and seeing which variation of the forum lured in more sales. Baseline was original, every other altercation afterwards was titled "Variation" with it's respective number. Let's crunch the numbers and analyze this data set together.</h4>

Let's start off with useful imports in IPython.
    %autosave 120
    import pandas as pd
    import numpy as np
    
    # For visualization
    import seaborn as sns
    import matplotlib.pyplot as plt
    %matplotlib inline
    
    galvanizeData = pd.read_csv('downloads/galvanizeData.csv')

    Autosaving every 120 seconds
    galvanizeData.head()




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Buckets</th>
      <th>Quotes</th>
      <th>Views</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Baseline</td>
      <td>32</td>
      <td>595</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Variation 1</td>
      <td>30</td>
      <td>599</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Variation 2</td>
      <td>18</td>
      <td>622</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Variation 3</td>
      <td>51</td>
      <td>606</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Variation 4</td>
      <td>38</td>
      <td>578</td>
    </tr>
  </tbody>
</table>
</div>


{% highlight Python3 linenos %}

    print ((32/595) * 100)
    print ((30/599) * 100)
    print ((18/622) * 100)
    print ((51/606) * 100)
    print ((38/578) * 100)

    5.378151260504202 #Percentages
    5.008347245409015
    2.8938906752411575
    8.415841584158416
    6.5743944636678195
{% endhighlight %}

<h3>Creating <em>Conversion Rates</em> column</h3>

{% highlight Python3 linenos %}
    galvanizeData['Conversion Rates'] = (galvanizeData['Quotes']/galvanizeData['Views']) * 100
    galvanizeData.head()
{% endhighlight %}



<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Buckets</th>
      <th>Quotes</th>
      <th>Views</th>
      <th>Conversion Rates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Baseline</td>
      <td>32</td>
      <td>595</td>
      <td>5.378151</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Variation 1</td>
      <td>30</td>
      <td>599</td>
      <td>5.008347</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Variation 2</td>
      <td>18</td>
      <td>622</td>
      <td>2.893891</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Variation 3</td>
      <td>51</td>
      <td>606</td>
      <td>8.415842</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Variation 4</td>
      <td>38</td>
      <td>578</td>
      <td>6.574394</td>
    </tr>
  </tbody>
</table>
</div>

<h4>By calculating the conversion rate in percentages, we can identify which variation was the best. However, the conversion rates are currently not sorted so let's do that. </h4>

{% highlight python3 linenos %}
    galvanizeData.sort(columns='Conversion Rates')
{% endhighlight %}

<h3>Time for some beautiful visualizations!</h3>

<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Buckets</th>
      <th>Quotes</th>
      <th>Views</th>
      <th>Conversion Rates</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>Variation 2</td>
      <td>18</td>
      <td>622</td>
      <td>2.893891</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Variation 1</td>
      <td>30</td>
      <td>599</td>
      <td>5.008347</td>
    </tr>
    <tr>
      <th>0</th>
      <td>Baseline</td>
      <td>32</td>
      <td>595</td>
      <td>5.378151</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Variation 4</td>
      <td>38</td>
      <td>578</td>
      <td>6.574394</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Variation 3</td>
      <td>51</td>
      <td>606</td>
      <td>8.415842</td>
    </tr>
  </tbody>
</table>
</div>

{% highlight numpy %}
  sns.barplot(x = 'Buckets', y = 'Conversion Rates', data=galvanizeData.sort(columns='Conversion Rates'))
{% endhighlight %}

<matplotlib.axes._subplots.AxesSubplot at 0x10bc10da0>

<h2>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Split Test Analysis</h2>

<h4>Which variation had the highest conversion rate?</h4>

![Graph]({{ site.url }}/images/output_5_1.png)

I would ask you how did you control for time (time of day, which weekday, etc), and did you account for the fact that maybe the companies were just more desperate due to some lurking/extraneous factor? Since the goal is to have a variation which outputs the highest conversion rate, here are the analysis of my results: version 3 is the best, version 4 is second, baseline is third, version 1 is fourth, and version 2 is the worst.

If I were to run it again, I would consider removing variations that offered a conversion rate below the baseline, so leaving us with baseline, variation 3, and variation 4. Baseline and version 1 have very close results so I would run some more tests with that because as of now it is not easy to tell. 


## Potential problems with collecting data from forms
- The result might have to do with the time of day. 
- The day might matter as well
- Maybe they just needed it as an emergency

## Possible suggestions for improvement
- Controlling for time (time of day, weekday vs weekend)
- Obtain data on similar days (ex: Every Saturday)

## Potential Lurking Factors
- Internet disconnection being disabled while filling out a quote
- Website acting glitchy at moments of quote purchasing


    * Program for python text content analyzer
    
    ** Requirements **
    * 1. total word count
    * 2. total unique word count
    * 3. total sentence count
    
    ** Brownie Points **
    * 1. The ability to find often used phrases (a phrase of 3 or more words used over 3 times)
    
    {% highlight python linenos %}
    #f = open('downloads/workfile.txt', 'r')
    
    def text_content_analyzer(f):
        words = []
        nbOfSentences = 0
        punctuation = []
        wordsCount = {}
    
        for line in f:
            nbOfSentences += len(re.split(r'[.!?]+', line.strip()))-1
            lineWords = line.split()
    
            words = words + lineWords
            for word in lineWords:
                if word in wordsCount:
                    wordsCount[word] += 1
                else:
                    wordsCount[word] = 1
       
        print("Total word count: %1.0f" %len(words))
        print(wordsCount)
        print("Unique words: " , len(wordsCount.keys()))
        print(nbOfSentences)
        return len(words), wordsCount, len(wordsCount.keys()), nbOfSentences
    
    #text_content_analyzer(f)
{% endhighlight %}

    
