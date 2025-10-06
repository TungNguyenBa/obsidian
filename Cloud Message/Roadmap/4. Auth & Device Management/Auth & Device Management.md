Mục tiêu: Quản lý user–device mapping và phân quyền message.

**Học:**

- JWT token flow nâng cao (access + refresh token)
    
- Role-based authorization
    
- Device registration (user ↔ device token)
    
- Topic & group membership
    

**Làm:**

- API: `/device/register`, `/device/group`, `/device/subscribe`
    
- Redis lưu token + group membership
    
- Kafka event cho device connect/disconnect
    

**Sản phẩm:**

- User có thể đăng nhập, đăng ký device, và gửi message đến nhóm device.