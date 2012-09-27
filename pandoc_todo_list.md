# Pandoc Todo List

## Todo
* Delimited code blocks
* --section-divs
* --toc|--table-of-contents
* > ## Ordered
> 
> Tight:
> 
> 1.	First
> 2.	Second
> 3.	Third
> 
> and:
> 
> 1. One
> 2. Two
> 3. Three

* automatic align in simple tables
* footers for whitespace-tables

* "whitespace" tables rowspan


	```
	-----------------------------------------------------------
                                  Attributes                   
	                                                           
	Origin   Fruit                   Price   Advantages        
	======== =============   -------------   ------------------
	Tropical Bananas                 $1.34   - built-in wrapper
	even                                     - bright color    
	more                                                       
	tropical Oranges                 $2.10   - cures scurvy    
	                                         - tasty           
	-----------------------------------------------------------
	```
	+ use `^` if you don't have text to span the lines. If there is nothing else in the 	  same line, the symbol will not be displayed. If the line above is empty, it is 	  treated like an 'arrow', thus only the last `^` in the example is needed.
		
		```
		-----------------------------------------------------------
	                                  Attributes                   
		                                                           
		Origin   Fruit                   Price   Advantages        
		======== =============   -------------   ------------------
		Tropical Bananas                 $1.34   - built-in wrapper
		^                                        - bright color    
		^                                                              
		^        Oranges                 $2.10   - cures scurvy    
		                                         - tasty           
		-----------------------------------------------------------
		```
	+ example of both colspan and rowspan (`ö` should be part of the cell that contains `uxxxxxxxxx\n y         \n y    ö    `):
	
		```
		--------------------
		qwer asdf tzui jklö 
		==== ---- ---- ----
		q    axxxxxxxxxxxxx
		 
		w    s    z    k    
		     y
		e    y    uxxxxxxxx
		     y    y         
		r    y    y    ö    
		 
		--------------------
		```
		
		```
		+----+----+----+----+
		|qwer|asdf|tzui|jklö|
		+====+====+====+====+
		|q   |axxxxxxxxxxxxx|
		+----+----+----+----+
		|w   |s   |z   |k   |
		+----+y   +----+----+
		|e   |y   |uxxxxxxxx|
		+----+y   |y        |
		|r   |y   |y    ö   | 
		+----+----+---------+
		```
		debug!!!
	
	script idea: split in lines, then append to above *if not empty*. Use coordinates and 	skip empty lines. Make an array that saves information about the row above, e.g. `[' ', '^', '<']` for 'new', 'add to above' and 'add to above left'. The table should be parsed line by line (not column by column)!
	
	
	
* whitespace tables rowspan?!?
* pipe tables multispan, e.g. `| seven cells span 7|`

### This should behave differently
asdf

1. one

2. two
3. three

qwer

1. asdf
b. qwer


## Completed
* Header identifiers
* require a blank line before a header
* require a blank line before a block quote

# Markdown Extra Todo List