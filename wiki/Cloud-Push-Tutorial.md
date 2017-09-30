This tutorial will show the basic usage of the BridgeIt cloud push API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### `bridgeit.usePushService()`
```html
var cloudPushReady;
    
if (!cloudPushReady)  {
    bridgeit.usePushService( window.pushHub, window.apiKey);
    cloudPushReady = true;
}
```
This javascript will configure and connect to the push service.
  
### `bridgeit.register()`
```html
if (!cloudPushReady)  {
    bridgeit.usePushService( window.pushHub, window.apiKey);
    cloudPushReady = true;
    bridgeit.register('_reg', 'handlePushRegistration');
}
```
This call will register a Cloud Push ID of the device so that notifications can be delivered when the user is not currently viewing your application in the browser.

The callback function will be called when Cloud Push registration completes.

### `bridgeit.addPushListener()`
```html
if (!cloudPushReady)  {
    bridgeit.usePushService( window.pushHub, window.apiKey);
    bridgeit.addPushListener(bridgeit.getId(), 'handlePush');
    cloudPushReady = true;
    bridgeit.register('_reg', 'handlePushRegistration');
}
```
Add a listener for notifications belonging to the specified group.

Any string can be used to uniquely identify a group.  In this instance we are using "bridgeit.getId()" for the group name.  This will return a persistent id that allows the application to persistently maintain information for an individual user without requiring a server-side session.

Callbacks must be passed by name to receive cloud push notifications.  In this case, our callback is the method "handlePush". 

### Add the `callback function`
```html
<script type="text/javascript">
function handlePush()  {
    document.getElementById('pushResult').firstChild.firstChild.innerText = 'Push Received';
}
</script>
```
BridgeIt will invoke the callback once the push notification is received. 

### Perform Push `bridgeit.push()`
```html
<a id="pushBtn" type="button"
    onclick="performPush();">Push</a>

function performPush()  {
    bridgeit.push( bridgeit.getId(),
        {subject:'BridgeIt Cloud Push',
        detail:'You have been notified.',
        url: bridgeit.cloudPushReturnURL()} );
}
```
This will result in an Ajax Push (and associated callback) to any web pages that have added a push listener to the specified group.  In this instance, we are pushing to ourselves using the bridgeit.getId() group.

If Cloud Push options are provided (options.subject and options.detail) a Cloud Push will be dispatched as a home screen notification to any devices unable to receive the Ajax Push via the web page.

bridgeit.cloudPushReturnURL(url) is used to augment a URL so that callbacks will be invoked upon Cloud Push return.  In this case it is called with no argument, meaning the current URL is used.


  

