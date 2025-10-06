Mục tiêu: Tạo base API có thể quản lý user, token, và gửi lệnh publish message.

**Học:**

- ASP.NET Core (.NET 8)
    
- Authentication: JWT Bearer
    
- EF Core + MariaDB
    
- Repository pattern
    
- Redis cache basics
    

**Làm:**

- API: `/auth/login`, `/user/register`, `/message/send`
    
- Service gửi message qua MQTT broker bằng MQTTnet
    
- Cache token bằng Redis
    

**Sản phẩm:**

- REST API hoàn chỉnh có thể “push MQTT message” đến client.
    
- Swagger demo push thử.