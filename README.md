# Chỉ đường khuôn viên (PWA)

Bản đồ 3D chỉ đường trong khuôn viên. Cài được lên màn hình chính điện thoại và dùng được khi không có mạng.

## Cấu trúc

```
index.html              ứng dụng (toàn bộ dữ liệu bản đồ nằm trong file này)
manifest.webmanifest    thông tin cài đặt (tên, màu, icon)
sw.js                   service worker: lưu bản dùng offline
icons/                  icon 192, 512, maskable, apple-touch, favicon
.nojekyll               để GitHub Pages phục vụ file nguyên trạng
```

## Đưa lên GitHub Pages

1. Vào https://github.com/new, tạo repo mới (ví dụ `chi-duong-khuon-vien`), để chế độ **Public**.
2. Tải toàn bộ nội dung thư mục này lên repo (giữ nguyên thư mục `icons`, và cả file `.nojekyll`).
   - Cách nhanh: trong repo bấm **Add file → Upload files**, kéo thả tất cả file rồi **Commit changes**.
   - Hoặc dùng lệnh:
     ```bash
     git init
     git add .
     git commit -m "PWA chỉ đường khuôn viên"
     git branch -M main
     git remote add origin https://github.com/<tên-tài-khoản>/chi-duong-khuon-vien.git
     git push -u origin main
     ```
3. Vào **Settings → Pages**. Ở mục **Build and deployment**, chọn **Source: Deploy from a branch**, **Branch: main**, thư mục **/ (root)**, bấm **Save**.
4. Đợi khoảng 1–2 phút. Địa chỉ ứng dụng sẽ là:
   `https://<tên-tài-khoản>.github.io/chi-duong-khuon-vien/`

GitHub Pages dùng HTTPS nên định vị GPS và service worker hoạt động bình thường.

## Cài lên điện thoại

- **Android (Chrome):** mở địa chỉ trên, bấm menu ⋮ → **Cài đặt ứng dụng** (hoặc **Thêm vào màn hình chính**).
- **iPhone (Safari):** mở địa chỉ trên, bấm nút Chia sẻ → **Thêm vào Màn hình chính**.

Mở ứng dụng một lần khi có mạng để máy lưu bản offline. Từ lần sau dùng được cả khi mất mạng. Phông chữ chỉ được lưu sau khi mở lần đầu có mạng, nếu chưa có thì máy dùng phông hệ thống.

## Cập nhật ứng dụng

1. Thay `index.html` bằng bản mới.
2. Mở `sw.js`, đổi `const VERSION = 'v1'` thành `'v2'` (lần sau `'v3'`...) rồi commit.

Khi có mạng, ứng dụng luôn tải bản mới nhất của trang. Việc đổi `VERSION` giúp máy xóa bộ nhớ đệm cũ.

## Chạy thử trên máy tính

Service worker không chạy khi mở file trực tiếp (`file://`). Chạy một máy chủ cục bộ:

```bash
python3 -m http.server 8000
```

rồi mở http://localhost:8000
