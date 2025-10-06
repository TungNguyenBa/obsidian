You can send messages to devices that are subscribed to a particular topic using the Admin SDK or the FCM v1 HTTP API
## Prerequisites

- Setup Env. See [Set up Your Server Env](https://firebase.google.com/docs/cloud-messaging/server-environment)
- Client app must be sub topic. See [Manage Topic Sub](https://firebase.google.com/docs/cloud-messaging/topic/manage-topic-subscriptions)
## Sending to a Topic

You can send message to a topic using Firebase Admin SDK or FCM HTTp v1 API
### Using the Admin SDK

See [[Using the Admin SDK]]
### Using the HTTP v1 API

See [[Using FCM v1 API]]
## Sending to Topic Conditions

There are 2 ways to send messages based on conditions combining multiple topics
1. Using condition expression
	  Ex: `"'TopicA' in topics && ('TopicB' in topics || 'TopicC' in topics)"`
	- That means only devices that have just sub TopicA and added TopicB or TopicC will receive it.
	- Limit: maximum 5 topics in 1 expression.
2. Using a new topic for topics
3. About sending technique:
	- **Admin SDK** (Node, Java, Python, Go, C#…): bạn code backend gọi `FirebaseMessaging.DefaultInstance.SendAsync(message)` với `Condition`.
    -  **REST API (HTTP v1)**: bạn POST JSON có `"condition"` vào endpoint `https://fcm.googleapis.com/v1/projects/.../messages:send`.