---
title: CREATE A SITE SEARCH ENGINE WITH MONGODB
description: The LIKE operator doesn't exist in MongoDB. This is not a problem.
header: CREATE A SITE SEARCH ENGINE WITH MONGODB
---
The LIKE operator doesn't exist in MongoDB. This is not a problem. The real problem here is to choose between two MongoDB operators that many people think are similar, namely $regex and $text.

The former implements regular expressions and doesn't require an index, the latter uses substrings and needs an index on the selected property of a document.

I didn't test myself the actual impact on performance of both operators, so I can't recommend you what is the best choice here from a pure performance perspective. Feel free to experiment.

As said above, with $text you need to create indexes:

``` javascript
db.posts.createIndex({title: "text"});
db.posts.createIndex({content: "text"});
db.posts.createIndex({excerpt: "text"});

```
