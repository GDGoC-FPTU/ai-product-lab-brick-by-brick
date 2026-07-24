### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Vinmec | Lặp lại | Y tá trực bàn tiếp khách phải tự điều phối bệnh nhân vào các phòng tương ứng, kiểm tra các phòng vắng hay bận |
| 2 | Xanh SM | Tốn thời gian | Điều phối viên phải trả lời những thắc mắc, yêu cầu có thể bị lặp lại của các tài xế xe 2 bánh về các trạm thay pin  |
| 3 | Vinhomes | AI-upgrade | Hệ thống CSKH Vinhomes nhận các ý kiến và phiếu bầu của các cư dân trong các kỳ bầu cử trưởng tổ dân phố. |
| 4 | VinFast | Lặp lại | Nhân viên kế toán hoàn thiện các đơn yêu cầu đăng ký thuê pin của các chủ xe 2 bánh theo các gói có sẵn |
| 5 | Vinhomes | Pain từ người khác | Cư dân bị mất, quên thẻ chung cư và không có cách nào lên, phải gọi BQL thủ công. |

---
```
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1 — từ bài toán #2                      │
│                                                             │
│ Bài toán: Điều phối viên Xanh SM phải thủ công trả lời      │
│ các thắc mắc lặp lại của tài xế xe 2 bánh về trạm thay pin. │
│ Công ty thành viên: [x] Xanh SM                 │
│                                                             │
│ Ai đang đau (Actor)?                                        │
│   Điều phối viên (bị gián đoạn liên tục), tài xế xe 2 bánh  │
│   (chờ trả lời, mất thời gian có thể đón khách).            │
│                                                             │
│ Workflow thủ công hiện tại (4 bước):                        │
│   1. Tài xế gọi/nhắn tin hỏi trạm thay pin gần nhất         │
│   ──> 2. Dispatch tra thủ công bản đồ trạm pin nội bộ       │
│   ──> 3. Dispatch trả lời từng tài xế qua App/điện thoại    │
│   ──> 4. Tài xế di chuyển (có thể hỏi lại nếu thông tin sai)│
│                                                             │
│ Bước nào tốn nhất? Bước 2–3 (⏱ 5–8 phút/lượt, ~40 lần/ngày)│
│ AI có thể nhảy vào ở bước nào?                              │
│   Bước 1–3: Chatbot AI tích hợp App tài xế tự động          │
│   tra cứu trạm thay pin còn slot gần nhất, trả lời tức thì. │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                        │
│   Giảm cuộc gọi tới Dispatch hỏi trạm pin từ ~40            │
│   xuống < 5 lượt/ngày. Thời gian tài xế nhận thông tin      │
│   từ 6 phút ──> dưới 30 giây.                               │
│                                                             │
│ Quick Architecture: [x] LLM │
└─────────────────────────────────────────────────────────────┘
```