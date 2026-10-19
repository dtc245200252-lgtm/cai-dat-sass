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

## 📂 4. Cấu Trúc Thư Mục Dự Án Chuẩn SASS (7-1 Pattern)

```text
📁 Hướng dẫn cài đặt SASS bằng npm & SASS CLI/
├── 📄 index.html              # Trang demo giao diện trực quan, bảng lệnh & showcase
├── 📄 demo-standard.html      # Trang demo thành quả chuyển đổi CSS sang SASS chuẩn
├── 📄 package.json            # Quản lý script biên dịch npm
├── 📄 styles.scss             # File SCSS thực hành biên dịch đơn lẻ
├── 📄 styles.css              # File CSS xuất xưởng từ styles.scss
├── 📄 styles.css.map          # Sourcemap hỗ trợ debug DevTools
├── 📁 original-css/           # Thư mục lưu file CSS ban đầu để đối chiếu
│   └── 📄 styles.css
├── 📁 scss/                   # Kiến trúc SASS Module chuẩn (Abstracts, Base, Layout, Components)
│   ├── 📁 abstracts/
│   │   ├── 📄 _variables.scss # Biến màu sắc, shadow, font, border
│   │   └── 📄 _mixins.scss    # Mixin button-style, box-shadow tái sử dụng
│   ├── 📁 base/
│   │   └── 📄 _global.scss    # Cấu hình body toàn cục
│   ├── 📁 layout/
│   │   └── 📄 _container.scss # Layout .container căn giữa
│   ├── 📁 components/
│   │   ├── 📄 _buttons.scss   # Component .button tái sử dụng mixin
│   │   └── 📄 _cards.scss     # Component .card kèm box-shadow và BEM nesting
│   └── 📄 main.scss           # File trung tâm import tất cả partials
├── 📁 css/                    # Thư mục đích nhận output từ scss/
│   ├── 📄 main.css            # File CSS hoàn chỉnh
│   └── 📄 main.css.map        # Sourcemap của main.css
├── 📄 .gitignore              # Bỏ qua node_modules và file tạm
└── 📄 README.md               # Tài liệu chi tiết hướng dẫn thực hành
```

---

## 🎯 5. Quy Trình Chuyển Đổi CSS Sang SASS Chuẩn

### Bước 1: Khảo sát CSS ban đầu
Các đoạn CSS truyền thống thường bị lặp giá trị màu sắc, padding, box-shadow và không có khả năng lồng nhau (nesting).

### Bước 2: Tách biến tại `scss/abstracts/_variables.scss`
```scss
$primary-color: #0056b3;
$text-color: #333;
$background-color: #f4f4f4;
$border-color: #ddd;
$box-shadow: 2px 2px 10px rgba(0, 0, 0, 0.1);
```

### Bước 3: Tạo Mixins tại `scss/abstracts/_mixins.scss`
```scss
@mixin button-style($bg-color) {
  background: $bg-color;
  color: white;
  padding: 10px 20px;
  border-radius: 5px;
}

@mixin box-shadow {
  box-shadow: $box-shadow;
}
```

### Bước 4: Viết các partials theo nhiệm vụ
- `base/_global.scss`: Thiết lập style chung cho `body`.
- `layout/_container.scss`: Khung layout `.container`.
- `components/_buttons.scss`: Áp dụng `@include button-style($primary-color)`.
- `components/_cards.scss`: Áp dụng `@include box-shadow` và cấu trúc BEM nesting.

### Bước 5: Nạp tất cả vào `scss/main.scss`
```scss
@import "abstracts/variables";
@import "abstracts/mixins";
@import "base/global";
@import "base/typography";
@import "layout/container";
@import "components/buttons";
@import "components/cards";
```
Biên dịch ra file CSS:
```bash
sass scss/:css/ --watch
```

---

## 🎨 6. Tối Ưu CSS Bằng Mixins & Biến (Website Mẫu)

### Bảng đối chiếu biến và mixin đã tạo:

| Thành phần | File SCSS | Mục đích sử dụng |
| :--- | :--- | :--- |
| `$primary-color` | `abstracts/_variables.scss` | Màu chủ đạo nút bấm (`red`) |
| `$text-color` | `abstracts/_variables.scss` | Màu chữ toàn cục (`#222`) |
| `$font-large`, `$font-medium` | `abstracts/_variables.scss` | Kích thước `h1` (32px), `h2` (28px) |
| `$padding-standard` | `abstracts/_variables.scss` | Khoảng cách đệm chuẩn (`10px 20px`) |
| `$box-shadow-default` | `abstracts/_variables.scss` | Cấu hình bóng đổ (`2px 2px 10px rgba(0,0,0,0.1)`) |
| `@mixin button-style($bg-color)` | `abstracts/_mixins.scss` | Tái sử dụng tạo nút bấm với màu nền tùy chọn |
| `@mixin box-style` | `abstracts/_mixins.scss` | Tái sử dụng tạo thẻ card (nền trắng, đệm, bo góc, bóng đổ) |

