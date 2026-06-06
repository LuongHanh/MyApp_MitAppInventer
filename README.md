# BÀI TẬP 1 - MÔN LẬP TRÌNH ỨNG DỤNG TRÊN THIẾT BỊ DI ĐỘNG
## GIÁO VIÊN HƯỚNG DẪN: TH.S ĐỖ DUY CỐP
## SINH VIÊN THỰC HIỆN: LƯỜNG VĂN HẠNH - MSSV: K225480106013

---

# MÔ TẢ ĐỀ BÀI & YÊU CẦU CỦA BÀI TẬP
Xây dựng một ứng dụng di động hoàn chỉnh trên nền tảng **MIT App Inventor** đáp ứng các tiêu chí kỹ thuật:
1. **Cấu trúc 3 Màn hình (Screens):**
   - **Screen1 (About):** Hiển thị thông tin cá nhân sinh viên, văn bản giới thiệu phần mềm và hệ thống nút điều hướng sang các màn hình còn lại.
   - **Screen2 (Xử lý bài toán):** Thực hiện giải quyết một bài toán thực tế (Quét mã QR, phân tích thuật toán logic nhận diện giao thức, lưu trữ và xử lý bộ lọc lịch sử thời gian thực).
   - **Screen3 (WebViewer):** Tích hợp trình duyệt nội bộ hiển thị trang web đích, hỗ trợ giao diện điện thoại mượt mà.
2. **Quy trình thực hiện:** Mô tả chi tiết thao tác trên thanh công cụ, kéo thả linh kiện, thay đổi thuộc tính (Designer) và tư duy xây dựng khối lệnh (Blocks).
3. **Đánh giá công nghệ:** Phân tích bản chất lập trình khối, ưu/nhược điểm so với viết mã nguồn truyền thống và kỹ thuật tái sử dụng khối lệnh (Backpack).

---

# BÀI LÀM

## TÊN ĐỀ TÀI: QR SHIELD ASSISTANT
**Ứng dụng Hỗ trợ Quét Mã QR An Toàn và Quản Lý Nhật Ký Truy Cập**

### I. Bối cảnh và Mục tiêu đề tài
Trong kỷ nguyên số, mã QR được sử dụng tràn lan dẫn đến các hình thức tấn công mạng thông qua mã QR độc hại (QR Phishing) ngày càng tinh vi. Ứng dụng **QR Shield Assistant** được xây dựng nhằm giúp người dùng chủ động phòng tránh các hiểm họa bảo mật bằng cách quét, phân tích độ tin cậy của liên kết (URL), đưa ra cảnh báo trực quan bằng hình ảnh/giọng nói, tích hợp trình duyệt nội bộ an toàn và quản lý lịch sử truy cập khoa học.

---

### II. Quy trình Tạo ra Phần mềm trên MIT App Inventor

Quy trình phát triển phần mềm trên MIT App Inventor được chia làm hai giai đoạn độc lập nhưng bổ trợ khăng khít cho nhau: **Thiết kế giao diện (Designer)** và **Lập trình tư duy logic (Blocks)**.

#### 1. Thao tác trên Thanh công cụ và Giao diện Designer
Giao diện Designer là nơi phân tách các thành phần hiển thị. Người dùng thực hiện chọn linh kiện từ thanh công cụ bên trái (**Palette**), kéo thả vào màn hình mô phỏng (**Viewer**), quản lý cấu trúc cây linh kiện (**Components**) và thay đổi thông số ở cột thuộc tính ngoài cùng bên phải (**Properties**).

##### A. Thanh công cụ (Palette) & Hành vi Kéo thả, Thay đổi thuộc tính:
- **User Interface (Giao diện):** - `Label`: Kéo thả để làm tiêu đề, hiển thị kết quả quét mã và chuỗi ký tự giới thiệu. Thay đổi thuộc tính `FontSize` (kích thước), `TextColor` (màu sắc) và tích chọn `HTMLFormat` để chuỗi text dài tự động ngắt dòng thẩm mỹ.
  - `Button`: Tạo các nút tương tác (Quét mã, Quay về, Xóa lịch sử). Thay đổi `BackgroundColor` thành màu đỏ, xanh để tăng tính định hướng trực quan.
  - `ListView`: Thành phần cốt lõi hiển thị danh sách dạng cuộn.
