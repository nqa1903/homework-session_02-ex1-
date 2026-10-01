# Bài 1: Khởi tạo Droplet trên DigitalOcean

## 1. Mục tiêu

- Đăng ký tài khoản DigitalOcean, chọn cấu hình phù hợp và khởi tạo Droplet chạy Ubuntu 22.04 LTS.
- Xác thực bằng cặp khóa SSH (ed25519) thay vì mật khẩu và kết nối thành công từ máy cá nhân bằng tài khoản `root`.

## 2. Cấu hình đã chọn

| Mục | Giá trị |
|---|---|
| Region | Singapore (SGP1) |
| Image | Ubuntu 22.04 (LTS) x64 |
| Droplet Type | Basic |
| CPU options | Regular (SSD) |
| Size | `<điền gói bạn chọn, ví dụ $4/mo>` |
| Authentication | SSH Key |
| Hostname | `<điền hostname>` |

## 3. Tạo cặp khóa SSH trên máy cá nhân

```bash
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/do_droplet
```

Lệnh tạo ra hai file:

- `~/.ssh/do_droplet`: private key (giữ bí mật, không đưa lên GitHub).
- `~/.ssh/do_droplet.pub`: public key (dán vào DigitalOcean).

Xem nội dung public key để copy:

```bash
# Linux / macOS / Git Bash
cat ~/.ssh/do_droplet.pub

# Windows PowerShell
Get-Content $env:USERPROFILE\.ssh\do_droplet.pub
```

> 📷 **Chèn ảnh/log bước tạo khóa của bạn:** `![ssh-keygen](images/01-ssh-keygen.png)`

## 4. Thêm Public Key vào DigitalOcean

1. Đăng nhập DigitalOcean, vào **Settings → Security → SSH Keys**.
2. Bấm **Add SSH Key**.
3. Dán toàn bộ nội dung file `do_droplet.pub`, đặt tên cho khóa rồi lưu.

> 📷 **Chèn ảnh:** `![add-ssh-key](images/02-add-ssh-key.png)`

## 5. Tạo Droplet

1. Bấm **Create → Droplets**.
2. Chọn Region **Singapore**.
3. Chọn Image **Ubuntu 22.04 (LTS) x64**.
4. Chọn **Basic → Regular (SSD)** và gói rẻ nhất.
5. Ở mục **Authentication**, chọn **SSH Key** và tick vào khóa đã thêm.
6. Đặt hostname và bấm **Create Droplet**.
7. Đợi Droplet khởi tạo xong và ghi lại địa chỉ IPv4.

> 📷 **Chèn ảnh trang tạo Droplet:** `![create-droplet](images/03-create-droplet.png)`
>
> 📷 **Chèn ảnh trang quản lý Droplet (thấy tên, IP, region, image):** `![droplet-dashboard](images/04-droplet-dashboard.png)`

## 6. Kết nối SSH

```bash
ssh -i ~/.ssh/do_droplet root@<IP_ADDRESS_DROPLET>
```

Lần đầu kết nối, SSH hỏi xác nhận fingerprint của máy chủ, nhập `yes`.

**Log kết nối thành công:**

```text
<dán log terminal của bạn ở đây: dòng lệnh ssh và màn hình chào Ubuntu>
```

> 📷 Hoặc chèn ảnh chụp terminal: `![ssh-success](images/05-ssh-success.png)`

Kết quả: truy cập được vào shell của Droplet mà không cần nhập mật khẩu.

## 7. Khó khăn gặp phải và cách xử lý

- `<ghi lỗi bạn thực sự gặp, nếu có. Ví dụ: Permission denied (publickey), UNPROTECTED PRIVATE KEY FILE>`
- Cách xử lý: `<...>`

## 8. Kết luận

`<1-2 câu về những gì bạn học được: vì sao dùng SSH key an toàn hơn mật khẩu, cách chọn cấu hình tiết kiệm chi phí...>`
