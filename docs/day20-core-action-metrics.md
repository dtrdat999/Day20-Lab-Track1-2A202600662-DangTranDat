# Core Action & Retention Metrics — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

Tài liệu này xác định hành động cốt lõi mang lại giá trị của ứng dụng, tiêu chí định nghĩa người dùng hoạt động (Active User), và công thức đo lường tỷ lệ giữ chân phù hợp với tần suất tự nhiên của sản phẩm.

---

## 1. Core Job & Core Action

### Core Job (Công việc cốt lõi)
Giúp người dùng biến nhu cầu mơ hồ ban đầu (“muốn đi chơi Ninh Bình cuối tuần nhưng chưa biết đi đâu, bằng gì, ăn gì”) thành một kế hoạch lịch trình khả thi, có thể kiểm chứng chi phí/độ khả thi, dễ dàng lưu trữ và chia sẻ cho người đồng hành.

### Core Action (Hành động cốt lõi)
> **Core Action:** User thực hiện Lưu lịch trình, Chia sẻ lịch trình cho bạn đi cùng, hoặc Xác nhận dùng lịch trình Ninh Bình 1 ngày sau khi đã xem các cảnh báo khả thi (Feasibility check) và thực hiện điều chỉnh (Revision).

#### Lý do hành động này chứng minh người dùng nhận được giá trị (Value Delivery):
* Việc điền form hay xem bản nháp chỉ là các hành động dẫn dắt (**Leading Actions**). User chỉ thực sự nhận được giá trị khi họ lưu lại kế hoạch để chuẩn bị sử dụng trên thực tế, hoặc chia sẻ cho nhóm đi cùng để thống nhất chặng đi.
* Việc lịch trình trải qua bước xem cảnh báo khả thi và có chỉnh sửa chứng minh AI đã giúp họ giải quyết các lỗi sắp xếp lịch trình thời gian thực, tạo ra giá trị khác biệt so với các lịch mẫu cố định trên mạng.

#### Điều kiện ghi nhận sự kiện Core Action xảy ra:
Sự kiện được kích hoạt khi người dùng nhấn vào một trong ba nút hành động chính ở màn hình xem lại cuối cùng:
1. Nút `💾 Lưu lịch trình` (lưu vào tài khoản/thiết bị).
2. Nút `📤 Chia sẻ cho bạn đi cùng` (tạo liên kết chia sẻ nhóm).
3. Nút `📞 Xác nhận lịch trình này` (gửi liên hệ dịch vụ).

---

## 2. Định nghĩa Active User

> **Active User:** Một người dùng được tính là hoạt động trong một chu kỳ lập kế hoạch chuyến đi (Planning Cycle) khi họ thực hiện tạo chặng đi, chọn phương án, chỉnh sửa lịch và lưu hoặc chia sẻ ít nhất một lịch trình Ninh Bình trong vòng **7 ngày trước chuyến đi**.

Các trường hợp **không** được tính là Active User để tránh chỉ số ảo:
* Chỉ tải trang rồi đóng ngay lập tức.
* Xem màn hình Onboarding Capability giới thiệu nhưng không nhập dữ liệu.
* Nhập dữ liệu và nhấn tạo lịch nháp nhưng thoát ra ngay lập tức mà không xem chi tiết chặng hay thực hiện lưu/chia sẻ.

---

## 3. Chỉ số Giữ chân chính: 7-day Planning Return Rate

Do lên kế hoạch du lịch Ninh Bình tự túc 1 ngày là nhu cầu diễn ra dồn dập trong khoảng thời gian ngắn ngay trước chuyến đi (thảo luận chặng, xem thời tiết, điều chỉnh chi phí ăn uống), NiBiGo sử dụng chỉ số giữ chân 7 ngày để theo dõi sát hành vi này:

$$7\text{-day Planning Return Rate} = \frac{\text{Số user quay lại và thực hiện Planning Action trong 7 ngày}}{\text{Tổng số user đã tạo Itinerary Draft đầu tiên}} \times 100\%$$

* **Planning Action** bao gồm: xem lại lịch trình đã lưu, chỉnh sửa đổi điểm đi, cập nhật ngân sách hoặc chia sẻ lại liên kết.
* **Thời gian 7 ngày:** Phản ánh chu kỳ vàng từ lúc bắt đầu chuẩn bị đến ngày khởi hành thực tế.

---

## 4. Các chỉ số phụ trợ (Proxy Metrics)

Để tối ưu hóa phễu chuyển đổi dẫn tới Core Action, NiBiGo theo dõi thêm 4 chỉ số hỗ trợ:

| Chỉ số phụ | Cách tính toán | Ý nghĩa giám sát |
|:---|:---|:---|
| **Draft-to-Save Rate** | Lượt lưu lịch / Số lượt xem bản nháp | Đo lường chất lượng nội dung lịch trình AI tạo ra. |
| **Option Selection Rate** | Lượt chọn option / Lượt tạo 3 phương án | Đánh giá mức độ rõ ràng của việc phân chia các gói dịch vụ. |
| **Time-to-Value (TTV)** | Số giây từ lúc mở app đến khi hiện 3 option | Đo tốc độ phản hồi của hệ thống, giảm thiểu sự nản lòng. |
| **Revision Completion Rate** | Lượt lưu sau sửa / Lượt kích hoạt chỉnh sửa | Đánh giá hiệu quả của luồng khôi phục lỗi (Recovery). |

---

## 5. Present Note
> **Present Note (Dành cho thuyết trình):**
> "Thưa hội đồng, chúng em không sử dụng DAU/WAU hay D1 Retention vì không ai lên kế hoạch đi chơi mỗi ngày. Thay vào đó, chúng em định nghĩa Core Action là hành động Lưu hoặc Chia sẻ lịch trình Ninh Bình 1 ngày sau khi đã qua hiệu chỉnh khả thi. Chỉ số giữ chân chính của chúng em là 7-day Planning Return Rate. Chỉ số này phản ánh chính xác chu kỳ lập kế hoạch 7 ngày của khách du lịch cuối tuần từ Hà Nội, giúp đo lường trực quan giá trị thực tế ứng dụng chuyển giao."
