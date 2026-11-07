# 🚀 CareerHub - Cổng Thông Tin Tuyển Dụng & Việc Làm Hàng Đầu

> **Đồ Án Môn Học CMS (WordPress)**  
> Nền tảng tuyển dụng việc làm trực tuyến chuyên nghiệp, hiện đại, vận hành trên kiến trúc **Docker & Docker Compose** (WordPress, MariaDB, phpMyAdmin).

---

## 📸 Giao diện tổng quan (Preview)

<p align="center">
  <img src="docs/screenshots/careerhub-homepage.jpg" alt="CareerHub Homepage Preview" width="100%" style="border-radius: 8px; box-shadow: 0 4px 12px rgba(0,0,0,0.15);" />
</p>

---

## ✨ Tính năng nổi bật

### 🎯 1. Dành cho Ứng viên (Job Seekers)
- **Tìm kiếm việc làm thông minh:** Bộ lọc đa tiêu chí ngay tại Hero Banner (theo từ khóa, chức danh, kỹ năng và vị trí địa lý).
- **Top Jobs:** Danh sách các vị trí tuyển dụng hàng đầu hiển thị trực quan (tên công việc, nhà tuyển dụng, địa điểm, chế độ làm việc và mô tả ngắn).
- **Trang chi tiết việc làm (Job Detail):** Cung cấp đầy đủ thông tin mô tả công việc, yêu cầu ứng viên, chế độ đãi ngộ và hạn nộp hồ sơ.
- **Nộp đơn trực tuyến (Online Apply):** Đính kèm CV và gửi thông tin ứng tuyển trực tiếp đến nhà tuyển dụng.
- **Cẩm nang nghề nghiệp (Newest Blog Entries):** Chuyên mục tin tức chia sẻ kinh nghiệm phỏng vấn, xu hướng tuyển dụng thời AI, kỹ năng giao tiếp và bí quyết tối ưu CV.
- **Đăng ký nhận bản tin (Newsletter):** Nhận email thông báo cơ hội việc làm mới định kỳ.

### 🏢 2. Dành cho Nhà tuyển dụng (Employers)
- **Đăng tin tuyển dụng (Submit Job):** Form nhập thông tin tuyển dụng nhanh chóng và chuyên nghiệp.
- **Hồ sơ doanh nghiệp (Company Profile):** Trang giới thiệu công ty, văn hóa doanh nghiệp và danh sách các vị trí đang mở.
- **Quản lý tin tuyển dụng (Job Dashboard):** Theo dõi trạng thái tin đăng và danh sách hồ sơ ứng tuyển.

### ⚙️ 3. Quản trị & Công nghệ (Tech Stack)
- **Nền tảng:** WordPress 6.x (PHP 8.3 Apache Container).
- **Cơ sở dữ liệu:** MariaDB 10.11 với volume lưu trữ bền vững.
- **Công cụ quản lý DB:** phpMyAdmin trực quan qua web.
- **Theme & Giao diện:** Theme **JobScout** tùy biến cao, tích hợp công cụ kéo thả **Elementor Page Builder** hỗ trợ tùy biến CSS/Layout linh hoạt.
- **Trợ năng (Accessibility):** Tích hợp công cụ hỗ trợ người dùng khiếm thị / khó thao tác theo tiêu chuẩn WCAG.
- **Gửi nhận Email:** Tích hợp cấu hình WP Mail SMTP & Contact Form 7.

---

## 📂 Cấu trúc thư mục

```text
JobScout/
├── .env                  # Cấu hình biến môi trường (Database credentials, Port)
├── .env.example          # File mẫu cấu hình môi trường
├── docker-compose.yml    # Cấu hình dịch vụ Docker (WordPress, MariaDB, phpMyAdmin)
├── database.sql          # File sao lưu cơ sở dữ liệu mẫu mới nhất
├── docs/                 # Tài liệu & hình ảnh chụp giao diện
│   └── screenshots/
│       └── careerhub-homepage.jpg
├── docker/
│   └── uploads.ini       # Cấu hình tối ưu PHP (upload 64MB, memory 256MB)
└── wordpress/            # Mã nguồn WordPress (gắn kết trực tiếp volume vào container)
    └── wp-content/
        ├── plugins/      # Các plugin: WP Job Manager, Elementor, SMTP, Newsletter...
        └── themes/       # Theme JobScout
```

---

## 🛠️ Hướng dẫn cài đặt & Khởi chạy

