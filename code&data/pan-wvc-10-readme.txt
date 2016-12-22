
PAN Wikipedia Vandalism Corpus 2010, PAN-WVC-10
Copyright 2010 Bauhaus-Universität Weimar. All rights reserved.


Table of Contents:
1. Introduction
2. Edit Sampling
3. Vandalism Annotation
4. Corpus Format
5. Acknowledging the Corpus
6. Contact Information


1. Introduction

This corpus contains edits from the edit logs of the Wikipedia encyclopedia
which have been annotated by humans with regard to whether they are regular
edits or rather vandalism edits. We believe this corpus will be useful to
evaluate automatic vandalism detection algorithms.


1.1 Edits and Article Revisions

An edit marks the transition of a old article revision on Wikipedia to a new
one. This corpus comprises 32,439 edits and a total of 64,441 article revisions.


1.2 Licence of the Corpus

All of the texts contained in this corpus are served under the Creative Commons
Attribution-ShareAlike Licence, the licence of the Wikipedia encyclopedia. 
The corpus can therefore be used free of charge and without any liabilities.
In this connection we release the annotations we have produced under the same
licence.


1.3 Wikipedia Vandalism

Wikipedia defines vandalism as "any addition, removal, or change of content
made in a deliberate attempt to compromise the integrity of Wikipedia". Put
another way, a vandalism edit is an edit made with bad intentions.
Further reading: http://en.wikipedia.org/wiki/Wikipedia:Vandalism

The vandalism that is annotated in this corpus has occurred exactly like this
on Wikipedia. Note that we have in no way encouraged others to vandalize
Wikipedia.


1.4 Algorithms to be Evaluated with the Corpus

The corpus can be used to evaluate the following vandalism detection task:
Given a set of edits on Wikipedia articles, the task is to separate the
ill-intentioned edits from the well-intentioned edits. 



2. Edit Sampling

The edits in this corpus have been taken from the live edit logs of Wikipedia.
From November 18th, 2009 to December 6th, 2009 edits have been recorded as they
occurred on Wikipedia, and then 32,439 edits were sampled at random. This means
that our sample resembles article importance with regard to edit frequency.


3. Vandalism Annotation

The corpus comprises 32,439 edits of which 2394 are considered vandalism.
The percentage of vandalism (7%) corresponds to that reported in the literature.

The annotations have been obtained via Amazon's Mechanical Turk. Each edit has
been reviewed by at least 3 and up to 28 annotators whose task was to decide
whether or not the respective edit is vandalism. Based on these votes we have
determined the class of each edit as 'regular' or 'vandalism'. If more than
1/2 of the annotators agreed on a given edit we have followed their voting, 
otherwise we have reviewed the edits manually and made a decision taking into
account the votes of the annotators. The latter was done in 91 cases.


4. Corpus Format

4.1 Contents of the Top-level Directory

Directory "article-revisions": this directory contains the revisions of
Wikipedia articles which are either source, or result of an edit operation.
Note that the resulting article revision of an edit is the source of the next
edit on the same article.


4.1.1 File "edits.csv"

List of edits to be used to train a vandalism detector.
Each edit is described by the following fields:
- editid:        unique edit identifier
- editor:        the user name / IP address of the editor who performed the edit
- oldrevisionid: the identifier of the old, source revision as found in the
                 article-revisions directory (foreign key)
- newrevisionid: the identifier of the new, destination revision as found in the
                 article-revisions directory (foreign key)
- diffurl:       URL pointing to a Wikipedia page which visualized the
                 difference between old and new revision
- edittime:      the time at which the edit was made
- editcomment:   the comment the editor left when submitting his edit
- articleid:     the unique identifier of an edited article
- articletitle:  the title of the edited article
The editid column is the primary key of this table.
Secondary keys are the pair (oldrevisionid,newrevisionid), and diffurl.


4.1.2 File "gold-annotations.csv"

Classification of each edit as vandalism or regular
edit. This classification is to be recreated by an vandalism detector.
Each classification is described by the following fields:
- editid:          reference to the editid of edits.csv (foreign key)
- goldclass:       classification of the referenced edit as regular or vandalism
- annotators:      number of annotators who concur with this classification
- totalannotators: total number of annotators who reviewed the referenced edit
The editid column is the primary key of this table.


4.1.3 File "annotations.csv"

List of annotations supplied by the different annotators.
Each annotation is described by the following fields:
- editid:       reference to the editid of edits.csv (foreign key)
- annotatorid:  reference to annotatorid of annotators.csv (foreign key)
- class:        classification of the referenced edit as 'regular', 
                'vandalism', 'dunno' in case the annotator was uncertain
- decisiontime: time in milliseconds the before the annotator made chose a class
- submittime:   the date the annotator submitted his annotation; this makes the
                annotators progress reproducible
The pair (editid,annotatorid) is the primary key of this table.


4.1.4 File "annotators.csv"

List of annotators which supplied the annotations in annotations.csv.
Each annotator is described by the following fields:
- annotatorid: unique annotator identifier
- age:         the age of the annotator
- sex:         gender of the annotator
- reading:     how often the annotator reads Wikipedia
- editing:     how often the annotator edits Wikipedia
- vandalizing: whether or not the annotator has vandalized Wikipedia
- noticing:    how often the annotator notices vandalism on Wikipedia
The annotatorid is the primary key of this table.
Note that not all annotators have supplied the above information, and some have
submitted only partial information. For the former, there is no line in this
table, and for the latter there may be empty cells.


4.2 Contents of the "article-revisions" directory

Directories "part1" through "part65": Each part directory contains up to 1000
text files, each of which being the revision of a Wikipedia article. The name of
a file is its revision identifier, which is referenced in the edits.csv file.
The contents of each text file is the plain wikitext of the revision.



5. Acknowledging the Corpus

We are pleased to release this corpus, and it is our hope that it will foster
the development of new vandalism detection approaches. We would be happy to
hear from you about how and with what success you used the corpus. If you use
the corpus we kindly ask you to refer to it as follows in your publications:

Citation template:

Martin Potthast. Crowdsourcing a Wikipedia Vandalism Corpus.
In Hsin-Hsi Chen, Efthimis N. Efthimiadis, Jaques Savoy, Fabio Crestani, and
Stéphane Marchand-Maillet, editors, 33rd Annual International ACM SIGIR
Conference (SIGIR 10), Geneva, Switzerland, pages 789-790, July 2010. ACM.
ISBN 978-1-4503-0153-4.

Bibtex:

@INPROCEEDINGS{potthast:2010b,
  AUTHOR     = {Martin Potthast},
  BOOKTITLE  = {33rd Annual International ACM SIGIR Conference},
  DOI        = {10.1145/1835449.1835617},
  EDITOR     = {Hsin-Hsi Chen and {Efthimis N.} Efthimiadis and Jaques Savoy
                and Fabio Crestani and St{\'e}phane Marchand-Maillet},
  ISBN       = {978-1-4503-0153-4},
  MONTH      = jul,
  PUBLISHER  = {ACM},
  SITE       = {Geneva, Switzerland},
  PAGES      = {789-790},
  TITLE      = {{Crowdsourcing a Wikipedia Vandalism Corpus}},
  YEAR       = {2010}
}



6. Contact Information

If you have comments, suggestions, questions about the corpus, or any other
feedback don't hesitate to send mail to corpora@webis.de.


Martin Potthast
Bauhaus-Universität Weimar
September 6, 2010

