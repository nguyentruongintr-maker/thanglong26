# Thăng Long 26 — Góc Trò Chơi

Static site (no build step) hosting small browser games. Deployed free on Vercel as project **`thanglong26`**.

## Cấu trúc

```
index.html              Trang chủ — lưới ô vuông, mỗi ô là một trò chơi
assets/shell.css        Style dùng chung (nền, nút, modal, toast)
dua-linh-sang-song/     Trò chơi 1 — Đưa Lính Sang Sông
manh-ghep-vo-cuc/       Trò chơi 2 — Mảnh Ghép Vô Cực
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

## Mảnh Ghép Vô Cực — luật

- 9 mảnh gốm nung, ghép vào khung vuông ở giữa. Mảnh chưa ghép nằm hai bên trái/phải.
- Kéo để di chuyển. Tới gần ô trống mà **vừa khít** thì mảnh bị **hút** vào đúng vị trí.
- Đặt sai: các cạnh không khớp **hiện đỏ** và mảnh **không** bị hút vào.
- Chạm 1 lần = quay phải 90°, chạm 2 lần liên tiếp = quay trái 90°, ấn giữ = lật mặt.
  Có thêm ba nút Quay trái / Lật mặt / Quay phải.
- Chỉ phân biệt được bằng **hình dạng đường viền** — mọi mảnh cùng một màu, không hoa văn.
- Có đồng hồ tính giờ; nút Chơi lại xáo lại toàn bộ và đưa mảnh ra ngoài khung.

## Thêm trò chơi mới

1. Tạo thư mục `<ten-tro-choi>/index.html`.
2. Link `../assets/shell.css`.
3. Đổi một ô `.tile.soon` trong `index.html` thành thẻ `<a class="tile live" href="...">`.
