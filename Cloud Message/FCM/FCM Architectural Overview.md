1.  Message building and targeting
	- You create message (notify or data) ở: 
		   -  Firebase console GUI: direct send from Firebase Console
		   - Admin SDK or HTTP API: from server/Cloud Functions - Trust Env
- You choose send to:
	- A device (theo FCM token)
	- A group or topic (ex: all user quan tâm to "news")
2. FCM backend
	- Message after are created will go into FCM backend
	- FCM backend có nhiệm vụ:
		- Verify validation
		- Handle options (ưu tiên, collapse key, TTL,....)
		- Coordination to hệ thống phù hợp theo nền tảng (Android, IOS, Web)
3. Platform-level message transport
	Tuỳ nền tảng. FCM chuyển message qua các "cổng" khác nhau:
	- Android transport layer: System của Google to push message Android devices
	- iOS/APNs (Apple Push Notification service): FCM giao tiếp với APNs để push to iPhone/iPad
	- Web Push: Using chuẩn Web Push API để gửi to browser
4. SDK on device
	- On devices client have Firebase SDK (client SDK)
	- SDK nhận message và xử lý:
		- If is "notify message" -> SDK/OS có thể tự hiển thị
		- If is "data message" -> chuyển sang app code để tự xử lý

![[Pasted image 20250926100225.png]]