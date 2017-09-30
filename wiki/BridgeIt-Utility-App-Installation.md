In order to provide native mobile features to the web application, BridgeIt relies on a native utility app being installed on the mobile device. The BridgeIt utility apps are available at the following locations:

- [Google Play Store](https://play.google.com/store/apps/details?id=mobi.bridgeit)
- [Apple App Store](https://itunes.apple.com/app/bridgeit/id727736414)

You can install the free BridgeIt utility directly from the app store, but it is not necessary for users of your BridgeIt-enabled web app to pre-install BridgeIt.  BridgeIt is designed to be installed as needed. The install-as-needed mechanism varies slightly by platform, but should achieve the same result of a seamless install on all platforms.

### Android

Here is a typical user scenario for iOS:

1. An Android user visits your web application for the first time and presses a 'Take a photo' button on your web page.  
2. As BridgeIt is not yet installed yet on the user's device, a web page will be loaded enabling the user to install BridgeIt or return to what they are doing. 
3. If they choose to install BridgeIt, they will be taken to the BridgeIt app in the Play Store, where the user can install BridgeIt.
4. Once BridgeIt is installed, the Play Store give the option to run BridgeIt. If the user chooses to do so, BridgeIt starts and presents a dialog allowing the user to 'Return To Browser', 'Run BridgeIt Demo' or 'Exit'
5. Should the user decide to return to browser, Chrome will be launched and you application page will be presented.  Now if the user presses 'Take a photo', an application selector will be presented. The user can now select BridgeIt as the default for handling BridgeIt-specific URLs.  
6. From this point on BridgeIt will seemlessly launch and handle all native requests from your web app.

### iOS

Here is a typical user scenario for iOS:

1. An iPhone user visits your web application for the first time and views a 'Take a photo' button on your web page.  
2. As BridgeIt is not yet installed yet on the user's device, the `bridgeit.launchFailed()` function will be called. 
3. As you've overridden the `bridgeit.launchFailed()` function in your web application with a custom popup that informs the user that they should follow the link to install the free app if they would like the best user experience possible, they do so.  
4. The user is taken to the BridgeIt Apple App install page where they can choose to install the BridgeIt utility app in one click, which they do.  
5. A few seconds later BridgeIt is installed on the user's iPhone, and they see another button that says 'Open', which they press.   
6. The BridgeIt utility app opens, and immediately redirects the user back to your web application where they can now take a photo with the native mobile camera feature.   

 