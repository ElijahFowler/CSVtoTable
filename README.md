#jQuery CSV to Table
The jQuery CSV to Table plugin reads in comma separated values (CSV) or tab separated values (TSV) data and generates an HTML table.  Common spreadsheet programs, such as Microsoft Excel, are capable of saving in both CSV and TSV format.

<a href='http://honestbleeps.com/csvtotable/demo.html'>[see it in action]</a>

By calling the CSVToTable() function on a DIV, and providing the path to a CSV or TSV file to download, the plugin loads in the data and creates an HTML table.  For example, if a file called 'test.csv' contains the following data:
```
album,artist,price
"lateralus","tool",13.00
"aenima","tool",12.00
"10,000 days","tool",14.00
"down in it","nine inch nails",3.00
"broken","nine inch nails",6.00
```

A simple plugin call like:
```html
<div id="CSVTable"></div>

<script>
$(function() {
	$('#CSVTable').CSVToTable('test.csv');
});
</script>
```

Would produce:

album | artist | price
----- | ------ | -----
lateralus | tool | 13.00
aenima | tool | 12.00
10,000 days | tool | 14.00
down in it | nine inch nails | 3.00
broken | nine inch nails | 6.00

## Configurable options: ##
  * **separator** - separator to use when parsing CSV/TSV data
    * value will almost always be "," or "\t" (comma or tab)
    * if not specified, default value is ","
  * **headers** - an array of headers for the CSV data
    * if not specified, plugin assumes that the first line of the CSV file contains the header names.
    * Example: headers: ['Album Title', 'Artist Name', 'Price ($USD)']
  * **tableClass** - class name to apply to the `<table>` tag rendered by the plugin.
  * **theadClass** - class name to apply to the `<thead>` tag rendered by the plugin.
  * **thClass** - class name to apply to the `<th>` tag rendered by the plugin.
  * **tbodyClass** - class name to apply to the `<tbody>` tag rendered by the plugin.
  * **trClass** - class name to apply to the `<tr>` tag rendered by the plugin.
  * **tdClass** - class name to apply to the `<td>` tag rendered by the plugin.
  * **loadingImage** - path to an image to display while CSV/TSV data is loading
  * **loadingText** - text to display while CSV/TSV is loading
    * if not specified, default value is "Loading CSV data..."


The plugin will also trigger a "loadComplete" event upon successful render, so that you may use other jQuery plugins/code to modify the resulting table.  One such example is a jQuery tablesorter plugin like https://www.datatables.net/

The example below shows how to fire code after the loadComplete event is triggered:

```js
$('#CSVTable').CSVToTable('test.csv', {
	loadingImage: 'images/loading.gif',
	startLine: 1,
	headers: ['Album Title', 'Artist Name', 'Price ($USD)']
}).bind("loadComplete", function() {
	$('#CSVTable').find('table').dataTable();
});
```
