# js-pandoc syntax

## Javascript usage

Load the javascript file in HTML (replace `folder_path` with your path):

```<script src="folder_path/js-pandoc.js"></script>```

Then call the ```Pandoc``` function.

```javascript
	//example :
	var html = Pandoc( text );
	//example :
	var html = text.Pandoc();
```

You can specify ```options```:

```javascript
	//example :
	var html = Pandoc( text, {html:true} );
	//example :
	var html = text.Pandoc( {html5:true} );
```