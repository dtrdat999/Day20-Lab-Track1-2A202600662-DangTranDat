# NiBiGo AI Trip Planner — Day 18 & Day 20 Lab Upgrade
## Nhóm thực hiện (Track 1)
- **Đặng Trần Đạt** - 2A202600662
- **Nguyễn Hoàng Dương** - 2A202600849
- **Cao Văn Hảo** - 2A202600874
- **Nguyễn Quang Hòa** - 2A202600986

Bộ sản phẩm tích hợp bao gồm Prototype tương tác và Hệ tài liệu Phân tích thiết kế Lập kế hoạch du lịch tự túc Ninh Bình nhằm tối ưu hóa tỷ lệ giữ chân khách hàng (Retention), mức độ tương tác (Engagement) và vòng lặp thói quen theo chuyến đi (Habit Loop).

---

## 1. Cấu trúc thư mục dự án (Repository Structure)

Dự án được tổ chức tự giải thích và đóng gói gọn gàng (Self-contained) để mở trực tiếp trên mọi trình duyệt:
* **Màn hình chính:**
  * [index.html](./index.html) — Bảng điều khiển thuyết trình tích hợp 18 mục và **Giả lập điện thoại di động (Mobile Simulator) kịch bản Day 20**.
* **Thư mục tài liệu phân tích (`docs/`):**
  * [day20-retention-canvas.md](./docs/day20-retention-canvas.md) — Customer Retention Canvas (Problem, Persona, Anti-Persona, Frequency).
  * [day20-core-action-metrics.md](./docs/day20-core-action-metrics.md) — Định nghĩa Core Job, Core Action, Active User và chỉ số giữ chân 7 ngày.
  * [day20-onboarding-audit.md](./docs/day20-onboarding-audit.md) — Phân tích ma sát (Friction) phễu cũ và các quyết định cải tiến.
  * [day20-measurement-ladder.md](./docs/day20-measurement-ladder.md) — Cây đo lường chỉ số phân cấp (Measurement Ladder) hướng doanh thu.
  * [day20-hook-tracking.md](./docs/day20-hook-tracking.md) — Sơ đồ Hook Model per-trip và đặc tả Event Tracking đo lường kỹ thuật.
  * [day20-roadmap-2d1n.md](./docs/day20-roadmap-2d1n.md) — Chiến lược MVP 1 ngày và lộ trình nâng cấp lên 2 ngày 1 đêm (2D1N) phòng ngừa rủi ro.
  * [day20-demo-path.md](./docs/day20-demo-path.md) — Kịch bản thuyết trình chi tiết 8 phút bằng tiếng Việt.

---

## 2. Hướng dẫn khởi chạy ứng dụng (Run Instructions)

Để đảm bảo các hiệu ứng chuyển trang và mã Javascript hoạt động mượt mà nhất, bạn nên khởi chạy thông qua một máy chủ HTTP tĩnh local thay vì mở trực tiếp đường dẫn file cục bộ:

