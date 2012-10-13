# Pandoc Todo List

## Todo
* Escaping!
* Delimited code blocks
* --section-divs
* --toc|--table-of-contents

* automatic align in whitespace tables
* overrule align in whitespace tables
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
	+ use `|` if you don't have text to span the lines. If there is nothing else in the 	  same line, the symbol will not be displayed. Alternatively, you can also use `^` to point to the cell above (use `^^` to point to the next non-empty cell).
		
		```
		-----------------------------------------------------------
	                                  Attributes                   
		                                                           
		Origin   Fruit                   Price   Advantages        
		======== =============   -------------   ------------------
		Tropical Bananas                 $1.34   - built-in wrapper
		|                                        - bright color    
		|                                                              
		|        Oranges                 $2.10   - cures scurvy    
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
	
	
	
* whitespace tables rowspan?!? Awsome!!!

```
---
1111 2222 mmmm
---- ---- ----
3333 4444 nnnn
5555 6666 oooo

7777 8888 pppp

99999aaaa qqqq
wwww xxxx yyyy

bbbbbcccc rrrr
dddd eeee ssss

ffff gggg tttt
hhhhhjjjj uuuu
kkkk llll vvvv

ffff gggggtttt
hhhh jjjj uuuu
kkkkkllll vvvv

ffff gggggtttt
hhhh jjjj  ^  
kkkkkllll vvvv

ffff gggggtttt
hhhh  ^    ^    
kkkkkllll vvvv

ffff gggggtttt
hhhh          
kkkk llll vvvv

edgecasebelow:

span one    
cell      two
----
```

```
--------------
1111 2222 mmmm
---- ---- ----
a a a a a * bb
          * bb
* cc dddd * bb
* cc      * bb
* cc      * bb
* cc
* cc eeeeeeeee
--------------
```

* how to handle the edge case on the bottom?!? Empty cells!

* optionally delay parsing with the time needed for parsing the last time, e.g. 300ms parsing => 300ms delay after last keyup (which is reset by another keyup): If you type quick enough, the parsing only starts after you finished typing.

* pipe tables multispan, e.g. `| seven cells span 7|`

* elastic tabstop tables should behave differently (`--->` symbolizes the tabs):

	Until now:
	
	```
	header one------------------->header two>header three
	cell one with large content-->---------->cell three
	```

	How it should be:
	
	```
	header one-------->header two>header three
	cell one with large content->>cell three	
	```
	
	That means that empty "cells" should behave like *cellspan*, which can be escaped by placing a blank in that cell.
	
	Until then, use `<` for colspan.
	
* different classes for `thead` and `tbody`, e.g. `hr1` for first row in head, `bra` for first row in body etc.

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