<h1>Lib4MOOCData</h1>

Library for processing MOOC data dumps.  Currently limited to Coursera data.

<h3>Coursera data export</h3>
Coursera exports data from its MOOCs after compeltion for use by the university that is hosting it on its platform. These data dumps are .sql exports from MySQL databases.
A typical data export consists of the following .sql files
<ol>
<li> &lt;Full_Coursename&gt;(&lt;coursecode&gt;)_SQL_anonymized_forum.sql </li>
<li> &lt;Full_Coursename&gt;(&lt;coursecode&gt;)_SQL_hash_mapping.sql </li>
<li> &lt;Full_Coursename&gt;(&lt;coursecode&gt;)_SQL_anonymized_general.sql </li>
<li> &lt;Full_Coursename&gt;(&lt;coursecode&gt;)_SQL_unanonymizable.sql </li>
</ol>

A .txt file with clickstream data is also provided. We do not process them yet in this library <br>
5. &lt;coursecode&gt;_clickstream_export.gz

For replicating our <a href="http://wing.comp.nus.edu.sg/~cmkumar/edm2015.pdf">EDM work</a>, it is sufficient to import files (1), (2) and (3).

<h3>Prerequisites</h3>
To use the library to process and analyse your data you will first need to install the MySQL database and ingest the .sql files into the database.
Command to ingest .sql files using MySQL command line interface (CLI):
mysql&gt; source &lt;path to .sql file&gt;/&lt;name of the.sql file&gt;

Note that Coursera supplies a sql export for every course. This means DDL statements across the files from different courses will be redundant. More importatnly there is no field for coursecode in any of the tables. So, you have to either:
i) create a separate MySQL database for each course dump (1 per each course iteration) or
ii) add a 'coursecode' field to every table and issue update statements to populate the coursecode field after running the *.sql import

<h3>Installation</h3>
The scripts require you to have installed Perl 5 and some dependant perl packages.

<b>For Windows users </b> <br>
Install Strawberyy Perl from here http://strawberryperl.com/lib4moocdata or Active Perl from here http://www.activestate.com/activeperl

<b> For Linux, Mac usesrs </b> <br>
Linux and Mac users should have perl already installed as part of your OS. You can check with by typing perl -v in your terminal.

<h4>Dependant Perl Modules (Packages) to install</h4>
CPAN has tools to easy install perl modules. Please see this step-by-step tutorial http://www.cpan.org/modules/INSTALL.html <br>
The packages to install are:
<ul>
<li>DBI</li>
<li>FindBin</li>
<li>Getopt::Long</li>
<li>Encode</li>
<li>HTML::Entities</li>
<li>Lingua::EN::Sentence qw( get_sentences add_acronyms)</li>
<li>Lingua::EN::Tokenizer::Offsets qw(token_offsets get_tokens)</li>
<li>Lingua::StopWords  qw( getStopWords )</li>
<li>Lingua::EN::StopWordList</li>
<li>Lingua::Stem::Snowball</li>
<li>Lingua::EN::Ngram</li>
<li>Lingua::EN::Bigram ## Fails on linux centos 6 </li>
<li>Lingua::EN::Tagger</li>
<li>Lingua::EN::PluralToSingular 'to_singular'</li>
<li>Config::Simple</li>
<li>File::Remove</li>
</ul>
