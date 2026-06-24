# Hook Model & Event Tracking Spec — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

Tài liệu này chi tiết hóa cơ chế tạo dựng hành vi lập kế hoạch của NiBiGo (Hook Model) và đặc tả kỹ thuật đo lường sự kiện (Event Tracking Specification) để thu thập chỉ số.

---

## 1. Thiết kế Hook Model cấp độ chuyến đi (per-trip)

Vì du lịch Ninh Bình là nhu cầu có tần suất thấp, chúng ta áp dụng vòng lặp Hook cho từng chuyến đi (per-trip hook loop):

* **Trigger (Kích tác):**
  * *Internal (Bên trong):* Cảm giác lo lắng chuyến đi chơi cuối tuần với gia đình gặp sự cố kẹt xe, trễ giờ ăn uống, mệt mỏi thể lực hoặc phát sinh chi phí.
  * *External (Bên ngoài):* Nhận được bài viết gợi ý mùa đẹp du lịch Tam Cốc, hoặc một đường link chia sẻ lịch trình Ninh Bình từ một người bạn.
* **Action (Hành động):** Mở ứng dụng, nhập nhanh 5 thông tin cơ bản và xem ngay 3 phương án gợi ý lịch trình khác biệt của AI chỉ trong 1 phút.
* **Variable Reward (Phần thưởng thay đổi):**
  * *The Hunt:* Khám phá các địa điểm tham quan đẹp, quán ngon đặc sản dê với chi phí tối ưu.
  * *The Self:* Cảm giác nhẹ nhõm, an tâm khi chốt được lịch trình khả thi mà không mất công tra cứu nhiều nguồn.
  * *The Tribe:* Nhận được sự đồng tình của nhóm bạn đi cùng khi chia sẻ lịch trình lên Zalo chat.
* **Investment (Sự đầu tư):** Người dùng bỏ công sức lưu chặng đi vào danh sách yêu thích, chỉnh sửa tối ưu lại lịch trình nhẹ hơn, hoặc gửi thông tin liên hệ dịch vụ vận chuyển.

> **Hook Statement:** "Mỗi khi user muốn đi Ninh Bình nhưng chưa có kế hoạch rõ, họ sẽ mở NiBiGo để nhận ngay 3 phương án lịch trình, chọn phương án phù hợp và lưu/chia sẻ kế hoạch với bạn đồng hành."

---

## 2. Đặc tả sự kiện theo dõi (Event Tracking Specification)

| Event Name | Điều kiện ghi nhận sự kiện | Properties (Thuộc tính thu thập) | Metric liên quan | Quy tắc chống trùng dữ liệu (Anti-duplication) |
|:---|:---|:---|:---|:---|
| `onboarding_started` | User mở trang web và tải thành công màn hình khởi động. | `session_id`, `device_type`, `source_referral`, `timestamp` | Completion Rate, TFS | Chỉ ghi nhận tối đa 1 lần trong mỗi phiên truy cập (session). |
| `trip_input_submitted` | User điền xong 5 thông số và nhấp nút "Xem 3 phương án". | `group_size`, `budget_range`, `preferences`, `mobility_level` | Completion Rate, TTV | Khóa nút gửi 1.5 giây sau khi nhấn để chặn sự kiện gửi đúp (double click). |
| `itinerary_options_generated` | 3 phương án lịch trình hiện ra đầy đủ trên màn hình. | `generation_time_ms`, `options_count` | Time-to-Value (TTV) | Chỉ ghi nhận khi giao diện vẽ xong 3 thẻ phương án thành công. |
| `option_selected` | User click chọn vào 1 trong 3 phương án. | `option_type` (saving/balanced/premium), `estimated_cost` | Option Selection Rate | Không ghi đè nếu click lại nhiều lần vào cùng một phương án đã chọn. |
| `feasibility_warning_viewed` | Banner cảnh báo khả thi (quá mệt/vượt chi phí) xuất hiện. | `warning_type` (fatigue/budget), `severity` (high/medium) | Warning Interaction Rate | Chỉ ghi nhận 1 lần per session khi thẻ cảnh báo được hiển thị trong DOM. |
| `itinerary_revised` | User bấm nút khôi phục lỗi để tối ưu chặng đi nhẹ hơn. | `revision_type` (mobility_adjustment), `stops_removed` | Revision Completion Rate | Ghi nhận khi lịch trình mới đã được AI vẽ lại hoàn chỉnh trên giao diện. |
| `itinerary_saved` | User bấm Lưu lịch trình ở màn hình cuối (**Core Action**). | `itinerary_id`, `option_type`, `final_cost`, `adjustment_count` | North Star Metric, TFS | Sử dụng khoá chống trùng: `session_id` + `timestamp` làm tròn 10 giây. |
| `itinerary_shared` | User nhấp nút Chia sẻ liên kết cho bạn đồng hành. | `itinerary_id`, `share_channel` (zalo/messenger) | North Star Metric, Share Rate | Chặn gửi sự kiện trùng trong vòng 60 giây nếu nhấn liên tục. |

---

## 3. Tiêu chí nghiệm thu hệ thống Đo lường (Acceptance Criteria)

1. **Tính chính xác của Core Action:** Sự kiện `itinerary_saved` chỉ được phép gửi khi người dùng thực hiện nhấn nút lưu thực tế thành công, không tính các lượt xem màn review mà chưa nhấn nút.
2. **Không trùng lặp:** Mọi sự kiện gửi về server lưu trữ phải có mã khóa chống trùng (Idempotency Key) tạo từ `session_id` và `timestamp` để loại bỏ dữ liệu ảo khi người dùng tải lại trang (reload).
3. **Đầy đủ thuộc tính bắt buộc:** Mọi sự kiện bắt buộc phải truyền kèm `session_id`, `user_id` (nếu có), và `timestamp` định dạng chuẩn ISO 8601.
4. **Không thu thập dữ liệu nhạy cảm:** Tuyệt đối không gửi các thông tin định danh cá nhân trực tiếp (họ tên, số điện thoại, vị trí GPS chính xác) lên hệ thống đo lường hành vi để đảm bảo quyền riêng tư.

---

## 4. Present Note
> **Present Note (Dành cho thuyết trình):**
> "Thưa hội đồng, thiết kế Hook Model của NiBiGo tập trung vào việc tạo thói quen theo chuyến đi (per-trip). Để chứng minh hiệu quả của vòng lặp Hook, bảng Event Tracking đặc tả 8 sự kiện cốt lõi từ lúc bắt đầu nhập form cho đến khi thực hiện Core Action là Lưu hoặc Chia sẻ. Chúng em áp dụng các quy tắc chống trùng nghiêm ngặt như Idempotency Key để đảm bảo dữ liệu ghi nhận luôn sạch và chính xác trước khi đưa vào phân tích tỷ lệ giữ chân."