- **Layout (Bố cục):** Sử dụng `VerticalArrangement` (Khung dọc) và `HorizontalArrangement` (Khung ngang). Chỉnh thuộc tính `Width` và `Height` thành `Fill parent` để ép các linh kiện co giãn chuẩn theo tỷ lệ màn hình, tránh tình trạng nút bấm bị đẩy ra khỏi khu vực hiển thị của điện thoại.
- **Sensors (Cảm biến) & Media (Truyền thông):** Kéo thả `BarcodeScanner1` (Quét mã), `TextToSpeech1` (Phát giọng nói) và `Clock1` (Bộ đếm thời gian). Các linh kiện này có thuộc tính ẩn (*Non-visible components*), hoạt động ngầm để xử lý dữ liệu đầu vào.
- **Storage (Lưu trữ):** Thành phần `TinyDB1` dùng để lưu trữ dữ liệu bền vững xuống bộ nhớ flash của điện thoại, giúp dữ liệu không bị mất khi tắt app.

---

### III. Kiến trúc và Mô tả chi tiết 3 Màn hình chức năng

#### 📱 Màn hình 1: Trang chủ & Giới thiệu (Screen1 - Home)
- **Thiết kế giao diện (UI):** Chứa ảnh thẻ cá nhân sinh viên, nhãn hiển thị thông tin MSSV, lớp và một `Label` lớn định dạng text giới thiệu chi tiết về phần mềm (Nguồn gốc QR từ *the-qrcode-generator.com*, cơ chế lọc HTTP/HTTPS, lịch sử lưu trữ). Dưới cùng bố trí nút điều hướng sang Screen2.
- **Mục đích thay đổi thuộc tính:** Tích chọn thuộc tính `Icon` tại `Screen1` cấu hình logo ứng dụng vuông kích thước 512 x 512 px hiển thị trên màn hình nền điện thoại sau khi cài đặt.
<img width="959" height="454" alt="image" src="https://github.com/user-attachments/assets/31793cc1-d078-41cc-9deb-dd399f97aefe" />

<img width="959" height="506" alt="image" src="https://github.com/user-attachments/assets/f714a963-a578-4833-9031-b5346006a63b" />

<img width="959" height="451" alt="image" src="https://github.com/user-attachments/assets/110b6182-1d15-44bd-abfe-6031a4f1eaa2" />

#### 📱 Màn hình 2: Quét Mã & Giải quyết Bài toán Phân tích Logic + Lịch sử
Đây là màn hình xử lý trung tâm của ứng dụng, giải quyết bài toán kiểm tra an toàn hệ thống một cách triệt để.
<img width="959" height="500" alt="image" src="https://github.com/user-attachments/assets/1ccea0e1-505f-45d4-a6fb-c5b4f691fcbe" />

##### A. Thuật toán phân tích giải quyết bài toán:
Khi `BarcodeScanner1` nhận kết quả chuỗi URL (`get result`), hệ thống kích hoạt cấu trúc rẽ nhánh điều kiện `if... then... else` để bóc tách dữ liệu:
- **Nhận diện nguy cơ:** Sử dụng khối text `contains` để tìm kiếm các ký tự định dạng lỗi thời hoặc rút gọn mang tính rủi ro cao như `http://`, `.xyz`, `.top`, `bit.ly`.
  <img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/72715d3d-2656-47cc-913b-79988166bec7" />

- **Hành vi xử lý:**
    - **Nếu dính mã độc (`http://`...):** Giao diện đổi sang màu đỏ rực. Gọi `TextToSpeech1` phát giọng nói cảnh báo khẩn cấp. Nút "Truy cập ngay" bị ẩn, thay bằng nút màu vàng "Vẫn tiếp tục truy cập" để ép người dùng cân nhắc rủi ro.
    - **Nếu an toàn (`https://`...):** Giao diện bật màu xanh lá. Hệ thống dùng thuật toán nâng cao kết hợp chuỗi `split at first` để bóc tách, trích xuất nguyên xi tên miền chính (Domain Name) hiển thị lên nhãn cho người dùng nhận biết.
<img width="959" height="434" alt="image" src="https://github.com/user-attachments/assets/17655b16-68e7-4f06-8793-6eef85107051" />

