# Phân tích Yêu cầu Day 20 Lab — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

> Tài liệu này là **bộ phân tích đầy đủ** theo yêu cầu Day 20 Lab (Retention, Engagement & Habit Loop),
> được viết dựa trực tiếp trên prototype [index.html](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/index.html)
> đã xây dựng ở Day 18, không phải bản khung mẫu.

---

## 00 — Prototype Ngày 18 / Current State

### Prototype hiện tại có 9 màn hình

| # | Screen ID | Tên hiển thị | Mục đích chính |
|---|-----------|--------------|---------------|
| 01 | `onboarding` | AI Capability Onboarding | Đặt kỳ vọng: AI có thể / chưa chắc / không được làm |
| 02 | `input` | Trip Input | User nhập ngày đi, số người, xuất phát, ngân sách, nhịp, sở thích |
| 03 | `draft` | AI Draft Itinerary | AI tạo bản nháp lịch trình 6 chặng theo timeline |
| 04 | `evidence` | Evidence & Assumptions | Minh bạch hóa: dữ kiện user / giả định AI / thông tin chưa chắc |
| 05 | `ask` | Ask State | AI hỏi phương tiện trước khi cập nhật lịch |
| 06 | `recovery` | Recovery | Điều chỉnh lịch khi user phản hồi "lịch quá dày" |
| 07 | `uncertainty` | Uncertainty | User chọn cách xử lý dữ liệu chưa chắc |
| 08 | `feedback` | Feedback Loop | User chọn lý do phản hồi (explicit + implicit) |
| 09 | `review` | Final Review | Xem lại lịch trình cuối trước khi lưu |

**Demo path hiện tại:** Onboarding → Input → Draft → Evidence → Ask → Recovery → Uncertainty → Feedback → Review

---

## 01 — Customer Retention Canvas

### Use Case được chọn
> Người dùng muốn lên lịch trình tự túc 1 ngày đến Ninh Bình nhưng không biết cách sắp xếp thứ tự điểm đến, ước tính thời gian di chuyển và kiểm soát ngân sách cho cả nhóm.

### The Problem *(góc nhìn người dùng)*
*"Tôi muốn đi Ninh Bình 1 ngày cùng gia đình nhưng mỗi lần tự lên kế hoạch mất cả buổi tra Google, vẫn không chắc lịch có hợp lý không, đặc biệt khi trong nhóm có người lớn tuổi và không muốn đi quá nặng."*

### The Persona
| Thuộc tính | Chi tiết |
|------------|----------|
| **Vai trò** | Người tổ chức chuyến đi trong gia đình hoặc nhóm bạn (22–35 tuổi) |
| **Hoàn cảnh** | Có 1–2 ngày nghỉ cuối tuần, muốn tận dụng tối đa nhưng không mệt |
| **Mục tiêu** | Có lịch trình khả thi, không vượt ngân sách, phù hợp với tất cả thành viên |
| **Kinh nghiệm** | Đã từng đi du lịch tự túc nhưng không có quy trình cố định |
| **Thiết bị** | Dùng điện thoại hoặc laptop khi lên kế hoạch, thường vào buổi tối |

### Anti-Persona *(không phải khách hàng mục tiêu)*
- Người đi tour trọn gói, không muốn tự lên lịch.
- Hướng dẫn viên du lịch chuyên nghiệp — đã có quy trình riêng.
- Người chỉ muốn tra cứu thông tin địa điểm đơn lẻ (Google Maps đủ dùng).
- Người đi công tác, không có nhu cầu tham quan.

### The Why *(động lực cốt lõi)*
Không chỉ là "tiết kiệm thời gian" — lý do sâu hơn là **không muốn phạm sai lầm khi đi cùng người thân**: đặt lịch quá dày làm mọi người mệt, vượt ngân sách gây khó xử, hoặc đến nơi thì đóng cửa.

### The Alternative *(giải pháp thay thế hiện tại)*
- Tra Google nhiều tab, copy-paste thủ công vào Notes/Excel.
- Hỏi nhóm du lịch Facebook, mất nhiều thời gian và không cá nhân hóa.
- Dùng blog hướng dẫn du lịch có sẵn (không điều chỉnh được theo nhóm cụ thể).
- Nhờ người quen đã đi trước tư vấn.

### The Frequency *(tần suất tự nhiên)*
| Tần suất | Ghi chú |
|----------|---------|
| **Quarterly / Seasonal** | Người Việt thường đi du lịch nội địa 2–4 lần/năm |
| Không đều | Phụ thuộc vào dịp lễ, kỳ nghỉ, sự kiện gia đình |
| **Kết luận** | Đây là **low-frequency product** — không thể dùng DAU hay D1 Retention |

