You can subscribe a client app to a topic from either the server or the client:
- On the server, using the Firebase Admin SDK
- On the client, using the client-side API within your app
## Manage topic sub using the Admin SDK

- Admin  SDK allows server sub or unsub multiple devices (via registration token) in/out a topic
- If topic don't have --> Self-generated FCM
- Up to 1000 devices/request
- Benefit: Instead of sending each token, just send 1 message to the topic → all devices in it receive it.
## Mange topic sub from your client app

- Self-manage client app topic sub via SDK 
- If topic is exists, Self-generated FCM
- Self-retry FCM if request initial fail --> Ensure sub successfully 