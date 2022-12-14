# Claim
This repo is forked from Chagall/notification-listener-service-example. I did some modification so it could show all notifications.

# Notification Listener Service Example 

This example aims to teach you how to intercept notifications received by the Android System.

## (Updated 18.03.2021) 

All the gradle files have been updated to the latest version available because people were having trouble getting it to compile. Some libraries were deprecated, so I updated them to the new ones, and the Android target version is now set to Android 10 instead of Android 5.

TLDR; It's still working!!

## What is a Notification
https://developer.android.com/guide/topics/ui/notifiers/notifications.html

As stated in the official Google Android Website, a notification is a message that can be displayed outside of the application normal User Interface

<b>It should look similar to this:</b> 

![alt text](https://i.stack.imgur.com/A0Y3K.jpg, "Notification")

## How to Intercept a Notification
In order to intercept a notification received by the android system we need to have a specific service running on the system's background. This service is called: <b>NotificationListenerService</b>. 

What the service basically does is: It registers itseft to the android system and after that starts to listen to the calls from the system when new notifications are posted or removed, or their ranking changed. 

When the <b>NotificationListenerService</b> identifies that a notification has been <b>posted</b>, <b>removed</b> or had its <b>ranking modified</b> it does what you told it to.

### Steps you need to follow to build a NotificationListenerService

<b>1.</b> Declare the Service in your AndroidManifest.xml file with the `BIND_NOTIFICATION_LISTENER_SERVICE` permission and include an intent filter with the `SERVICE_INTERFACE action`. 

Like this:

```xml
 <service android:name=".NotificationListener"
          android:label="@string/service_name"
          android:permission="android.permission.BIND_NOTIFICATION_LISTENER_SERVICE">
     <intent-filter>
         <action android:name="android.service.notification.NotificationListenerService" />
     </intent-filter>
 </service>
```
<b>2.</b> Extend the NotificationListenerService class and implement at least the following methods:

```java
  public class NotificationListenerExampleService extends NotificationListenerService {
  
    @Override
    public IBinder onBind(Intent intent) {
        return super.onBind(intent);
    }
  
    @Override
    public void onNotificationPosted(StatusBarNotification sbn){
      // Implement what you want here
    }

    @Override
    public void onNotificationRemoved(StatusBarNotification sbn){
      // Implement what you want here
    }
  }
```

##  How This Example Works
To illustrate the interception of notifications I've built a <b>NotificationListenerService</b> that does the following:

It changes the <b>ImageView</b> present on the screen whenever it receives a notification from the following apps: 

* Facebook
* Instagram
* Whatsapp

#### Tested in:
- 2016 on a ZenPhone2 (Android Lollipop 5.0)
- 2021 on a Samsung Galaxy S7 (Android Oreo 8.0.0)

### Here are some images of the app. working, so you can see what it looks like:

![alt text](http://imgur.com/zkQ2S9P.jpg)
![alt text](http://imgur.com/gSOYgZm.jpg)
![alt text](https://i.imgur.com/8xvHoF2.jpg)
![alt text](http://imgur.com/asSZT0n.jpg)
