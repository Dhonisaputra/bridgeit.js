This tutorial will show the basic usage of the BridgeIt beacons API. The Beacons BridgeIt feature allows a web application to detect nearby iBeacons. For more information on the underlying technology of iBeacons, please refer to the Apple [documentation](http://support.apple.com/kb/HT6048).

*Please Note:* The beacons api is currently only available on iOS7.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.beacons()` call to an element
```html
<a id='beaconsBtn' type="button" 
   onclick="bridgeit.beacons('id', 'callback', options);">Detect Nearby Beacons</a>
```

### Add the `id` argument
```html
<a id='beaconsBtn' type="button" 
   onclick="bridgeit.beacons('beaconsBtn', 'callback', options);">Detect Nearby Beacons</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'beaconsBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='beaconsBtn' type="button" 
   onclick="bridgeit.beacons('beaconsBtn', 'onAfterBeaconScan', options);">Detect Nearby Beacons</a>
```
BridgeIt will invoke the callback after the audio has been captured. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterBeaconScan'.

### Add the `{options}` argument
```html
<a id='beaconsBtn' type="button" 
   onclick="bridgeit.beacons('beaconsBtn', 'onAfterBeaconScan', {beacons: [{uuid: 'E2C56DB5-DFFB-48D2-B060-D0F5A71096E0',name: 'BridgeItBeacon'}]});">
    Detect Nearby Beacons
</a>
```
The options argument will specify parameters for the BridgeIt native command. Here we're specifying the 'beacons' argument, which is a list of beacons to scan for. For beacons to be scannable, they must be identified by their UUIDs prior to scanning. The optional 'name' parameter, can also be supplied for display purposes.  

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterBeaconScan(event){   
    var beacons = event.value,
        beaconsString = '';
    for (var i = 0; i < beacons.length; i++)  {
        beaconsString += beacons[i].name;
        beaconsString += ' UUID: ' + beacons[i].uuid;
        beaconsString += '(' + beacons[i].major + "," + beacons[i].minor + ')';
        beaconsString += beacons[i].proximity;
        beaconsString += 'Accuracy: ' + parseFloat(beacons[i].accuracy).toFixed(2) + 'm';
    }
    alert('Beacons Found: ' + beaconsString);
}
</script>
```
BridgeIt will invoke the callback once the beacon scanning is complete. An event object is passed as an argument to the callback, and will include a 'value' array, which will include a list of detected beacons, each item containing various identification and location information for the beacon. This information can be inspected by the application. 

### `event.value`
The response from the server will be passed back to the web application in the event.value property. 
