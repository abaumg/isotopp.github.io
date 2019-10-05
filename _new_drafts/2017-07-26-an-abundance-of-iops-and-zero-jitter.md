---
layout: post
status: publish
published: true
title: An abundance of IOPS and Zero Jitter
author: isotopp
author_login: kris
author_email: kristian.koehntopp@gmail.com
wordpress_id: 2250
wordpress_url: http://blog.koehntopp.info/?p=2250
date: '2017-07-26 14:51:55 +0200'
date_gmt: '2017-07-26 13:51:55 +0200'
categories:
- Data Centers
- Containers and Kubernetes
tags: []
---
<p>Two weeks ago, I wrote about&nbsp;[The Data Center in the Age of Abundance](http://blog.koehntopp.info/index.php/2088-the-data-center-in-the-age-of-abundance/)&nbsp;and claimed that IOPS are - among other things - a solved problem. What does a solved problem look like? Here is a benchmark running 100k random writes of 4K per second, with zero Jitter, at 350µs end-to-end write latency across six switches. Databases really like reliably timed writes like these. Maximum queue depth would be 48, the system is not touching that.<!--more-->[![](http://blog.koehntopp.info/wp-content/uploads/2017/07/pure-storage1.jpg)](http://blog.koehntopp.info/wp-content/uploads/2017/07/pure-storage1.jpg) and here is iostat on the iSCSI client running the test [![](http://blog.koehntopp.info/wp-content/uploads/2017/07/pure-storage2-1024x238.jpg)](http://blog.koehntopp.info/wp-content/uploads/2017/07/pure-storage2.jpg) 100k random writes, 4k write size, inside a 2 TB linux file of random data, on a 15 TB filesystem with XFS, on an LVM2 volume provided by iSCSI over a single 10 GBit/s interface, with six switch hops between the linux client and the array.</p>
<p>The array claims 150µs latency, on the linux we measure around 350µs. Out of that, there are less than 50µs from the switches and 150µs or more from the Linux storage stack (and that is increasingly becoming an issue).</p>
<p>Tested product was a [Purestore Flasharray-X](https://www.purestorage.com/products/flasharray-x.html), client was Dell PowerEdge R630, 2x E5-2620v4, 128G, 10GBit/s networking. Thanks, Peter Buschman!</p>