##### B. Logic cấu trúc lưu trữ và hiển thị Nhật ký (Lịch sử):
Màn hình này sử dụng cơ chế đồng bộ song song **hai danh sách độc lập (List)** thông qua `TinyDB1`:
1. `LichSuQuet`: Lưu chuỗi hiển thị gồm: `[Kết quả trạng thái] + [URL] + [Ký tự xuống dòng \n] + [Thời gian định dạng dd/MM/yyyy HH:mm:ss trích xuất từ Clock1]`.
2. `LinkGoc`: Chỉ lưu duy nhất chuỗi URL sạch phục vụ cho việc kích hoạt mở trang web.
- **Ghim nút xóa ở đáy màn hình:** Toàn bộ `ListView1` và nút "Xóa lịch sử" được nhốt vào khung dọc đặt chiều cao cố định. Khi danh sách lịch sử dài ra, `ListView1` tự động kích hoạt thanh cuộn độc lập, giữ cho nút bấm xóa toàn bộ luôn nằm cố định ở đáy màn hình, không bị che khuất.
<img width="959" height="500" alt="image" src="https://github.com/user-attachments/assets/4dc6d31e-2594-4020-980e-3c034cde5ea3" />

<img width="959" height="449" alt="image" src="https://github.com/user-attachments/assets/cc63f60c-700b-4b50-9164-7d1984584728" />

#### 📱 Màn hình 3: Trình duyệt Nội bộ (Screen3 - WebViewer)
- **Nội dung:** Chứa thành phần `WebViewer1` chiếm 100% diện tích màn hình (`Fill parent`).
  <img width="959" height="503" alt="image" src="https://github.com/user-attachments/assets/adc8d268-644b-4d7b-9e38-299aa22fd955" />

- **Hành vi:** Khi người dùng chọn một mục trong lịch sử ở Màn hình 2 và nhấn "Truy cập Link", ứng dụng thực hiện lệnh `open another screen with start value`. Màn hình 2 sẽ gửi đi tham số URL sạch trích xuất từ danh sách `LinkGoc` dựa trên vị trí index (`SelectionIndex`).
- Sang đến Màn hình 3, sự kiện `when Screen3.Initialize` ngay lập tức bắt lấy tham số này thông qua khối `get start value` và truyền thẳng vào lệnh `call WebViewer1.GoToUrl` để tải trang web trực tiếp trong ứng dụng.

---

### IV. Bản chất của Lập trình Khối (Blocks) và Đánh giá Công nghệ

#### 1. Bản chất của việc kéo thả Block
Lập trình khối trong MIT App Inventor thực chất là một dạng **Lập trình trực quan (Visual Programming)**. Đằng sau mỗi khối lệnh đầy màu sắc (Khung điều khiển màu vàng, toán học màu xanh dương, biến số màu cam) là các đoạn mã nguồn Java/Kawa được đóng gói sẵn thành các hàm API. Việc lắp ghép các khớp nối của khối lệnh tuân thủ chặt chẽ tư duy logic toán học và lập trình hướng sự kiện (Event-driven programming) - ví dụ: *Khi sự kiện X xảy ra (Bấm nút) -> thực hiện hành động Y (Quét mã)*.

[Bản chất kết nối khối lệnh thực tế trong ứng dụng]
when ListView1 .AfterPicking do
   └── call Notifier1 .ShowChooseDialog (Hiển thị popup lựa chọn hành động)

#### 2. Ưu điểm và Nhược điểm so với viết Code truyền thống (Java/Kotlin/Flutter)

| Tiêu chí | Lập trình Khối (MIT App Inventor) | Lập trình Mã nguồn (Code truyền thống) |
| :--- | :--- | :--- |
| **Ưu điểm** | - **Tốc độ cực nhanh:** Loại bỏ hoàn toàn lỗi cú pháp (Syntax error) như thiếu dấu chấm phẩy `;`, sai đóng mở ngoặc `{}`.<br>- **Trực quan hóa logic:** Nhìn thấy luồng đi của dữ liệu thông qua màu sắc và hình khối, cực kỳ phù hợp cho việc phát triển nhanh (Prototyping).<br>- Quản lý vòng đời màn hình và phần cứng (Camera, DB) tự động, không cần khai báo quyền phức tạp. | - Kiểm soát tối đa hiệu năng phần cứng, can thiệp sâu vào nhân hệ điều hành.<br>- Giao diện tùy biến vô hạn, mượt mà, đáp ứng các hiệu ứng chuyển động phức tạp.<br>- Khả năng tối ưu dung lượng file cài đặt (APK/AAB) siêu nhỏ gọn. |
| **Nhược điểm** | - Khi ứng dụng có logic quá lớn, số lượng khối lệnh lên tới hàng ngàn sẽ gây hiện tượng rối mắt, khó quản lý (Spaghetti blocks).<br>- Giới hạn khả năng tùy biến giao diện chuyên sâu.<br>- Phụ thuộc vào các thư viện linh kiện có sẵn của nền tảng. | - Đường cong học tập dốc, tốn nhiều thời gian cấu hình môi trường.<br>- Chỉ một lỗi cú pháp nhỏ có thể khiến toàn bộ hệ thống ngừng biên dịch. |

