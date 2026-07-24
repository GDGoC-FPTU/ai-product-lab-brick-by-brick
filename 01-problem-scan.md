### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 | Xanh SM| Pain từ người khác| Phân tích tự động ghi âm/chat lý do khách hủy cuốc & phàn nàn tài xế (Mất 12-15% cuốc/ngày; ngốn 450tr VNĐ/tháng CSKH thủ công)|
| 2 | VinFast| Lặp lại| So khớp dữ liệu sạc điện hằng tuần & phát hiện bất thường hóa đơn trụ sạc đối tác (Tốn 150-200 giờ kế toán/tháng; rò rỉ 2-3% tiền sạc).|
| 3 | Vinhomes| Tốn thời gian| Phân loại & tự động gán ticket phản ánh/khiếu nại cư dân trên App Vinhomes Resident (Mất 45-60 phút/ticket ban đầu; trễ SLA 22%).|
| 4 | Vinmec| Tốn thời gian| Soạn thảo tóm tắt hồ sơ xuất viện (Discharge Summary) tự động từ EMR cho bác sĩ duyệt (Tốn 15-20 phút/bệnh nhân; lãng phí 1.200 giờ bác sĩ/tháng).|
| 5 | VinFast| AI-upgrade| Trợ lý AI chẩn đoán mã lỗi kỹ thuật ban đầu từ mô tả tiếng Việt của chủ xe (Tốn 10-15 phút/lượt; nghẽn 25% cuộc gọi tổng đài giờ cao điểm).|

---

```
┌────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                          │
│                                                                │
│ Bài toán: So khớp dữ liệu sạc điện hằng tuần từ trạm sạc       │
│ đối tác liên kết với hệ thống tài chính VinFast.               │
│ Công ty thành viên: [x] VinFast                                │
│                                                                │
│ Ai đang đau? Kế toán viên (quá tải), Phòng Tài chính (rò rỉ)   │
│                                                                │
│ Workflow thủ công hiện tại (4 bước):                           │
│   1. Nhận file log sạc (Excel/CSV) từ các trạm sạc đối tác     │
│   → 2. Đối chiếu tay từng dòng giao dịch với telemetry VinFast │
│   → 3. Lọc ra các dòng sai lệch (lệch kWh, lệch đơn giá)       │
│   → 4. Lập biên bản giải trình & gửi yêu cầu điều chỉnh        │
│                                                                │
│ Bước nào tốn nhất? Bước 2 & 3 (⏱ 150-200 giờ/tháng)            │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Bước 2 & 3               │
│ (Trích xuất file log -> Auto-match -> Phát hiện sai lệch)      │
│                                                                │
│ Đo thành công bằng gì (Metric có số)?                          │
│ 1. Giảm 80% thời gian đối chiếu thủ công (từ 200h ──> 40h).    │
│ 2. Giảm thất thoát doanh thu do phát hiện sai lệch từ 3% ──> 0%│
│                                                                │
│ Quick Architecture: [x] LLM Feature (Data Anomaly Extract)     │
└────────────────────────────────────────────────────────────────┘
```