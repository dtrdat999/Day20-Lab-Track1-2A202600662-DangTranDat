# Measurement Ladder — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

Tài liệu này thiết lập hệ thống chỉ số đo lường hiệu năng của NiBiGo dưới dạng cây phân cấp (Measurement Ladder), liên kết các hoạt động kỹ thuật với mục tiêu kinh doanh cuối cùng.

---

## 1. Cấu trúc cây chỉ số Measurement Ladder cho NiBiGo

Hệ thống chỉ số được chia thành 5 tầng từ lượng truy cập đầu vào đến giá trị kinh doanh:

```
                            ┌───────────────────────────────────────────┐
                            │            BUSINESS VALUE                 │
                            │  Doanh thu từ giới thiệu xe Limousine,    │
                            │  đặt vé thuyền và bán tour du lịch Ninh Bình │
                            └─────────────────────┬─────────────────────┘
                                                  │
                            ┌─────────────────────┴─────────────────────┐
                            │           NORTH STAR METRIC               │
                            │   Useful Itineraries Saved or Shared      │
                            │         per Month (Lịch lưu/chia sẻ)      │
                            └─────────────────────┬─────────────────────┘
                                                  │
         ┌────────────────────────────────────────┼────────────────────────────────────────┐
         ▼                                        ▼                                        ▼
  ┌──────────────┐                         ┌──────────────┐                         ┌──────────────┐
  │   TRAFFIC    │                         │  ACTIVATION  │                         │  RETENTION   │
  │ Lượng khách  │                         │ Thời gian    │                         │ Tỷ lệ quay   │
  │ truy cập SEO │                         │ tiếp cận     │                         │ lại lập lịch │
  │ tìm chặng đi │                         │ giá trị đầu  │                         │ trong 7 ngày │
  └──────────────┘                         └──────────────┘                         └──────────────┘
```

---

## 2. Đặc tả Chi Tiết Các Tầng Đo Lường

### Tầng 1: Traffic (Lưu lượng đầu vào)
* **Chỉ số:** SEO Landing Page Traffic (Lượng khách truy cập tự nhiên).
* **Định nghĩa:** Tổng số người dùng truy cập trang web thông qua các từ khóa tìm kiếm liên quan đến *"lịch trình Ninh Bình tự túc 1 ngày"*, *"kinh nghiệm đi Tràng An"* trên Google.
* **Mục tiêu:** Thu hút tệp khách hàng có nhu cầu thực tế cao, giảm chi phí quảng cáo (CAC).

### Tầng 2: Activation (Kích hoạt người dùng & Time-to-Value)
* **Chỉ số:** Time-to-Value (TTV) & Submit Rate.
* **Định nghĩa:**
  * **Submit Rate:** % số lượng user hoàn thành biểu mẫu 5 trường trên tổng số lượt truy cập.
  * **TTV:** Số giây trung bình từ lúc người dùng nhấn nút khởi động đến khi 3 phương án lịch trình hiện ra trên màn hình.
* **Mục tiêu:** Đảm bảo người dùng nhìn thấy bản nháp đầu tiên nhanh nhất có thể, tránh nản lòng thoát ứng dụng (drop-off).

### Tầng 3: Core Action (Hành động giá trị cốt lõi)
* **Chỉ số:** Option Selection Rate & Draft-to-Save/Share Rate.
* **Định nghĩa:**
  * **Option Selection Rate:** % người dùng nhấp chọn 1 trong 3 phương án.
  * **Draft-to-Save Rate:** % người dùng nhấn Lưu lịch trình hoặc Chia sẻ liên kết cho bạn đồng hành sau khi xem cảnh báo khả thi.
* **Mục tiêu:** Chuyển đổi đề xuất AI thành kế hoạch thực tế có thể dùng của người dùng.

### Tầng 4: Retention (Giữ chân người dùng)
* **Chỉ số:** 7-day Planning Return Rate.
* **Định nghĩa:** Tỷ lệ người dùng quay trở lại ứng dụng trong vòng 7 ngày kể từ lần tạo lịch trình đầu tiên để chỉnh sửa, cập nhật thời tiết hoặc chia sẻ lại lịch.
* **Mục tiêu:** Đo lường sự hữu ích của lịch trình đã tạo trong suốt chu kỳ chuẩn bị chuyến đi cuối tuần Ninh Bình.

### Tầng 5: Business Value (Giá trị kinh doanh - Lagging Metric)
* **Chỉ số:** Consultation Leads generated & Affiliate Commission.
* **Định nghĩa:**
  * **Leads:** Số yêu cầu liên hệ dịch vụ vận chuyển (thuê xe Limousine) hoặc đặt tour du lịch Ninh Bình gửi về hệ thống đối tác.
  * **Commission:** Doanh thu thực tế trích từ hoa hồng giới thiệu dịch vụ thành công.
* **Mục tiêu:** Bảo đảm ứng dụng tự nuôi sống được tài chính và có lãi dựa trên giá trị chuyển giao hữu ích.

---

## 3. Present Note
> **Present Note (Dành cho thuyết trình):**
> "Thưa hội đồng, mô hình Measurement Ladder giúp chúng em kết nối trực tiếp hoạt động kỹ thuật với doanh thu. Ở đáy thang đo, chúng em tối ưu SEO và giảm TTV (Activation). Ở giữa, chúng em theo dõi số lịch hữu ích được lưu/chia sẻ (North Star Metric). Ở đỉnh thang đo, chỉ số kinh doanh là số leads giới thiệu xe limousine hay đặt phòng homestay gửi cho các đối tác Ninh Bình của chúng em. Cây chỉ số này bảo đảm mọi tối ưu hóa UX đều hướng tới việc gia tăng doanh thu cuối cùng."
