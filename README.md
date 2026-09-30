# Phân tích Trade-off phần cứng Storage cho FastShip

## 1\. Bối cảnh

Máy chủ cơ sở dữ liệu FastShip thường xuyên bị treo vào giờ cao điểm. Hệ thống cần:

* Tốc độ truy xuất dữ liệu cực nhanh.  
* Phục vụ hàng triệu đơn hàng real-time.  
* Bổ sung khoảng 2 TB dung lượng.  
* Ngân sách tối đa 20 triệu VNĐ.

---

## 2\. Đề xuất 2 giải pháp

### Giải pháp 1: Sử dụng HDD

Sử dụng HDD khoảng 2 TB cho máy chủ.

Ưu điểm:

* Giá thành trên mỗi GB thấp.  
* Dễ mua dung lượng lớn.  
* Phù hợp với nhu cầu lưu trữ dữ liệu lớn.

Nhược điểm:

* Tốc độ đọc/ghi chậm hơn SSD.  
* Độ trễ cao do có bộ phận cơ học.  
* Không phù hợp bằng SSD với cơ sở dữ liệu cần truy xuất real-time.  
* Có bộ phận chuyển động nên dễ hao mòn cơ học.

### Giải pháp 2: Sử dụng SSD

Sử dụng SSD khoảng 2 TB, ưu tiên loại phù hợp với máy chủ.

Ưu điểm:

* Tốc độ đọc/ghi rất nhanh.  
* Độ trễ thấp.  
* Không có bộ phận chuyển động cơ học.  
* Phù hợp với Database và hệ thống cần truy xuất dữ liệu liên tục.

Nhược điểm:

* Giá thành trên mỗi GB cao hơn HDD.  
* SSD dung lượng lớn có chi phí cao hơn.  
* Có giới hạn độ bền ghi, cần chọn loại phù hợp với workload máy chủ.

---

## 3\. So sánh HDD và SSD

| Tiêu chí | HDD | SSD |
| ----- | ----- | ----- |
| Tốc độ đọc/ghi | Chậm | Nhanh |
| Độ trễ | Cao | Thấp |
| Giá thành/GB | Rẻ hơn | Đắt hơn |
| Dung lượng | Dễ mua dung lượng lớn với giá thấp | Dung lượng lớn đắt hơn |
| Độ bền cơ học | Có bộ phận chuyển động | Không có bộ phận chuyển động |
| Database real-time | Hạn chế | Phù hợp hơn |

---

## 4\. Lựa chọn giải pháp

Chọn: SSD

Lý do:

1. FastShip yêu cầu tốc độ truy xuất cực nhanh, SSD có độ trễ thấp và tốc độ đọc/ghi cao hơn HDD.  
2. Database phải xử lý hàng triệu đơn hàng real-time, nên hiệu năng I/O rất quan trọng.  
3. Nhu cầu chỉ khoảng 2 TB, không quá lớn nên lợi thế giá/GB của HDD không phải yếu tố chính.  
4. Ngân sách 20 triệu VNĐ có thể dành cho một SSD dung lượng và hiệu năng phù hợp.

Nếu máy chủ hỗ trợ NVMe, có thể ưu tiên SSD NVMe để có độ trễ thấp và IOPS cao. Nếu server chỉ hỗ trợ SATA/SAS, cần chọn SSD đúng chuẩn tương thích.

---

## 5\. Ba bước nâng cấp Storage

### Bước 1: Khảo sát hệ thống

* Kiểm tra server hỗ trợ SATA, SAS hay NVMe.  
* Kiểm tra dung lượng hiện tại.  
* Kiểm tra tốc độ đọc/ghi và IOPS.  
* Kiểm tra cấu hình RAID.

### Bước 2: Lắp đặt và cấu hình

* Sao lưu dữ liệu quan trọng.  
* Lắp SSD mới.  
* Cấu hình RAID nếu cần.  
* Khởi tạo Storage.  
* Di chuyển Database hoặc dữ liệu sang Storage mới.

### Bước 3: Kiểm thử và vận hành

* Kiểm tra tốc độ đọc/ghi và độ trễ.  
* Kiểm thử Database với tải cao.  
* Theo dõi CPU, RAM và Disk I/O.  
* Nếu hệ thống ổn định thì đưa vào vận hành chính thức.

## Kết luận

FastShip nên ưu tiên SSD thay vì HDD vì yêu cầu quan trọng nhất là tốc độ truy xuất dữ liệu nhanh và xử lý đơn hàng real-time. Với nhu cầu khoảng 2 TB và ngân sách 20 triệu VNĐ, SSD phù hợp hơn về hiệu năng.

