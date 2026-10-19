# 🚀 Hướng Dẫn Cài Đặt SASS Bằng npm & SASS CLI

> Dự án thực hành môn Phát Triển Giao Diện Web - CodeGym.  
> Cung cấp quy trình làm việc chuẩn công nghiệp từ cài đặt môi trường, biên dịch tệp đơn lẻ, kích hoạt chế độ **--watch** và quản lý cấu trúc module thư mục SASS nâng cao.

---

## 📌 1. Kết Quả Kiểm Tra Môi Trường Trên Máy Tính

| Công cụ | Lệnh kiểm tra | Trạng thái | Phiên bản |
| :--- | :--- | :--- | :--- |
| **Node.js** | `node -v` | ✅ Đã sẵn sàng | **v24.18.0** |
| **npm** | `npm -v` | ✅ Đã sẵn sàng | **11.16.0** |
| **Dart Sass** | `sass --version` | ✅ Đã cài đặt toàn cục | **1.105.2** |
| **Git** | `git --version` | ✅ Đã sẵn sàng | **2.55.0** |

---

## 🛠️ 2. Các Bước Cài Đặt Chi Tiết

### Bước 1: Cài đặt SASS qua npm
Mở Terminal / PowerShell và chạy:
```bash
npm install -g sass
```
> **Giải thích:** Cờ `-g` (global) giúp bạn có thể sử dụng câu lệnh `sass` ở bất kỳ thư mục hay dự án nào trên máy tính mà không cần cài lại.

### Bước 2: Kiểm tra phiên bản SASS
```bash
sass --version
```
Kết quả hiển thị:
```text
1.105.2 compiled with dart2js 3.13.5
```

---

## 💻 3. Các Lệnh Thực Hành SASS CLI

### 🔹 Biên dịch 1 tệp SCSS đơn lẻ sang CSS
```bash
sass styles.scss styles.css
```
Tự động chuyển đổi `styles.scss` thành `styles.css` và tạo kèm sourcemap `styles.css.map`.

### 🔹 Kích hoạt chế độ theo dõi tự động (--watch)
```bash
sass styles.scss styles.css --watch
```
Khi bật lệnh này, bất cứ khi nào bạn nhấn `Ctrl + S` chỉnh sửa mã nguồn SCSS, SASS CLI sẽ tự động biên dịch lại CSS tức thì mà không cần gõ lại lệnh.

### 🔹 Biên dịch toàn bộ thư mục (Modular SASS)
```bash
sass scss/:css/ --watch
```
- `scss/`: Thư mục chứa toàn bộ mã nguồn SCSS và các partial files.
- `css/`: Thư mục lưu kết quả CSS sau khi biên dịch.
- `--watch`: Lắng nghe mọi file `.scss` con trong thư mục `scss/`.

---

## 📂 4. Cấu Trúc Thư Mục Dự Án

```text
📁 Hướng dẫn cài đặt SASS bằng npm & SASS CLI/
├── 📄 index.html              # Trang demo giao diện trực quan, bảng lệnh & showcase
├── 📄 package.json            # Quản lý script biên dịch npm
├── 📄 styles.scss             # File SCSS thực hành biên dịch đơn lẻ
├── 📄 styles.css              # File CSS xuất xưởng từ styles.scss
├── 📄 styles.css.map          # Sourcemap hỗ trợ debug DevTools
├── 📁 scss/                   # Kiến trúc SASS Module theo chuẩn mới (@use)
│   ├── 📄 _variables.scss     # Khai báo mã màu Neon, font chữ, shadow, border-radius
│   ├── 📄 _mixins.scss        # Mixin Flexbox, Glassmorphism, Responsive breakpoint
│   ├── 📄 _base.scss          # Reset CSS và thiết lập typography, container
│   ├── 📄 _components.scss    # Styling thẻ Card, Button, Navbar, Badges
│   └── 📄 main.scss           # File trung tâm import các partials
├── 📁 css/                    # Thư mục đích nhận output từ scss/
│   ├── 📄 main.css            # File CSS hoàn chỉnh
│   └── 📄 main.css.map        # Sourcemap của main.css
├── 📄 .gitignore              # Bỏ qua node_modules và file tạm
└── 📄 README.md               # Tài liệu chi tiết hướng dẫn thực hành
```

---

## ⚡ 5. Tiện Ích Scripts Trong `package.json`

Bạn cũng có thể chạy trực tiếp thông qua `npm run`:
- `npm run sass:single` : Biên dịch file đơn lẻ `styles.scss` -> `styles.css`.
- `npm run sass:watch-single` : Bật watch file đơn lẻ.
- `npm run sass:build` : Biên dịch thư mục `scss/` -> `css/`.
- `npm run sass:watch` : Bật watch cả thư mục `scss/` -> `css/`.
- `npm run build` : Biên dịch toàn bộ file một lần.

---

## ⚠️ 6. Xử Lý Lỗi Set-ExecutionPolicy Trên Windows PowerShell

Nếu gặp lỗi `cannot be loaded because running scripts is disabled on this system`, hãy mở PowerShell dưới quyền **Administrator** hoặc chạy lệnh sau cho tài khoản hiện tại:
```powershell
Set-ExecutionPolicy Unrestricted -Scope CurrentUser
```

---

## 🌐 7. Hướng Dẫn Đưa Lên GitHub

Thực hiện các lệnh sau trong Terminal tại thư mục dự án:
```bash
# 1. Khởi tạo repository Git
git init

# 2. Thêm tất cả các file vào khu vực chuẩn bị commit
git add .

# 3. Tạo commit đầu tiên
git commit -m "feat: complete SASS setup with npm, SASS CLI and modular SCSS architecture"

# 4. Đặt tên nhánh chính là main
git branch -M main

# 5. Liên kết tới remote repo trên GitHub (thay username và tên repo của bạn)
git remote add origin https://github.com/<your-username>/<your-repo-name>.git

# 6. Đẩy mã nguồn lên GitHub
git push -u origin main
```

*(Hoặc với CodePen: Bạn có thể copy nội dung `styles.scss` vào ô CSS của CodePen và chọn CSS Preprocessor là **SCSS**)*.
