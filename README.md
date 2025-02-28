# TF-IDF Okapi BM25 Dirichlet Smoothing
### Overview
In this assignment, you will use the index you created in Assignment 1 to rank documents and
create a search engine. You will implement different scoring functions and compare their results
against a baseline ranking produced by expert analysts.
Running Queries
For this assignment, you will need the following two files:
- queries: It contains the queries you will be testing.
- qrels: It contains the relevance grades from expert assessors. While these grades are not
necessarily entirely correct (and defining correctness unambiguously is quite difficult),
they are fairly reliable and we will treat them as being correct here.

The format here is:

o <topic> is the ID of the query for which the document was assessed
o <doc> is the name of one of the documents which you have indexed.
o <grade> is a value in the set {1, 2, 3, 4}, where a higher value means that the
document is more relevant to the query. The value 1 indicates a document which
is non-relevant.

This QREL does not have assessments for every (query, document) pair. If an assessment
is missing, we assume the correct grade for the pair is 1 (non-relevant).
You will write a program which takes the name of a scoring function as a command line
argument and which prints a ranked list of documents for all queries found in topics.xml using
that scoring function. For example:


$ ./query.py --score TF-IDF

202 clueweb12-0000tw-13-04988 1 0.73 run1
202 clueweb12-0000tw-13-04901 2 0.33 run1
202 clueweb12-0000tw-13-04932 3 0.32 run1
...



214 clueweb12-0000tw-13-05088 1 0.73 run1
214 clueweb12-0000tw-13-05001 2 0.33 run1
214 clueweb12-0000tw-13-05032 3 0.32 run1
...
250 clueweb12-0000tw-13-05032 500 0.002 run1

The output should have one row for each document which your program ranks for each query it
runs. These lines should have the format:

<topic> <docid> <rank> <score> <run>
- <topic> is the ID of the query for which the document was ranked.
- <docid> is the document identifier.
- <rank> is the order in which to present the document to the user. The document with the
highest score will be assigned a rank of 1, the second highest a rank of 2, and so on.
- <score> is the actual score the document obtained for that query.
- <run> is the name of the run. You can use any value here. It is meant to allow research
teams to submit multiple runs for evaluation in competitions such as TREC.
