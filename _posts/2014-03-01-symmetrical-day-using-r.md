---
layout: post
title: Symmetrical Days from 2000 to 9999
categories: [R language, symmetry]
tags: [fun]
comments: yes
---

I still clearly remembered in November 2nd, 2011, someone said we may never meet another symmetrical day in your lifetime, so please cherish for this special day. The so-called symmetrical day means that in the date format, like "yyyymmdd", the first letter of the year is the last letter of the day, and the second letter of the year is the first letter of the day, and so on. Yes, these cases are rare, but I want to check what is the next symmetrical day? Does it not exist in the 21st Century? At the time, I was a beginner of R language, so I wrote several lines of code to check how many symmetrical days are from year 2000 to year 9999? 

Here is the code:

{% highlight r %}
a <- 2000:9999
b <- c(paste("0",1:9,sep=""),10,11,12)
c <- c(paste("0",1:9,sep=""),10:31)
mmdd <- paste(rep(b,each=31),rep(c,time=12),sep="")
all <- paste(rep(a,each=length(mmdd)),rep(mmdd,time=length(a)),sep="")
s12 <- substr(all,1,2)
s34 <- substr(all,3,4)
s56 <- substr(all,5,6)
s78 <- substr(all,7,8)
rev.s56 <- paste(substr(s56,2,2),substr(s56,1,1),sep="")
rev.s78 <- paste(substr(s78,2,2),substr(s78,1,1),sep="")
all1 <- all[(s12==rev.s78)&(s34==rev.s56)]
res <- all1[which(substr(all1,1,1)=="2")]
res
{% endhighlight %}

After running around one minute, the result comes out:

`> res`

 [1] "20011002" "20100102" "20111102" "20200202" "20211202" "20300302"
 [7] "20400402" "20500502" "20600602" "20700702" "20800802" "20900902"
[13] "21011012" "21100112" "21111112" "21200212" "21211212" "21300312"
[19] "21400412" "21500512" "21600612" "21700712" "21800812" "21900912"
[25] "22011022" "22100122" "22111122" "22200222" "22211222" "22300322"
[31] "22400422" "22500522" "22600622" "22700722" "22800822" "22900922""
[31] "22400422" "22500522" "22600622" "22700722" "22800822" "22900922"

The result shows we will meet another symmetrical day in February 2nd, 2020. Not far away from now, just waiting for 10 years. So, with the help of the R language, I can easily figure it out. Although I wrote the code for fun, it was my first step entering the paradigm of R language.
