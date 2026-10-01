# Bài 1 – Khởi tạo VPS và kết nối SSH

## 1. Mục tiêu

Thực hành khởi tạo một máy chủ VPS chạy Ubuntu Server trên nền tảng cloud và kết nối tới máy chủ bằng SSH Key thay vì đăng nhập bằng mật khẩu.

---

## 2. Thông tin VPS

| Thành phần | Thông tin |
|---|---|
| Nhà cung cấp | AZVPS |
| Tên VPS | `azvps-tm7e9b1th` |
| Gói VPS | Cheap 1 |
| Hệ điều hành | Ubuntu 22.04.1 LTS |
| RAM | 1 GB |
| Disk | 20 GB |
| IPv4 | `160.30.157.207` |
| Tài khoản | `root` |
| Trạng thái | Online |

---

## 3. Kiểm tra VPS trên AZVPS

Sau khi tạo VPS, kiểm tra trên giao diện quản lý AZVPS:

- VPS đang ở trạng thái **Online**.
- Hệ điều hành là **Ubuntu 22.04.1 LTS**.
- Có địa chỉ IPv4 để kết nối SSH.
- Tài khoản đăng nhập là `root`.

**Ảnh minh chứng:** `azvps-overview.png`

---

## 4. Kiểm tra SSH Key trên máy cá nhân

Trên Windows CMD:

```cmd
dir %USERPROFILE%\.ssh
```

Máy tính đã có SSH Key:

```text
C:\Users\Admin\.ssh\id_ed25519
C:\Users\Admin\.ssh\id_ed25519.pub
```

Kiểm tra public key:

```cmd
type %USERPROFILE%\.ssh\id_ed25519.pub
```

Trong đó:

- `id_ed25519`: private key, **không được chia sẻ**.
- `id_ed25519.pub`: public key dùng để cấu hình SSH.

---

## 5. Đăng nhập VPS lần đầu

```cmd
ssh root@160.30.157.207
```

Sau khi nhập mật khẩu:

```text
root@azvps-tm7e9b1th:~#
```

---

## 6. Cấu hình SSH Key trên VPS

Tạo thư mục SSH:

```bash
mkdir -p /root/.ssh
```

Mở file:

```bash
nano /root/.ssh/authorized_keys
```

Dán nội dung **public key** vào file, sau đó lưu lại.

Kiểm tra:

```bash
cat /root/.ssh/authorized_keys
```

Thiết lập quyền:

```bash
chmod 700 /root/.ssh
chmod 600 /root/.ssh/authorized_keys
```

---

## 7. Kết nối VPS bằng SSH Key

Thoát khỏi VPS:

```bash
exit
```

Từ Windows CMD:

```cmd
ssh -i %USERPROFILE%\.ssh\id_ed25519 root@160.30.157.205
```

Nếu cấu hình đúng, SSH sẽ đăng nhập mà **không yêu cầu nhập mật khẩu VPS**.

Kết quả:

```text
Welcome to Ubuntu 22.04.1 LTS
...
root@azvps-tm7e9b1th:~#
```

**Ảnh minh chứng:** `ssh-success.png`

---

## 8. Kiểm tra hệ điều hành

Sau khi đăng nhập:

```bash
lsb_release -a
```

Kết quả:

```text
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.1 LTS
Release:        22.04
Codename:       jammy
```

---

## 9. Kết quả đạt được

- [x] Tạo VPS trên **AZVPS**.
- [x] VPS sử dụng **Ubuntu 22.04.1 LTS**.
- [x] Có địa chỉ IP public.
- [x] Kết nối được bằng SSH.
- [x] Cấu hình Public Key vào `authorized_keys`.
- [x] Thiết lập quyền cho SSH.
- [x] Đăng nhập bằng SSH Key.
- [x] Không cần nhập mật khẩu khi đăng nhập bằng SSH Key.

---

## 10. Minh chứng nộp bài

Thư mục bài tập:

```text
homework/
└── session_02/
    └── ex1/
        ├── README.md
        ├── azvps-overview.png
        └── ssh-success.png
```

### Ảnh giao diện AZVPS

Ảnh nên thể hiện:

- Tên VPS.
- Trạng thái Online.
- IPv4.
- Hệ điều hành Ubuntu.
- Thông tin cấu hình VPS.

### Ảnh Terminal

Ảnh nên thể hiện:

```cmd
ssh -i %USERPROFILE%\.ssh\id_ed25519 root@160.30.157.205
```

và:

```text
Welcome to Ubuntu 22.04.1 LTS
root@azvps-tm7e9b1th:~#
```