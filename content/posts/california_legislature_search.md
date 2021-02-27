---
title: "Bug in California legislative information bill search text highlighting"
date: 2021-02-24
tags: ['blogs', 'programming', 'bugs']
draft: false
---

Recently I was working on [automating some legislation tracking tasks](https://github.com/EthanHolleman/pyCaliLegi)
for the UC Davis Legislative Affairs Committee and noticed a potential
bug in displaying the results of bill information searches and wanted to
note it.

If you are interested in California legislation you can go to
the [state website](https://leginfo.legislature.ca.gov/faces/home.xhtml)
and search for bills by a number of parameters, including by keywords as an example ce can search for "housing".

<img src="https://www.rd.com/wp-content/uploads/2019/09/Cute-cat-lying-on-his-back-on-the-carpet.-Breed-British-mackerel-with-yellow-eyes-and-a-bushy-mustache.-Close-up-e1573490045672.jpg" alt="Cat">

![](/posts/images/legi_search.png)

Which brings up a number of bills. Clicking on one gives us the bill's 
full text with out keyword highlighted. 

![](/posts/images/housing_legi.png)

The bug occurs when we search for specific html tags like `div` or `span`.

![](/posts/images/span_legi.png)

When these terms are searched the source html ends up being rendered on the actual page with tags highlighted. 

Looking at the actual html at locations where this occurs it looks
like the highlighting is resulting in unescaped `<` characters.

```html
<div style="margin:0 0 1em 0"><<b><span style='background-color:yellow'>span</span></b>
```

```html
</<b><span style='background-color:yellow'>span</span></b>><<b><span style='background-color:yellow'>span</span></b>
```

This bug seems to basically be an aesthetics issues and may confuse
a user or two who's search terms overlap with html tags but that
is about it. I opened an [issue](https://leginfo.legislature.ca.gov/faces/feedbackDetail.xhtml?primaryFeedbackId=prim1614185686704) on 
the state website to inform the web administrator. 
