# Bài 1: Khởi tạo Droplet trên DigitalOcean

## Mục tiêu
- Thực hành đăng ký tài khoản, lựa chọn cấu hình phần cứng phù hợp và khởi tạo thành công Droplet chạy hệ điều hành Ubuntu Server trên hạ tầng đám mây DigitalOcean.
- Cấu hình xác thực an toàn bằng cặp khóa SSH (SSH Keypair) thay vì mật khẩu thô và thực hiện kết nối thành công từ máy cá nhân.

## Các bước thực hiện chi tiết

### Bước 1: Tạo khóa SSH trên máy tính cá nhân
Mở Terminal (hoặc PowerShell/Command Prompt trên Windows) và chạy lệnh sau để tạo cặp khóa SSH mới:
```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```
*(Bạn có thể thay đổi email bằng email cá nhân của mình. Cứ nhấn Enter để lưu vào đường dẫn mặc định và có thể bỏ qua passphrase nếu muốn).*

Khóa công khai (Public Key) sẽ được lưu tại `~/.ssh/id_ed25519.pub` (đối với Windows thường là `C:\Users\Tên_User\.ssh\id_ed25519.pub`). 
Mở file này và copy toàn bộ nội dung bên trong để sử dụng cho bước sau.

### Bước 2: Khởi tạo Droplet trên DigitalOcean
1. Đăng nhập vào DigitalOcean Console. Nhấn vào nút **Create** ở góc trên cùng bên phải và chọn **Droplets**.
2. **Choose Region**: Chọn khu vực **Singapore** (đây là khu vực gần Việt Nam nhất giúp tối ưu độ trễ).
3. **Choose an image**: Chọn hệ điều hành **Ubuntu**, phiên bản **22.04 LTS** (hoặc mới nhất).
4. **Choose Size**:
   - Chọn **Basic** plan.
   - Chọn **Regular SSD**.
   - Chọn CPU loại **Shared** (chọn gói rẻ nhất, ví dụ: $4/tháng hoặc $6/tháng).
5. **Choose Authentication Method**:
   - Chọn **SSH Keys**.
   - Nhấn vào **New SSH Key**.
   - Dán toàn bộ nội dung khóa công khai đã copy ở Bước 1 vào ô trống. Đặt tên cho khóa để dễ quản lý, sau đó nhấn **Add SSH Key**.
6. Kéo xuống dưới, đặt tên cho Droplet (tùy chọn) và nhấn **Create Droplet**.

> *Chèn ảnh chụp màn hình giao diện quản lý Droplet trên DigitalOcean sau khi tạo thành công (hiển thị rõ IP của máy chủ) vào đây:*
> 
> `[Chèn ảnh chụp DigitalOcean Console tại đây]`

### Bước 3: Kết nối tới Droplet qua SSH
Đợi khoảng vài phút để Droplet được khởi tạo hoàn tất. Khi đó, DigitalOcean sẽ cấp cho máy chủ một địa chỉ IPv4 (Public IP). Hãy copy địa chỉ IP này.

Mở lại Terminal trên máy cá nhân và chạy lệnh kết nối (thay `<IP_ADDRESS_DROPLET>` bằng IP bạn vừa copy):
```bash
ssh -i ~/.ssh/id_ed25519 root@<IP_ADDRESS_DROPLET>
```

> *Ghi chú: Nếu bạn sử dụng đường dẫn khóa khác lúc tạo, hãy thay `~/.ssh/id_ed25519` bằng đường dẫn tới file Private Key thực tế của bạn.*

Hệ thống sẽ hỏi xác nhận kết nối (fingerprint), hãy gõ `yes` và nhấn Enter. 
Truy cập thành công, bạn sẽ thấy dấu nhắc lệnh của Ubuntu Server mà không cần phải nhập mật khẩu rườm rà.

> *Chèn ảnh chụp màn hình log Terminal kết nối thành công vào máy chủ Ubuntu vào đây:*
> 
> `[Chèn ảnh chụp log Terminal tại đây]`
