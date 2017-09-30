Several BridgeIt commands, such as camera, camcorder and microphone rely on a server-side upload handler to store the uploaded files. This is specified in the options.postURL parameter of these bridgeit.js functions. 

BridgeIt will send an HTTP multi-part POST, which includes the captured media to the server. You can handle this multi-part post with a custom server-side handler, implemented in any platform language, such as Java or PHP, or you can use a public upload service, such as api.bridgeit.mobi/storage. 

[BridgeIt Storage Service Docs](https://github.com/bridgeit/bridgeit.io.js/blob/gh-pages/docs/bridgeit-storage-service.md)
