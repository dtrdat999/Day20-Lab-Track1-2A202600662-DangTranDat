# Demo Path & Presentation Script (8 Mins) — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

Kịch bản thuyết trình chi tiết chia theo thời gian biểu để tối ưu hóa hiệu quả báo cáo trước Mentor hoặc Hội đồng chấm điểm.

---

## 1. Thời gian biểu thuyết trình 8 phút

| Thời gian | Nội dung thuyết trình chính | Thao tác hiển thị trên màn hình |
|:---:|:---|:---|
| **0:00 - 0:45** | **Giới thiệu sản phẩm:** Tên dự án NiBiGo AI, Use Case cốt lõi (Ninh Bình 1 ngày tự túc), Định vị phạm vi MVP và lộ trình mở rộng lên 2 ngày 1 đêm (2D1N). | Mở **Section 00** (Cover/Positioning) trên trang trình chiếu. Chỉ rõ định hướng thiết kế tinh gọn của nhóm. |
| **0:45 - 1:30** | **Hành vi tự nhiên & Retention Canvas:** Phân tích tần suất đi du lịch Ninh Bình nội địa (2-4 lần/năm). Định nghĩa Problem, Persona và loại bỏ Anti-persona để chống phình to scope. | Mở **Section 03** (Retention Canvas). Giải thích tại sao ứng dụng không cố tạo thói quen mở app hằng ngày (daily). |
| **1:30 - 2:15** | **Kiểm toán Onboarding (Audit):** Trình bày các điểm ma sát của luồng 9 bước cũ (form nhập quá dài, Evidence ngắt quãng). Thuyết minh logic cải tiến luồng 7 bước mới gọn nhẹ hơn. | Chuyển sang **Section 06** (Onboarding Audit) và giới thiệu sơ đồ luồng 7 bước mới ở **Section 07**. |
| **2:15 - 3:30** | **Demo tương tác - Lập lịch nhanh:** Thao tác trên thiết bị di động giả lập. Nhập 5 thông số cơ bản → AI lập tức hiển thị 3 phương án gợi ý so sánh chi phí/độ mệt (Aha Moment). | Mở **Section 08** (Prototype Scenario). Nhấp chọn các trường trên điện thoại đến bước hiển thị 3 options. |
| **3:30 - 4:30** | **Demo đánh giá khả thi & Luồng khôi phục:** Trình diễn cách AI phát hiện rủi ro leo núi Hang Múa lúc nắng nóng gay gắt, cảnh báo inline và đưa ra gợi ý khôi phục tối ưu lại lịch trình nhẹ hơn. | Nhấp chọn "Option 2: Cân bằng" trên điện thoại -> xem Cảnh báo khả thi -> Nhấn "Tối ưu lại nhẹ hơn" để xem lịch trình mới đã được AI sửa. |
| **4:30 - 5:30** | **Ghi nhận Core Action:** User thực hiện Lưu lịch trình, Chia sẻ cho bạn bè đi cùng để chốt chuyến đi, lồng ghép khảo sát đánh giá nhanh tại màn cuối. | Nhấn nút "Lưu lịch trình" hoặc "Chia sẻ" trên điện thoại giả lập. Hiển thị thông báo Core Action kích hoạt thành công. |
| **5:30 - 6:30** | **Chỉ số đo lường hiệu quả (Metrics):** Giới thiệu North Star Metric ("Useful Itineraries Saved/Shared per Month"), sơ đồ Measurement Ladder và phân tích sự đánh đổi (Trade-offs). | Chuyển sang **Section 11 & 12**. Trình bày cây chỉ số phân cấp từ lượng truy cập đến giá trị doanh nghiệp. |
| **6:30 - 7:20** | **Nature vs Nurture & Vòng lặp Hook:** Giải thích cơ chế gửi thông báo đẩy trước chuyến đi 3 ngày dựa trên thời tiết, và vòng lặp Hook Model per-trip kích thích người dùng chia sẻ lịch. | Mở **Section 13 & 14**. Chỉ rõ NiBiGo không spam thông báo để xây dựng lòng tin lâu dài. |
| **7:20 - 8:00** | **Roadmap 2D1N & Kết luận:** Tóm tắt lộ trình mở rộng quy mô dịch vụ lưu trú homestay Ninh Bình và kết thúc buổi thuyết trình. | Mở **Section 16**. Sẵn sàng trả lời các câu hỏi phản biện từ Mentor. |

