- import java.util.*;
- Hash = cơ chế "ghi nhớ & tra cứu rất nhanh"
- O(1)
- Apply: Hash dùng để tránh so sánh lặp đi lặp lại
# 1. HashSet
- Lưu value không đc trùng
- Apply: Khi cần biết CÓ or KHÔNG
- Dấu hiệu: 
		- contains
		- exists
		- duplicate
		- unique
		- visited
		- seen before

![[Pasted image 20260112225736.png]]
  
  
  
## 2. HashMap
- Key, value. Cùng key nếu value thay đổi -> Ghi đè
- Cần nhớ, thêm thông tin cho mỗi key
- Dấu hiệu:
		- count
		- frequency
		- how many
		- index
		- mapping
		
![[Pasted image 20260112225950.png]]