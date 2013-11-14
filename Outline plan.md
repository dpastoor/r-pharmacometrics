Outline plan
========================================

1. Intro (split into 2 sections - RMD lab notebook and Improving_workflow)
	1. using Rmd as a lab notebook
		a. caching
		b. setting local and global chunk options
		c. knitting caveats
	2. some useful Rstudio keyboard shortcuts
		a. http://www.rstudio.com/ide/docs/using/keyboard_shortcuts
	3. material to provide
		presentation/document
		knitr template with common options set
		
2. Core R
	1. environments
	2. object orientation - just touch on
	3. data structures
		a. dataframe, lists, matrices, etc
			i`. attributes
			ii. str
	4. best practices
		a. nomenclature
		b. style guidelines
		c. commenting
material to create
		presentation/document
		pretest

3. pragmatic programming
	1. DRY - don't repeat yourself
	2. thinking in terms of 'R'

4. Object Orientation
	1. encapulation
	2. polymorphism
	3. inheritence
	4. Resources
		a. chapter 9 of art of R programming
		b. hadley's advanced R

5. Intro to commonly used R 'commands(name?)'
	• str
	• ls
	• attributes
	• names
	• head
	• tail
	• summary
	• nrow
	• ncol
	• all()
	• any()
	• which()
	• unique()
	• duplicated()
	• match()
	• %in%
	• by()
	• rep
	• replicate
	• seq
	• length()
	• seq_along()
	• is.na
	• !<>
	• rbind/cbind
	• interaction()

6. Relevant Input/Output
	1. some commonly used input/output settings
		a. stringsAsFactors = F
		b. asis
		c. …
		
7. Intro to Data Manipulation
	1. subsetting
		a. hadley adv-R
		b. chapter 3.1 R inferno subscripting!
	2. with/within
	3. dealing with factors
		a. ordered/unordered
		b. labels
	4. reorder and rename rows/columns
	5. merging 
	6. %in%, any, which http://stackoverflow.com/questions/17984600/fast-way-to-figure-out-if-a-number-is-inside-a-vector-in-r/17993464#17993464
	
	material to create
		presentation/document
		decide on example dataset

		
8. introduction to functions
	1. Understanding arguments
		a. defaults
	2. Understanding variable scope (ie what happens if you have a variable “dose” in your global env when you define a “dose” variable in your function)
	
9. Additional R commands
	1. SetNames
	2. complete.cases
	3. rownames
	4. colnames
	5. <row/col>Sums
	6. <row/col>Means
	7. cumsum?
	8. sort/order
		
	

10. control structures
	1. if
	2. ifelse
	3. for 
	4. while
	
11. Apply Functions
	1. **vectorization tidbit**
	2. apply
	3. lapply
	4. sapply
	5. mapply
	6. rapply
	7. tapply
		
12. Data Manipulation
	1. plyr
	2. reshape2
	3. possibly data.tables
	
13. "advanced" R functions
		a. split
		b. do.call
		
14. String Manipulation
		a. paste<0>, cat, sprintf
		b. substr, strsplit
		c. maybe regular expressions
		d. resources
			i. ch 11 art of r prog
			ii. metrum 205
		
15. "Advanced" Function Writing and Debugging
	1. Asserts
	2. Alerting users of errors and handling problems
	3. traceback
	4. Debug
	5. Using Rstudio for debugging

16. R for "pharmacometrics"
		a. Functions to incorporate/checkout from metrumrg
			i. metaSub
			ii. Resample.data.frame
			iii. As.nm
		b. Data assembly
		o Combining vertical and horizontal criteria 
			§ Ex: automatically set an EVID value for all non-zero concentrations before the first dose stratified for each subject 
		o Dosing/simulation datasheet generation
		
			
17. Speeding up R
	1. Rprof

18. Other tidbits
	1. methods
	2. ::
	3. Introduction to data.table

Introduction to regular expressions