---

## 2. Kịch Bản Chi Tiết Cho Người Thuyết Trình (Script)

### Mở đầu (0:00 - 0:45)
*"Kính chào mentor và các bạn. Nhóm chúng em xin trình bày giải pháp nâng cấp ứng dụng NiBiGo AI Trip Planner. Nhận diện việc lập kế hoạch du lịch là hành vi có tần suất tự nhiên rất thấp, NiBiGo Day 20 được thiết kế lại toàn bộ luồng onboarding nhằm hướng người dùng tới giá trị sử dụng thực sự nhanh nhất có thể. MVP của chúng em tập trung trọn vẹn vào lịch trình Ninh Bình 1 ngày tự túc xuất phát từ Hà Nội."*

### Phân tích hành vi & Kiểm toán (0:45 - 2:15)
*"Qua việc khảo sát hành vi trên bản thiết kế Day 18, chúng em phát hiện biểu mẫu nhập nhu cầu quá dài (7 trường) làm người dùng nản lòng. Việc bắt người dùng đi qua 9 bước riêng biệt trước khi lưu lịch là quá rườm rà. Do đó, trong Day 20, chúng em cắt giảm phễu còn 7 bước: chuyển đổi ô nhập liệu thành các thẻ chọn nhanh, và di chuyển câu hỏi về phương tiện (Ask State) lên trước để đảm bảo AI tính toán đúng ngay từ đầu."*

### Demo tương tác (2:15 - 5:30)
*(Thao tác trên simulator điện thoại)*
*"Bây giờ, xin mời quý hội đồng xem bản mô phỏng di động thực tế. Khi người dùng chỉ cần chọn nhanh nhóm 2 người, ngân sách tầm trung, AI sẽ lập tức đưa ra 3 phương án: Tiết kiệm, Cân bằng và Trải nghiệm tốt với các trade-off chi phí rõ ràng. Đây chính là Aha Moment. Khi người dùng chọn phương án Cân bằng, AI lập tức chạy tính năng Feasibility Check và cảnh báo inline rằng leo Hang Múa lúc 2h chiều sẽ cực kỳ nắng nóng, kèm nút khôi phục lỗi. Khi bấm 'Tối ưu lại nhẹ hơn', AI điều chỉnh dời Hang Múa sang chiều mát mẻ và thêm 30 phút nghỉ trưa. Người dùng cảm thấy an tâm và thực hiện Core Action: bấm 'Lưu lịch trình' hoặc 'Chia sẻ cho bạn đi cùng'."*

### Chỉ số & Kết luận (5:30 - 8:00)
*"Để theo dõi hiệu năng, chúng em sử dụng North Star Metric là 'Số lịch trình hữu ích được lưu hoặc chia sẻ hàng tháng' thông qua cây chỉ số Measurement Ladder. Về mặt nuôi dưỡng (Nurture), NiBiGo chỉ can thiệp gửi nhắc nhở thời tiết trước ngày đi 3 ngày. Roadmap tiếp theo sau khi chứng minh được giá trị sẽ là tích hợp Homestay cho lịch trình 2 ngày 1 đêm. Xin cảm ơn mentor đã lắng nghe."*

---

## 3. Present Note
> **Present Note (Dành cho thuyết trình):**
> "Kịch bản này đã được tối ưu hóa để phân bổ thời gian cân bằng. Nhóm thuyết trình cần phân công rõ: 1 bạn chuyên thao tác nhấp click trên điện thoại giả lập của màn hình `day20.html`, 1 bạn trình bày script. Việc phối hợp nhịp nhàng giữa lời nói và chuyển động trực quan trên giao diện demo sẽ giúp ghi điểm tuyệt đối trong mắt hội đồng chấm điểm."
