How to set up Firebase Cloud Message in your mobile and web client app.
FCM are handled differently depending on the app (web app) state:
- Foreground (focusing app) --> always run callback 'onMessage' in JS (app tự xử lý nội dung)
- Background (tab is hided or web is closed):
	--> Run into Service Worker, callback is 'onBackgroundMessage'
	--> If playload have 'notification' --> The browser will automatically display a notification popup.
	--> If only 'data' --> App must be handle into 'onBackgroundMessage'
- Both notification + data --> still into 'onBackgroundMessage', notification is automatically displayed