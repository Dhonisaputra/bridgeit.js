This tutorial will show the basic usage of the BridgeIt camcorder API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.camcorder()` call to an element
```html
<a id='camcorderBtn' type="button" 
   onclick="bridgeit.camcorder('id', 'callback', options);">Record Video</a>
```

### Add the `id` argument
```html
<a id='camcorderBtn' type="button" 
   onclick="bridgeit.camcorder('camcorderBtn', 'callback', options);">Record Video</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'camcorderBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='camcorderBtn' type="button" 
   onclick="bridgeit.camcorder('camcorderBtn', 'onAfterVideoCapture', options);">Record Video</a>
```
BridgeIt will invoke the callback after the video has uploaded. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterVideoCapture'.

### Add the `{options}` argument
```html
<a id='camcorderBtn' type="button" 
   onclick="bridgeit.camcorder('camcorderBtn', 'onAfterVideoCapture', {postURL:'/upload'});">Record Video</a>
```
The options argument will specify parameters for the BridgeIt native command. For the camcorder call, you must specify the server-side upload target URL. After a video is captured, BridgeIt will use this URL to send the video file in an HTTP multipart form POST to the server. 

BridgeIt provides an Echo service at http://api.bridgeit.mobi/echo. Media resources may be stored and re-served from here, if you would like to use the BridgeIt service. For instance, video can be uploaded to http://api.bridgeit.mobi/echo/blob/. This service will return a URL identifying the image, such as 'http://api.bridgeit.mobi/echo/store/d0edf3a3-79ae-4075-b567-7539496007ff'. The client could then request the video from http://api.bridgeit.mobi/echo/icemobile-store/d0edf3a3-79ae-4075-b567-7539496007ff. The Gist at the end of the tutorial includes the BridgeIt Echo service URL.

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterVideoCapture(event){   
    if (event.preview)  {
        //show the thumbnail preview
        var thumbnailElem = document.createElement('img');
        thumbnailElem.setAttribute('src', event.preview);
    }
    if (event.response)  {
        //show a link to the video
        //assume the server is sending back the url of the uploaded video
        var videoURL = event.response; 
        var videoLink = document.createElement('a');
        videoLink.setAttribute('href', videoURL);
        //set the thumbnail img as the link child
        videoLink.appendChild(thumbnailElem);
        //append the new link after the camcorder btn
        var btn = document.getElementById('camcorderBtn');
        btn.parentNode.appendChild(imageLink);
    }
}
</script>
```
BridgeIt will invoke the callback once the video has been uploaded to the server. An event object is passed as an argument to the callback and, if the upload was successful, will contain an image preview URL (as a data URL), as well as the response from the server. 

### `event.preview`
BridgeIt will generate a thumbnail preview of the image, and pass that back to the web application as a data URL in the event.preview property.

### `event.value`
The response from the server will be passed back to the web application in the event.value property. 

### Server-side Upload Handling
BridgeIt will post the captured video to the specified options.postURL camera argument. You may create your own upload handler or use a public upload service, such as http://api.bridgeit.mobi/echo/. 

Please see [Media Upload Handling](https://github.com/bridgeit/bridgeit.js/wiki/Media-Upload-Handling) for more information.

### Error Handling


[Get the Camcorder Tutorial Gist](https://gist.github.com/philipbreau/7567384)

  
