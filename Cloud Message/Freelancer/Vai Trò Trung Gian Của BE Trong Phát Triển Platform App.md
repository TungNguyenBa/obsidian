### **Tại Sao Cần Một BE Trung Gian? (Vấn Đề)**

Nếu chỉ có React app gọi thẳng API Shopify/Wix:

1. **Bảo mật thảm họa:** API keys, secrets sẽ lộ trên frontend.
    
2. **Không xử lý logic phức tạp được:** Mọi tính toán phải làm ở client-side.
    
3. **Không lưu trữ dữ liệu riêng:** App của bạn sẽ chỉ là "cái bóng" của platform.
    
4. **Không tích hợp dịch vụ khác:** Không thể kết nối với hệ thống nội bộ của merchant.
### **BE (.NET 8) Là "Trung Gian Thông Minh"**

Đây là **7 vai trò sống còn** của BE trung gian:

| Vai Trò                                                    | Mô Tả                                                                                                                                                                                                       | Ví Dụ Cụ Thể                                                                                                                                                                             | Lợi Ích                                                             |
| ---------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| **1. Cổng Bảo Mật (Security Gateway)**                     | **"Người gác cổng"** cho tất cả API calls.  <br>• Lưu trữ an toàn API keys/oauth tokens trong server.  <br>• Thêm headers (authentication, rate limiting).  <br>• Validate & sanitize requests từ frontend. | Merchant cài app → app lưu `access_token` vào DB của bạn → mọi request từ React đều gọi qua .NET BE → BE dùng token đó để gọi Shopify API.                                               | **Không bao giờ** lộ secret keys cho browser.                       |
| **2. Bộ Xử Lý Logic Nghiệp Vụ (Business Logic Processor)** | **"Bộ não"** xử lý logic mà platform không có.  <br>• Tích hợp nhiều nguồn dữ liệu.  <br>• Chạy batch jobs, scheduled tasks.                                                                                | App "dự đoán tồn kho": BE lấy lịch sử đơn hàng từ Shopify + dữ liệu weather API + dữ liệu promotion từ Postgres → chạy thuật toán ML → lưu kết quả.                                      | Logic phức tạp được xử lý an toàn phía server.                      |
| **3. Kho Dữ Liệu Riêng (Private Data Vault)**              | **"Ngân hàng dữ liệu"** của riêng app.  <br>• Lưu cấu hình app, settings của từng merchant.  <br>• Lưu dữ liệu mở rộng (ví dụ: tags, notes về sản phẩm).                                                    | Merchant dùng app để "gắn nhãn" sản phẩm → nhãn đó KHÔNG có trong Shopify → lưu vào Postgres của bạn, liên kết qua `product_id`.                                                         | App có giá trị độc lập, không phụ thuộc hoàn toàn vào platform.     |
| **4. Trạm Trung Chuyển Webhook (Webhook Hub)**             | **"Trạm thu phát tín hiệu"** nhận sự kiện từ platform.  <br>• Xác thực webhook signatures.  <br>• Xử lý async, đưa vào queue.  <br>• Kích hoạt logic phản hồi.                                              | Shopify gửi webhook `orders/create` → BE của bạn nhận → xác thực chữ ký → đưa vào Hangfire/Background service → gửi email thông báo qua SendGrid.                                        | Xử lý sự kiện thời gian thực, không block main thread.              |
| **5. Bộ Điều Phối API (API Orchestrator)**                 | **"Nhạc trưởng"** kết hợp nhiều dịch vụ.  <br>• Gộp nhiều API calls thành 1 response.  <br>• Transform data format cho frontend.                                                                            | React cần hiển thị dashboard: 1 call duy nhất đến BE → BE đồng thời gọi: (1) Shopify API lấy orders, (2) Google Analytics API, (3) Internal Postgres → merge data → trả về unified JSON. | Frontend đơn giản hóa, performance tốt hơn (giảm số lượt API call). |
| **6. Bộ Đệm & Tối Ưu (Cache & Optimizer)**                 | **"Bộ nhớ đệm thông minh"**.  <br>• Cache response từ platform API.  <br>• Implement retry logic khi API fail.  <br>• Logging & monitoring.                                                                 | Cache danh sách sản phẩm trong Redis 5 phút → giảm tải cho Shopify API + tăng tốc app.                                                                                                   | Tăng performance, giảm rate limit issues, dễ debug.                 |
| **7. Công Cụ Quản Trị (Admin Toolkit)**                    | **"Bảng điều khiển"** cho chủ app.  <br>• Analytics tổng hợp across merchants.  <br>• Billing & subscription management.  <br>• Health check system.                                                        | Bạn có 1000 merchants dùng app → BE của bạn có trang super-admin để xem tổng doanh thu, active users, errors.                                                                            | Quản lý app hiệu quả, phát hiện vấn đề sớm.                         |
### **Xây dựng Storefront scripts (JavaScript/TypeScript/jQuery + Liquid) để nhúng vào theme của merchant khi cần**
**Tưởng tượng:** Shopify store của merchant như một **căn nhà đã xây sẵn và đang ở (live production)**.

- **Theme Liquid** = **Kết cấu và nội thất gốc** của ngôi nhà.
    
- **Storefront Script của bạn** = **Những đồ trang trí, thiết bị điện tử thông minh** bạn **lắp thêm vào** nhà họ.
    
- **Yêu cầu:** Lắp thêm mà **không đục tường, không làm hỏng đồ hiện có, và dễ dàng tháo ra** nếu họ không thích.

### **GraphQL vs REST**
**GraphQL** là ngôn ngữ cho phép frontend **'đặt hàng' chính xác data cần** từ backend, thay vì nhận cả đống data thừa như REST. Trong phát triển Shopify app, nó là công cụ **không thể thiếu** để build admin app hiệu quả, đặc biệt với áp lực timeline ngắn như 2 tuần MVP.

# So sánh JavaScript và TypeScript

### Tổng quan nhanh

|Tiêu chí|JavaScript|TypeScript|
|---|---|---|
|Bản chất|Ngôn ngữ động|Superset thêm kiểu tĩnh|
|Kiểu dữ liệu|Động, kiểm tra lúc chạy|Tĩnh, kiểm tra lúc biên dịch|
|Công cụ|Hoạt động với mọi IDE|IDE mạnh mẽ hơn nhờ type info|
|Đường chạy|Chạy trực tiếp|Biên dịch về JS rồi chạy|
|Mục tiêu|Tốc độ và linh hoạt|An toàn, dễ bảo trì, mở rộng|

## Hệ thống kiểu và an toàn

- **Kiểu tĩnh vs động:** **JavaScript:** không ép kiểu, dễ xảy ra lỗi runtime khi dữ liệu sai. **TypeScript:** ép kiểu tĩnh, bắt lỗi tại compile, giảm bug sớm.
    
- **Tính năng TypeScript:**
    
    - **Generics:** mô tả quan hệ kiểu tổng quát, tái sử dụng an toàn.
        
    - **Union/Intersection:** kết hợp nhiều kiểu, mô tả dữ liệu phức tạp.
        
    - **Type narrowing:** thu hẹp kiểu theo điều kiện runtime.
        
    - **Structural typing:** dựa theo hình dạng đối tượng, linh hoạt nhưng vẫn an toàn.
        
    - **Utility types:** `Partial`, `Pick`, `Omit`, `Readonly`, `Record`, hỗ trợ biến đổi kiểu.