### Kết quả đạt được:
- ✔ **CSS gọn gàng, giảm thiểu lặp code**.
- ✔ **Kiểm soát giao diện tập trung**: chỉ cần đổi biến tại `_variables.scss` là toàn bộ màu sắc, kích thước cập nhật theo.
- ✔ **Tính tái sử dụng cao**: dễ dàng tạo biến thể `.button--secondary`, `.button--success`.

---

## 📐 7. Tái Cấu Trúc Mã CSS Cho Sẵn (`codegym-vn/responsive-grid`)

Dự án nằm tại thư mục [responsive-grid-sass/](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/responsive-grid-sass/):
- **Phân tích vấn đề ở mã cũ**: Mã nguồn ban đầu lạm dụng quá nhiều inline styles (`style="height:90px;"`, `style="width:25%;"`, mã màu hex lặp lại), tính toán cứng độ rộng cột (`width: 8.33%`).
- **Giải pháp SASS hiện đại**:
  1. Tách cấu trúc vào thư mục `responsive-grid-sass/scss/`:
     - `_variables.scss`: Quản lý số cột (`$grid-columns: 12;`), màu sắc và chiều cao.
     - `_mixins.scss`: Hàm tính toán độ rộng cột `col-width($span)`.
     - `_grid.scss`: Vòng lặp SASS `@for $i from 1 through 12` tự động sinh 12 cột `.col-1` đến `.col-12`.
     - `_layout.scss`: Quy ước đặt tên BEM sạch sẽ (`.layout-header`, `.layout-body`, `.layout-footer`).
  2. File HTML `responsive-grid-sass/index.html`: Sạch sẽ 100%, không còn bất kỳ inline style nào.
- **Biên dịch**:
  ```bash
  npm run grid:build
  # hoặc
  npm run grid:watch
  ```

---

## 🚀 8. Tái Cấu Trúc Toàn Bộ Landing Page Bằng Kiến Trúc SASS 7-1

Dự án hoàn chỉnh đặt tại thư mục [landing-page-sass/](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/landing-page-sass/), tổng hợp lại 4 bài tập giao diện mẫu của CodeGym:

1. **Navigation & Header** ([scss/layout/_navbar.scss](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/landing-page-sass/scss/layout/_navbar.scss) & [_header.scss](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/landing-page-sass/scss/layout/_header.scss)):
   - Navbar cố định trên đỉnh, hiệu ứng kính mờ (glassmorphism blur 12px), đổi màu liên kết khi hover.
   - Header banner có nền ảnh, hiệu ứng mờ đa tầng (`filter: blur(10px)`), overlay tương phản cao và nút kêu gọi hành động (CTA).
2. **Sản phẩm nổi bật (Featured Products)** ([scss/components/_cards.scss](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/landing-page-sass/scss/components/_cards.scss)):
   - Bố cục dạng lưới CSS Grid 3 cột (`@mixin grid-columns(3, 28px)`).
   - Card sản phẩm có hình ảnh bo góc, hiệu ứng phóng to ảnh khi hover (`transform: scale(1.08)`), phân cấp nội dung bằng dấu chấm (`•`).
3. **Số liệu thống kê (Statistics Section)** ([scss/components/_stats.scss](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/landing-page-sass/scss/components/_stats.scss)):
   - 4 khối thẻ thống kê trực quan (15,000+ khách hàng, 99.8% hài lòng, 650+ dự án, hỗ trợ 24/7).
   - Nền gradient tối sang trọng kết hợp icon màu neon nổi bật.
4. **Footer 2 cột chuyên nghiệp** ([scss/layout/_footer.scss](file:///d:/M%E1%BA%B8%20CODE%20GYM%20ALL/H%C6%B0%E1%BB%9Bng%20d%E1%BA%ABn%20c%C3%A0i%20%C4%91%E1%BA%B7t%20SASS%20b%E1%BA%B1ng%20npm%20&%20SASS%20CLI/landing-page-sass/scss/layout/_footer.scss)):
   - Cột trái: Thông tin thương hiệu & bản quyền.
   - Cột phải: Danh mục liên kết phân cấp bằng dấu chấm (`•`).

### Lệnh biên dịch:
```bash
npm run landing:build
# hoặc chế độ tự động theo dõi:
npm run landing:watch
```

---

## ⚡ 9. Tiện Ích Scripts Trong `package.json`

Bạn có thể chạy trực tiếp thông qua `npm run`:
- `npm run sass:single` : Biên dịch file đơn lẻ `styles.scss` -> `styles.css`.
- `npm run sass:watch-single` : Bật watch file đơn lẻ.
- `npm run sass:build` : Biên dịch thư mục `scss/` -> `css/`.
- `npm run sass:watch` : Bật watch cả thư mục `scss/` -> `css/`.
- `npm run grid:build` : Biên dịch dự án `responsive-grid-sass`.
- `npm run grid:watch` : Bật watch dự án `responsive-grid-sass`.
- `npm run landing:build` : Biên dịch dự án `landing-page-sass`.
- `npm run landing:watch` : Bật watch dự án `landing-page-sass`.
- `npm run build` : Biên dịch toàn bộ các dự án SCSS trong 1 lệnh duy nhất.

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