---

## 02 — Core Action & Active User

### Core Action (Hành động cốt lõi)

> **Core Action = User lưu lịch trình Ninh Bình hoàn chỉnh sau khi AI đã điều chỉnh ít nhất 1 lần theo phản hồi.**

Lý do chọn hành động này:
- Hành động **"Lưu lịch trình"** (nút `Lưu lịch trình` tại màn `review`) là điểm user nhận được giá trị thực sự — không chỉ xem, mà có kế hoạch dùng được.
- Điều kiện "đã điều chỉnh ít nhất 1 lần" xác nhận AI đã thực sự có ích (không chỉ tạo draft rồi bỏ qua).
- Các click trước đó (mở onboarding, nhập form) là **Leading Action**, chưa phải Core Action.

### Định nghĩa Active User

> *"Một user được tính là **active** khi họ hoàn thành Core Action (lưu lịch trình đã chỉnh sửa) ít nhất **1 lần trong vòng 90 ngày**."*

Giải thích: chu kỳ 90 ngày (1 quý) phù hợp với tần suất đi du lịch nội địa của người dùng mục tiêu.

### Không nên dùng
- ❌ DAU (Daily Active User) — tần suất tự nhiên quá thấp, không ai mở Trip Planner mỗi ngày.
- ❌ D1 Retention — không phù hợp với sản phẩm lên kế hoạch theo mùa.
- ❌ WAU (Weekly Active User) — vẫn quá cao so với nhu cầu thực.

---

## 03 — Natural Frequency & Retention Metric

### Natural Frequency Analysis

| Câu hỏi | Trả lời |
|---------|---------|
| Vấn đề xảy ra bao lâu 1 lần? | ~2–4 lần/năm (dịp lễ, nghỉ hè, cuối tuần dài) |
| User cần sản phẩm liên tục không? | Không — chỉ cần trước chuyến đi |
| Có thể tạo thói quen dùng hàng tuần không? | Không nên — sẽ là forced habit, không có nhu cầu thật |

### Retention Metric phù hợp

**→ Quarterly Retention (QR):**

```
Quarterly Retention = (Số user đã lưu lịch trình trong Q trước VÀ lưu lịch trình trong Q này) / (Số user đã lưu lịch trình trong Q trước) × 100%
```

**Chỉ số bổ sung:**
- **Trip Completion Rate:** % user bắt đầu nhập form → lưu lịch trình thành công.
- **Adjustment Rate:** % user chỉnh sửa lịch ít nhất 1 lần trước khi lưu (chỉ số chất lượng AI).
- **Time-to-First-Save:** Thời gian từ lần đầu mở app đến lần đầu lưu lịch.

---

## 04 — Onboarding Audit (Đánh giá Luồng Hiện Tại)

Dựa trên 9 màn hình trong [index.html](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/index.html):

### Bảng Audit từng bước

| Bước | Màn hình | Nhãn | Lý do |
|------|----------|------|-------|
| 1 | **Onboarding** — AI có thể / chưa chắc / không được làm | **Keep** | Cần thiết để đặt kỳ vọng đúng; tránh user hiểu sai khả năng AI |
| 2 | **Trip Input** — Nhập ngày, số người, xuất phát, ngân sách, nhịp, sở thích, ghi chú | **Simplify** | 7 trường nhập + dropdown — cần giảm xuống 3–4 trường tối thiểu; các trường ít quan trọng (nhịp đi, sở thích) có thể Delay |
| 3 | **AI Draft** — Bản nháp 6 chặng theo timeline | **Keep** | Đây chính là First Core Value — user thấy AI có ích ngay tại đây |
| 4 | **Evidence & Assumptions** | **Delay** | Quan trọng về trust calibration nhưng chưa cần hiển thị ngay sau draft; có thể dời thành tab phụ hoặc tooltip |
| 5 | **Ask State** — Hỏi phương tiện | **Keep** | Thiết yếu, ảnh hưởng trực tiếp đến lịch trình; nhưng nên hỏi trước khi tạo Draft, không phải sau |
| 6 | **Recovery** — Điều chỉnh lịch quá dày | **Keep** | Đây là Recovery Path quan trọng từ Day 18, phải giữ lại |
| 7 | **Uncertainty** — Xử lý dữ liệu chưa chắc | **Keep** | Thiết yếu cho trust calibration, giữ nguyên |
| 8 | **Feedback Loop** — Chọn lý do phản hồi | **Simplify** | Nên gộp vào màn Review để giảm số bước; không cần màn riêng |
| 9 | **Final Review** — Xem lại trước khi lưu | **Keep** | Đây là điểm Core Action (lưu lịch trình), phải giữ |

