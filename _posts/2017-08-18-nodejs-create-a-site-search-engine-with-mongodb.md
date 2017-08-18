---
title: NODEIS | CREATE A SITE SEARCH ENGINE WITH MONGODB
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

Then you can run a query similar to the following:

``` javascript

db.posts.find({'$and': [{'title': {'$text': 'query'}},
 {'content': {'$text': 'query'}}, {'excerpt': {'$text': 'query'}}]});

```
With the $and operator we're including possible alternatives, with $or instead we're excluding some alternatives.

Since $text doesn't use regular expressions, install and Install are not the same thing. The match here is exact, so in order to get more results we should use $regex:


``` javascript
db.posts.find({'$and': [{'title': {'$regex': 'query', '$options': 'i'}},
{'content': {'$regex': 'query', '$options': 'i'}}, {'excerpt': {'$regex': 'query', '$options': 'i'}}]});
```