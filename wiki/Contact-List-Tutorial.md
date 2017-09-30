This tutorial will show the basic usage of the BridgeIt contact list API.

Please see the [Getting Started](https://github.com/bridgeit/bridgeit.js/wiki/Getting-Started) wiki page for information on how to add BridgeIt support to your web app.

### Add the `bridgeit.fetchContact()` call to an element
```html
<a id='contactListBtn' type="button" 
   onclick="bridgeit.fetchContact('id', 'callback');">Fetch a Contact</a>
```

### Add the `id` argument
```html
<a id='contactListBtn' type="button" 
   onclick="bridgeit.fetchContact('contactListBtn', 'callback');">Fetch a Contact</a>
```
The id will be used by BridgeIt as the HTTP Post form element name, and will also be passed back to the client in the callback. 

We'll call our id 'contactListBtn', which is also the id of the button (although it isn't necessary to match these ids).

### Add the `callback` argument
```html
<a id='contactListBtn' type="button" 
   onclick="bridgeit.fetchContact('contactListBtn', 'onAfterReturnFromContacts');">Fetch a Contact</a>
```
BridgeIt will invoke the callback after the contact is fetched from the device. The callback should be passed in as a string, rather than as a function reference, or anonymous function, so that the callback can be stored and later invoked by name on platforms that require a page refresh, such as Android. 

We'll call our callback 'onAfterReturnFromContacts'.

### Optional `{options}` argument
The options argument will specify parameters for the BridgeIt native command. You can specify the contact fields to retrieve.  Default = {fields:"name,email,phone"}.

### Add the `callback function`
```html
<script type="text/javascript">
function onAfterReturnFromContacts(event)  {
    if( event.value ){
        var text = unescape(event.value);

        var record = bridgeit.url2Object(text);
        var elem = document.getElementById('contacts');
        var ul = document.createElement('ul');
        ul.setAttribute('data-role', 'listview');
        ul.setAttribute('data-inset', 'true');
        ul.setAttribute('data-divider-theme','d');
        var recordHTML = '';
        for (var key in record)  {
            recordHTML += "<li><span class='ellipsis'><strong>" 
            + key + ": </strong>" + record[key] + "</span></li>";
        }
        ul.innerHTML = recordHTML;
        $(elem).prepend(ul);
        $('#contacts ul:first-child').listview().listview('refresh');
    }
}
</script>
```
BridgeIt will invoke the callback after the contact is fetched from the device. An event object is passed as an argument to the callback and, if the contact was fetched, will contain the contact information. 

### `event.value` and `bridgeit.url2Object(encoded)`
The contact fields will be passed to the web application in the event.value property.  BridgeIt provides the url2Object(encoded) utility method to unpack the url-encoded parameters into an object.  By default this object will contain name, email and phone values unless other fields have been specified with the optional "{options}" argument. 

  

