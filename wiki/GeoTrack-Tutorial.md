GeoTrack allows you to track the position of a user's device by receiving geoJSON posted to the server.  This allows tracking to occur even when your web application is not active in the user's browser.

###Start GeoTrack

To initiate tracking, invoke the geoTrack device command:

```html
<button onclick="bridgeit.geoTrack('tracker','handleTrack', 
    {postURL: 'http://api.bridgeit.mobi/echo/service/echoput/geotrack-tutorial'});">Track</button>
```

By default, this will cause the device position to be uploaded whenever there is significant change (such as a change in the cell tower on iOS) for a duration of one hour.  The handleTrack callback is not essential for geoTrack since the position data is uploaded directly to the server, but you may want to implement it to detect failure conditions (such as GPS being disabled for the device).

For finer control, such as continuous geolocation (only use this for testing and when attached to a power source) for a quarter hour:

```javascript
bridgeit.geoTrack('tracker','handleTrack', 
    {postURL: 'http://api.bridgeit.com/echo/echoput/geotrack-tutorial', 
    parameters: {strategy:'continuous',duration:0.25}})
```

###Fetch the position data

Once the position data is uploaded, you may process it on the server or in the browser.  For instance, to fetch the data from the echo service using jQuery:

```html
<button onclick="$.get( 'http://api.bridgeit.mobi/echo/service/echofetch/geotrack-tutorial', 
    function (data) {
        alert('coordinates ' + data[data.length - 1].geometry.coordinates);
    } )">Fetch</button>
```
Here we use an alert to display the last (most recent) coordinate entry of the geometry.coordinates field in the geoJSON structure.
