# Thăng Long 26 — Góc Trò Chơi

Static site (no build step) hosting small browser games. Deployed free on Vercel as project **`thanglong26`**.

## Cấu trúc

```
index.html              Trang chủ — lưới ô vuông, mỗi ô là một trò chơi
assets/shell.css        Style dùng chung (nền, nút, modal, toast)
mai-lo-qua-song/        Trò chơi 1 — Mãi Lộ Qua Sông (tên cũ: Đưa Lính Sang Sông,
                        thư mục cũ `dua-linh-sang-song/` được chuyển hướng
                        trong vercel.json để link đã chia sẻ không chết)
manh-ghep-vo-cuc/       Trò chơi 2 — Mảnh Ghép Vô Cực
thien-nien-su-sudoku/   Trò chơi 3 — Thiên Niên Sử Sudoku (kèm img/1..9.png)
ky-uc-di-san/           Trò chơi 4 — Ký Ức Di Sản (kèm img/1..16.png)
vercel.json             cleanUrls
```

## Chạy thử ở máy

Mở thẳng `index.html` bằng trình duyệt — không cần server, không cần cài gì.

## Mãi Lộ Qua Sông — luật

- 4 người lính ở vạch xuất phát (bên phải), mỗi người 100 quan tiền.
- Ngoài vạch xuất phát còn 4 vạch. Lá cờ đỏ ở vạch 4 (trái nhất), **hàng thứ 2** từ trên xuống.
- Mỗi bước đi (tiến/lùi) tốn 25 quan tiền.
- Chuyền 25 quan tiền cho người lính ngay trên/dưới — **bắt buộc cùng một vạch**.
- Một người chỉ cầm được tối đa 100 quan tiền, đang đủ 100 thì không nhận chuyền được.
- Quan tiền vẽ bằng SVG (hằng `COIN`): vành vàng, lỗ vuông ở giữa — thay cho
  biểu tượng tia sét của bản trước.
- Chỉ người lính ở đúng hàng của cờ mới giành được cờ.
- Lá cờ là **cờ hội ngũ sắc** (5 ô vuông lồng nhau theo ngũ hành, viền răng cưa
  hình ngọn lửa), vẽ bằng SVG trong `flagSVG()` / `heldFlagSVG()`. Cùng một hình
  được dùng lại làm favicon, brand-mark và ô trên trang chủ.
- **Thắng:** lấy được cờ **và** cả 4 người lính đều đã xuống sông (rời vạch xuất phát)
  ít nhất một lần **và** cả 4 người đều đã quay về vạch xuất phát.

### Lời giải (16 nước, dùng đúng trọn 400 quan tiền)

Tổng 400 quan tiền = đúng 16 nước đi. Lời giải **không được phí một nước nào**.

```
L1 tiến · L4 tiến · L3 tiến · L4 chuyền lên L3 · L3 tiến
L2 tiến · L1 chuyền xuống L2 · L2 tiến · L3 chuyền lên L2
L2 tiến · L2 tiến (lấy cờ) · L2 lùi · L2 lùi
L3 chuyền lên L2 · L2 lùi · L1 chuyền xuống L2 · L2 lùi (về đích, mang cờ)
L1 lùi · L3 lùi · L4 chuyền lên L3 · L3 lùi · L4 lùi
```

Kết thúc: cả 4 người lính ở vạch 0, quan tiền 0/0/0/0.

## Mảnh Ghép Vô Cực — luật

- 9 mảnh gốm nung, ghép vào khung vuông ở giữa. Mảnh chưa ghép nằm hai bên trái/phải.
- Kéo để di chuyển. Tới gần ô trống mà **vừa khít** thì mảnh bị **hút** vào đúng vị trí.
- Đặt sai: các cạnh không khớp **hiện đỏ** và mảnh **không** bị hút vào.
- Chạm 1 lần = quay phải 90°, chạm 2 lần liên tiếp = quay trái 90°, ấn giữ = lật mặt.
  Có thêm ba nút Quay trái / Lật mặt / Quay phải.
- Chỉ phân biệt được bằng **hình dạng đường viền** — mọi mảnh cùng một màu, không hoa văn,
  không còn vành vát bên trong.
