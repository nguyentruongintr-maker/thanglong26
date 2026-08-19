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
- **Thắng:** một chú vịt mang cờ về vạch xuất phát **và** cả 4 chú đều đã rời vạch xuất phát ít nhất một lần.

### Một lời giải

`Vịt 1` tiến ×2 · `Vịt 3` tiến ×2 · `Vịt 4` tiến ×1 ·
`Vịt 2` tiến ×2 → nhận 25 từ trên + 25 từ dưới → tiến ×2 (lấy cờ) → lùi ×2 → nhận 25 + 25 → lùi ×2.

## Thêm trò chơi mới

1. Tạo thư mục `<ten-tro-choi>/index.html`.
2. Link `../assets/shell.css`.
3. Đổi một ô `.tile.soon` trong `index.html` thành thẻ `<a class="tile live" href="...">`.
