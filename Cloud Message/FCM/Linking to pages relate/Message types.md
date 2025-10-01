With FCM, you can send ==*two types*== of messages to your client apps:
- Notify message, are handled by the FCM SDK automatically
- Data message, are handled by the client app
1.  Notify message
-  App đang chạy nền (background/ bị kill) -> Hệ điều hành + FCM SDK display notify on ==status bar==
- App đang mở trực tiếp (foreground) -> FCM will không tự display notify mà chuyển quyền quyết định cho ==code trong app== (write logic to display ex: show dialog, custom in-app banner,..)
*Note*:
- If want to send notify, you shouldn't send direction from client app (because dễ bị lộ key API). Thay vào đó, send from ==server== or ==Cloud==: Firebase Admin SDK, HTTP v1 API. Use the Notify composer. Enter message text, title,... and send
1.  Data message
- Không tự hiển thị. App bắt buộc handler = code
- Cũng gửi từ Firebase Admin SDK, HTTP v1 API