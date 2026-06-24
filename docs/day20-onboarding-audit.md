# Onboarding Audit — NiBiGo AI Trip Planner
**Học viên:** Đặng Trần Đạt - 2A202600662 · Nguyễn Hoàng Dương - 2A202600849 · Cao Văn Hảo - 2A202600874 · Nguyễn Quang Hòa - 2A202600986

Tài liệu này đánh giá chi tiết từng màn hình trong luồng onboarding của Prototype Day 18, xác định các điểm ma sát (Friction) làm giảm tỷ lệ chuyển đổi, và đưa ra quyết định cải tiến cho luồng Day 20 tối ưu.

---

## 1. Bảng Audit Chi Tiết phễu Onboarding

| Bước | Màn hình | Trải nghiệm hiện tại (Day 18) | Điểm ma sát (Friction) xác định | Quyết định (D20) | Lý do và Phương án cải tiến chi tiết |
|:---:|:---|:---|:---|:---:|:---|
| **1** | **AI Onboarding** | Giới thiệu khả năng AI (Act / Ask / Don't Act) qua các cột văn bản dài. | Người dùng có xu hướng lướt qua nhanh, không muốn đọc nhiều chữ trước khi được dùng sản phẩm. | **Simplify** | Rút ngắn văn bản giới thiệu chỉ còn các gạch đầu dòng trực quan. Thêm nút bấm trực tiếp "Bắt đầu lập lịch" để đi tiếp. |
| **2** | **Trip Input** | Biểu mẫu điền thông tin dài gồm **7 trường** (ngày đi, số người, xuất phát, ngân sách, nhịp đi, sở thích, ghi chú). | Rào cản lớn nhất. Điền quá nhiều trường làm tăng tỷ lệ thoát (drop-off) ngay từ đầu. | **Simplify** | Giảm số trường đầu vào xuống còn **5 trường** cốt lõi. Sử dụng các nút bấm chọn nhanh (Quick chips) thay vì ô nhập tự do. |
| **3** | **AI Draft** | Tạo và hiển thị 1 bản nháp lịch trình duy nhất. | Ép buộc người dùng vào 1 phương án duy nhất, họ phải tự đánh giá xem có phù hợp túi tiền hay không. | **Modify** | AI tạo ngay **3 phương án** (Tiết kiệm, Cân bằng, Trải nghiệm) kèm so sánh chi phí/độ mệt để user dễ lựa chọn. |
| **4** | **Evidence** | Màn hình riêng giải thích dữ kiện, giả định và cảnh báo an toàn của AI. | Tách rời 1 màn hình làm gián đoạn luồng chính, buộc người dùng đọc thông tin kỹ thuật không cần thiết. | **Delay** | Ẩn thông tin giả định vào ngăn kéo "Xem chi tiết & kiểm soát →" nằm trực tiếp trong màn hình Bản nháp, chỉ mở ra khi user click. |
| **5** | **Ask State** | AI hỏi về phương tiện di chuyển sau khi đã dựng xong bản nháp 6 chặng. | Hỏi phương tiện quá muộn. Nếu phương tiện thay đổi, AI buộc phải tính toán lại lịch chặng từ đầu gây phiền phức. | **Move Up** | Di chuyển việc lựa chọn phương tiện di chuyển lên **trước khi** AI tạo ra 3 bản nháp lịch trình. |
| **6** | **Recovery** | Điều chỉnh lịch trình khi người dùng nhấn "Lịch quá dày/quá mệt". | Tách rời một bước phụ làm kéo dài thời gian đến Core Action. | **Simplify** | Tích hợp nút điều chỉnh nhanh "Tối ưu lại nhẹ hơn" ngay tại bước xem chi tiết lịch trình. |
| **7** | **Uncertainty** | User chọn cách xử lý khi dữ liệu giờ mở cửa/thời tiết chưa chắc chắn. | Tách riêng một màn hình gây mệt mỏi và phân tâm nhận thức. | **Delay** | Tích hợp các cảnh báo dữ liệu inline trực tiếp ở vị trí các chặng (ví dụ: cảnh báo thời tiết/giá vé ngay dưới chặng leo Hang Múa). |
| **8** | **Feedback Loop** | Chọn lý do phản hồi lịch trình chưa phù hợp. | Màn hình khảo sát riêng gây đứt mạch lưu lịch trình cuối. | **Simplify** | Lồng ghép widget khảo sát ý kiến siêu ngắn ngay trong màn hình chốt cuối cùng (Review Screen). |
| **9** | **Final Review** | Xem lại lịch trình hoàn chỉnh và nhấn nút Lưu. | Điểm kích hoạt Core Action, cần làm nổi bật. | **Keep** | Giữ lại và tập trung toàn bộ sự chú ý của người dùng vào 2 nút hành động lớn: Lưu lịch trình và Chia sẻ. |

---

## 2. Kết quả so sánh Phễu chuyển đổi (Onboarding Funnel)

Sau khi tiến hành kiểm toán và cải tiến, luồng phễu được rút ngắn đáng kể:
* **Day 18:** 9 màn hình riêng biệt → Thời gian chạm Core Action ước tính từ **8 - 10 phút** (Friction rất cao).
* **Day 20:** 7 bước tích hợp trong một màn hình di động → Thời gian chạm Core Action giảm xuống còn **3 - 4 phút** (Tối ưu hóa phễu, giảm 60% thời gian trễ nhận giá trị).

---

## 3. Present Note
> **Present Note (Dành cho thuyết trình):**
> "Thưa mentor, kết quả kiểm toán phễu Onboarding Audit chỉ ra 3 lỗi thiết kế ma sát lớn ở Day 18: Một là biểu mẫu nhập quá dài (7 trường), hai là hỏi phương tiện (Ask State) quá muộn sau khi tạo bản nháp, và ba là tách riêng các màn hình kỹ thuật như Evidence hay Uncertainty. Ở Day 20, chúng em đã quyết định đơn giản hóa (Simplify) biểu mẫu thành 5 trường chọn nhanh, dời Ask State lên trước và tích hợp các cảnh báo an toàn inline trực tiếp tại chặng đi. Việc này giúp cắt giảm phễu từ 9 bước xuống còn 7 bước tối giản, tăng trải nghiệm mượt mà cho khách hàng."