### Chỉ số Onboarding Hiện Tại

| Chỉ số | Giá trị hiện tại |
|--------|-----------------|
| Số bước đến First Core Value (thấy Draft) | **3 bước** (Onboarding → Input → Draft) |
| Số trường nhập thông tin | **7 trường** (ngày, số người, xuất phát, ngân sách, nhịp, sở thích, ghi chú) |
| Số bước đến Core Action (lưu lịch) | **9 bước** (toàn bộ flow) |
| Thời gian ước tính đến First Core Value | ~3–4 phút |
| Thời gian ước tính đến Core Action | ~8–10 phút |
| Điểm drop-off ước tính cao nhất | **Bước 2 — Trip Input** (7 trường quá nhiều) |

---

## 05 — Redesigned Onboarding → First Core Action

### Luồng mới đề xuất (6 bước thay vì 9)

```
[Bước 1] Onboarding nhanh (Keep — rút gọn còn 1 màn hình, loại bỏ mô tả dài)
    ↓
[Bước 2] Nhập nhanh 3 trường tối thiểu: Điểm đến | Ngày đi | Số người  (Simplify)
    ↓
[Bước 3*] Ask: Phương tiện di chuyển (Keep — dời lên TRƯỚC Draft để lịch chính xác hơn)
    ↓
[Bước 4] AI Draft Itinerary — First Core Value hiển thị  (Keep)
    ↓
[Bước 5] Recovery / Điều chỉnh (Keep — Recovery Path từ Day 18)
    ↓
[Bước 6] Final Review + Lưu lịch — Core Action  (Keep + gộp Feedback vào đây)
```

> **Delay:** Evidence & Assumptions → chuyển thành tab phụ "Xem chi tiết" trong màn Draft.
> **Delay:** Nhịp đi, Sở thích, Ghi chú → hỏi sau khi user thấy Draft (nếu muốn tinh chỉnh).
> **Remove:** Màn Feedback riêng → gộp vào Final Review.
> **Remove:** Màn Uncertainty riêng → tích hợp thành banner cảnh báo inline trong Draft.

### Nguyên tắc thiết kế luồng mới
1. **Show value first:** Đưa user thấy bản nháp lịch trình (First Core Value) nhanh nhất có thể.
2. **Progressive disclosure:** Giả định & độ tin cậy hiện dần theo từng tương tác, không đổ hết một lúc.
3. **Ask before draft (không phải sau):** Hỏi phương tiện trước khi AI tạo lịch — tránh tạo lịch sai rồi phải sửa.
4. **Recovery path intact:** Giữ nguyên luồng Recovery từ Day 18 (user phản hồi "quá dày" → AI điều chỉnh).

---

## 06 — Before/After & Recovery Path

### So sánh Before / After

| Chỉ số | Before (Day 18) | After (Redesign) | Thay đổi |
|--------|----------------|-----------------|---------|
| Số bước đến First Core Value | 3 bước | **2 bước** | −1 |
| Số trường nhập tối thiểu | 7 trường | **3 trường** | −4 |
| Số bước đến Core Action | 9 bước | **6 bước** | −3 |
| Thời gian đến First Core Value | ~3–4 phút | **~1–2 phút** | ↓ 50% |
| Thời gian đến Core Action (TTV) | ~8–10 phút | **~5–6 phút** | ↓ 40% |
| Điểm drop-off chính | Trip Input (7 trường) | Sau Ask State | Cải thiện |
| Recovery Path | Màn 06 riêng biệt | **Giữ nguyên** | ✓ |

### Recovery Path được giữ lại (từ Day 18)

**Kịch bản:** User nhập lịch trình, AI tạo Draft → User phản hồi "lịch quá dày / có người lớn tuổi" → AI điều chỉnh giảm điểm, thêm thời gian nghỉ, thay địa điểm leo nhiều bằng địa điểm nhẹ hơn.

Đây là Recovery Path thiết yếu cần giữ lại vì:
- Thể hiện AI thực sự "lắng nghe" user (không chỉ là kết quả một chiều).
- Giúp user tin tưởng AI hơn sau khi thấy nó sửa đúng vào điểm được phản hồi.
- Là tín hiệu Explicit Feedback quan trọng nhất trong toàn bộ flow.

