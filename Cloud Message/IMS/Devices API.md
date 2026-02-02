1. Register
-  Request
```
	{
		  "appId": 1,
		  "userId": 1,
		  "deviceId": 1,
		  "osVersion": "17.0",
		  "platForm": "iOS",
		  "isOnline": "true",
		  "lastActive": "date"
	}
```
public class DeviceService : IDeviceService
{
    private readonly IUnitOfWork _uow;

    public DeviceService(IUnitOfWork uow)
    {
        _uow = uow;
    }

    public async Task<RegisterDeviceResponse> RegisterAsync(RegisterDeviceRequest request)
    {
        // 1. Kiểm tra device đã tồn tại chưa
        var existing = await _uow.Devices.GetByDeviceIdAsync(request.DeviceId);
        string newDeviceToken = Guid.NewGuid().ToString("N");
        string newAccessToken = Convert.ToBase64String(Guid.NewGuid().ToByteArray());

        if (existing == null)
        {
            // 2. Nếu chưa tồn tại → tạo mới
            var device = new Device
            {
                DeviceId = request.DeviceId,
                DeviceToken = newDeviceToken,
                OsVersion = request.OsVersion,
                Platform = request.Platform,
                AppId = request.AppId,
                UserId = request.UserId,
                IsOnline = true,
                LastActive = DateTime.UtcNow
            };

            await _uow.Devices.AddAsync(device);
        }
        else
        {
            // 3. Nếu đã tồn tại → cập nhật trạng thái, reset token
            existing.IsOnline = true;
            existing.LastActive = DateTime.UtcNow;
            existing.DeviceToken = newDeviceToken;
            await _uow.Devices.UpdateAsync(existing);
        }

        await _uow.CommitAsync();

        return new RegisterDeviceResponse
        {
            DeviceToken = newDeviceToken,
            AccessToken = newAccessToken
        };
    }
}

- Response
```
	{
		 "deviceId": 10,
		 "deviceToken": "c4d23acb-5bfe-4d22-b4c3-0bde7c99a7a5",
         "expiredAt": "2025-12-31T23:59:59Z"
	}
```
2. Remove
3. List
4. CheckStatus
5. Get