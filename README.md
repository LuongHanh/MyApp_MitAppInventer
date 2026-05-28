# BÀI TẬP 1 - MÔN LẬP TRÌNH ỨNG DỤNG TRÊN THIẾP BỊ DI ĐỘNG
## LƯỜNG VĂN HẠNH - K225480106013

# MÔ TẢ ĐỀ BÀI
Xây dựng 1 app chủ đề tùy chọn.
Có 3 màn hình
 - Màn hình 1: Hiển thị thông tin và có link đến màn hình 2, 3
 - Màn hình 2 + 3: Làm gì đó?
 - Sử dụng linh hoạt, dùng các thư viện như: Chuyển văn bản thành giọng nói, chuyển giọng nói thành văn bản, đọc QR xử lý gì đó...

# BÀI LÀM

## TÊN ĐỀ TÀI: QR Shield Assistant
**Ứng dụng Hỗ trợ Quét Mã QR An Toàn và Quản Lý Nhật Ký Truy Cập**

### 1. Bối cảnh và Mục tiêu đề tài
Trong bối cảnh mã QR đang được sử dụng tràn lan như hiện nay, các hình thức tấn công mạng thông qua mã QR độc hại (QR Phishing) ngày càng tinh vi. Ứng dụng **QR Shield Assistant** được xây dựng nhằm giúp người dùng chủ động phòng tránh các hiểm họa bảo mật. 

Ứng dụng sẽ thực hiện quét, phân tích độ tin cậy của đường liên kết (URL) ẩn sau mã QR, đưa ra cảnh báo trực quan trước khi truy cập và tự động lưu trữ nhật ký quét để người dùng dễ dàng quản lý.

---

### 2. Kiến trúc và Mô tả chi tiết 3 Màn hình chức năng

#### 📱 Màn hình 1: Màn hình chính (Home / Dashboard)
* **Nội dung hiển thị:**
  * Thông tin sinh viên thực hiện và bản quyền ứng dụng.
  * Giao diện chào mừng trực quan, thân thiện với người dùng.
* **Chức năng chính:** 
  * Cung cấp các nút điều hướng (hoặc menu) để chuyển hướng nhanh sang **Màn hình 2** (Bắt đầu quét mã) và **Màn hình 3** (Xem lịch sử bảo mật).

#### 📱 Màn hình 2: Quét Mã & Phân Tích Cảnh Báo Bảo Mật
* **Luồng hoạt động:** Người dùng kích hoạt camera để quét mã QR chứa đường dẫn URL. Hệ thống tiến hành bóc tách dữ liệu và đối chiếu thực hiện phân loại bảo mật.
* **Xử lý logic & Giao diện ứng xử:**
  * **Trường hợp URL An toàn:** Giao diện hiển thị nhãn xanh (**Safe**). Kích hoạt (`enable`) nút "Truy cập ngay" để mở trình duyệt trực tiếp.
  * **Trường hợp URL Nghi ngờ/Độc hại:** Giao diện chuyển sang tông màu đỏ cảnh báo nguy hiểm. Nút truy cập nhanh bị vô hiệu hóa (`disable`). Hệ thống hiển thị một nút chờ với dòng chữ **"Tôi biết rủi ro, Vẫn tiếp tục truy cập"** nhằm buộc người dùng phải xác nhận trước khi mở liên kết.
* **Tích hợp thư viện nâng cao:** Sử dụng thư viện **Text-to-Speech (TTS)** để phát âm thanh cảnh báo bằng giọng nói (Ví dụ: *"Cảnh báo: Liên kết này có dấu hiệu lừa đảo, hãy cẩn trọng"*).

#### 📱 Màn hình 3: Nhật Ký & Lịch Sử Bảo Mật (Security Log)
* **Nội dung hiển thị:** Danh sách (`ListView`) toàn bộ các mã QR đã từng quét, được sắp xếp theo thứ tự thời gian mới nhất lên đầu.
* **Chi tiết cấu trúc mỗi dòng log (Item):**
  * **Tiêu đề liên kết:** Tên miền hoặc tiêu đề ước lượng của link.
  * **Đường dẫn URL chi tiết.**
  * **Trạng thái bảo mật:** Hiển thị trực quan bằng màu sắc/icon (An toàn hoặc Nguy hiểm).
  * **Thời gian chi tiết:** Ngày, giờ cụ thể khi thực hiện hành vi quét (Định dạng: `HH:mm - DD/MM/YYYY`).
* **Chức năng phụ:** Hỗ trợ tính năng xóa lịch sử hoặc bấm vào từng log để xem lại chi tiết.

---

### 3. Các công nghệ và Thư viện dự kiến sử dụng
* **QR Scanner Library:** Tích hợp camera quét mã QR thời gian thực (ví dụ: `ZXing` cho Android hoặc `mobile_scanner` cho Flutter).
* **Text-to-Speech (TTS):** Sử dụng Engine giọng nói mặc định của hệ điều hành để tối ưu hiệu năng và xử lý offline.
* **Local Database:** Sử dụng `SQLite` / `Room Database` (Android) hoặc `Sqflite` / `Hive` (Flutter) để lưu trữ bền vững dữ liệu lịch sử quét tại Màn hình 3.

## Cài đặt và triển khai app

Truy cập https://appinventor.mit.edu/
<img width="959" height="427" alt="image" src="https://github.com/user-attachments/assets/5e7de1b0-d2ee-4ba0-9658-57e3eda7ddc7" />

<img width="1919" height="948" alt="image" src="https://github.com/user-attachments/assets/64d9d2c6-9e5c-4828-b4ce-761cdc1185fb" />

<img width="1919" height="906" alt="image" src="https://github.com/user-attachments/assets/bbb78be4-ea7b-4c2a-9b7a-173f5f2997a8" />

Sau đó, ta thực hiện thiết kế UI

<img width="1919" height="869" alt="image" src="https://github.com/user-attachments/assets/c435d5ff-5206-4ea9-8b8f-e8a686c565e2" />

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/bb39513e-5894-40e7-81d7-d74a70f788ad" />

<img width="1919" height="991" alt="image" src="https://github.com/user-attachments/assets/ef292405-6cd1-4aeb-a2ee-fea8464fc29c" />

