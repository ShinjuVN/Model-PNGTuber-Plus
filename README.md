# Hướng dẫn ghép layer & tạo chuyển động cho model PNGTuber Plus

Tài liệu này hướng dẫn import, sắp xếp thứ tự lớp (Z-order), tạo quan hệ cha–con (Parent) và cài chuyển động (Wobble, Follow Mouse, Drag, Blink, Talking, Costume) cho bộ layer trong thư mục `Layer Model/`.

> **Lưu ý:** Tên các ô thiết lập dưới đây dùng đúng tên tiếng Anh trong giao diện PNGTuber Plus (Wobble, Drag Speed, Rotational Limits, Follow Mouse, Costumes...). Tùy phiên bản, vị trí nút có thể khác đôi chút. Các con số chỉ là **giá trị khởi điểm**, hãy tinh chỉnh khi xem trực tiếp.

---

## 1. Cấu trúc thư mục

```
Layer Model/
├── Biểu cảm thêm/          (7 file)  – biểu cảm tùy chọn & hiệu ứng
├── Mặt và biểu cảm/        (13 file) – mắt, mày, miệng, má hồng...
├── Phụ kiện-vạt sau thân/  (2 file)  – vạt áo khoác sau, dây trang trí
├── Tay và áo khoác/        (7 file)  – tay, bàn tay, áo khoác sau
├── Thân dưới/              (6 file)  – chân, giày, tất, dây đùi
├── Thân trên/              (4 file)  – thân, cổ, yếm, choker
├── Tóc phía sau/           (4 file)  – tóc sau, lọn tóc, đuôi tóc
├── Váy và đai lưng/        (5 file)  – váy, thắt lưng, gấu bông...
└── Đầu/                    (8 file)  – đầu, mái, tóc mai, ahoge, kẹp, nơ
```

**Quy tắc cho mọi file PNG:**
- Cùng kích thước canvas (ví dụ 2000×2000 px), nền trong suốt, mỗi bộ phận nằm đúng vị trí của nó trên canvas. Nhờ vậy khi import, các bộ phận tự khớp nhau mà không cần dịch tay.
- Không để chữ có dấu/ký tự lạ trong tên file nếu gặp lỗi import (có thể đổi tên ngắn gọn, ví dụ `back_hair_bottom.png`).
- Mỗi phần chuyển động phải được vẽ **dư vùng giấu** (phần chân tóc, gốc vạt áo nằm dưới lớp khác) để lúc lắc không lộ khoảng hở.

---

## 2. Quy trình chung

1. **Import** toàn bộ PNG vào PNGTuber Plus (nút *Add Sprite / Import*, chọn nhiều file cùng lúc).
2. **Đặt tên** sprite rõ ràng (giữ nguyên tên file là đủ).
3. **Sắp xếp Z-order** theo bảng ở mục 3.
4. **Chỉnh tâm xoay (Offset/Origin)** cho từng bộ phận cần chuyển động: đặt tâm ở **điểm bám** (gốc tóc, vai, eo, khớp tay...), không để ở giữa ảnh.
5. **Gắn Parent** theo sơ đồ ở mục 4 để các bộ phận con đi theo bộ phận cha.
6. **Cài chuyển động** theo mục 5.
7. **Cài biểu cảm** (Blink, Talking, Costume) theo mục 6 và 7.
8. **Kiểm tra** theo mục 8 rồi lưu file `.save`.

---

## 3. Thứ tự lớp (Z-order) – từ SAU ra TRƯỚC

Số càng lớn càng nằm phía trước.

