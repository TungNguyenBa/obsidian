For server env, see [[Your server env and FCM]]
# Set up a Js Firebase Cloud Messaging client app
- The FCM JS API lets you receive notification messages in web apps running in browsers that support the [[Push API]] (includes Chrome extensions)
- Mandatory conditions: run on HTTPs, vì FCM use Service Worker (only run on HTTPs). If chưa có hosting HTTPs, can use Firebase App Hosting (free for basic)
- Initial step, intergration Firebase into web app and write logic to get registration token nhằm nhận được thông báo
	-> Note: 
	Want web app received push notification through FCM -> need to HTTps + Service worker + intergration Firebase + token
# Add and initialize the FCM SDK

# Configure web credentials with FCM
- FCM trên Web need to Web credentials (VAPID keys) để được quyền send pusj notification qua các service web push
- Want app web subscrible recieved notify, you phải gắn 1 cặp VAPID keys with project Firebase
- Cặp này có thể:
	- Tự sinh mới trong Firebase Console 
	- Nhập key sẵn có (if you used Web push trước đó). See [The Web Push Protocol  |  Articles  |  web.dev](https://web.dev/articles/push-notifications-web-push-protocol#application_server_keys)
	-> VAPID keys = chìa khoá xác thực để web app nhận push notification qua FCM
# Access the registration token
- Want to get registration token (mã định danh thiết bị/app instance) trong FCM Web thì phải:
	- If user allows -> can get token
	- If user reject -> can't get token
- Have file firebase-messaging-sw.js trong root domain (server woker for FCM). Although initially is empty but must have
- Using API getToken() with vapidKey to get registration token. The first, will call network, after được cache lại
- Send token to server to store (use for send notify sau này)