---

## 07 — Measurement Ladder

```
                    ┌─────────────────────────────────────┐
                    │       NORTH STAR METRIC              │
                    │  Tổng số lịch trình Ninh Bình        │
                    │  được lưu thành công sau khi         │
                    │  AI điều chỉnh ≥ 1 lần               │
                    └──────────────┬──────────────────────┘
                                   │
          ┌────────────────────────┼────────────────────────┐
          ▼                        ▼                        ▼
   ┌─────────────┐        ┌─────────────────┐      ┌─────────────────┐
   │ INPUT 1     │        │ INPUT 2         │      │ INPUT 3         │
   │ Trip        │        │ Adjustment      │      │ Time-to-First   │
   │ Completion  │        │ Rate            │      │ Save (TFS)      │
   │ Rate (%)    │        │ (% user sửa ≥1) │      │ (phút)          │
   └─────────────┘        └─────────────────┘      └─────────────────┘
          │                        │                        │
          ▼                        ▼                        ▼
   Đo: Số user             Đo: Số lần click         Đo: Thời gian
   hoàn thành /            Recovery, Feedback /     từ session đầu
   Số user bắt đầu         Tổng session             đến Core Action
```

---

## 08 — North Star Metric & Input Metrics

### North Star Metric (NSM)

> **"Tổng số lịch trình Ninh Bình được lưu thành công sau khi AI điều chỉnh ít nhất 1 lần theo phản hồi của user"**

**Lý do chọn:**
- Thể hiện giá trị cốt lõi: user nhận được lịch trình *phù hợp với họ*, không phải lịch mẫu cứng nhắc.
- Điều kiện "điều chỉnh ≥ 1 lần" đảm bảo AI thực sự có ích, không chỉ đóng vai trò tạo template.
- Gắn trực tiếp với hành vi quan sát được trong prototype (màn Recovery + màn Review → nút Lưu).

### Input Metrics (3 chỉ số)

| Metric | Định nghĩa | Tác động đến NSM |
|--------|-----------|-----------------|
| **Trip Completion Rate** | % user bắt đầu nhập form → lưu lịch thành công | Tăng completion → tăng NSM |
| **Adjustment Rate** | % user kích hoạt ít nhất 1 Recovery/Feedback trước khi lưu | Tăng Adjustment → NSM chất lượng cao hơn |
| **Time-to-First-Save (TFS)** | Trung bình số phút từ lần đầu vào app đến lần đầu lưu lịch | TFS càng thấp → friction càng ít → NSM tăng |

### Mid/Long-term Value

- **Business:** Dữ liệu về điểm đến phổ biến, ngân sách trung bình, nhóm đi → cơ sở để kết nối với đơn vị cung cấp dịch vụ du lịch Ninh Bình.
- **Customer:** User có lịch trình cá nhân hóa ngày càng tốt hơn khi AI học từ lịch sử chỉnh sửa.

### Leading vs Lagging Indicator

| Loại | Metric | Lý do |
|------|--------|-------|
| **Leading** | Adjustment Rate, TFS, số lần Ask State được kích hoạt | Dự báo khả năng lưu thành công trước khi xảy ra |
| **Lagging** | NSM (Tổng lịch đã lưu), Quarterly Retention | Đo kết quả sau khi đã xảy ra |

### Trade-off

| Tối ưu hóa | Rủi ro đánh đổi |
|------------|----------------|
| Giảm số bước onboarding | AI nhận ít thông tin hơn → Draft kém chính xác → Adjustment Rate tăng không phải vì AI tốt, mà vì AI thiếu dữ liệu |
| Tăng số gợi ý điểm đến (cross-sell) | Làm nhiễu flow lên kế hoạch → tăng cognitive load → giảm Completion Rate |
| Hỏi nhiều câu Ask State để chắc chắn hơn | Tăng friction → user bỏ cuộc trước khi thấy Draft |

---

## 09 — Nature vs Nurture

### Nature (Hành vi Tự Nhiên)

Người dùng NiBiGo chỉ có nhu cầu lên lịch du lịch **2–4 lần/năm**. Đây là sản phẩm **low-frequency by nature** — không thể tạo thói quen dùng hàng tuần theo cách ép buộc.

Điều đó có nghĩa là:
- Retention strategy không thể dựa vào daily/weekly engagement.
- Giá trị sản phẩm phải cực kỳ rõ ràng ngay trong **session đầu tiên** (first-trip experience).
- Mỗi lần quay lại phải cảm thấy quen thuộc và dễ hơn lần trước (memory of past trips).

