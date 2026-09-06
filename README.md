# Thăng Long 26 — Góc Trò Chơi

Static site (no build step) hosting small browser games. Deployed free on Vercel as project **`thanglong26`**.

## Cấu trúc

```
index.html              Trang chủ — lưới ô vuông, mỗi ô là một trò chơi
assets/shell.css        Style dùng chung (nền, nút, modal, toast)
dua-linh-sang-song/     Trò chơi 1 — Đưa Lính Sang Sông
vercel.json             cleanUrls
```

## Chạy thử ở máy

Mở thẳng `index.html` bằng trình duyệt — không cần server, không cần cài gì.

## Đưa Lính Sang Sông — luật

- 4 người lính ở vạch xuất phát (bên phải), mỗi người 100 năng lượng.
- Ngoài vạch xuất phát còn 4 vạch. Lá cờ đỏ ở vạch 4 (trái nhất), **hàng thứ 2** từ trên xuống.
- Mỗi bước đi (tiến/lùi) tốn 25 năng lượng.
- Chuyền 25 năng lượng cho người lính ngay trên/dưới — **bắt buộc cùng một vạch**.
- Người lính đang đủ 100 năng lượng không nhận chuyền được.
- Chỉ người lính ở đúng hàng của cờ mới giành được cờ.
- **Thắng:** lấy được cờ **và** cả 4 người lính đều đã rời vạch xuất phát ít nhất một lần
  **và** cả 4 người đều đã quay về vạch xuất phát.

### Lời giải (16 nước, dùng đúng trọn 400 năng lượng)

Tổng năng lượng 400 = đúng 16 nước đi. Lời giải **không được phí một nước nào**.

```
L1 tiến · L4 tiến · L3 tiến · L4 chuyền lên L3 · L3 tiến
L2 tiến · L1 chuyền xuống L2 · L2 tiến · L3 chuyền lên L2
L2 tiến · L2 tiến (lấy cờ) · L2 lùi · L2 lùi
L3 chuyền lên L2 · L2 lùi · L1 chuyền xuống L2 · L2 lùi (về đích, mang cờ)
L1 lùi · L3 lùi · L4 chuyền lên L3 · L3 lùi · L4 lùi
```

Kết thúc: cả 4 người lính ở vạch 0, năng lượng 0/0/0/0.

## Thêm trò chơi mới

1. Tạo thư mục `<ten-tro-choi>/index.html`.
2. Link `../assets/shell.css`.
3. Đổi một ô `.tile.soon` trong `index.html` thành thẻ `<a class="tile live" href="...">`.
