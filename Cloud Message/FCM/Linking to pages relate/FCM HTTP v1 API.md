FCM HTTP vs API is REST raw Google protocol provide to server communicate direct with FCM
Server want to send message need to:
- Send a HTTP POST request -> endpoint FCM
- Add header (Contains Access Token for authentication)
- Add body JSON (Contains content message + target infor: token, topic, condition)
--> HTTP v1 API = cách trực tiếp, "thấp tầng" để server gửi message đến FCM. Khác với Admin SDK (cao tầng, tiện lợi hơn)