| # | Sprite | Nhóm |
|---|--------|------|
| 1 | Long side-tail sections | Tóc sau |
| 2 | Back hair – bottom layer | Tóc sau |
| 3 | Back hair – left lock | Tóc sau |
| 4 | Back hair – right lock | Tóc sau |
| 5 | Back coat flap | Phụ kiện |
| 6 | Long decorative strapsribbons on left and right | Phụ kiện |
| 7 | Coat – back sectionfolded collar | Tay & áo khoác |
| 8 | Left leg | Thân dưới |
| 9 | Right leg | Thân dưới |
| 10 | Right white sock | Thân dưới |
| 11 | Thigh strap | Thân dưới |
| 12 | Left shoe | Thân dưới |
| 13 | Right shoe | Thân dưới |
| 14 | Torso - Body | Thân trên |
| 15 | Side-slit skirt panel | Váy |
| 16 | Black skirt | Váy |
| 17 | Black belt + gold buckle | Váy |
| 18 | Decorative harnessstraps at the hip | Váy |
| 19 | White bear charm at the waist | Váy |
| 20 | Neck, shoulders | Thân trên |
| 21 | Shoulder straps | Thân trên |
| 22 | Choker + triangular pendant | Thân trên |
| 23 | Right arm – upper arm + sleeve | Tay |
| 24 | Right hand | Tay |
| 25 | Black armband on bicep | Tay |
| 26 | Left arm (raised arm) – upper arm | Tay |
| 27 | Left arm – forearm + oversized sleeve | Tay |
| 28 | Bangs – back layer | Đầu |
| 29 | Headface | Đầu |
| 30 | Blush | Mặt |
| 31 | Left eye white / Right eye white | Mặt |
| 32 | Left-Right iris-pupil (x2) | Mặt |
| 33 | Eye highlights | Mặt |
| 34 | Left closed eye / Right closed eye | Mặt |
| 35 | Left eyebrow / Right eyebrow | Mặt |
| 36 | Nose | Mặt |
| 37 | Closed mouth / Small open mouth / Wide open mouth | Mặt |
| 38 | Side hair – left / Side hair – right | Đầu |
| 39 | Bangs – front layer | Đầu |
| 40 | Ahoge | Đầu |
| 41 | X-shaped hair clip (blue + yellow) | Đầu |
| 42 | Yellow hair ribbontie | Đầu |
| 43 | Left hand (fingers brushing hair) | Tay (**trên cùng** để chạm tóc) |
| 44 | Các file trong `Biểu cảm thêm/` | Hiệu ứng (trên cùng) |