### Điều kiện tiên quyết:
- Đã cài đặt và đang bật **[Docker Desktop](https://www.docker.com/products/docker-desktop/)**.
- Hỗ trợ tốt trên **Windows (WSL2), macOS và Linux**.

---

### Bước 1: Cấu hình Domain cục bộ (Khuyên dùng)
Để hệ thống hoạt động đầy đủ tính năng và đúng link điều hướng của WordPress, hãy thêm dòng sau vào file `hosts` của máy tính:

- **Windows:** Mở Notepad với quyền Administrator file `C:\Windows\System32\drivers\etc\hosts`
- **macOS / Linux:** Mở terminal chạy `sudo nano /etc/hosts`

Thêm dòng sau vào cuối file và lưu lại:
```text
127.0.0.1 wordpress.local
```

---

### Bước 2: Tạo file cấu hình `.env`
Nhân bản file `.env.example` thành `.env`:
```bash
# Trên Windows PowerShell
Copy-Item .env.example .env

# Trên Linux / macOS
cp .env.example .env
```
*(Mặc định `.env` đã cấu hình `WP_PORT=80`, `PMA_PORT=8081` và thông tin kết nối MariaDB).*

---

### Bước 3: Khởi động hệ thống Docker
Tại thư mục gốc của dự án, mở Terminal / PowerShell và chạy:
```bash
docker compose up -d
```
> Quá trình khởi động sẽ tạo mạng nội bộ và chạy 3 container: `wordpress_db`, `wordpress_app`, `wordpress_pma`.

---

### Bước 4: Import Cơ sở dữ liệu mẫu
Sau khi container database chuyển sang trạng thái **healthy**, tiến hành nạp dữ liệu từ file `database.sql`:

```bash
# Trên Windows PowerShell / Command Prompt:
cmd /c "docker exec -i wordpress_db mariadb -u wp_user -pwp_user_password cms-cuoiky < database.sql"

# Trên macOS / Linux:
docker exec -i wordpress_db mariadb -u wp_user -pwp_user_password cms-cuoiky < database.sql
```

---

## 🌐 Địa chỉ truy cập hệ thống

| Phân hệ | Đường dẫn truy cập | Ghi chú |
| :--- | :--- | :--- |
| **Trang chủ CareerHub** | [http://wordpress.local](http://wordpress.local) | Giao diện người dùng chính thức |
| **Quản trị viên (Admin)** | [http://wordpress.local/wp-admin](http://wordpress.local/wp-admin) | Dashboard quản lý WordPress |
| **phpMyAdmin** | [http://localhost:8081](http://localhost:8081) | Quản trị CSDL MariaDB trực quan |

---

## 🔑 Thông tin đăng nhập mặc định

### 1. Quản trị WordPress (Admin Portal)
- **Đường dẫn:** `http://wordpress.local/wp-login.php`
- **Tài khoản:** `root`
- **Mật khẩu:** `admin123`

### 2. Tài khoản Demo kiểm thử phân quyền
| Loại tài khoản | Username | Password | Quyền hạn |
| :--- | :--- | :--- | :--- |
| **Nhà tuyển dụng** | `employer_demo` | `demo123` | Đăng tin tuyển dụng, xem ứng viên nộp hồ sơ |
| **Người tìm việc** | `jobseeker_demo` | `demo123` | Tìm kiếm, lưu việc làm, nộp CV ứng tuyển |

### 3. phpMyAdmin
- **Server:** `db`
- **Tài khoản Root:** `root` / `root_secret_password`
- **Tài khoản thường:** `wp_user` / `wp_user_password`
- **Tên cơ sở dữ liệu:** `cms-cuoiky`

---

## 💻 Các lệnh quản lý thường dùng

```bash
# Xem trạng thái các container đang chạy
docker compose ps

# Xem nhật ký hoạt động (logs) của WordPress
docker compose logs -f wordpress

# Dừng toàn bộ hệ thống
docker compose down

# Khởi động lại hệ thống
docker compose restart

# Export (sao lưu) dữ liệu mới nhất từ container ra database.sql
cmd /c "docker exec wordpress_db mariadb-dump -u wp_user -pwp_user_password cms-cuoiky > database.sql"

# Xóa toàn bộ dữ liệu database volume để nạp lại từ đầu
docker compose down -v
```

---

<p align="center">
  <i>Được phát triển phục vụ mục đích học tập & nghiên cứu đồ án môn học Quản Trị Nội Dung (CMS).</i>
</p>
