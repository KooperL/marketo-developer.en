---
title: '[!DNL Adobe Launch] Extension Installation'
feature: Mobile Marketing
description: '[!DNL Adobe Launch] extension installation overview'
exl-id: d71b7cd7-309b-4882-9bba-7daaaa5ef32d
---
# [!DNL Adobe Launch] Extension Installation

Installation instructions for [!DNL Adobe Launch] Marketo extension. The steps below are required to send Push Notifications and/or In-App Messages.

## Prerequisites

1. [Add an application in Marketo Admin](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/mobile-marketing/admin/add-a-mobile-app) (obtain your application Secret Key and Munchkin Id)
1. [Configure the property in [!DNL Adobe Launch] portal](https://experience.adobe.com/#/@amc/data-collection/home)
1. Configure application secret key & Munchkin ID for the property in the [!DNL Adobe Launch] portal
1. [Setup Push Notifications](push-notifications.md) (optional)

## How to Install Marketo Extension on iOS

### Setup Swift Bridging Header

1. Go to [!UICONTROL File] > [!UICONTROL New] > [!UICONTROL File] and Select **[!UICONTROL Header File]**.

1. Name the file "<_ProjectName_>-Bridging-Header".

1. Go to [!UICONTROL Project] > [!UICONTROL Target] > [!UICONTROL Build Settings] > [!UICONTROL Swift Compiler] > [!UICONTROL Code Generation]. Add the following path to the "Objective-Bridging" Header:

  `$(PODS_ROOT)/<_ProjectName_>-Bridging-Header.h`

## Initialize Extension

>[!BEGINTABS]

>[!TAB Objective C]

Update the `applicationDidBecomeActive` method like below

```
(void)applicationDidBecomeActive:(UIApplication*) application
{
 [[ALMarketo sharedInstance] initializeMarketo:nil];
}
```

>[!TAB Swift]

Update the `applicationDidBecomeActive` method like below

```
func applicationDidBecomeActive(_ application: UIApplication)
{
 ALMarketo.sharedInstance().initializeMarketo(nil)
}
```

>[!ENDTABS]

## iOS Test Devices

1. Select **[!UICONTROL Project]** > **[!UICONTROL Target]** > **[!UICONTROL Info]** > **[!UICONTROL URL Types]**.
1. Add identifier: ${PRODUCT_NAME}
1. Set URL Schemes: mkto-<S_ecret Key_> 
1. Include `application:openURL:sourceApplication:annotation:` to `AppDelegate.m file` (Objective-C)

### Handle Custom Url Type in AppDelegate

>[!BEGINTABS]

>[!TAB Objective C]

```
#ifdef __IPHONE_10_0
-(BOOL)application:(UIApplication *)application 
           openURL:(NSURL *)url 
           options:(NSDictionary *)options{
    return [[ALMarketo sharedInstance] application:application
                                         openURL:url
                               sourceApplication:nil
                                      annotation:nil];
}
#endif

- (BOOL)application:(UIApplication *)application
            openURL:(NSURL *)url
  sourceApplication:(NSString *)sourceApplication
         annotation:(id)annotation {
    return [[ALMarketo sharedInstance] application:application
                                         openURL:url
                               sourceApplication:nil
                                      annotation:nil];
}

```

>[!TAB Swift]

```
func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
    return ALMarketo.sharedInstance().application(application, open: url, sourceApplication: nil, annotation: nil)
}
```

>[!ENDTABS]

## How to Install Marketo SDK on Android

### Android Extension Setup

Follow instructions in [!DNL Adobe Launch] portal

### Configure Permissions

Open `AndroidManifest.xml` and add following permissions. Your app must request the "INTERNET" and "ACCESS_NETWORK_STATE" permissions. If your app already requests these permissions, then skip this step.

```xml
<uses‐permission android:name="android.permission.INTERNET"></uses‐permission>
<uses‐permission android:name="android.permission.ACCESS_NETWORK_STATE"></uses‐permission>
```

## Initialize Extension

ProGuard Configuration (Optional)

If you are using ProGuard for your app, then add the following lines in your `proguard.cfg` file. The file is located within your `project` folder. Adding this code excludes the Marketo SDK from the obfuscation process.

```
-dontwarn com.marketo.*
-dontnote com.marketo.*
-keep class com.marketo.**{ *; }
```

## Android  Test  Devices

Add "MarketoActivity" to `AndroidManifest.xml` inside the application tag.

```xml
<activity android:name="com.marketo.MarketoActivity"  android:configChanges="orientation|screenSize" >
    <intent-filter android:label="MarketoActivity" >
        <action  android:name="android.intent.action.VIEW"/>
        <category  android:name="android.intent.category.DEFAULT"/>
        <category  android:name="android.intent.category.BROWSABLE"/>
        <data android:host="add_test_device" android:scheme="mkto" />
    </intent-filter>
</activity>
```

## Firebase Cloud Messaging Support

The MME Software Development Kit (SDK) for Android has been updated to a more modern, stable, and scalable framework that contains more flexibility and new engineering features for your Android app developer.

Android app developers can now directly use Google's [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/) (FCM) with this SDK.

### Adding FCM to your Application

1. Integrate latest Marketo Android SDK in Android App.  Steps are available at [GitHub](https://github.com/Marketo/android-sdk).
1. Configure Firebase App on Firebase Console.
    1. Create/Add a Project on [](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/)Firebase Console.
        1. In the [Firebase console](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/), select **[!UICONTROL Add Project]**.
        1. Select your GCM project from the list of existing Google Cloud projects, and select **[!UICONTROL Add Firebase]**.
        1. In the Firebase welcome screen, select **[!UICONTROL Add Firebase to your Android App]**.
        1. Provide your package name and SHA-1, and select **[!UICONTROL Add App]**. A new `google-services.json` file for your Firebase app is downloaded.
        1. Select **[!UICONTROL Continue]** and follow the detailed instructions for adding the Google Services plugin in Android Studio.
            
    1. Navigate to **[!UICONTROL Project Settings]** in [!UICONTROL Project Overview]
        1. Click **[!UICONTROL General]** tab. Download the `google-services.json` file.
        1. Click on **[!UICONTROL Cloud Messaging]** tab. Copy [!UICONTROL Server Key] & [!UICONTROL Sender ID]. Provide these [!UICONTROL Server Key] & [!UICONTROL Sender ID] to Marketo.
    1. Configure FCM changes in Android App
        1. Switch to the Project view in Android Studio to see your project root directory
            1. Move the downloaded `google-services.json` file into your Android app module root directory
            1. In Project-level `build.gradle` add the following:
                
                ```
                buildscript {
                  dependencies {
                    classpath 'com.google.gms:google-services:4.0.0'
                  }
                }
                ```
                
            1. In App-level build.gradle, add the following:
                
                ```
                dependencies {
                  compile 'com.google.firebase:firebase-core:17.4.0'
                } 
                // Add to the bottom of the file 
                apply plugin: 'com.google.gms.google-services'
                ```
                
            1. Finally, click on **[!UICONTROL Sync now]** in the bar that appears in the ID
    1. Edit your app's manifest The FCM SDK automatically adds all required permissions and the required receiver functionality. Make sure to remove the following obsolete (and potentially harmful, as they may cause message duplication) elements from your app's manifest:
        
        ```xml
        <uses-permission android:name="android.permission.WAKE_LOCK" />
        <permission android:name="<your-package-name>.permission.C2D_MESSAGE" android:protectionLevel="signature" />
        <uses-permission android:name="<your-package-name>.permission.C2D_MESSAGE" />
        
        ...
        
        <receiver>
          android:name="com.google.android.gms.gcm.GcmReceiver"
          android:exported="true"
          android:permission="com.google.android.c2dm.permission.SEND">
          <intent-filter>
            <action android:name="com.google.android.c2dm.intent.RECEIVE" />
            <category android:name="<your-package-name> />
          </intent-filter> 
        </receiver>
        ```
        

### FCM FAQ

Frequently asked questions regarding Firebase Cloud Messaging support.

**Q: Where can I find instructions to update to the latest version of the MME SDK?** Instructions can be found on the Marketo Developer Site [HERE](installation.md).

**Q: Will updating to the latest version of the SDK require me to publish an updated version of my Android Application to my existing users?** No.

**Q: How does it impact the existing MME customers that have published Android Apps integrated with Marketo Android SDK?** They can migrate an existing GCM client app on Android to Firebase Cloud Messaging (FCM) as follows:

1. In the [Firebase console](https://accounts.google.com/ServiceLogin?passive=1209600&osid=1&continue=https://console.firebase.google.com/&followup=https://console.firebase.google.com/), select **[!UICONTROL Add Project]**.
1. Select your GCM project from the list of existing Google Cloud projects, and select **[!UICONTROL Add Firebase]**.
1. In the Firebase welcome screen, select **[!UICONTROL Add Firebase to your Android App]**.
1. Provide your package name and SHA-1, and select **[!UICONTROL Add App]**. A new google-services.json file for your
1. Firebase app is downloaded.
1. Select **[!UICONTROL Continue]** and follow the detailed instructions for adding the Google Services plugin in Android Studio.

**Q: Can we target the leads created using the old Marketo SDK which used GCM App ?** Yes. All the leads created using Marketo SDK can be targeted for sending the push notifications.