> **Mẹo:** Tay trái giơ lên chạm tóc nên **Left hand** phải nằm trước tóc mai/mái trước (#38–39) thì mới thấy ngón tay lướt qua tóc.

---

## 4. Sơ đồ Parent (cha → con)

Gắn Parent đúng thì chỉ cần cài chuyển động cho bộ phận cha, các con tự đi theo.

```
Torso - Body  (GỐC – có Bounce nhẹ khi nói)
├── Neck, shoulders
│   ├── Choker + triangular pendant
│   ├── Shoulder straps
│   └── Headface  (đầu, xoay nhẹ theo chuột)
│       ├── Bangs – back layer
│       ├── Bangs – front layer
│       ├── Side hair – left
│       ├── Side hair – right
│       ├── Ahoge
│       ├── X-shaped hair clip (blue + yellow)
│       ├── Yellow hair ribbontie
│       ├── Blush, Nose
│       ├── Eye white (L/R) ── iris-pupil (L/R) ── Eye highlights
│       ├── Closed eye (L/R)
│       ├── Eyebrow (L/R)
│       ├── Closed mouth / Small open mouth / Wide open mouth
│       └── (Biểu cảm thêm: Smiling eyes, Surprised eyes, Pouting..., Grinning mouth, hearts, sweat drop, angry vein)
├── Back hair – bottom layer
│   ├── Back hair – left lock
│   ├── Back hair – right lock
│   └── Long side-tail sections
├── Coat – back sectionfolded collar
│   ├── Back coat flap
│   └── Long decorative strapsribbons on left and right
├── Black belt + gold buckle
│   ├── Black skirt
│   │   └── Side-slit skirt panel
│   ├── Decorative harnessstraps at the hip
│   └── White bear charm at the waist
├── Right arm – upper arm + sleeve
│   ├── Right hand
│   └── Black armband on bicep
├── Left arm (raised arm) – upper arm
│   └── Left arm – forearm + oversized sleeve
│       └── Left hand (fingers brushing hair)
├── Left leg ── Left shoe
└── Right leg ── Right white sock ── Right shoe
    └── Thigh strap
```

---

## 5. Cài chuyển động theo từng nhóm

### 5.1 Tóc phía sau (chuyển động mềm)

| Sprite | Tâm xoay (Origin) | Thiết lập đề xuất |
|--------|-------------------|-------------------|
| Back hair – bottom layer | Đỉnh phần tóc sau, sát sau gáy | **Drag Speed** nhẹ (~5–8), **Rotational Limits** −8° → +8° |
| Back hair – left lock | Gốc lọn tóc (chỗ gắn vào đầu) | **Wobble** (X nhỏ, tần số thấp) + Drag Speed ~6, Rotational Limits −15° → +15° |
| Back hair – right lock | Tương tự lọn trái | Giống lọn trái nhưng **đổi Frequency/Phase khác chút** để hai bên không lắc đồng bộ |
| Long side-tail sections | Gốc đuôi tóc | **Wobble** biên độ lớn hơn, tần số thấp; Drag Speed ~8–10; Rotational Limits −20° → +20° |

> Mẹo: tóc sau dài thì tâm xoay nằm ở **trên cùng**; biên độ càng xa gốc càng thấy rõ, nên giữ số nhỏ để không bị "bay" quá.

### 5.2 Phụ kiện & vạt sau thân

| Sprite | Tâm xoay | Thiết lập đề xuất |
|--------|----------|-------------------|
| Coat – back sectionfolded collar | Sau cổ/vai | Bám cố định theo thân, chỉ **Bounce** cùng thân |
| Back coat flap (dài tới gối) | Chỗ gắn ở eo/lưng | Drag Speed ~8, Rotational Limits −6° → +6°, **Wobble** Y rất nhẹ |
| Long decorative strapsribbons | Điểm treo trên vạt áo | **Wobble** X (biên độ vừa) + Drag Speed ~8, Rotational Limits −12° → +12° |

### 5.3 Thân dưới

- **Left leg / Right leg**: tâm xoay ở hông. Thường để **tĩnh**; nếu muốn sống động chỉ cho **Bounce** nhẹ theo thân. File chân là 1 khối (đùi + cẳng) nên **không** xoay khớp gối, chỉ nghiêng rất nhẹ (±2°).
- **Right white sock**: con của Right leg, không cần thiết lập riêng.
- **Thigh strap**: con của chân phải; có thể thêm Drag Speed ~3 để dây hơi trễ.
- **Left shoe / Right shoe**: con của chân, đứng yên.

### 5.4 Váy & đai lưng

| Sprite | Tâm xoay | Thiết lập đề xuất |
|--------|----------|-------------------|
| Black skirt | Eo | Drag Speed ~4, Rotational Limits −3° → +3° |
| Side-slit skirt panel | Mép trên của tấm váy | **Wobble** nhẹ + Drag Speed ~6, Rotational Limits −8° → +8° |
| Black belt + gold buckle | Giữa eo | Không chuyển động riêng (cha của váy) |
| Decorative harnessstraps at the hip | Điểm gắn ở hông | Drag Speed ~5, Rotational Limits −8° → +8° |
| White bear charm at the waist | Điểm treo | **Wobble** rõ hơn (đây là điểm nhấn), Rotational Limits −20° → +20°, Drag Speed ~8 |

### 5.5 Thân trên

- **Torso - Body**: làm gốc; bật **Bounce** (nhún khi nói) với biên độ nhỏ.
- **Neck, shoulders**: đi theo thân, không cần chỉnh.
- **Shoulder straps, Choker + triangular pendant**: Drag Speed ~3 để hơi trễ khi đầu/thân di chuyển; mặt dây tam giác có thể thêm Wobble rất nhẹ.

### 5.6 Tay & áo khoác

- **Right arm – upper arm + sleeve**: tâm xoay ở vai; Rotational Limits −5° → +5°, Drag Speed ~4.
- **Right hand**: con của tay phải; Drag Speed ~6 để tạo độ trễ.
- **Black armband on bicep**: con của tay phải, chỉ đi theo.
- **Left arm (raised arm) – upper arm**: tâm xoay ở vai trái; Rotational Limits −4° → +4°.
- **Left arm – forearm + oversized sleeve**: tâm xoay ở **khuỷu tay**; Drag Speed ~6–8, Rotational Limits −8° → +8° (tay áo rộng nên có độ trễ).
- **Left hand (fingers brushing hair)**: tâm xoay ở cổ tay; Drag Speed ~8, Rotational Limits −10° → +10°.

### 5.7 Đầu

| Sprite | Thiết lập đề xuất |
|--------|-------------------|
| Headface | **Follow Mouse** nhẹ cho đầu (Distance nhỏ), Rotational Limits −6° → +6°, Drag Speed ~4 |
| Bangs – back layer | Giữ cố định theo đầu |
| Bangs – front layer | Drag Speed ~5, Rotational Limits −3° → +3° (mái cứng thì chỉ cần rất ít) |
| Side hair – left / right | **Wobble** nhẹ + Drag Speed ~6, Rotational Limits −8° → +8°; hai bên lệch pha |
| Ahoge | Tâm xoay ở **chân sợi tóc**; **Wobble** rõ, Rotational Limits −25° → +25°, Drag Speed ~8 |
| X-shaped hair clip | Chỉ đi theo đầu (không cần chuyển động riêng) |
| Yellow hair ribbontie | Drag Speed ~6, Rotational Limits −10° → +10°, có thể thêm Wobble nhẹ |

> Không có file **Ears** riêng trong bộ layer này (tai nằm chung với `Headface.png`), nên bỏ qua bước tách tai.

---

## 6. Khuôn mặt & biểu cảm cơ bản

### 6.1 Mắt

| Sprite | Cài đặt |
|--------|---------|
| Left eye white / Right eye white | Hiển thị khi **không chớp** (Blinking: *Only when not blinking*) |
| Left-Right iris-pupil | Import **2 lần** (1 cho mắt trái, 1 cho mắt phải), đặt đúng vị trí từng mắt. Bật **Follow Mouse**, Distance X ~15–25 px, Y ~10–15 px để con ngươi không lòi ra ngoài tròng trắng. Cũng *Only when not blinking* |
| Eye highlights | Parent vào iris; hiển thị cùng iris |
| Left closed eye / Right closed eye | Hiển thị khi **chớp** (Blinking: *Only when blinking*) |
| Left eyebrow / Right eyebrow | Luôn hiển thị; Drag Speed ~3, có thể cho Follow Mouse rất nhẹ |

> Lưu ý: bộ file **không có** "upper eyelid/lash line" riêng; nếu viền mi đã vẽ liền vào `Left/Right eye white.png` hoặc `Headface.png` thì không cần thêm.

### 6.2 Miệng (trạng thái nói)

PNGTuber Plus chỉ phân biệt 2 trạng thái **đang nói / không nói**:

| Sprite | Cài đặt |
|--------|---------|
| Closed mouth | Talking: **Only when not talking** |
| Small open mouth | Talking: **Only when talking** (miệng mặc định khi nói) |
| Wide open mouth | Gắn vào **Costume riêng** (ví dụ Costume 2) cho lúc cười/la lớn, vì không có mức độ mở miệng theo âm lượng |

### 6.3 Má hồng & mũi

- **Blush**: luôn hiển thị, hoặc chỉ bật ở costume "ngại ngùng".
- **Nose**: luôn hiển thị; chỉ cần đi theo đầu.

---

## 7. Biểu cảm thêm (Costume)

Dùng hệ thống **Costumes** (phím số 1–0): mỗi costume là tập hợp các sprite được bật/tắt.

| Costume | Phím | Bật | Tắt |
|---------|------|-----|-----|
| 1 – Mặc định | `1` | Eye white, iris, Closed mouth / Small open mouth, Eyebrow | Toàn bộ file trong `Biểu cảm thêm/` |
| 2 – Cười toe | `2` | Smiling eyes, Grinning mouth, Blush, Wide open mouth (tùy) | Eye white, iris, Closed mouth, Small open mouth |
| 3 – Ngạc nhiên | `3` | Surprised eyes, Wide open mouth, sweat drop | Eye white, iris, Closed mouth |
| 4 – Giận dỗi | `4` | Pouting-pressed lips, angry vein | Closed mouth, Small open mouth |
| 5 – Yêu thích | `5` | Smiling eyes, hearts, Blush | Eye white, iris |

**Cách làm:** chọn từng sprite → mục **Costumes** → tick costume mà sprite đó được hiển thị. Sprite không tick sẽ ẩn trong costume đó.

> Các hiệu ứng (hearts, sweat drop, angry vein) có thể thêm **Wobble** nhẹ hoặc Drag Speed để trông sống động.

---

## 8. Kiểm tra & xử lý lỗi thường gặp

| Hiện tượng | Cách xử lý |
|------------|------------|
| Lọn tóc/vạt áo lộ khoảng trống khi lắc | Giảm Rotational Limits/Wobble, hoặc vẽ dư vùng giấu dưới lớp phía trước |
| Bộ phận xoay quanh giữa ảnh thay vì gốc | Chỉnh lại **Origin/Offset** về điểm bám |
| Đầu chuyển động nhưng tóc mai/mái đứng yên | Kiểm tra **Parent** đã gắn vào Headface chưa |
| Con ngươi lòi ra ngoài mắt | Giảm Distance của **Follow Mouse** |
| Chớp mắt thấy cả mắt mở và mắt nhắm | Kiểm tra Blinking của Eye white/iris = *Only when not blinking*, closed eye = *Only when blinking* |
| Miệng nói nhưng không đổi hình | Kiểm tra Talking của Closed mouth / Small open mouth đúng như mục 6.2, và Microphone đã chọn đúng thiết bị |
| Hai bên tóc lắc đồng bộ, trông cứng | Đổi **Frequency/Phase** khác nhau giữa trái và phải |
| Tay trái bị tóc che | Đưa **Left hand** lên trên Bangs/Side hair trong Z-order |

**Checklist trước khi hoàn tất:**
- [ ] Mọi sprite đã đúng Z-order
- [ ] Tâm xoay đặt đúng điểm bám
- [ ] Parent đã gắn theo sơ đồ mục 4
- [ ] Tóc/vạt áo/ahoge lắc mềm, không lộ hở
- [ ] Chớp mắt và nói hoạt động đúng
- [ ] Costume 1–5 chuyển được và không chồng hình
- [ ] Đã lưu file `.save` và sao lưu

---

## 9. Mẹo tinh chỉnh

- Bắt đầu với số **nhỏ**, tăng dần; chuyển động tinh tế trông "đắt" hơn chuyển động mạnh.
- Càng xa điểm bám thì càng lắc nhiều: đuôi tóc, ahoge, dây ruy băng nên có biên độ lớn nhất.
- Các bộ phận đối xứng (trái/phải) hãy lệch tần số một chút để tự nhiên.
- Bộ phận cứng (kẹp tóc, khóa thắt lưng, giày) không nên có chuyển động riêng.
- Nên quay thử màn hình vài chục giây khi nói chuyện để xem tổng thể trước khi livestream.