- **Bụi gốm chỉ phủ trên các mảnh ghép**, sàn và bàn ghép để trơn. Vân sinh bằng
  `#dustTex` trên một `<rect>` phủ cả sân chơi và **đứng yên**; chỉ khuôn cắt
  `#pieceDust` (9 đường bao, `applyDustClip()`) chạy theo mảnh.
- Vì vân đứng yên còn khuôn cắt chạy, mảnh xê dịch thì vân dưới nó đổi theo chỗ
  đứng — vân **không dính vào mảnh nào**. Đây là ràng buộc bắt buộc: vân bám theo
  mảnh sẽ giúp người chơi nhớ mảnh và lộ lời giải. Kiểm bằng cách đặt hai mảnh khác
  nhau vào cùng toạ độ: khuôn cắt ra y hệt nhau, và trong mảnh không có phần tử vân riêng.
- Không dùng nguồn sáng có hướng: mọi mảnh chung một bóng đổ `#pcShadow`.
- Ghép trúng ô: mảnh **nhún xuống**, loé sáng, kèm **sóng lan + bụi gốm** bắn ra.
  Hiệu ứng nhún đặt trên `.lift` chứ không phải `.art`, vì `.art` đang giữ phép
  xoay/lật bằng thuộc tính `transform` — animation CSS sẽ ghi đè mất.
- Không còn tấm lót hai bên; bàn ghép được đôn lên `LIFT` và dày khối đùn
  để trông cao hơn hai khay. Ba nút ↺ ⇋ ↻ không nền, ký hiệu màu xanh lá.
- **Một bố cục duy nhất** cho mọi bề ngang: 3 mảnh chờ bên trái, 3 bên dưới,
  3 bên phải (`pickLayout` + `traySpot`). SVG tự co nên không dựng lại khi resize.
- `buildScene()` đặt ba biến CSS trên `.wrap`: `--inset-frac` (mép bàn ghép cách
  rìa sân chơi bao nhiêu phần), `--board-frac` (bề ngang bàn ghép) và `--scene-ar`.
  Nhờ đó hàng ba nút và bộ đếm **dóng đúng hai mép bàn ghép**, còn `--stage-w`
  giới hạn sân chơi theo `100dvh` để trang không phải cuộn.
- HUD bị bó trong bề ngang bàn ghép, nên ở màn ≤700px nhãn rút còn `Ghép:`
  và chữ nhỏ lại — nếu không, đồng hồ và bộ đếm sẽ chồng lên nhau.
- Có đồng hồ tính giờ; nút Chơi lại xáo lại toàn bộ và đưa mảnh ra ngoài khung.

## Thiên Niên Sử Sudoku — luật

- Sudoku 9×9 thường lệ, nhưng thay chữ số 1–9 bằng **9 hiện vật gốm**.
- Chọn ô rồi chạm hiện vật ở dải dưới để điền (hoặc gõ phím 1–9).
- Chạm ô đã điền: ô đó và mọi ô **cùng hiện vật** sáng lên; hàng, cột,
  khu 3×3 của ô đang chọn được làm mờ.
- **Ghi chú**: hiện vật thu nhỏ nằm quanh mép ô, chừa trống vùng giữa.
- Điền sai → ô **viền đỏ**; nút **Xóa ô** để bỏ. Sai **3 lần** thì màn
  chơi được đặt lại từ đầu.
- **Cấp độ** (nút 🏅 ở hàng trên): vào trang là chọn cấp độ trước, sau đó
  đổi lúc nào cũng được. Tạm có hai cấp mở:
  - **Luyện tập** — 13 màn: 3 màn đầu đọc từ `Màn 1/2/3.jpg`, 10 màn sau đọc
    từ các ảnh trong `Cấp luyện tập/` (bản 300 điểm, 41–44 ô cho sẵn).
  - **Thi đấu** — 13 màn, đề đọc từ 14 ảnh trong `Cấp thi đấu/` (một ảnh
    trùng đề nên chỉ còn 13 màn), 36–40 ô cho sẵn nên khó hơn.
  - Ba dòng còn lại ghi **Cập nhật sau**, chưa bấm được.
