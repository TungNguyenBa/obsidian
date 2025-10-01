## Your server environment and FCM

- The server side of FCM consists of two components:
	- The FCM backend provied by Google
	- Your app server or other trusted server env where your server logic run, such as Cloud Functions for Firebase or other cloud env managed by Google
	 --> App server send request -> FCM backend -> FCM routes message to client apps 
## Requirements for the trusted server env

- Your app server env must meet:
	- Able to send properly formatted message request to FCM BE  
	- Able to handle request and resend them using [exponential back-off](https://developers.google.com/api-client-library/java/google-http-java-client/backoff)
	- Able to securely store server author credentials and client registration tokens
## Required credentials for Firebase project 

| ==Creadentials==   | ==Description==                                                                                                                                                          |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ProjectID          | Unique identifier for project, use when call API HTTp v1                                                                                                                 |
| Registration token | - Unique string that FCM BE provide for each instance app<br>- Like "address home" -> server know must to send to device. See [[Push token]]                             |
| Sender ID          | Unique number, the same as projectID. Used to identify each sender that can send message to client app. Registration token will be attached to SenderID                  |
| Access token       | A short-lived (ex: 1h) OAuth 2.0 token that authorizes requet to HTTP v1 API.  It prove that your server really belong to that project and be authorized to send message |
## Choose a server option

When want server interact with FCM BE, you have 2 main option:
1. Firebase Admin SDK (recommend)
	- Support many language (Node, Java, Python, C#, Go)
	- Auto handle Authen&Author
	- Provide a convenient way to send message without manually coding the Access Token generation part
	--> See [[Firebase Admin SDK]]
2. FCM HTTp v1 APi (REST)
	- Using HTTP to comunicate
	- Flexible cross-platform
	- Need to manage access tokens yourself (OAuth 2.0)
	- This is the platform that Admin SDK is also based on.
	--> See [[FCM HTTP v1 API]]