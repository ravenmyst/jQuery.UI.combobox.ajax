# jquery.ui.combobox.ajax.js

This is an easy to implement tiny jQuery UI Widget that spawns a combobox that allows a user to search, select, from a select list, and throttles ajax calls against a datasource! <a href="https://ravenmyst.net/work/combobox/" target="_blank">Demo/Example here</a>

```javascript
$( document ).ready(function() {
	initializeComboBox('data.php', 'getItems', 'item_id', 'Select or type an item..');
	$( "#items" ).combobox();
});

```

**initializeComboBox()**

| Parameter  | Description |
| ------------- | ------------- |
| path | relative path to datasource file |
| method | the invoked function in the file |
| html element | html element that stores the current selection |
| placeholder text | the default text that appears in the select input |

To integrate a select element with this widget, insert this html markup:
```html
<form action="./" id="searchForm" method="post">
	<input type="hidden" name="item_id" id="item_id">
	Item ID: 
	<select id="items" size="25">
	<option selected="selected">{item.LABEL}</option>
	</select>
</form>
```

The data that results from the Ajax call must be an array of objects, structured with these attributes, then delivered as a JSON. Your implementation may vary depending on language used:
```php
// basic php example of the array of objects structure
<?php
	// this function name must match the name of the method above
	function getItems() {
		result = [];
		// when included in the array, selecting 0 will reset combobox to default state
		$obj = [];
		$obj["VALUE"] = 0;
		$obj["LABEL"] = "- None -";
		array_push($result, $obj);
		$obj["VALUE"] = 1;
		$obj["LABEL"] = "Item 1";
		array_push($result, $obj);
		$obj["VALUE"] = 2;
		$obj["LABEL"] = "Item 2";
		array_push($result, $obj);

		// ensure the header sent via Ajax is a JSON.
		header("Content-type:application/json");
		echo json_encode($result_array);
	}
?>
```
To filter the query results, use this GET variable:
```
term
```

For a full working code example, check <a href="https://github.com/ravenmyst/jQuery.UI.Combobox.Ajax/blob/master/example/data.php" target="_blank">/examples/data.php</a>