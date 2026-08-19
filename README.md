# Thăng Long 26 — Góc Trò Chơi

Static site (no build step) hosting small browser games. Deployed free on Vercel as project **`thanglong26`**.

## Cấu trúc

```
index.html              Trang chủ — lưới ô vuông, mỗi ô là một trò chơi
assets/shell.css        Style dùng chung (nền, nút, modal, toast)
vit-con-vui-ve/         Trò chơi 1 — Vịt Con Vui Vẻ
vercel.json             cleanUrls
```

## Chạy thử ở máy

Mở thẳng `index.html` bằng trình duyệt — không cần server, không cần cài gì.

## Vịt Con Vui Vẻ — luật

- 4 chú vịt ở vạch xuất phát (bên phải), mỗi chú 100 năng lượng.
- Ngoài vạch xuất phát còn 4 vạch. Lá cờ đỏ ở vạch 4 (trái nhất), **hàng thứ 2** từ trên xuống.
- Mỗi bước đi (tiến/lùi) tốn 25 năng lượng.
- Chuyền 25 năng lượng cho vịt ngay trên/dưới — **bắt buộc cùng một vạch**.
- Vịt đang đủ 100 năng lượng không nhận chuyền được.
- Chỉ vịt ở đúng hàng của cờ mới ngậm được cờ.
- **Thắng:** lấy được cờ **và** cả 4 chú vịt đều đã rời vạch xuất phát ít nhất một lần
  **và** cả 4 chú đều đã quay về vạch xuất phát.

### Lời giải (16 nước, dùng đúng trọn 400 năng lượng)

Tổng năng lượng 400 = đúng 16 nước đi. Lời giải **không được phí một nước nào**.

```
D1 tiến · D4 tiến · D3 tiến · D4 chuyền lên D3 · D3 tiến
D2 tiến · D1 chuyền xuống D2 · D2 tiến · D3 chuyền lên D2
D2 tiến · D2 tiến (lấy cờ) · D2 lùi · D2 lùi
D3 chuyền lên D2 · D2 lùi · D1 chuyền xuống D2 · D2 lùi (về đích, mang cờ)
D1 lùi · D3 lùi · D4 chuyền lên D3 · D3 lùi · D4 lùi
```

Kết thúc: cả 4 chú ở vạch 0, năng lượng 0/0/0/0.

## Thêm trò chơi mới

1. Tạo thư mục `<ten-tro-choi>/index.html`.
2. Link `../assets/shell.css`.
3. Đổi một ô `.tile.soon` trong `index.html` thành thẻ `<a class="tile live" href="...">`.
