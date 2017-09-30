This tutorial will show the basic usage of the BridgeIt camera API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.camera()` call to an element
```html
<a id='cameraBtn' type="button" 
   onclick="bridgeit.camera('id', 'callback', options);">Take a Photo</a>
```

### Add the `id` argument
```html
<a id='cameraBtn' type="button" 
   onclick="bridgeit.camera('cameraBtn', 'callback', options);">Take a Photo</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'cameraBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='cameraBtn' type="button" 
   onclick="bridgeit.camera('cameraBtn', 'onAfterPhotoCapture', options);">Take a Photo</a>
```
BridgeIt will invoke the callback after the image has completed uploading. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterPhotoCapture'.

### Add the `{options}` argument
```html
<a id='cameraBtn' type="button" 
   onclick="bridgeit.camera('cameraBtn', 'onAfterPhotoCapture', {postURL:'/upload'});">Take a Photo</a>
```
The options argument will specify parameters for the BridgeIt native command. For the camera call, you must specify the server-side upload target URL. After a photo is captured, BridgeIt will use this URL to send the image in an HTTP multipart form POST to the server. 

BridgeIt provides an Echo service at http://api.bridgeit.mobi/echo. Media resources may be stored and re-served from here, if you would like to use the BridgeIt service. For instance, photos can be uploaded to http://api.bridgeit.mobi/echo/blob/. This service will return a URL identifying the image, such as 'http://api.bridgeit.mobi/echo/store/d0edf3a3-79ae-4075-b567-7539496007ff'. The client could then request the image from http://api.bridgeit.mobi/echo/store/d0edf3a3-79ae-4075-b567-7539496007ff. The Gist at the end of the tutorial includes the BridgeIt Echo service URL.

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterPhotoCapture(event){
    var id = event.name;
    var cameraBtn = document.getElementById(id);
    if (event.preview)  {
        //show the thumbnail preview
        var thumbnailElem = document.createElement("img");
        thumbnailElem.setAttribute("src", event.preview);
    }
    if (event.response)  {
        //show the image
        //assume the server is sending back the url of the uploaded image
        var photoURL = event.response; 
        var imageLink = document.createElement('a');
        imageLink.setAttribute('href', photoURL);
        //set the thumbnail img as the link child
        imageLink.appendChild(thumbnailElem);
        //append the new link after the camera btn
        cameraBtn.parentNode.appendChild(imageLink);
    }
}
</script>
```
BridgeIt will invoke the callback once the image has been uploaded to the server. An event object is passed as an argument to the callback and, if the upload was successful, will contain an image preview URL (as a data URL), as well as the response from the server. 

### `event.preview`
BridgeIt will generate a thumbnail preview of the image, and pass that back to the web application as a data URL in the event.preview property.

### `event.value`
The response from the server will be passed back to the web application in the event.value property. 

### Server-side Upload Handling
BridgeIt will post the captured photo to the specified options.postURL camera argument. You may create your own upload handler or use a public upload service, such as http://api.bridgeit.mobi/echo/. 

Please see [Media Upload Handling](https://github.com/bridgeit/bridgeit.js/wiki/Media-Upload-Handling) for more information.

### Error Handling


[Get the Camera Tutorial Gist](https://gist.github.com/philipbreau/7555046)

  

