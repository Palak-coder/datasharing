@@ -1,11 +1,11 @@

How to share data with a statistician
===========

This is a guide for anyone who needs to share data with a statistician. The target audiences I have in mind are:
This is a guide for anyone who needs to share data with a statistician or data scientist. The target audiences I have in mind are:

* Scientific collaborators who need statisticians to analyze data for them
* Students or postdocs in scientific disciplines looking for consulting advice
* Junior statistics students whose job it is to collate/clean data sets
* Collaborators who need statisticians or data scientists to analyze data for them
* Students or postdocs in various disciplines looking for consulting advice
* Junior statistics students whose job it is to collate/clean/wrangle data sets

The goals of this guide are to provide some instruction on the best way to share data to avoid the most common pitfalls
and sources of delay in the transition from data collection to data analysis. The [Leek group](http://biostat.jhsph.edu/~jleek/) works with a large
@@ -23,7 +23,7 @@ have to work through all the pre-processing steps first.
What you should deliver to the statistician
====================

### How to collect data in 5 steps?
1. Determine What Information You Want to Collect.
2. Set a Timeframe for Data Collection.
3. Determine Your Data Collection Method.
4. Collect the Data.
5. Analyze the Data and Implement Your Findings.


For maximum speed in the analysis this is the information you should pass to a statistician:
To facilitate the most efficient and timely analysis this is the information you should pass to a statistician:

1. The raw data.
2. A [tidy data set](http://vita.had.co.nz/papers/tidy-data.pdf) 
@@ -35,35 +35,36 @@ Let's look at each part of the data package you will transfer.

### The raw data

It is critical that you include the rawest form of the data that you have access to. Here are some examples of the
It is critical that you include the rawest form of the data that you have access to. This ensures
that data provenance can be maintained throughout the workflow.  Here are some examples of the
raw form of data:

* The strange [binary file](http://en.wikipedia.org/wiki/Binary_file) your measurement machine spits out
* The unformatted Excel file with 10 worksheets the company you contracted with sent you
* The complicated [JSON](http://en.wikipedia.org/wiki/JSON) data you got from scraping the [Twitter API](https://twitter.com/twitterapi)
* The hand-entered numbers you collected looking through a microscope

You know the raw data is in the right format if you: 
You know the raw data are in the right format if you: 

1. Ran no software on the data
1. Did not manipulate any of the numbers in the data
1. Did not modify any of the data values
1. You did not remove any data from the data set
1. You did not summarize the data in any way

If you did any manipulation of the data at all it is not the raw form of the data. Reporting manipulated data
If you made any modifications of the raw data it is not the raw form of the data. Reporting modified data
as raw data is a very common way to slow down the analysis process, since the analyst will often have to do a
forensic study of your data to figure out why the raw data looks weird. 
forensic study of your data to figure out why the raw data looks weird. (Also imagine what would happen if new data arrived?)

### The tidy data set

The general principles of tidy data are laid out by [Hadley Wickham](http://had.co.nz/) in [this paper](http://vita.had.co.nz/papers/tidy-data.pdf)
and [this video](http://vimeo.com/33727555). The paper and the video are both focused on the [R](http://www.r-project.org/) package, which you
may or may not know how to use. Regardless the four general principles you should pay attention to are:
and [this video](http://vimeo.com/33727555). While both the paper and the video describe tidy data using [R](http://www.r-project.org/), the principles
are more generally applicable:

1. Each variable you measure should be in one column
1. Each different observation of that variable should be in a different row
1. There should be one table for each "kind" of variable
1. If you have multiple tables, they should include a column in the table that allows them to be linked
1. If you have multiple tables, they should include a column in the table that allows them to be joined or merged

While these are the hard and fast rules, there are a number of other things that will make your data set much easier
to handle. First is to include a row at the top of each data table/spreadsheet that contains full row names. 
@@ -82,12 +83,12 @@ ids and one row for each data type).

If you are sharing your data with the collaborator in Excel, the tidy data should be in one Excel file per table. They
should not have multiple worksheets, no macros should be applied to the data, and no columns/cells should be highlighted. 
Alternatively share the data in a [CSV](http://en.wikipedia.org/wiki/Comma-separated_values) or [TAB-delimited](http://en.wikipedia.org/wiki/Tab-separated_values) text file.
Alternatively share the data in a [CSV](http://en.wikipedia.org/wiki/Comma-separated_values) or [TAB-delimited](http://en.wikipedia.org/wiki/Tab-separated_values) text file. (Beware however that reading CSV files into Excel can sometimes lead to non-reproducible handling of date and time variables.)


### The code book

For almost any data set, the measurements you calculate will need to be described in more detail than you will sneak
For almost any data set, the measurements you calculate will need to be described in more detail than you can or should sneak
into the spreadsheet. The code book contains this information. At minimum it should contain:

1. Information about the variables (including units!) in the data set not contained in the tidy data 
@@ -118,8 +119,8 @@ When you put variables into a spreadsheet there are several main categories you
Continuous variables are anything measured on a quantitative scale that could be any fractional number. An example
would be something like weight measured in kg. [Ordinal data](http://en.wikipedia.org/wiki/Ordinal_data) are data that have a fixed, small (< 100) number of levels but are ordered. 
This could be for example survey responses where the choices are: poor, fair, good. [Categorical data](http://en.wikipedia.org/wiki/Categorical_variable) are data where there
are multiple categories, but they aren't ordered. One example would be sex: male or female. [Missing data](http://en.wikipedia.org/wiki/Missing_data) are data
that are missing and you don't know the mechanism. You should code missing values as `NA`. [Censored data](http://en.wikipedia.org/wiki/Censoring_\(statistics\)) are data
are multiple categories, but they aren't ordered. One example would be sex: male or female. This coding is attractive because it is self-documenting.  [Missing data](http://en.wikipedia.org/wiki/Missing_data) are data
that are unobserved and you don't know the mechanism. You should code missing values as `NA`. [Censored data](http://en.wikipedia.org/wiki/Censoring_\(statistics\)) are data
where you know the missingness mechanism on some level. Common examples are a measurement being below a detection limit
or a patient being lost to follow-up. They should also be coded as `NA` when you don't have the data. But you should
also add a new column to your tidy data called, "VariableNameCensored" which should have values of `TRUE` if censored 
@@ -135,7 +136,7 @@ Always encode every piece of information about your observations using text. For

### The instruction list/script

You may have heard this before, but [reproducibility is kind of a big deal in computational science](http://www.sciencemag.org/content/334/6060/1226).
You may have heard this before, but [reproducibility is a big deal in computational science](http://www.sciencemag.org/content/334/6060/1226).
That means, when you submit your paper, the reviewers and the rest of the world should be able to exactly replicate
the analyses from raw data all the way to final results. If you are trying to be efficient, you will likely perform
some summarization/data analysis steps before the data can be considered tidy. 
@@ -186,5 +187,6 @@ Contributors
* [Jeff Leek](http://biostat.jhsph.edu/~jleek/) - Wrote the initial version.
* [L. Collado-Torres](http://bit.ly/LColladoTorres) - Fixed typos, added links.
* [Nick Reich](http://people.umass.edu/nick/) - Added tips on storing data as text.
* [Nick Horton](https://www.amherst.edu/people/facstaff/nhorton) - Minor wording suggestions.
* [Anjali Singh](linkedin.com/in/anjali-singh-b72604184) - Added tips on collecting data.