* idea for parallel viewing: put an `<a>` element to the position of the cursor.

Tables until now:

FirstHeader|SecondHeader
-------------|-------------
ContentCell|ContentCell
ContentCell|ContentCell

| First Header  | Second Header |
| ------------- | ------------- |
| Content Cell  | Content Cell  |
| Content Cell  | Content Cell  |

| Item      | Value |
| --------- | -----:|
| Computer  | $1600 |
| Phone     |   $12 |
| Pipe      |    $1 |

---

New tables idea:

* Write columns *below* each other
* Use a symbol (e.g. `~`) to append a column to the right of a table
* You can also glue two tables together side by side

```

head A
-------
A1
A2
A3

~

head B with colspan
-----
B1
B2
B3

~

>
-----
C1 with rowspan
^
C3
```

The *simple table* example from the Pandoc Readme:

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


----

```
th | Item      | Value |
===|-----------|------:|
th |: * Computer  | $1600 |
   ^  * Computer
   ^  * Computer
th | Phone     |   $12 |
   ' Phone     |;$12   |
   ' Phone     | $12   |
   | Pipe             ||
===|-----------|------:|
ft | footer    | asdf  |
```

```
th | Item      | Value |
===+-----------+------:+
th |: * Computer  | $1600 |
   '  * Computer
   '  * Computer
th | Phone     |   $12 |
   ^ Phone     |;$12   |
   ^ Phone     | $12   |
   | Pipe             ||
===+-----------+------:+
ft | footer    | asdf  |
```

```
th ? td | td | td
```

instead of "|" also accept ";" and tab
http://en.wikipedia.org/wiki/Comma-separated_values

*.csv support in tables

instead of "!" use "\"?

```
th | Item      | Value |
===+-----------+------:+
th;td;td;
th;td;td;
th;td;td;
th;td;td;
===+-----------+------:+
ft | footer    | asdf  |


th | Item      | Value |
===+-----------+------:+
+:file.csv
===+-----------+------:+
ft | footer    | asdf  |

```

gridtables:

```
+-----------+-------+
| Item      | Value | thead
+===========+=======+

: Computer  | $1600 | tbody
| Computer  |       |
| Computer  |       |
+-----------+-------+
| Phone     |   $12 |
| Phone     +;------+
| Phone     | $12   |
|           +-------+
|           | $12   |

+----------;+-------+
| Pipe     ^!       | tfoot
+===================+
```

```
+           +       +
  Item        Value  
#===========#=======#
: Computer    $1600  
  Computer           
  Computer           
+           +       +
  Phone         $12  
  Phone     +;      +
  Phone       $12    
            +       +
              $12    
#          ;#       #
  Pipe     ^!        
+===================+
```

```
+           +       +
  Item        Value  
+===========+=======+

: Computer    $1600  
  Computer           
  Computer           
+           +       +
  Phone         $12  
  Phone     +;      +
  Phone       $12    
            +       +
              $12    
              
+          ;+       +
  Pipe     ^!        
+===================+
```

```
+           +       +
  Item        Value  
~===========~=======~
: Computer    $1600  
  Computer           
  Computer           
+           +       +
  Phone         $12  
  Phone     +;      +
  Phone       $12    
            +       +
              $12    
~          ;~       ~
  Pipe     ^!        
+===================+
```

```
+           +       +
  Item        Value  
#===========#=======#
: Computer    $1600  
  Computer           
  Computer           
+           +       +
  Phone         $12  
  Phone     +;      +
  Phone       $12    
            +       +
              $12    
#          ;#       #
  Pipe     ^!        
+===================+
```

```
+-----------+-------+
| Item      | Value | thead
~===========~=======~
: Computer  | $1600 | tbody
| Computer  |       |
| Computer  |       |
+-----------+-------+
| Phone     |   $12 |
| Phone     +;------+
| Phone     | $12   |
|           +-------+
|           | $12   |
~----------;~-------~
| Pipe     ^!       | tfoot
+===================+
```

```
+-----------+-------+
| Item      | Value | thead
+===========+=======+

: Computer  | $1600 | tbody
| Computer  |       |
| Computer  |       |
+-----------+-------+
| Phone     |   $12 |
| Phone     +;------+
| Phone     | $12   |
|           +-------+
|           | $12   |

+----------;+-------+
| Pipe     ^!       | tfoot
+===================+
```

```
+-----------+-------+
| a         | b     |
+===========+=======+
| c         | d     |
+-----------+-------+
| e         | f     |
+===========+=======+
| Pipe              |
+-------------------+
```
forced "  " newline style not in cells!
=> use "\"$ instead! However, in MMD this is not possible as it would escape the "|"? ==> "\ "$

"\|" should escape! in js-markdown-extra!!!

| 1
! 2
' 3

| Pipe             ||
!        |

+----++----+
| th || td | ?
+----++----+

+-------------------+
|   b l a h s o m e |
+:==========+=======+
| Item      | Value |
+:==========+======:+


+-----------+-------+
| Phone     |   $12 |
| Phone     +;------+
| Phone     | $12   |
|           +-------+
|           | $12   |
+-----------+-------+
| summe: =:#2_1:2_3 |
+-------------------+