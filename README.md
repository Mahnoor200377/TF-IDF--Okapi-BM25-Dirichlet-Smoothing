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


###  Query Processing
Before running any scoring function, you should process the text of the query in exactly the same
way that you processed the text of a document for your inverted index. That is:
1. Split the query into tokens
2. Apply stop-wording to the query using the same list you used in assignment 1
3. Apply the same stemming algorithm to the query which you used in your indexer

### Scoring Function 1: TF-IDF
The parameter --score TF-IDF directs your program to use a vector space model with TF-IDF
scores. This should be very similar to the TF score, but use the following scoring function:

 d=oktf(d,i). log D/df(i)
 
where D is the total number of documents, and df(i) is the number of documents which contain term
i.

### Scoring Function 2: Okapi BM25
Implement BM25 scores. 

### Scoring Function 3: Language model with Dirichlet Smoothing
Implement a language model with Dirichlet smoothing. The parameter mu should be set equal to
average document length in collection.
Evaluation

To evaluate your results, we will write a program that computes mean average precision (MAP)
of the rank list of documents for different queries. The input to program will be the qrel file
(relevance judgments) and scoring file that has rank list of documents. The output should be
following measures

P@5
P@10
P@20
P@30
MAP

These measures should be computed for each query. Average for all queries should also be
computed.
