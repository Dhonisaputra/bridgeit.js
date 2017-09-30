This tutorial will show the basic usage of the BridgeIt microphone API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.microphone()` call to an element
```html
<a id='micBtn' type="button" 
   onclick="bridgeit.microphone('id', 'callback', options);">Record Audio</a>
```

### Add the `id` argument
```html
<a id='micBtn' type="button" 
   onclick="bridgeit.microphone('micBtn', 'callback', options);">Record Audio</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'micBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='micBtn' type="button" 
   onclick="bridgeit.microphone('micBtn', 'onAfterAudioCapture', options);">Record Audio</a>
```
BridgeIt will invoke the callback after the audio has uploaded. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterAudioCapture'.

### Add the `{options}` argument
```html
<a id='micBtn' type="button" 
   onclick="bridgeit.microphone('micBtn', 'onAfterAudioCapture', {postURL:'/upload'});">Record Audio</a>
```
The options argument will specify parameters for the BridgeIt native command. For the microphone call, you must specify the server-side upload target URL. After an audio recording is captured, BridgeIt will use this URL to send the audio file in an HTTP multipart form POST to the server. 

BridgeIt provides an Echo service at http://api.bridgeit.mobi/echo. Media resources may be stored and re-served from here, if you would like to use the BridgeIt service. For instance, audio can be uploaded to http://api.bridgeit.mobi/echo/blob/. This service will return a URL identifying the audio, such as 'http://api.bridgeit.mobi/echo/store/d0edf3a3-79ae-4075-b567-7539496007ff'. The client could then request the audio from http://api.bridgeit.mobi/echo/store/d0edf3a3-79ae-4075-b567-7539496007ff. The Gist at the end of the tutorial includes the BridgeIt Echo service URL.

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterAudioCapture(event){   
    if (event.response)  {
        var btn = document.getElementById('micBtn');
        var audioSrc = event.response;
        var audioElem = document.createElement('audio');
        audioElem.setAttribute('src',  audioSrc);
        audioElem.setAttribute('controls', 'controls');
        audioElem.setAttribute('preload', 'auto');
        audioElem.setAttribute('type', 'audio/mp3');
        micBtn.parentNode.appendChild(audioElem);
    }
}
</script>
```
BridgeIt will invoke the callback once the audio has been uploaded to the server. An event object is passed as an argument to the callback and, if the upload was successful, will contain the response from the server. 

### `event.value`
The response from the server will be passed back to the web application in the event.value property. 

### Server-side Upload Handling
BridgeIt will post the captured audio to the specified options.postURL camera argument. You may create your own upload handler or use a public upload service, such as http://api.bridgeit.mobi/echo/. 

Please see [Media Upload Handling](https://github.com/bridgeit/bridgeit.js/wiki/Media-Upload-Handling) for more information.

### Error Handling


[Get the Microphone Tutorial Gist](https://gist.github.com/philipbreau/7760631)