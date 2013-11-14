TODO
====================

schedule:
Thursday:
-1) Improving your Workflow in Rstudio and Rmd ~30 minutes
2) “best practices” in nomenclature and style ~ 15 minutes
+3) Core R + R Vocabulary primer ~ 1 hour
+4) Object Orientation ~ 30-45 minutes
5) Thinking-in-R
+5) Introduction to Data Manipulation ~1-1.5 hours
-6) Pragmatic Programming ~15 minutes
+7) Introduction to Function writing part 1: ~ 30 minutes
+8) Scoping and Environments ~30 minutes
+(more examples ending) 9) Introduction to Function Writing part 2: ~30 minutes
+10) Input/output ~15 minutes
+11) Control Structures ~ 45 minutes

Friday
1. Apply Functions ~ 45 minutes
2. String Manipulations ~ 45 minutes
3. Intermediate Function Writing and Debugging ~1-1.5 hours
4. Intermediate Data Manipulation ~1.5 hours
5. R for “Pharmacometricians” ~ 1.5 hours
6. Evaluating and Speeding up your code ~30 minutes
7. Miscellaneous topics – to end

example hands-on tasks


Potential "assignment" ideas:

Datasets available
* RichPK dataset
    * ID, TIME, DOSE, CMT CONC AGE WEIGHT GENDER RACE
* Painscore
    * ID, painscore, PScat, Cmax, TRT, isTRT, WT, GENDER
* sub102metabolites-raw
    * id, day, time, conc, evid, analyte, dose ralt, dose type, conc, analyte, conc, analyte, dose mida, dose type, conc, analyte (mutiple columns with same name, in conc column has numeric and character values (n.d.))

Intro-Data-Manipulation 
- create subsetting practice scenarios
- coerce the factor'd subjects of Theoph to numeric ID numbers so they can be sorted
input/output
- fake dataset with T/R test/reference column - what happens when it is read - how do you handle it?
- source an R script from another file
- source an R script on the command line in linux
- change all values for male/female to M/F


Function writing
- create a new function using `...` and what we've learned about closures to set some different default behaviors
    - to our 'parametric' summary function? 
    - to the read.* to set StringsAsFactors = FALSE by default

- create a new function and use `source` to load it into a new R script/document

- create a dosing function factory to create different dosing functions
    - BIDdosing <- dosing(12)
    - TIDdosing <- dosing(8)

control statements
- write a creatinine clearance script that they can pass male/female


Advanced Function Writing
- update a creatinine clearance script that they can pass male/MALE/Male,etc - if incorrectly pass male/female warn them and print out message for possible correct inputs



write a function that you can pass the column names for any column that has categorical covariates such that it will make a new column with "colname + _nm" and covert to numeric values



Hard challenge - take sub102metabolites and modify it to convert from wide to long, gracefully handling conc character strings, make dataset phoenix then nonmem-ready
