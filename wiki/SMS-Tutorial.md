This tutorial will show the basic usage of the BridgeIt SMS API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.sms()` call to an element
```html
<a id='smsBtn' type="button" 
   onclick="bridgeit.sms('number', 'message');">Send an SMS</a>
```

### Add the `number` argument
```html
<a id='smsBtn' type="button" 
   onclick="bridgeit.sms(document.getElementById('smsnumber').value, 'message');">Send an SMS</a>
```
The SMS message will be sent to the number. 

### Add the `message` argument
```html
<a id='smsBtn' type="button" 
   onclick="bridgeit.sms(document.getElementById('smsnumber').value, document.getElementById('smsmessage').value);">Send an SMS</a>
```
This is the message sent to the number using SMS.

### SMS
On iOS and Android devices (Android supported since BridgeIt 1.04), a native SMS call is made through the BridgeIt utility app. On other platforms an SMS URL protocol is used in a DOM anchor element, which the browser may use to launch the device SMS functionality, if available.