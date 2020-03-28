# FCM Push Notification Kotlin

### Introduction:

This project is created in the intention to understand the FCM PushNotification and make it as
readily usable component to integrate it with any projects

----------------------------------------------------------------------------------------------------

### Installation:

1.	In Our Project  Click Tools -> Firebase   -	Assistant Sidebar will open, in that click Cloud
        Messaging and Select Set up Firebase Cloud Messaging.

2.	Set up Firebase Cloud Messaging  -> click Connect to Firebase, it will prompt below window for
        project creation in firebase.

3.	If you login firebase for the first time it will shown as per screenshot 0.1.

![alt text](https://i.postimg.cc/CMjtrXTN/screenshot-0-1.png)

4.	Login to your firebase configuration Email. After login to mail it will ask for firebase trust.
        Click trust it will go to another window as per screenshot 0.2.
![alt text](https://i.postimg.cc/y8NbdNJQ/screenshot-0-2.png)

5.	As per above click firebase it will direct into Firebase home page.

6.	In firebase home page click Go to console, we can see the list of projects already created in
        firebase and we can able to create new project in the console window as per screenshot 0.4.
![alt text](https://i.postimg.cc/SRqZpQFG/screenshot-0-4.png)

7.	If you already logged in your firebase account it will show as per screenshot 0.5.
![alt text](https://i.postimg.cc/3wsSnCtV/screenshot-0-5.png)

8.	In screenshot 0.5 window click connect to Firebase, it will create our project in firebase.
        Then click Add FCM to your app. It will prompt dialog windown as per screenshot 0.6.
![alt text](https://i.postimg.cc/nrk3V8nf/screenshot-0-6.png)

9.	Click Accept Changes it will automatically add the required dependencies in gradle file.

10.	We can see our project has created  in firebase Console page as per screenshot 0.7.
![alt text](https://i.postimg.cc/HkPP7CXp/screenshot-0-7.png)

11.	Click out project in Firebase it will go to project overview page as per screenshot 0.8.
![alt text](https://i.postimg.cc/MT1s4M4T/screenshot-0-8.png)

12.	Once done with the above steps, check inside of our project  app folder google-services.json
        file will be there, if we create project using android studio tools it will automatically
        places the file inside of app folder.


----------------------------------------------------------------------------------------------------

### Configuration:

Now our Project has connected with Firebase successfully.

1. Add below user permissions in AndroidManifest file:

    ```
    <uses-permission android:name="android.permission.INTERNET" />
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
    ```

2. We need to create service in our project to send push notification.
    Click File -> New ->Service -> Service.

In Manifest file add the following within the <service>

	```
	<service
        android:name=".FireBaseMessageService"
        android:enabled="true"
        android:exported="true">
        <intent-filter>
            <action android:name="com.google.firebase.MESSAGING_EVENT" />
        </intent-filter>
    </service>
	```

----------------------------------------------------------------------------------------------------

### Coding Part:

1. Inside service class we need to extend the FirebaseMessagingService().

2. Add onMessageReceived override method (inside the sevice class click left -> Generate ->
                Override Methods -> onMessageReceived).

3. Add the below code(Kotlin) inside onMessageArrived().

	    ```
	     override fun onMessageReceived(message: RemoteMessage) {
         
                 if(message.notification !=null){
                     sendNotification(message.notification?.title,message.notification?.body)
                 }
             }
         
             private fun sendNotification(title:String?, body: String?) {
         
                 val notificationBuilder = NotificationCompat.Builder(this, "default_channel_id")
                     .setSmallIcon(R.mipmap.ic_launcher)
                     .setContentTitle(title)
                     .setContentText(body)
                     .build()
             }
	    ```

----------------------------------------------------------------------------------------------------

#### Test Flow:

1. Go to our Project Overview page in Firebase. In that page scroll down and click Cloud
            Messaging as per screenshot 0.9.
![alt text](https://i.postimg.cc/Wp6WwZgY/screenshot-0-9.png)

2. The screenshot 0.9 will be for the first time message send after that this cloud messaging
            tab will be in top of our page as per screenshot 1.0.
![alt text](https://i.postimg.cc/7LGt3QnS/screenshot-1-0.png)

3. Inside Clound Messaging  - > Compose Notification
      a. Notification:
            Notification title
            Notification text
      b. Target:
            User Segment tab  select our project package name.
      c. Scheduling:
            Now(You can schedule based on your requirement)

4. Click Review popup will prompt in this click publish as per screenshot 1.1.
![alt text](https://i.postimg.cc/Jztp8dgS/screenshot-1-1.png)

    You will receive your push notification.
