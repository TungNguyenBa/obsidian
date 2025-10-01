## Send a Message using FCM HTTP v1 API

Using the [FCM HTTP vs API](https://firebase.google.com/docs/reference/fcm/rest/v1/projects.messages?_gl=1*twss1l*_up*MQ..*_ga*MTQ2MjU3NjcxNS4xNzU4NjE3MDQ2*_ga_CW55HF8NVT*czE3NTkyODIwMzUkbzMkZzAkdDE3NTkyODIwMzUkajYwJGwwJGgw), you can build message requests and send them to:
* These types of targets:
	- Topic -> All devices subscribe topic
	- Condition -> Devices thoả mãn condition logic (ex: 'sports' in topics || 'news' in topics)
	- Device registration token -> Send direction to a device
	- Device group name -> Send to devices group (only support through protocol old)
- These types of payload:
	- Notification payload -> available field chuẩn (title, body, icon, ..) -> FCM hiển thị luôn
	- Data payload -> key-value do you define, app tự xử lý
	- Both types 

## Authorize HTTP v1 send request

In order for the server to be eligible to send request to FCM via HTTP v1 API, you must be authorization. Have 3 main options:
1. Google Application Default Credentials (ADC)
    - Use when server run in Google infrastructure (Compute Engine, Kubernetes Engine, App Engine, Cloud Functions)
    - Auto get service account default -> Convenient,  don't need to manage a file manual
    - Allow test local use set env variable GOOGLE_APPLICATION_CREDENTIALS.
    --> Server run into Google Cloud
2. Service account JSON file
	- Use when the server is running outside of Google Cloud
	- Need to download file JSON (contains private key) from Firebase project
	- Point to this file via GOOGLE_APPLICATION_CREDENTIALS or load direct into code ( nguy hiểm hơn, dễ lộ credentials)
	--> Server run into Google Cloud
3. OAuth 2.0 short-live access token
	- Token is generated from service account, short-live
	- Use to authorize direct when call API
	--> Server run outside Gg cloud
See [Details]([Send a Message using FCM HTTP v1 API  |  Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/send/v1-api?_gl=1*1ils594*_up*MQ..*_ga*MTQ2MjU3NjcxNS4xNzU4NjE3MDQ2*_ga_CW55HF8NVT*czE3NTg3OTQ4MzYkbzIkZzAkdDE3NTg3OTQ4MzYkajYwJGwwJGgw))

## Authorize with a Service Account from a Different Project