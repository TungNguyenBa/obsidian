Mục tiêu: Xây logic broker giả lập FCM.

**Học:**

- MQTTnet Server (C#)
    
- Topic routing / PubSub / Retain message
    
- Offline queue (Redis list)
    
- Delivery acknowledgment (QoS)
    

**Làm:**

- Tự build MQTT broker nhỏ (có auth, topic, QoS)
    
- Khi client offline → lưu message vào Redis → resend khi online
    

**Sản phẩm:**

- Broker của riêng bạn có thể push offline message giống FCM.