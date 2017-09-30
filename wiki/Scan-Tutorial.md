This tutorial will show the basic usage of the BridgeIt scan API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.scan()` call to an element
```html
<a id='scanBtn' type="button" 
   onclick="bridgeit.scan('id', 'callback');">Scan a Code</a>
```

### Add the `id` argument
```html
<a id='scanBtn' type="button" 
   onclick="bridgeit.scan('scanBtn', 'callback');">Scan a Code</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'scanBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='scanBtn' type="button" 
   onclick="bridgeit.scan('scanBtn', 'onAfterCaptureScan');">Scan a Code</a>
```
BridgeIt will invoke the callback after the scan is complete. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterCaptureScan'.

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterCaptureScan(event)  {
    var text = event.value;
    var scans = document.getElementById("scans");
    var row1 = document.createElement('div');
    row1.setAttribute('class','row');
    row1.innerHTML = text;
    scans.insertBefore(row1, scans.firstChild);
}
</script>
```
BridgeIt will invoke the callback after the scan is complete. An event object is passed as an argument to the callback and, if the scan was successful, will contain the QR Code. 

### `event.value`
The QR Code will be passed to the web application in the event.value property. 

  

