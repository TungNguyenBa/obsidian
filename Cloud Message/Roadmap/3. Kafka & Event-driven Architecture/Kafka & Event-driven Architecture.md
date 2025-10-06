Mục tiêu: Xây hệ thống event streaming giữa các service.

**Học:**

- Kafka core: topic, partition, consumer group
    
- Kafka producer & consumer trong .NET (Confluent.Kafka)
    
- Idempotent message & retry logic
    

**Làm:**

- Producer khi có yêu cầu gửi message → đẩy vào Kafka.
    
- Consumer đọc event từ Kafka và đẩy message sang MQTT broker.
    

**Sản phẩm:**

- Message gửi qua REST API → Kafka → MQTT broker → client.
    
- Cấu trúc event rõ ràng (`MessageSent`, `MessageDelivered`, v.v.)