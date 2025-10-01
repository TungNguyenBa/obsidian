## Progress create Registration token

When app install, SDK Firebase will:
- Send to request to FCM BE của Google
- FCM BE generate Registration token for app instance
- SDK trả token về cho app
- App is responsibility send this token to server riêng của bạn (app server)
## Role token

- Server store this token assign to user/device
- When want send message to device, server will send request to FCM BE attach with Registration token
- FCM rely on token to know route message to devies nào
## Importance feature

- Token can change (when app reinstall, when user clear data,.... )
---> App must have logic refresh token (Firebase SDK will inform sự kiện when token change)
- Token must be security. If will be spam message to device
## Why does the SDK work when you install the app?

When you add Firebase SDK (Firebase Messaging) into project and build app:
- This SDK comes with built-in code to communicate with the FCM BE
- As soon as app is installed and run the first, SDK will start background service to:
	- Contact with Google Play (Android) service or APNs (iOS)
	- Send request register to FCM BE to ask for 1 registration token