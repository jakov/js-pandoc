* idea for parallel viewing: put an `<a>` element to the position of the cursor.


# Tables

## State of the art

### Pipe Style

This table style uses the `|` ([vertical bar](http://en.wikipedia.org/wiki/Vertical_bar) symbol) to divide columns. Markdown Extra uses this style. It divides the `thead` and `tbody` through dashes (`-`) and uses colons (`:`) to set alignment. 

It's main advantage is its independence from monospace font. You can only use single-line span elements.

```
| Item      | Value |
| --------- | -----:|
| Computer  | $1600 |
| Phone     |   $12 |
| Pipe      |    $1 |
```

[MultiMarkdown](https://github.com/fletcher/MultiMarkdown/wiki/MultiMarkdown-Syntax-Guide#tables) uses repeated bars to set colspan, like this: `| two cols || one col |`. Until now there is no rowspan and neither multiline span elements nor block level elements can be used.

### Blank Style

Following a proposal by Michel Fortin on the [Markdown discussion list](http://six.pairlist.net/pipermail/markdown-discuss/2005-March/001097.html), Pandoc implemented what they call 'simple tables', where the columns are separated by blanks only, which is very beautiful.

Another great idea was to set the alignment by the placement of the header itself. This could be easily implemented in Pipe Style too.

Pandoc also supports a multi-line version, where you have to enclose the table in rows of dashes. However, you can't use block elements there, that's why Pandoc has the Grid Style tables.

```
  Right     Left     Center     Default
-------     ------ ----------   -------
     12     12        12            12
    123     123       123          123
      1     1          1             1
```

### Grid Style

This table style uses lines of dashes (`-`) to sperate the rows from each other. In the corners it uses pluses (`+`). `thead` and `tbody` are separated through equal signs (`=`).

It's main advantage is that you can freely use block level elements. This is the example grid table from the [Pandoc User Guide](http://johnmacfarlane.net/pandoc/README.html#tables). In Pandoc, there is no align yet. Also colspan and rowspan are not supported.

```
+---------------+---------------+--------------------+
| Fruit         | Price         | Advantages         |
+===============+===============+====================+
| Bananas       | $1.34         | - built-in wrapper |
|               |               | - bright color     |
+---------------+---------------+--------------------+
| Oranges       | $2.10         | - cures scurvy     |
|               |               | - tasty            |
+---------------+---------------+--------------------+
```

## My proposals

* All tables styles should get coordinates. The second cell in the third row would get the HTML attribute `class="r2 c3 re co"` with `r2` being row two, `c3` being column three, `re` being an even row and `co` being an odd column. If it would span to another cell it would get the additional classes too.

	If there is a table header in column three, e.g. 'Total revenue', then it gets cut down like a header ID in Pandoc and will be added to the classes; e.g. `class="r2 c3 re co c_total_revenue"`.


### Pipe Style

*	As it was already proposed on the Markdown discussion list, numbers next to the 	finishing bar will be interpreted like multiple bars. E.g. `| cell 7|` will be the 	same as `| cell |||||||` (with seven bars on the right). To 'escape' this behavior, 	just place a blank before the pipe: `| cell 7 |` will say 'cell 7'.

	```
	|a |b |c |d |e |f |
	|--|--|--|--|--|--|
	|r |s |t      3|u |
	|v |w         4|x |
	```
	
	```
	|a |b |c |d |e |f |
	|--|--|--|--|--|--|
	|r |s |t     |||u |
	|v |w       ||||x |
	```


* In addition to the colspan feature of MultiMarkdown, *rowspan* could be provided using `^` instead of a bar. In the following example the fruits will each span two rows:

	```
| Fruit     | Advantages       |
| --------- | ---------------- |
| Bananas   | built-in wrapper |
^           | bright color     |
| Oranges   | cures scurvy     |
^           | tasty            |
```

* Similarly, to enable multi-line content for table cells, I propose to use the apostrophe (`'`) to widen the cell vertically for writing. This will however not affect the rowspan, but provide a way to use block elements inside a table cell! Compare also a [proposal in the discussion list](http://six.pairlist.net/pipermail/markdown-discuss/2009-June/001600.html) (which I stumbled upon after my initial idea, that's why i used `'` instead of `:`. Also in my version the cells get extended *below*.).

	The following table should result in the exactly the same output as the grid table example above (even the col width should be the same), with a list for each of the fruits' advantages:

	```
| Fruit         | Price         | Advantages         |
| ------------- | ------------- | ------------------ |
| Bananas       | $1.34         | - built-in wrapper |
'               '               ' - bright color     '
| Oranges       | $2.10         | - cures scurvy     |
'               '               ' - tasty            '
```

	As you can see, there's no mixing of apostrophes and bar symbols in a line as this would lead to confusion for both the user and the parser.

* Exchanging the dashes with equal signs should set the whole column to be header elements. Thus, in the following the fruits should be contained in `<th>`-elements. It would be best to also add the `scope="row"` attribute (For the normal headers `scope="col"` should be used).

	```
| Fruit         | Price         | Advantages         |
| ============= | ------------- | ------------------ |
| Bananas       | $1.34         | - built-in wrapper |
'               '               ' - bright color     '
| Oranges       | $2.10         | - cures scurvy     |
'               '               ' - tasty            '
```

* Pipe Style Tables should also accept tabular data for easy pasting from a spreadsheet (Not yet implemented):

	```
| Fruit         | Price         | Advantages         |
| ============= | ------------- | ------------------ |
"Bananas";"$1.34";"- built-in wrapper\n- bright color";
"Oranges";"$2.10";"- cures scurvy\n- tasty";
… more data
```


### Blank Style

* As in Pipe Style equal signs should set the whole column to be header elements: (Not yet implemented)


```
  Right     Left     Center     Default
=======     ------ ----------   -------
     12     12        12            12
    123     123       123          123
      1     1          1             1
```

* In simple BlankTables, rowspan and colspan should be achieveable by pointing to the neighboring cell with a single `^` or `<`. In the example, 'Attributes' would span over 'Price' and 'Advantages' and 'Tropical' would span over both of the rows. (Not yet implemented)

```
                         Attributes                                          <
Origin   Fruit                   Price   Advantages        
=======  =============   -------------   -------------------------------------
Tropical Bananas                 $1.34   has built-in wrapper and bright color
^        Oranges                 $2.10   cures scurvy and is tasty
```


```
-----------------------------------------------------------
                         Attributes                       <
                         
Origin   Fruit                   Price   Advantages        
=======  =============   -------------   ------------------  
Tropical Bananas                 $1.34   - built-in wrapper  
                                         - bright color      

^        Oranges                 $2.10   - cures scurvy      
                                         - tasty             
-----------------------------------------------------------
```

* Doubling the symbol (`^^` or `<<`) will span until the next cell with content by skipping all empty cells. (Note that in the following table, `ö` will be ignored, because it is "below" the span of the cell continuing `u`.)

```
qwer asdf tzui jklö 
==== ---- ---- -----
q    a         <<   
w    s    z    k    
e         u    <    
r    ^^   ^    ö    
```

* typing through the whitepaces borders (the last column of spaces) should make the neighboring cells span (However this makes it a lot more complex to code!). In the example below the `u` in `Attributes` crosses the whitespace border and the `more` in `Tropical even more tropical` makes the row be non-empty only in the left cell column. (The later would conflict with an empty line deciding between "simple" and "multiline" mode!!! It could also just be a simple table with empty cells!!!). (Not yet implemented)

```
-----------------------------------------------------------
                                  Attributes               

Origin   Fruit                   Price   Advantages        
=======  =============   -------------   ------------------
Tropical Bananas                 $1.34   - built-in wrapper
even                                     - bright color    
more 
tropical Oranges                 $2.10   - cures scurvy    
                                         - tasty           
-----------------------------------------------------------
```



### Grid Style

* Every cell in a grid style table has four borders. The bottom border should be used to determine, whether the cell should be a `<th>`-cell (with `=`) or a `<td>`-cell (only `-`).

* The first row that contains a `<td>`-cell automatically ends the `<thead>` and starts the `<tbody>` (the same should apply for the footer, just the other way around which is a little more difficult, i know).

* To manually set the point where the table should be split into its head and its body (e.g. if you want to use `<td>` in the header or the footer) replace the pluses `+` with stars `*`. (Not yet implemented)

* It is obvious that the grid style could be easily used with colspan and rowspan:

```
+                          +-----------------;------------------+
                           |             Attributes             |
+==========+===============+==============:+====================+
| Origin   | Fruit         |         Price | Advantages         |
+==========+===============+===============+====================+
| Tropical | Bananas       |         $1.34 | - built-in wrapper |
|          |               |               | - bright color     |
|          +---------------+---------------+--------------------+
|          | Oranges       |         $2.10 | - cures scurvy     |
|          |               |               | - tasty            |
+==========+---------------+---------------+--------------------+
```

* Horizontal Cell alignment is also determined in the upper border[^1]. Use `+----;+` to set right alignment like in Pipe Style. `+----:+` will set the alignment for the the whole *column*. (For spanning cells only the first part of the border is used[^2]: `+===;+====+` will align right.) (Not yet implemented)

[^1]: Maybe it should be on the *bottom* border to be more consistent with Pipe Style?!
[^2]: Not yet implemented, until now the whole border is used.

	* `;----` will align the cell below it *left*.
	* `----;` will align the cell below it *right*.
	* `--;--` will align the cell below it *centered*[^center]
	* `;---;` will align the cell below it *justified*. (Maybe this is not needed and 	  should instead align *centered*).	

[^center]: the `;` can be anywhere in the middle and there can be more than just one symbol.

* Vertical align is determined by the left border. Just as with before, `;` sets the align only for a single cell, whereas `:` sets the vertical align for the whole *row*

	* `;||||` (vertically) will align the cell right to it *top*.
	* `||||;` (vertically) will align the cell right to it *bottom*.
	* `;|||;` (vertically) will align the cell right to it *middle*.
	* `||;||` (vertically) will align the cell right to it *middle*; [^center]
	

* You should be able to not type the bars and the dashes if you are lazy. Only the pluses must be typed. If there is a non-border symbol between two pluses (vertically or horizontally) the two cells will span. To manually set span just use `-+-` or `|+|` (vertically) on the right or bottom side.

	In the example below, *D* and *E* as well as *H* and *I* (because *J* is in the line between the pluses) span horizontally, *C* and *F* span vertically.
	
	Note that the line with the equal signs must not contain `=+=`, otherwise it would trigger colspan. (Buggy)


```
+   +   +   +
  0   1   2
+ = + = + = +
  A   B   C |
+   +   +   +
  D   E   F |
+  -+-  +   +
  G   H J I  
+   +   +   +
```




### Table Glue
Sometimes a table might exceed the character width of you editor resulting in a mess like this (soft wrapped of course; for the example i hard-wrapped at 40 chars):

```
+---------------+---------------+-------
-------------+ | Fruit         | Price  
      | Advantages         |
+===============+===============+=======
=============+ | Bananas       | $1.34  
      | - built-in wrapper | |          
    |               | - bright color    
|
+---------------+---------------+-------
-------------+ | Oranges       | $2.10  
      | - cures scurvy     | |          
    |               | - tasty           
|
+---------------+---------------+-------
-------------+
```

You might want to split your table (just in your editor) and tell the parser to glue it back together side by side: (Not yet implemented)

```
+---------------+---------------+
| Fruit         | Price         |
+===============+===============+
| Bananas       | $1.34         |
|               |               |
+---------------+---------------+
| Oranges       | $2.10         |
|               |               |
+---------------+---------------+
~
+--------------------+
| Advantages         |
+====================+
| - built-in wrapper |
| - bright color     |
+--------------------+
| - cures scurvy     |
| - tasty            |
+--------------------+
```

You should be able to glue all kinds of tables together, e.g. mix a grid tables with a Pipe table (so you don't have to change all of it when you combine them). Therefore a symbol for vertical combination might be needed too; I suggest `*` for vertical glue. (Not yet implemented)

Like this you could also write columns **below** each other, which is a lot easier to edit in simple notepads and is *independent from monospaced adjustment*. The 'simple table' example from the Pandoc Readme would get:

```
  Right
-------
     12
    123
      1

~

Left
------
12
123
1
      
~

  Center
----------
   12
   123
    1
    
~

Default
-------
    12
   123
     1

Table:  Demonstration of simple table syntax.
```

### Table caluclations

* Like in a spreadsheet, there should be a syntax for performing some simple calculations, e.g. `{= 3+5 =}` should simply output `8`.

* Inside a table `{= #2_3 =}` should reference to the 3rd cell in the 2nd row. Outside of it you should be able to reference it by `{= tableid#2_3 =}`.

	`{= #2_3:#3_6 =}` should return an array of the cells in that area, so that you can perform calculations like `{= #2_3:#3_6.sum() =}`.

# Smart smart punctuation

* There should be a way to set the language (using the [ISO 693-3 codes](http://en.wikipedia.org/wiki/ISO_639-3) like `eng`) for the 'smart punctuation' function. It would be the best to be able to set the language for a single paragraph (like a quote) or even for a single quotation `"le mot"{:fra}` should be parsed as `« le  mot »`.

* Alternatively there should be a way to change the language at a certain point in the document e.g. `{deu:}`, so that all coming quotes will be parsed in that language. There would be no need for a closing entity as you can simply change back to english anywhere in the document.