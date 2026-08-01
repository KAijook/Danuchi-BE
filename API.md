# List API

* 1. Auth & Users
POST	/api/auth/register	        Đăng ký tài khoản 
POST	/api/auth/login	                Đăng nhập 
POST	/api/auth/refresh-token	Cấp lại access_token khi hết hạn

* 2. Stores
GET 	/api/stores               	                  Danh sách quán (phân trang)
POST	/api/stores	                                  Tạo quán mới
GET 	/api/stores/:id	                                  Chi tiết quán
PUT	        /api/stores/:id	                                  Cập nhật quán
GET  	/api/stores/:id/products                      Lấy danh sách món của quán
POST      /api/stores/:id/products                      Thêm món cho quán
PUT        /api/stores/:id/products/product_id     Sửa thông tin món
DELETE /api/stores/:id/products/product_id     Xóa món

* 3. Menu
GET	        /api/menus	               Danh sách menu
POST	    /api/menus	                           Tạo menu 
GET	        /api/menus/:id                     Xem chi tiết menu
PUT         /api/menus/:id                     Sửa menu được chọn

* 4. Participants
GET 	/api/menus/:menuId/participants      	Danh sách người tham gia menu 
        
* 5. Orders

GET 	/api/menus/:id/orders                 Chi tiết order + tổng hợp
PUT	        /api/menus/:id/orders	          Cập nhật trạng thái đơn: opening/ordered/received/completed
POST	        /api/menus/:id/orders	          Tạo đơn

* 6. Order Items
GET 	/api/menus/:id/orders/:order_id  Lấy đơn đặt hàng
PUT 	/api/menus/:id/orders/:order_id  Chỉnh sửa đơn hàng
POST	/api/menus/:id/orders/:order_id  Gửi đơn đặt hàng


# Setting cho các màn

* Màn Login
POST	/api/auth/login                Đăng nhập 

* Màn Dashboard
GET 	/api/menus/:menuId/participants/Limit&status=...	Danh sách người tham gia menu 
GET	        /api/menus	               Danh sách menu


Thống kê đặt hàng?

* Màn tạo menu mới
POST	    /api/menus	                           Tạo menu 

* Màn chi tiết menu
GET	        /api/menus/:id                     Xem chi tiết menu
PUT         /api/menus/:id                     Sửa menu được chọn
GET  	/api/stores/:id/products               Lấy danh sách món của quán
GET 	/api/menus/:id/orders                  Chi tiết order + trạng thái order
GET 	/api/menus/:id/orders/:order_id        Lấy đơn đặt hàng
POST	/api/menus/:id/orders/:order_id        Gửi đơn đặt hàng
GET 	/api/menus/:menuId/participants      	Danh sách người tham gia menu 
PUT	        /api/menus/:id/orders	          Cập nhật trạng thái menu: opening/ outdated / done

* Màn tổng hợp đơn hàng
GET 	/api/menus/:id/orders                  Chi tiết order + trạng thái order
PUT	        /api/menus/:id/orders	          Cập nhật trạng thái đơn: opening/ordered/received/completed
GET 	/api/menus/:id/orders/:order_id        Lấy đơn đặt hàng
GET 	/api/menus/:menuId/participants      	Danh sách người tham gia menu 

* Màn quản lý quán
GET 	/api/stores               	                  Danh sách quán (phân trang)
POST	/api/stores	                                  Tạo quán mới
PUT	        /api/stores/:id	                                  Cập nhật quán


* Màn chi tiết quán
GET 	/api/stores/:id	                                  Chi tiết quán
PUT	        /api/stores/:id	                                  Cập nhật quán
GET  	/api/stores/:id/products                      Lấy danh sách món của quán
POST      /api/stores/:id/products                      Thêm món cho quán
PUT        /api/stores/:id/products/product_id     Sửa thông tin món
DELETE /api/stores/:id/products/product_id     Xóa món