### Nurture (Kích hoạt Chủ Động từ Sản Phẩm)

| Kênh | Nội dung Nurture | Thời điểm |
|------|-----------------|----------|
| **Email / Push Notification** | "Sắp đến dịp 30/4 — bạn muốn lên kế hoạch đi Ninh Bình không?" | 3–4 tuần trước dịp lễ lớn |
| **In-app suggestion** | "Lần trước bạn đã đi Tràng An. Lần này thử thêm Bái Đính không?" | Khi user mở app lần 2+ |
| **Seasonal nudge** | Gợi ý điểm đến theo thời tiết/mùa (tránh mùa mưa, khuyến nghị mùa thu) | Trigger theo calendar |
| **Trip reminder** | "Lịch trình của bạn còn 5 ngày nữa — bạn muốn xác nhận giờ mở cửa không?" | Dựa trên ngày đi đã lưu |

---

## 10 — Hook Review

### Đánh giá Hook Model cho NiBiGo

Vì tần suất tự nhiên thấp (quarterly), **không nên cố tạo habit loop Daily/Weekly**. Tuy nhiên, trong phạm vi **1 chuyến đi**, Hook Model vẫn có thể hoạt động:

| Thành phần | Áp dụng trong NiBiGo |
|------------|---------------------|
| **Trigger (External)** | Email nhắc dịp lễ, push notification gợi ý điểm đến theo mùa |
| **Trigger (Internal)** | Cảm giác lo lắng khi sắp đến kỳ nghỉ mà chưa có kế hoạch |
| **Action** | Mở app → nhập 3 trường tối thiểu → xem Draft lịch trình |
| **Variable Reward** | *The Self:* Cảm giác kiểm soát được chuyến đi, tự tin hơn khi đặt lịch; *The Hunt:* Khám phá điểm đến mới AI gợi ý mà mình chưa biết |
| **Investment** | Lưu lịch trình, đánh dấu điểm cần xác nhận, chia sẻ với người đi cùng → tăng commitment, tạo lý do quay lại lần sau |

**Kết luận:** Hook Model áp dụng được ở **cấp độ per-trip** (mỗi chuyến đi là 1 vòng hook), không phải hàng ngày. Đây là thiết kế hợp lý với tần suất tự nhiên của sản phẩm.

---

## 11 — Metric Tracking Requirement

### Bảng định nghĩa Metric

| Metric | Câu hỏi cần trả lời | Định nghĩa | Công thức | Chu kỳ | Segment |
|--------|---------------------|-----------|-----------|--------|---------|
| **NSM** | AI có thực sự giúp user tạo lịch phù hợp không? | Số lịch trình được lưu sau khi AI điều chỉnh ≥ 1 lần | COUNT(save_events WHERE adjustment_count ≥ 1) | Hàng tháng | Nhóm đi, ngân sách |
| **Trip Completion Rate** | Bao nhiêu % user hoàn thành toàn bộ flow? | % user bắt đầu nhập form → lưu lịch | COUNT(save) / COUNT(form_start) × 100 | Hàng tuần | Thiết bị, nguồn truy cập |
| **Adjustment Rate** | AI có đủ linh hoạt để phù hợp với từng user không? | % session có ít nhất 1 lần Recovery hoặc Feedback | COUNT(sessions WITH recovery_or_feedback) / COUNT(sessions WITH draft_viewed) × 100 | Hàng tuần | Loại phương tiện, nhịp đi |
| **Time-to-First-Save (TFS)** | Onboarding có đủ nhanh không? | Thời gian (phút) từ session_start → save_itinerary | MEDIAN(save_timestamp − session_start_timestamp) | Hàng tuần | Lần dùng đầu / lần dùng lại |
| **Quarterly Retention** | User có quay lại sau 90 ngày không? | % user lưu lịch trong Q1 VÀ cũng lưu trong Q2 | Cohort retention theo quý | Hàng quý | Nhóm đầu tiên dùng |

### Bảng yêu cầu Tracking Event

