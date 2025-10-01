# Firebase Cloud Messaging

- A message can transfer a payload of up to 4096 bytes to a client app
- ---
# Key capabilities

- Send notification messages or data messages. See [[Message types]]
- Nhắm mục tiêu tin nhắn đa năng: Distribute messages to your client app in any of 3 ways: single devices, groups devices, devices subscribed to topics
---
# How does it work?

FCM implement includes 2 main components for send and received:
-  A trusted environment: Cloud Functions for Firebase or app server
- An Apple, Android or web client app that receives messages via the corresponding platform-specific transport service. 