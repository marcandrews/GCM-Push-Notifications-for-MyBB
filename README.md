# GCM Push Notifications for MyBB
This plugin for MyBB pushes notifications via Google Cloud Messaging to Chrome after a post is made to a user's subscribed thread.


## Requirements
- MyBB 1.8x hosted over HTTPS
- Modern version of Chrome (tested on Windows and Android, but all platforms should work)


## Demo
 1. Make sure your Chrome browser is synced with a Google account
 2. Navigate to my [MyBB Dev Forums](https://chivegaming.org/dev/) and register
 3. Enable GCM Push Notifications from your User CP > [Edit Options](https://chivegaming.org/dev/usercp.php?action=options) (under Default Thread Subscription Mode)
    - note that this is my development forum so if I'm currently working on the plugin, the demo may not function correctly; however, I will try to always have a functioning/tested version on GitHub
 4. Post a new thread and subscribe to it or subscribe to an exisiting thread
 5. Open a new Chrome incognito window, and register a second account on my MyBB Dev Forum
 6. Post to your first account's subscribed thread to see notification


## Installation instructions

 1. Obtain your Google Sender ID and API key
    1. Go to [Google Developer Console](https://console.developers.google.com/) and create a new project
    2. Near the top of the screen your Google Sender ID is your Project ID
    3. Under APIs & auth > Credentials, create a new key
    4. Your API key is your Google API key

 1. [Download ZIP](https://github.com/marcandrews/gcm-push-notifications-for-mybb/archive/master.zip) and extract the contents of the upload folder to your forum's root

 2. Update [manifest.json](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/manifest.json)
   - add your [2](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/manifest.json#L2):`name`, [3](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/manifest.json#L3):`short_name` and [11](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/manifest.json#L11):`gcm_sender_id` (from 1.ii)

 3. Update [service-worker.js](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/service-worker.js)
   - add your-forum-name to [24](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/service-worker.js#L24),[65](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/service-worker.js#L65):`tag`
   - add Your Forum Name to [62](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/service-worker.js#L62):`title`

 4. Update [gcm_push_notifications_plugin.php](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/gcm_push_notifications.php)
   - define your Google API Key at [9](https://github.com/marcandrews/gcm-push-notifications-for-mybb/blob/master/upload/gcm_push_notifications.php#L9):`GOOGLE_API_KEY` (from 1.iv)

 5. Make sure gcm_push_notifications_plugin.log is writable

 6. In your theme's User Control Panel Templates > usercp_options template, directly after `{$headerinclude}`, add: 
    ```
    <script type="text/javascript" src="jscripts/gcm_push_notifications.js"></script>
    <link rel="manifest" href="manifest.json">
    ```

 7. Activate the plugin from your MyBB Admin CP


## Screenshots

### Android
<img src=assets/i/android.png width=360 height=640 />
### Desktop
<img src=assets/i/desktop.png />
