# Cấu hình Chặn Quảng Cáo YouTube Cho Shadowrocket

Dự án này chứa cấu hình cá nhân để chặn quảng cáo YouTube trên iOS sử dụng Shadowrocket thông qua phương pháp MitM (Man-in-the-Middle). Dựa trên module của Maasea và quy tắc Johnshall, tối ưu hóa băng thông bằng việc tải script trực tiếp từ GitHub để tránh hiện tượng phân rã mã lệnh (Script Decay).

## Tính năng nổi bật
- **Main.conf**: Tích hợp các quy tắc định tuyến tối ưu (dựa trên Johnshall) và kết hợp thêm bộ lọc chặn quảng cáo, tracker của Việt Nam (từ hostsVN).
- **YouTube.sgmodule**: Mượn mã nguồn mạnh mẽ của Maasea để bóc tách tệp định dạng JSON. Chặn hoàn toàn quảng cáo YouTube (kể cả trên trang chủ, trong video, shorts) và mở khóa tính năng tự động phát trong nền (Background Playback) giống như tài khoản Premium.

---

## Hướng dẫn cài đặt

### Bước 1: Thêm Cấu hình chính (Main.conf)
1. Mở ứng dụng Shadowrocket trên iOS.
2. Tại màn hình **Home**, nhấn vào tên cấu hình hiện tại đang chọn để mở danh sách cấu hình (Local Files).
3. (Tùy chọn) Chọn biểu tượng dấu `+` góc phải màn hình, chọn **Download Config** và dán link RAW `.conf` trên repo GitHub của bạn, hoặc copy thẳng file `Main.conf` từ máy tính sang app thông qua tính năng Import.
4. Chạm vào cấu hình `Main.conf` vừa được liệt kê và chọn **Use Configuration** (Sử dụng Cấu hình).

### Bước 2: Thêm các Module tăng cường
Bạn có thể thêm các module để kích hoạt thêm nhiều tính năng cho thiết bị của mình mà không lo bị ghi đè sau mỗi lần Actions tự động chạy:

**1. Module YouTube (YouTube.sgmodule)**
- Mở tab **Modules** ở phần dưới cùng của màn hình chính Shadowrocket.
- Nhấn vào dấu `+` ở góc trên cùng bên phải và dán link RAW tới `YouTube.sgmodule` trên GitHub của bạn.
- Nếu thành công, module `YouTube Enhance (Shadowrocket)` sẽ hiện ra. Hãy đảm bảo công tắc bên cạnh nó báo màu xanh.

**2. Module NextDNS (NextDNS.sgmodule)**
- Tương tự như trên, copy link RAW của `NextDNS.sgmodule` trên GitHub và import vào bằng dấu `+` trong mục **Modules**.
- Sau khi được tải xuống (tên sẽ hiện là `NextDNS (DoH)`), bấm vào **biểu tượng chữ `i`** (hoặc nhấn giữ/nhấn vào dòng code phụ thuộc phiên bản giao diện) cạnh tên module đó.
- Sẽ có một ô điền thông số có tên `NextDnsID`. Bạn hãy nhập ID NextDNS ngắn của mình vào (ví dụ: `123abc`).
- Đảm bảo công tắc màu xanh được bật là máy tính của bạn đã chạy NextDNS.

### Bước 3: Kích hoạt Giải mã HTTPS (QUAN TRỌNG)
*Bạn bắt buộc phải thực hiện bước này để Shadowrocket có thể can thiệp được định dạng HTTPS của YouTube.*

1. Trong tab **Home**, nhấn vào chữ `i` bên cạnh cấu hình `Main.conf`.
2. Chọn **HTTPS Decryption** (Giải mã HTTPS).
3. Bật công tắc kích hoạt HTTPS lên.
4. Chọn **Generate a new certificate** (Tạo chứng chỉ mới) và sau đó nhấn **Install Certificate** (Cài đặt chứng chỉ).
5. Hồ sơ cấu hình này sẽ được tải về máy của bạn. Mở ứng dụng **Cài đặt (Settings)** cài mặc định trên iPhone -> Bấm vào thông báo **Đã tải về hồ sơ (Profile Downloaded)** phía trên cùng. (Hoặc Cài đặt Chung -> Quản lý VPN & Thiết bị). 
6. Cấp quyền cài đặt bằng mật khẩu mở khóa màn hình thiết bị.
7. **BẮT BUỘC:** Vào **Cài đặt chung (General)** -> Nhấn **Giới thiệu (About)** -> Cuộn xuống khu vực dưới cùng chọn **Cài đặt tin cậy chứng chỉ (Certificate Trust Settings)**. 
8. Bật công tắc gạt sang màu xanh (Full Trust) cho chứng chỉ do *Shadowrocket* cấp phát.

### Bước 4: Tận hưởng
- Bật công tắc `Not Connected` trên cùng ở màn hình Shadowrocket để mở đường hầm VPN (hãy đảm bảo đang dùng `Global Routing` là `Config` để tối ưu mạng cá nhân).
- Mở ứng dụng YouTube và dùng bình thường. Nếu ở lần đầu vẫn thấy video còn dính quảng cáo, hãy đăng xuất tài khoản YouTube của bạn rồi đăng nhập lại hoặc gỡ app YouTube tải mới để ép hệ thống xóa bộ nhớ đệm (Cache). 

Chúc bạn có trải nghiệm YouTube iOS sạch sẽ và cực kì mượt mà!


## Tính năng Tự động Cập nhật (Auto-Update)
Cấu hình này đã tích hợp **GitHub Actions Workflow** (.github/workflows/auto_update.yml) giúp tự động cập nhật bản chặn quảng cáo mới nhất của hệ thống Johnshall về vào lúc 7:00 sáng mỗi ngày. Khi tải về, hệ thống tự động dịch các chú thích ra tiếng Anh và thêm bộ lọc nội địa Việt Nam (hostsVN).

*Riêng tệp YouTube.sgmodule sẽ không cần cập nhật file bằng Actions vì trong đó đã lập trình kéo URL bản vá lỗi từ nguồn của Maasea (script-path=https://raw...) liên tục vào thời gian thực.*

**Cách thiết lập trên GitHub:**
1. Đi tới phần **Settings** trên Kho lưu trữ Repository của bạn.
2. Chọn **Actions** -> **General**.
3. Cuộn xuống phần Workflow permissions, đánh dấu tích vào **Read and write permissions**.
4. Nhấn **Save**. Hành động tự động lấy file mỗi ngày sẽ chính thức chạy bảo vệ thiết bị bạn!
