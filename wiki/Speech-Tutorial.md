This tutorial will show the basic usage of the BridgeIt speech-to-text and text-to-speech API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.speech()` call to an element
```html
<a id='speechBtn' type="button" 
   onclick="bridgeit.speech('id', 'callback', options);">Speak</a>
```

### Add the `id` argument
```html
<a id='speechBtn' type="button" 
   onclick="bridgeit.speech('speechBtn', 'callback', options);">Speak</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'speechBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='speechBtn' type="button" 
   onclick="bridgeit.speech('speechBtn', 'onAfterAudioCapture', options);">Speak</a>
```
BridgeIt will invoke the callback after the audio has been captured. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterAudioCapture'.

### Add the `{options}` argument
```html
<a id='speechBtn' type="button" 
   onclick="bridgeit.speech('speechBtn', 'onAfterAudioCapture', {text:'What is your password?', respond: true});">Speak</a>
```
The options argument will specify parameters for the BridgeIt native command. Here we're specifying the 'text' argument, which is what BridgeIt will speak, and setting 'respond' to true, so that BridgeIt will wait for the user to respond. You may also specify other parameters, such as rate, pitch, and volume. After the audio is captured, BridgeIt will convert the words spoken by the user to text and pass this information back to the web app. 

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterAudioCapture(event){   
    var answer = event.value;
    if (answer)  {
        alert(answer);
    }
}
</script>
```
BridgeIt will invoke the callback once the audio has been converted to text. An event object is passed as an argument to the callback, and will include the property 'value', which can be inspected by the application. 

### `event.value`
The response from the server will be passed back to the web application in the event.value property. 