```bash
# Di chuyển vào thư mục dự án đã clone
cd <tên-thư-mục-dự-án>

# Chạy server tĩnh bằng npx serve (mặc định mở ở cổng 3000)
npx serve
```
Sau đó truy cập địa chỉ: **[http://localhost:3000/index.html](http://localhost:3000/index.html)** để xem bảng thuyết trình kèm giả lập di động.

---

## 3. Khung Tóm Tắt Bài Lab Day 18 & Day 20

### Prototype Day 18 (Nguyên bản)
* **Lát cắt thiết kế:** Tạo lịch trình Ninh Bình 1 ngày tự túc, tập trung vào thiết kế AI lấy con người làm trung tâm (Human-Centered AI).
* **Đặc tính:** Giúp người dùng phân định rõ AI biết gì/chưa biết gì (Evidence & Assumptions) và kiểm soát hoàn toàn thông tin qua luồng Recovery (Lịch quá dày) và Uncertainty (Xử lý dữ liệu không chắc chắn).
* **Demo path 9 bước:** Onboarding → Input (7 trường) → Draft → Evidence → Ask (Phương tiện) → Recovery → Uncertainty → Feedback → Review.

### Nâng cấp Day 20 (Retention & Habit Loop)
* **Tư duy cốt lõi:** Dịch chuyển từ *"giao diện đẹp"* sang *"giá trị sử dụng rõ rệt để người dùng quay lại đúng tần suất tự nhiên"*.
* **Cải tiến Onboarding:** Cắt giảm phễu từ 9 bước xuống còn 7 bước tối giản. Di chuyển việc lựa chọn phương tiện (Ask State) lên trước, ẩn bảng giả định Evidence kỹ thuật vào ngăn kéo, và inline các cảnh báo Uncertainty để giảm thiểu tối đa ma sát nhận thức (Cognitive load).
* **Core Action:** Lưu, chia sẻ cho bạn bè, hoặc chốt liên hệ tư vấn dịch vụ chặng đi thực tế.
* **Retention Metric:** Tỷ lệ người dùng quay lại lập lịch trình trong 7 ngày trước khi chuyến đi diễn ra (**7-day Planning Return Rate**).
* **Hook Model:** Kích hoạt theo từng chuyến đi (per-trip) thay vì cố tạo thói quen dùng hàng ngày ép buộc.

---

## 4. Kịch bản Thuyết trình Demo 8 phút (Vietnamese Script Outline)

* **0:00 - 0:45 | Giới thiệu:** Sử dụng [index.html](./index.html) (Mục 00). Nêu rõ use case Ninh Bình 1 ngày và lộ trình 2D1N.
* **0:45 – 1:30 | Canvas & Tần suất:** Trình bày bảng Customer Retention Canvas (Mục 03) và đặc tính Low-frequency của sản phẩm du lịch.
* **1:30 – 2:15 | Kiểm toán & Sơ đồ phễu:** Chỉ rõ các điểm nghẽn ở Day 18 cũ (Mục 06) và giải pháp rút ngắn luồng ở Mục 07.
* **2:15 – 3:30 | Demo lập lịch nhanh:** Mở giả lập di động ở **Mục 08**. Nhập 5 thông số chọn nhanh và nhận ngay 3 phương án đối sánh kinh tế / độ mệt (Aha Moment).
* **3:30 – 4:30 | Demo Feasibility & Recovery:** AI cảnh báo inline việc leo Hang Múa buổi trưa nắng gắt. Nhấp "Tối ưu lại nhẹ hơn" để xem AI tự động dời chặng sang chiều mát và thêm nghỉ trưa.
* **4:30 – 5:30 | Demo Core Action:** Người dùng hoàn toàn hài lòng, tiến hành nhấn Lưu hoặc Chia sẻ lịch trình chốt kế hoạch.
* **5:30 – 6:30 | Chỉ số NSM:** Trình bày North Star Metric ("Useful Itineraries Saved/Shared") và Measurement Ladder ở Mục 11 & 12.
* **6:30 – 7:20 | Nature vs Nurture & Hook Model:** Thuyết minh nguyên tắc nhắc nhở thời tiết 3 ngày trước chuyến đi và mô hình Hook 4 chặng (Mục 13 & 14).
* **7:20 – 8:00 | Roadmap & Kết luận:** Phân tích rủi ro kỹ thuật vỡ chặng khi lên lịch 2 ngày 1 đêm và kết luận bài báo cáo.

---

## 5. Mức độ đáp ứng tiêu chí đánh giá (Checklist Compliance)

Dự án đã đáp ứng đầy đủ các tiêu chí đánh giá của bài Lab Day 20:

- [x] **Product logic:** Xác định Use Case rõ ràng (Ninh Bình 1 ngày). Đã mapping chuẩn Persona, Natural Frequency và Core Action logic với nhau. 
- [x] **Onboarding → First Core Action:** Có Audit Current Flow cụ thể. Cắt giảm ma sát (từ 9 bước xuống 7 bước). Có thiết kế Before/After tường minh dẫn tới First Core Action. Giữ và cải thiện tốt Recovery Flow cảnh báo khả thi từ Day 18.
- [x] **Metrics & Habit:** Xây dựng Measurement Ladder bài bản. Định nghĩa "7-day Planning Return Rate" làm Retention Metric cực kì hợp lý với du lịch (low-frequency). Xây dựng vòng lặp Nature/Nurture và Hook theo cấp độ chuyến đi.
- [x] **Tracking:** Event Tracking có định nghĩa đo lường, property đi kèm, giúp tính toán trực tiếp được Input Metrics.
- [x] **Submission:** Hoàn thiện giao diện Day 20 (`index.html`) kèm đầy đủ bảng điều khiển thuyết trình. Cung cấp sẵn Demo Path kịch bản tối ưu trong 8 phút (Section 17).