#### 3. Kỹ thuật tái sử dụng mã nguồn bằng chiếc Balo (Backpack)
- **Khái niệm:** `Backpack` (Chiếc Balo) là một tính năng lưu trữ tạm thời cực kỳ thông minh nằm ở góc trên cùng bên phải của tab Blocks.
- **Cách thức hoạt động:** Khi sinh viên xây dựng xong một cụm khối phức tạp (Ví dụ: Cụm khối thuật toán phân tích chuỗi dài cắt tên miền ở nút quét mã `Button1`), thay vì phải kéo thả lại từng khối một ở nút bấm `Button2`, sinh viên chỉ cần click chuột phải vào cụm khối đó và chọn **"Add to Backpack"**.
- **Ý nghĩa thực tế:** Khi chuyển sang màn hình khác hoặc khối sự kiện khác, chỉ cần bấm mở chiếc Balo ra và kéo cụm khối đó thả vào vùng làm việc. Đây chính là biểu hiện trực quan của nguyên lý **DRY (Don't Repeat Yourself)** trong công nghệ phần mềm, giúp tiết kiệm 80% thời gian lập trình và hạn chế tối đa sai sót đồng bộ dữ liệu giữa các màn hình.

---

### V. Quy Trình Thực Hiện Chi Tiết Và Các Lưu Ý Kỹ Thuật

Phần này mô tả chi tiết quy trình xây dựng ứng dụng **QR Shield Assistant** trên nền tảng MIT App Inventor, chia làm 3 giai đoạn cốt lõi tương ứng với 3 màn hình.

---

#### 1. GIAI ĐOẠN 1: Thiết Kế & Lập Trình Điều Hướng (Screen1 - Home)

##### A. Quy trình thực hiện giao diện (Designer)
1. Chọn thành phần `Screen1` tại cột Components, di chuyển sang cột Properties bên phải ngoài cùng:
   - Thay đổi thuộc tính `AppName` thành `"QR Shield Assistant"`.
   - Tìm đến thuộc tính `Icon`, chọn `Upload File...` và tải lên tệp ảnh logo vuông dạng `.png` để làm ảnh đại diện cho ứng dụng trên điện thoại.
2. Kéo một `VerticalArrangement` (Khung dọc tổng) vào màn hình, đặt thuộc tính `Width = Fill parent` và `Height = Fill parent`.
3. Thả vào trong khung dọc các linh kiện:
   - Một `Image` để hiển thị ảnh thẻ cá nhân sinh viên.
   - Các `Label` hiển thị thông tin sinh viên (Họ tên, MSV, Lớp) và đoạn văn bản giới thiệu tổng quan các tính năng của phần mềm.
   - 2 `Button` làm nút bấm chuyển màn hình, chỉnh `Shape = Oval` và đổi màu nền nổi bật để hướng dẫn người dùng tương tác.
<img width="959" height="446" alt="image" src="https://github.com/user-attachments/assets/f2733bce-9922-4fd5-98f9-a53b0445f562" />

##### B. Quy trình lập trình khối (Blocks)
1. Vào danh mục khối của Button1, kéo sự kiện `when Btn_BatDau.Click do`.
2. Vào danh mục khối `Control`, kéo lệnh `open another screen screenName` gắn vào trong.
3. Lấy một khối chuỗi `text ""` kết nối vào ô `screenName` và gõ chính xác tên màn hình tiếp theo: `"Screen2"`.
<img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/a40419f7-dc8f-40a4-b652-8e237d075431" />

---

#### 2. GIAI ĐOẠN 2: Xử Lý Logic Trung Tâm & Đồng Bộ Lịch Sử (Screen2)

Đây là giai đoạn phức tạp nhất, tích hợp toàn bộ các tính năng cốt lõi của bài toán phân tích logic và hiển thị tất cả trên cùng một giao diện (All-in-one).

##### A. Quy trình thực hiện giao diện (Designer)
1. Khóa cứng chiều cao tổng thể bằng cách kéo một `VerticalArrangement` tổng (đặt tên là `Khung_GiaoDien_Tong`), chỉnh thuộc tính `Width = Fill parent` và `Height = Fill parent`.
2. **Khu vực Quét và Hiển thị kết quả (Nửa trên):**
   - Thả các `Button` kích hoạt quét mã, các `Label` hiển thị kết quả chuỗi URL nhận được sau khi camera bóc tách dữ liệu.
   - Kéo linh kiện ẩn `BarcodeScanner1` (trong mục Sensors) và `TextToSpeech1` (trong mục Media) thả ngầm vào màn hình.
3. **Khu vực Quản lý Lịch sử (Nửa dưới):**
   - Kéo một `Label` làm tiêu đề: `"LỊCH SỬ QUÉT MÃ"`.
   - Kéo linh kiện `ListView1` đặt ngay dưới tiêu đề. **Lưu ý cực kỳ quan trọng:** Phải đặt thuộc tính `Height = Fill parent` cho `ListView1` để nó tự động chiếm trọn vùng diện tích còn lại của màn hình.
   - Kéo nút bấm `Btn_XoaTatCa` xuống vị trí dưới cùng. 
   - Kéo linh kiện ẩn `TinyDB1` (trong mục Storage) và `Clock1` (trong mục Sensors) thả ngầm vào màn hình.
<img width="959" height="503" alt="image" src="https://github.com/user-attachments/assets/ae4af5b9-a24b-453d-96d2-221f311ed27c" />

##### B. Quy trình lập trình khối (Blocks)
Giai đoạn này xử lý 4 mạch logic tương tác chặt chẽ với nhau:

- **🛠️ Mạch 1: Đọc và Nạp dữ liệu ban đầu khi mở App (`Screen2.Initialize`)**
  - Gọi sự kiện `when Screen2.Initialize do`.
  - Ép `ListView1` tải lại toàn bộ nhật ký cũ từ bộ nhớ đệm bằng cách gọi lệnh `set ListView1.Elements to`.
  - Sử dụng khối `reverse list` bọc ngoài lệnh `call TinyDB1.GetValue` với tag `"LichSuQuet"` để đảo ngược danh sách (đưa các mục mới quét lên trên cùng đầu danh sách). 
  - *Lưu ý:* Tại ô `valueIfTagNotThere`, bắt buộc phải cắm khối `create empty list` để tránh lỗi ứng dụng bị crash trắng khi người dùng vừa cài đặt app lần đầu và DB chưa có dữ liệu.
<img width="959" height="278" alt="image" src="https://github.com/user-attachments/assets/34854732-cbed-480a-ac00-2c6e87349ee2" />

- **🛠️ Mạch 2: Quét mã, Phân tích chuỗi an toàn & Ghi nhật ký thời gian (`BarcodeScanner1.AfterScan`)**
  - Khi camera trả về kết quả chuỗi URL (`get result`), hệ thống dùng cấu trúc `if... then... else` để kiểm tra độ an toàn của chuỗi thông qua việc tìm kiếm ký tự `http://` hoặc `https://`.
  - Dùng khối toán học `add items to list` để đẩy phần tử mới vào 2 mảng lưu trữ toàn cục chạy song song:
    - Mảng hiển thị (`global LichSu`): Dùng khối `join` để ghép: `[Kết quả quét] + [\n 🕒 Lúc: ] + [call Clock1.FormatDateTime(instant: call Clock1.Now, pattern: "dd/MM/yyyy HH:mm:ss")]`.
    - Mảng link sạch (`global LinkGoc`): Chỉ lưu nguyên văn chuỗi URL thô để phục vụ điều hướng mở WebViewer sau này.
  - Gọi lệnh `call TinyDB1.StoreValue` để lưu đè ngay 2 mảng này vào bộ nhớ flash điện thoại.
  - Gọi lại khối cập nhật dữ liệu hiển thị `set ListView1.Elements to` để danh sách tự động nhảy số thời gian thực ngay trước mắt người dùng.
<img width="959" height="417" alt="image" src="https://github.com/user-attachments/assets/20f57701-6ff5-4500-87b7-b7f6cb6a6e53" />

<img width="959" height="503" alt="image" src="https://github.com/user-attachments/assets/f94d7316-1183-4024-b662-0c1e8b2dccb0" />

- **🛠️ Mạch 3: Click chọn dòng lịch sử và Xử lý điều hướng đa nhiệm (`ListView1.AfterPicking`)**
  - Khi người dùng click chọn một mục trên danh sách, gọi sự kiện `when ListView1.AfterPicking do`.
  - Gọi hộp thoại thông báo tùy chọn `call Notifier1.ShowChooseDialog` để hiển thị 2 nút bấm: `"Truy cập Link"` và `"Xóa mục này"`.
  - *Lưu ý nghiêm ngặt:* Tuyệt đối không được nạp lại dữ liệu `set ListView1.Elements to...` ở đầu khối này, vì việc nạp lại sẽ làm reset mất vị trí con trỏ chuột (`SelectionIndex`), khiến các khối lệnh phía sau không xác định được người dùng đang tương tác với dòng số mấy.
<img width="959" height="381" alt="image" src="https://github.com/user-attachments/assets/8324f03d-547c-4dd4-b880-8e75b9692835" />

- **🛠️ Mạch 4: Thực thi Lệnh Xóa từng dòng dùng biến cục bộ nâng cao**
  - Tại sự kiện `when Notifier1.AfterChoosing (get choice)`, nếu người dùng chọn `"Xóa mục này"`, hệ thống khởi tạo biến cục bộ `initialize local viTriThucTe to 0`.
  - Chuyển toàn bộ phép toán tìm chỉ số thực tế xuống phần ruột của ô `in`: `set viTriThucTe to (length of list(get global LichSu) + 1) - ListView1.SelectionIndex`. Thuật toán đảo ngược này giúp tìm chính xác vị trí phần tử gốc trong Database (vì hiển thị trên màn hình đã bị đảo ngược bằng `reverse list`).
  - Gọi lệnh `remove list item` cho cả 2 mảng dữ liệu dựa theo vị trí `viTriThucTe` vừa tính toán, sau đó lưu lại vào TinyDB và cập nhật màn hình.

<img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/77baa87b-90c0-453b-ad8b-4813077fac4a" />

#### 3. GIAI ĐOẠN 3: Trình Duyệt Nội Bộ Tốc Độ Cao (Screen3)

##### A. Quy trình thực hiện giao diện (Designer)
1. Thêm màn hình mới đặt tên chính xác là `Screen3`.
2. Kéo thành phần `WebViewer1` trong mục User Interface thả vào màn hình.
3. Chỉnh thuộc tính `Width = Fill parent` và `Height = Fill parent` để trình duyệt chiếm trọn không gian hiển thị, hỗ trợ tối đa giao diện hiển thị phiên bản di động của các trang web.
4. Bố trí một nút bấm `Btn_DongWeb` ở góc trên cùng để hỗ trợ người dùng thoát trang.
<img width="959" height="425" alt="image" src="https://github.com/user-attachments/assets/5c584166-da65-4fe8-821a-0fe2e7d9371c" />

##### B. Quy trình lập trình khối (Blocks)
1. Tại sự kiện `when Screen3.Initialize do`, gọi lệnh màu tím hành động `call WebViewer1.GoToUrl`.
2. Kết nối ô `url` của khối web với khối hệ thống `get start value` (nằm trong mục Control) để đón lấy tham số liên kết URL sạch do Màn hình 2 truyền sang thông qua lệnh `open another screen with start value`.
3. Lập trình nút đóng web: `when Btn_DongWeb.Click do` -> gọi lệnh `close screen`. Lệnh này sẽ tự động giải phóng bộ nhớ của Screen3 và đưa người dùng quay trở lại danh sách lịch sử của Screen2 một cách an toàn mà không làm mất trạng thái app.

<img width="959" height="448" alt="image" src="https://github.com/user-attachments/assets/d18dfad7-c467-4fe7-a9c3-e5a6825394d1" />

### VI. CÁC LƯU Ý KỸ THUẬT QUAN TRỌNG KHI TRIỂN KHAI APP

Trong quá trình xây dựng phần mềm, cần đặc biệt lưu ý các "bẫy" logic sau để đảm bảo ứng dụng vận hành ổn định, không phát sinh bug ngoài ý muốn:

- **Phân tách dữ liệu hiển thị và dữ liệu thực thi:** Do `ListView1` hiển thị chuỗi ký tự đã được chèn thêm ngày giờ (`\n 🕒 Lúc:...`), tuyệt đối không được bốc nguyên chuỗi chữ hiển thị này đi ép `WebViewer` chạy, điều đó sẽ dẫn đến lỗi không tìm thấy trang (Error 404). Bắt buộc phải duy trì mảng `LinkGoc` song song để lấy ra URL nguyên bản.
- **Đồng bộ hóa chỉ số mảng đảo ngược:** Khối `reverse list` chỉ đảo ngược lớp vỏ hiển thị trên `ListView`, không làm thay đổi thứ tự phần tử gốc trong `TinyDB`. Do đó, khi lập trình tính năng xóa một mục bất kỳ, bắt buộc phải dùng thuật toán lấy tổng số phần tử cộng 1 rồi trừ đi chỉ số đang chọn (`SelectionIndex`) để tìm ra vị trí thực tế trong cơ sở dữ liệu.
- **Ghim giao diện bằng Layout ép chiều cao:** Để nút "Xóa toàn bộ lịch sử" không bị đẩy văng xuống dưới khi danh sách lịch sử quét dài ra, bắt buộc các thành phần phải được bao bọc bởi một Khung dọc tổng có thuộc tính chiều cao cố định (`Fill parent`), đồng thời ép chiều cao của `ListView1` thành `Fill parent`. Điều này giúp ghim chặt nút bấm ở đáy màn hình và kích hoạt thanh cuộn nội bộ cho danh sách lịch sử.

---

### VII. Kết luận và Hướng phát triển
Ứng dụng **QR Shield Assistant** đã hoàn thành đầy đủ tất cả các yêu cầu của đề tài, giải quyết tốt bài toán phân tích bảo mật URL, tối ưu bố cục giao diện không bị che khuất và truyền nhận tham số mượt mà giữa 3 màn hình qua trình duyệt nội bộ. Hướng phát triển tiếp theo của ứng dụng là tích hợp các API kiểm tra link độc hại trực tuyến (như VirusTotal API) để tăng cường khả năng phòng vệ thời gian thực cho người dùng.

# Một số ảnh demo ứng dụng trên điện thoại

Copy link bất kỳ, ở đây em sử dụng youtube

<img width="959" height="491" alt="image" src="https://github.com/user-attachments/assets/3b7d9317-da33-41f1-a61a-f3704e4959c3" />

Dán link vừa copy vào https://www.the-qrcode-generator.com/ để tạo mã QR

<img width="959" height="508" alt="image" src="https://github.com/user-attachments/assets/c1c5e131-daf4-44db-b58d-8bfbe0825e44" />

Mở MIT AI2 Companion trên điện thoại và kết nối với máy tính qua AI Companion

<img width="959" height="489" alt="image" src="https://github.com/user-attachments/assets/a824b401-4e7e-4318-a93e-e6484ad59c41" />

<img width="959" height="502" alt="image" src="https://github.com/user-attachments/assets/f5c2716c-e584-4036-bb44-03d5fb17d826" />

<img width="480" height="1080" alt="image" src="https://github.com/user-attachments/assets/83ae8545-1645-4a94-9181-2c8756fa84a2" />

Thực hiện quét mã

<img width="480" height="1080" alt="11" src="https://github.com/user-attachments/assets/702b82b7-d007-4123-b540-e8a697e0a2d5" />

<img width="480" height="1080" alt="image" src="https://github.com/user-attachments/assets/2a9243c6-daab-4170-ad23-8d13a7ff2c7b" />

Ấn nút Truy cập ngay sẽ ra được web ta cần

<img width="480" height="1080" alt="image" src="https://github.com/user-attachments/assets/6b5da9ee-942d-4317-b3db-725fe9c87adf" />

Ấn nút Quay lại, ta sẽ thấy lịch sử mới nhất được hiển thị rõ ràng kèm ngày giờ cụ thể và có thể truy cập bất cứ lúc nào.

<img width="480" height="1080" alt="image" src="https://github.com/user-attachments/assets/42c6a8ba-7d74-4088-aafc-152c3344d901" />

Trường hợp link không an toàn; ta đổi https sang http của link vừa rồi; app sẽ nhận diện link có nguy cơ nguy hiểm

<img width="480" height="1080" alt="image" src="https://github.com/user-attachments/assets/3e2a2f37-8dfa-431d-b1b7-ff47a461ecb1" />

<img width="480" height="1080" alt="image" src="https://github.com/user-attachments/assets/3dffb0ec-a84f-479a-88f5-a36e4f7e9dde" />