| Tên Event | Điều kiện kích hoạt | User Identity | Properties | Metric sử dụng | Tránh ghi trùng |
|-----------|---------------------|---------------|-----------|----------------|----------------|
| `session_start` | User mở app / load index.html | `user_id` (ẩn danh nếu chưa đăng nhập) | `device`, `source`, `timestamp` | TFS, Completion Rate | Dedupe theo session_id trong 30 phút |
| `form_start` | User bắt đầu nhập trường đầu tiên trong Trip Input | `user_id` | `trip_date`, `group_size`, `timestamp` | Completion Rate | Không ghi lại nếu đã có form_start trong cùng session |
| `draft_viewed` | Màn `draft` được render và hiển thị đầy đủ | `user_id`, `session_id` | `num_stops`, `transport_mode`, `timestamp` | Adjustment Rate, TFS | Chỉ ghi 1 lần per session ngay cả khi user quay lại màn draft |
| `adjustment_triggered` | User click vào Recovery / Feedback / Ask State selection | `user_id`, `session_id` | `trigger_type` (recovery/feedback/ask), `reason`, `timestamp` | NSM, Adjustment Rate | Ghi theo từng lần click; không collapse |
| `save_itinerary` | User click nút "Lưu lịch trình" tại màn `review` | `user_id`, `session_id` | `adjustment_count`, `num_stops_final`, `time_to_save`, `timestamp` | NSM, TFS, Completion Rate | Idempotency key = session_id + timestamp rounded to 10s |
| `share_draft` | User click "Chia sẻ bản nháp" | `user_id`, `session_id` | `share_method`, `timestamp` | Investment signal | Dedupe theo session_id + share_method trong 60s |

### Vị trí gắn Event trên flow

```
[session_start]
      ↓
[Onboarding] → không gắn event riêng (chỉ view)
      ↓
[Trip Input] → [form_start] khi user bắt đầu nhập
      ↓
[Ask State] → [adjustment_triggered, trigger_type: "ask"]  ← nếu user trả lời
      ↓
[AI Draft] → [draft_viewed]
      ↓
[Recovery] → [adjustment_triggered, trigger_type: "recovery"]  ← nếu user click
      ↓
[Feedback] → [adjustment_triggered, trigger_type: "feedback"]  ← nếu user chọn lý do
      ↓
[Final Review] → [save_itinerary] hoặc [share_draft]
```

### Tiêu chí nghiệm thu Tracking (≥ 4 tiêu chí)

1. **Tính chính xác:** `save_itinerary` chỉ được ghi khi user thực sự click nút Lưu — không tính các lần xem màn Review mà chưa click.
2. **Không trùng lặp:** Dùng idempotency key (session_id + timestamp) để tránh ghi double khi user click nhanh hoặc retry.
3. **Đủ thuộc tính:** Mỗi event phải chứa `user_id`, `session_id`, `timestamp`; các event key (`save_itinerary`, `draft_viewed`) phải có thêm `adjustment_count` và `time_to_save`.
4. **Phân biệt lần đầu / lần lại:** Event `save_itinerary` phải có thuộc tính `is_first_save: boolean` để phân biệt cohort user mới và user quay lại.
5. **Không track hành vi nhạy cảm:** Không lưu nội dung ghi chú của user; không track vị trí địa lý khi chưa có consent rõ ràng.

---

## 12 — Demo Path (Cập nhật cho Day 20)

### Demo 8 phút đề xuất

| Thời gian | Nội dung |
|-----------|---------|
| 0:00–0:45 | Giới thiệu: Persona, Use Case, Core Action của NiBiGo (Day 20 lens) |
| 0:45–1:30 | Customer Retention Canvas: Problem, Why, Alternative, Frequency |
| 1:30–2:15 | Onboarding Audit: Chỉ ra 7 trường → 3 trường, Evidence Delay, Feedback gộp |
| 2:15–3:00 | Demo luồng mới: Nhập nhanh 3 trường → Ask phương tiện → Draft (First Core Value) |
| 3:00–4:00 | Demo Recovery Path (giữ từ Day 18): Lịch quá dày → AI điều chỉnh → Review |
| 4:00–5:00 | North Star Metric + Measurement Ladder + Trade-off analysis |
| 5:00–6:30 | Nature vs Nurture: Khi nào nudge, khi nào không; Hook Model per-trip |
| 6:30–8:00 | Tracking Event table: 5 events chính, tiêu chí nghiệm thu, Q&A |

---

*Tài liệu hoàn thiện lần 1 — 24/06/2026*
*Dựa trên: [index.html](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/index.html), [scenario-list.md](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/docs/scenario-list.md), [flow-map.md](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/docs/flow-map.md), [feedback-matrix.md](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/docs/feedback-matrix.md), [act-ask-dont-act.md](file:///c:/Vinuni/D20/Day18-2A202600662-DangTranDat-Track1/docs/act-ask-dont-act.md)*
