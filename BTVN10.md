# BTVN 10 (SESSION 21)
## Phần 1: Lập bảng So sánh Trade-off Toàn diện
### **1.** Lập bảng so sánh chi tiết giữa Phương án 1 (Hỗ trợ cảm tính) và Phương án 2 (Troubleshooting 4 Chẳng) dựa trên 4 tiêu chí cốt lõi:

| Tiêu chí đánh giá | Phương án 1: Hỗ trợ Cảm tính/Nhóm chat | Phương án 2: Troubleshooting 4 Chặng Chuẩn hóa |
| :--- | :--- | :--- |
| 1.Thời gian xử lý sự cố (Downtime) | Kéo dài — Phụ thuộc hoàn toàn vào việc Senior Dev có rảnh để đọc tin nhắn và trả lời hay không. | Rút ngắn 80% — Kỹ thuật viên tự giải quyết tại chỗ trong 5-10 phút đầu tiên. |
| 2.Áp lực & Chi phí cho Senior Devs | Rất cao — Bị phân tâm liên tục bởi các câu hỏi cơ bản lặp đi lặp lại, ảnh hưởng tiến độ phát triển tính năng mới. | Tối ưu — Senior chỉ tiếp nhận các ca lỗi thực sự phức tạp, đã có sẵn Phiếu Bug Report đầy đủ thông tin. |
| 3.Năng lực & Tính tự chủ của KTV | Thụ động — "Thợ bấm máy", sợ hãi thông báo lỗi tiếng Anh, thói quen ỷ lại, không tiến bộ nghề nghiệp. | Chủ động — Tư duy phân tích sắc bén, tự tin làm chủ trọn vẹn hệ thống máy tính tại trạm. |
| 4.Khả năng lưu vết tri thức (Knowledge Base) | Thất thoát — Tin nhắn trôi mất trên Zalo, người đi sau gặp lại lỗi cũ vẫn phải hỏi lại từ đầu. | Lưu trữ tập trung — Tích lũy tài liệu (Wiki/Knowledge Base) sửa lỗi nội bộ, dùng để đào tạo nhân sự mới. |

### **2.** Đưa ra kết luận lựa chọn: Vì sao Ban Giám đốc VoltCharge bắt buộc phải chọn Phương án 2 nếu muốn mở rộng quy mô lên 1,000 trạm sạc?

- **Lý do cốt lõi:** Phương án 1 không thể mở rộng. Không một công ty nào có thể thuê đủ lượng Senior Dev đắt đỏ chỉ để trực chat Zalo sửa lỗi vặt. Nếu cứ để 1 trạm sạc chết 1 tiếng mất 500.000 VNĐ vì chờ đợi Dev trả lời, công ty sẽ phá sản vì chi phí Downtime. Phương án 2 là con đường duy nhất để "nhân bản" năng lực vận hành, biến mỗi KTV thành một chốt chặn kỹ thuật độc lập.

## Phần 2:Thiết kế Sơ đồ Luồng Ra Quyết Định (Decision Flowchart)

### **3.** Vẽ sơ đồ (dưới dạng văn bản phân cấp hoặc ASCII/bước tuần tự) thể hiện Sơ đồ luồng ra quyết định gỡ lỗi khi Kiosk gặp sự cố:

#Chặng 1: Khi gặp Error Pop-up ➔ Bóc tách từ khóa gõ Google toán tử `site:`, \`\`, \`-\`.

-Hành động: Bóc tách từ khóa lỗi. Mở Google gõ toán tử: "mã lỗi chính xác" site:stackoverflow.com hoặc site:github.com -từ_khóa_không_liên_quan.

-Quyết định:

Có kết quả trả về? ➔ Đi tiếp Chặng 2.

Không có kết quả hoặc toàn tiếng Anh quá khó hiểu? ➔ Nhảy sang Chặng 3.

#Chặng 2: Nếu có kết quả StackOverflow/GitHub ➔ Áp dụng quy tắc đọc lướt 30s & kiểm tra Tích xanh `✓` / Upvote.

-Hành động: Đọc lướt trong 30 giây. Tìm các câu trả lời có Tích xanh (✓) hoặc Lượt Upvote cao nhất. Thử áp dụng cách khắc phục đó vào máy.

-Quyết định:

Máy chạy lại bình thường? ➔ KẾT THÚC (Sự cố được giải quyết).

Vẫn báo lỗi cũ hoặc không hiểu cách làm? ➔ Đi tiếp Chặng 3.

#Chặng 3: Nếu thông báo lỗi khó hiểu ➔ Gửi Prompt 3 thành phần cho Trợ lý AI để lấy giải thích tiếng Việt.

-Hành động: Gửi Prompt 3 thành phần chuẩn: [Ngữ cảnh đang làm gì] + [Copy nguyên văn mã lỗi] + [Yêu cầu giải thích tiếng Việt & 3 bước xử lý]. (Lưu ý che đi các mã API Key bảo mật).

-Quyết định:

Áp dụng 2 giải pháp AI gợi ý và thành công? ➔ KẾT THÚC (Sự cố được giải quyết).

Đã loay hoay quá 15 phút mà AI vẫn bó tay? ➔ Đi tiếp Chặng 4.

#Chặng 4: Nếu thử 2 giải pháp của AI vẫn thất bại sau 15 phút ➔ Điền phiếu Bug Report chuẩn 4 bước gửi về phòng IT Helpdesk.

-Hành động: Chấp nhận đây là lỗi lõi hệ thống. KTV tiến hành điền Phiếu Bug Report 4 bước chuẩn:

1.Tiêu đề lỗi ngắn gọn.

2.Các bước thao tác dẫn đến lỗi (Steps to reproduce).

3.Kết quả mong đợi vs. Thực tế xảy ra.

4.Đính kèm ảnh chụp màn hình / File Log gốc.

-Đích đến: Gửi Ticket này về hệ thống IT Helpdesk cho Senior Devs. Chuyển Kiosk sang chế độ "Bảo trì" để khách không nạp tiền oan.
