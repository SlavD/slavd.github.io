---
layout: post
title: "Windows Azure Table Storage query performance"
description: "Analysis of Windows Azure table storage query performance"
category: articles
tags: [azure, cloud, performance]
---

Recently when working with Azure Table Storage I was wondering what are the performance implications of not using PartitionKey.

We all know that Microsoft highly recommends to use PartitionKey for all queries but in reality it's not always possible - plus it really helps to know what kind of performance hit are we going to get when not using PartitionKey for queries.

So I decided to put this to a test. I quickly put together MVC website that would allow me to:

* Insert rows with predefined partition key
* Query with partition key and row key specified
* Query with just the rowkey
* Query by arbitrary but unique column
* Query by arbitrary but not unique column
* I did 5 queries of each kind randomly picking rows for the query - I did 5 queries each to get average query time.

I started with 1,000 rows within partition and finished with a bit over a 1,000,000.

The results confirm what Microsoft was saying all along (no surprise here) - use partition and row keys whenever you can to get top performance.

But what about using just the rowkey alone - for small table - less than 10,000 rows the difference is from 10 - 20 ms after that it starts to increase to over 1s for 1,000,000 rows.

Queries for arbitrary columns behave in similar manner, although they deteriorate quicker and for 1,000,000 rows the difference is over 2s comparing to query with partition and rowkey used.

These are the results on the graph:
<figure>
	<img src="https://docs.google.com/spreadsheet/oimg?key=0AlccCc4c7XAPdFNPWnZBSHZydWZQbG56UnFkV1g3Z1E&amp;oid=2&amp;zx=ga9civ9t60ge" width="400">
</figure>

And here is raw data:

<iframe frameborder="0" height="300" src="https://docs.google.com/spreadsheet/pub?key=0AlccCc4c7XAPdFNPWnZBSHZydWZQbG56UnFkV1g3Z1E&amp;single=true&amp;gid=0&amp;output=html&amp;widget=true" width="600"></iframe>


