Mục tiêu: Gần như có thể replace Firebase console về BE.

**Làm:**

- Thêm message status tracking (Delivered, Read)
    
- Thêm retry queue cho message thất bại
    
- Thêm push group key (giống FCM Notification Key)
    
- Viết doc & test toàn bộ system
    
- Viết CLI tool / web admin gửi thử message
    

**Sản phẩm cuối:**  
🔥 Hệ thống push messaging:

- Quản lý user, device, group, topic
    
- Gửi push message (REST + MQTT)
    
- Có logging, offline queue, analytics
    
- Scale qua Kafka + Redis + K8s