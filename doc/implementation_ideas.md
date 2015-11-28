## Overview of the Conceptual Architecture

A "project" is initially defined by a GitHub repo.

A project has "entry points" -- public protocols, functions, etc. Each entry point may have
"documentation" -- human-readable text describing that entry point.

One project can "reference" the entry point of another. A "reference" is a single mention in one
project of an entry point in another project. (A project cannot reference itself in this model.)

More specifically, a project references entry points through its "files".

Other entities can "reference" a project. One early example will be a Stack Exchange answer. Then we
may use a broader web crawl, such as by filtering [Common Crawl](http://commoncrawl.org) down to web
pages containing source code.

A project has "versions". We are going to try not to think too much about this too soon, nor too
late.

An "author" is initially defined by a GitHub user.

## Relevance Counterpart to Page-Rank 

We need some sort of transitive-authority mechanism that would be the counterpart to page-rank in
this domain. Eventually, this will no doubt become mathematically complex. Before we go there,
however, let's get experience with a simple, intutive algorithm. The real-world dynamics of
transitive software references may be quite different from the dynamics of transitive HTML links.

Here is a starting point:

A project has "value", which we define for now to be the number of references to that project in
(the current versions of) other projects.

An entry point also has "value", defined the same way as for a project.

An author "creates" a certain "creation fraction" of a project. For now, we define this to be the total
net line count of the author's commits divided by the total net line count of all of the
project's commits.

An author has "authority". For now, we define this to be the total of (project value * creation
fraction) across projects the author has created.

A project has "authority". For now, we define this to be the weighted average, by creation fraction,
of  the project's authors' authoritites.

A reference has "file code context" -- the set of other entry points referenced by the file in which
the reference appears. Eventually, we may add the notion of "local code context" -- the set of other
entry points referenced by the local scope in which the reference appears.

A reference may also have "descriptive context" -- human-readable text associated with the
reference. For example, for a reference in a Stack Exchange answer, the text of the answer is the
descriptive context.

## Searching

A "programmer" searches for a useful entry point, which may be found in his own project or in
another project. He initiates the search in the code context in which he expects to use the entry
point. He provides a "query", which is search text in Google style.

Query results are entry points. Here are some candidate relevance signals, starting with the ones we
suspect will be the strongest:

* query match to entry point symbols

* query match to entry point documentation

* authority of the entry point's project

* value of the entry point

* value of the entry point's project

* query match to combined descriptive context across a sample of references to the entry point

* query code context match to combined code context across a sample of references to the entry point

## Implementation Overview

The main activities that must be supported by the implementation architecture are

* fetching inputs

  * GitHub repos

  * Stack Exchange answers

  * Other web pages

* parsing inputs

  * identifying all references in a GitHub repo

  * resolving references to the projects that define them and the referenced entry points

  * identifying committers to a GitHub repo and gathering statistics for them

  * separating source code, relevant human-readable text, and junk from a Stack Exchange answer

  * separating source code, relevant human-readable text, and junk from an arbitary web page

* gathering our index inputs by entry point (Conceptually, this is the "map" in map-reduce: the key is a unique identifier for the entry point.)

* indexing entry points (This is the "reduce" in our map-reduce.)

## "Big Data" engine

As a starting point, we will simply use Postgres for data storage, indexing, and retrieval. It is a simple solution that might (with sharding) be fine forever. Although it is natural to suspect that solutions like [Apache Spark](https://spark.apache.org) and [Lucene](http://lucene.apache.org) may be necessary in the long run, they would certainly slow development in the short term by adding complexity.