- **Chọn màn**: bấm vào dòng `cấp độ · Màn x/y` ngay trên bàn cờ. Màn được
  đánh số **1..hết theo đúng thứ tự khai báo trong `TIERS`**; màn nào cũng
  chơi được, không phải mở khoá. Màn đã giải xong trong phiên có dấu ✓.
- Trong bảng chọn màn (và trong hộp chúc mừng, hộp sai 3 lần) luôn có lối
  **chơi lại chính màn đó** hoặc **sang màn kế tiếp**; ở màn cuối thì nút
  "Màn kế tiếp" mờ đi.
- Mỗi cấp độ **nhớ riêng** màn đang chơi, nên đổi qua đổi lại không mất chỗ.
- Cả 26 đề đều đã kiểm bằng thuật toán quay lui: có lời giải, lời giải là
  **DUY NHẤT**, và không đề nào trùng đề nào.

## Ký Ức Di Sản — luật

- Trò lật mảnh ghép trí nhớ với **16 hiện vật** (`img/1..16.png`, cắt sát và
  thu nhỏ từ thư mục nguồn `Ký Ức Di Sản/`).
- Đầu ván có cửa sổ **chọn loại bàn**: 6×8, 7×8 hoặc 8×8, bấm **Xác nhận** mới vào chơi.
- Mỗi hiện vật luôn xuất hiện ở **4 mảnh ghép** (tức 2 cặp), nên số hiện vật
  dùng trong ván = tổng số mảnh ÷ 4 → 12 / 14 / 16, bốc ngẫu nhiên từ 16 ảnh.
- Lật 2 mảnh **giống nhau** → giữ nguyên trạng thái ngửa, **+2 điểm**.
  Lật 2 mảnh **khác nhau** → rung báo sai rồi úp trở lại.
- Đồng hồ ở **giữa hàng trên** (giống Thiên Niên Sử Sudoku), chỉ chạy từ mảnh đầu tiên.
- Nút **1 người / 2 người** ở **góc trên bên trái**, khoá lại ngay khi lật mảnh đầu tiên.
- 1 người: điểm ở góc dưới bên trái. 2 người: hai bảng điểm ở hai góc dưới —
  người chơi 1 màu **cam đất**, người chơi 2 màu **xanh**.
- 2 người: người lật đầu tiên là người chơi 1; khớp cặp thì được lật tiếp,
  không khớp thì **mất lượt** (có thông báo). Chế độ 1 người không có thông báo này.
- Lật hết bàn thì hiện thông báo chiến thắng; ở chế độ 2 người nêu rõ ai thắng
  và hiện điểm của **cả hai** ngay dưới dòng chúc mừng.
- Kích thước bàn tính bằng CSS `--ar = 8 × 0.85 / số hàng` nên cả ba loại bàn
  đều vừa màn hình, không bị vỡ.
- **Bất biến của cặp khớp:** điểm và trạng thái `done` được chốt **đồng bộ** ngay
  tại cú lật thứ hai, không chờ hiệu ứng. `rejectPair` chỉ úp lại mảnh đang ở
  trạng thái `up`, nên mảnh đã khớp không thể bị úp xuống.
- Mặt ngửa của mảnh do một CSS transition tạo ra. Bàn 8×8 có 128 mặt trong ngữ
  cảnh 3D nên trình duyệt đôi khi tạo transition rồi không chạy (`currentTime`
  kẹt ở 0), làm mảnh đã khớp vẫn hiện mặt úp. `settleFace()` đối chiếu ma trận
  đang hiển thị với trạng thái mong muốn, ép transition về đích, và nếu vẫn sai
  thì đặt thẳng `transform` — chạy sau mỗi lần lật lên và lật xuống.

## Thêm trò chơi mới

1. Tạo thư mục `<ten-tro-choi>/index.html`.
2. Link `../assets/shell.css`.
3. Đổi một ô `.tile.soon` trong `index.html` thành thẻ `<a class="tile live" href="...">`.

Lưới trang chủ cố định **4 cột** (2 cột khi màn hình ≤760px) nên mỗi hàng đúng 4 ô:
hàng trên là 4 trò đang chơi được, hàng dưới là 4 ô `.tile.soon` chờ trò mới.
