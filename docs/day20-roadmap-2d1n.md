# Product Roadmap: Scaling from 1D to 2D1N — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

Tài liệu này trình bày tư duy chiến lược đằng sau việc khoanh vùng phạm vi MVP và lộ trình kỹ thuật chi tiết để mở rộng ứng dụng lên lịch trình 2 ngày 1 đêm (2D1N).

---

## 1. Tại sao bắt đầu với lát cắt Ninh Bình 1 Ngày?

Việc tập trung vào lịch trình du lịch tự túc Ninh Bình trong 1 ngày giúp giải quyết các rào cản nghiên cứu sản phẩm ban đầu:
* **Kiểm soát biến số dữ liệu:** Lịch 1 ngày không có biến số về lưu trú (chọn homestay hay khách sạn, giờ check-in/check-out). Điều này giúp thuật toán AI chỉ tập trung tối ưu hóa chặng di chuyển và ăn uống.
* **Thời gian Time-to-Value cực nhanh:** Người dùng nhận được đề xuất hoàn chỉnh tức thì, dễ dàng ra quyết định lưu trữ.
* **Thuận tiện cho việc Demo thuyết trình:** Một lịch trình 1 ngày với 5-6 chặng là độ dài hoàn hảo để trình bày toàn bộ tính năng và luồng tương tác của AI trong vòng 8 phút của bài báo cáo Lab.

---

## 2. Lộ trình mở rộng lên 2 Ngày 1 Đêm (2D1N Roadmap)

Sau khi core loop (lập lịch -> tối ưu khả thi -> lưu/chia sẻ) được chứng minh có tỷ lệ giữ chân tốt ở phân khúc 1 ngày, NiBiGo sẽ nâng cấp lên lịch trình 2 ngày 1 đêm với các bổ sung cốt lõi:

* **Tích hợp sở thích lưu trú (Accommodation Preference):** Bổ sung trường chọn loại hình lưu trú mong muốn (Resort sang trọng, Homestay chill view núi đồng lúa, hay Nhà nghỉ tiết kiệm gần trung tâm Tam Cốc).
* **Phân bổ chặng thông minh theo ngày:** AI tự động chia điểm đi hợp lý (Ngày 1: Chùa Bái Đính + Tràng An; Tối: dạo phố cổ Hoa Lư; Ngày 2: Hang Múa + Tuyệt Tình Cốc trước khi lên xe về Hà Nội).
* **Cơ chế Handoff sang đại lý du lịch:** Tích hợp nút kết nối nhanh gửi trực tiếp lịch trình đã lưu cho các đối tác homestay/nhà xe limousine tại Ninh Bình để nhận báo giá trọn gói ưu đãi.

---

## 3. Phân tích Rủi ro và Giải pháp phòng ngừa cho luồng 2 Ngày

Việc kéo dài thời lượng chuyến đi lên 2 ngày làm xuất hiện nhiều rủi ro biến động dữ liệu hơn:

| Rủi ro kỹ thuật phát sinh | Mức độ ảnh hưởng | Giải pháp thiết kế phòng ngừa của NiBiGo AI |
|:---|:---:|:---|
| **Lịch trình bị vỡ dây chuyền giữa các ngày** (Ví dụ: Ngày 1 trễ thuyền làm dồn chặng sang ngày 2 gây quá tải thể lực). | <span class="badge badge-danger">High</span> | Thiết lập **Buffer Time tự động 2 tiếng** nghỉ ngơi vào cuối ngày 1 và đầu ngày 2. AI tự động kiểm tra dự báo thời tiết của cả 2 ngày để đảo chặng trong nhà/ngoài trời linh hoạt. |
| **Giá phòng lưu trú biến động theo thời gian thực** (AI đề xuất giá cũ, lúc user đặt thực tế bị tăng giá gây mất lòng tin). | <span class="badge badge-warning">Medium</span> | AI chỉ hiển thị khoảng giá phòng ước tính trung bình kèm nhãn cảnh báo độ tin cậy. Tích hợp liên kết API trực tiếp của Booking.com/Agoda để user tự chốt phòng thực tế. |
| **Sự khó thống nhất ý kiến trong nhóm đi đông người** (Đi 2 ngày phát sinh nhiều lựa chọn ăn uống, điểm đi hơn). | <span class="badge badge-blue">Medium</span> | Bổ sung tính năng **Bình chọn nhóm (Group Voting)**. Link lịch trình chia sẻ cho phép bạn đồng hành thả tim chọn món ăn hoặc điểm check-in mong muốn trực tiếp. |

---

## 4. Các Chỉ số theo dõi mới (New Metrics)

Khi nâng cấp lên 2D1N, NiBiGo bổ sung thêm 3 chỉ số đo lường hiệu quả chuyển đổi kinh doanh:
1. **2D1N Itinerary Saved Rate:** Tỷ lệ người dùng lập lịch trình 2 ngày trên tổng số lượt sử dụng.
2. **Accommodation Click-through Rate:** % người dùng nhấp vào đề xuất Homestay liên kết.
3. **Zalo Lead Conversion Rate:** % người dùng gửi thông tin liên hệ dịch vụ chốt xe và phòng qua Zalo OA.

---

## 5. Present Note
> **Present Note (Dành cho thuyết trình):**
> "Thưa mentor, Roadmap mở rộng lên 2 ngày 1 đêm là bước đi chiến lược tiếp theo của NiBiGo. Bằng cách giới hạn MVP ở 1 ngày để chứng minh sự hữu dụng trước, chúng em giảm thiểu rủi ro kỹ thuật. Khi nâng cấp lên 2 ngày, thuật toán AI sẽ tích hợp thêm biến số lưu trú và phân bổ chặng nghỉ. Chúng em đã dự phòng sẵn các giải pháp như tự động đảo chặng theo thời tiết 2 ngày và cơ chế Group Voting để giải quyết các rủi ro phát sinh khi nhóm đi dài ngày, đảm bảo tính khả thi cao nhất cho người sử dụng."
