# 01 - Problem Scan & Quick Cards

## Thông tin cá nhân

- Họ và tên: Nguyen Hoang Khoi
- MSSV: 2A202601383
- Nhóm: Brick by brick

---

## Phase 1 - SCAN: Tìm kiếm cơ hội

Hãy sử dụng 4 lenses để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại ít nhất 5 bài toán/bottleneck thực tế.

### List bài toán của tôi

| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|---------------------------------|------|---------------------|
| 1 | Vinhomes | Lặp lại | Phân loại khiếu nại cư dân và chuyển đến đúng bộ phận xử lý. |
| 2 | VinFast | Tốn thời gian | Tổng hợp phản hồi bảo hành từ nhiều đại lý để tạo báo cáo lỗi. |
| 3 | Vinpearl | AI-upgrade | Phân tích review khách sạn để phát hiện vấn đề dịch vụ. |
| 4 | Vinmec | Tốn thời gian | Soạn tóm tắt hồ sơ xuất viện từ bệnh án điện tử. |
| 5 | Xanh SM | Pain từ người khác | Phân tích nguyên nhân khách hủy chuyến từ ghi âm cuộc gọi. |

---

## Phase 2 - QUICK-ASSESS: 3 Quick Problem Cards

Chọn top 3 từ danh sách SCAN:
**#1 (Vinhomes), #2 (VinFast), #3 (Vinpearl).**

---

## Thẻ bài toán tiêu biểu: Card #1 - Vinhomes phân loại khiếu nại cư dân

```text
QUICK PROBLEM CARD #1

Bài toán:
Tự động phân loại khiếu nại của cư dân và chuyển đến đúng bộ phận xử lý.

Công ty thành viên:
[ ] VinFast   [ ] Xanh SM   [x] Vinhomes   [ ] Vinmec   [ ] Khác

Ai đang đau?

- Cư dân.
- Nhân viên CSKH.
- Ban quản lý tòa nhà.

Workflow thủ công hiện tại (4 bước):

-> 1. Cư dân gửi phản ánh qua ứng dụng Vinhomes Resident
-> 2. Nhân viên CSKH đọc toàn bộ nội dung phản ánh
-> 3. Xác định loại sự cố và bộ phận phụ trách
-> 4. Chuyển ticket đến đúng bộ phận

Bước nào tốn thời gian/lỗi nhất?

Bước 2-3 (~6 phút/ticket)

AI có thể nhảy vào hỗ trợ bước nào?

Đọc nội dung phản ánh, phân loại tự động và gợi ý bộ phận xử lý.

Đo thành công bằng gì (Metric)?

- Giảm thời gian phân loại từ 6 phút xuống dưới 1 phút.
- Tăng độ chính xác phân loại lên trên 95%.

Quick Architecture:

[ ] No AI   [ ] Rule   [x] LLM   [ ] Agent

LLM đọc nội dung phản ánh và đề xuất loại sự cố + bộ phận xử lý.
```

---

## Thẻ bài toán tiêu biểu: Card #2 - VinFast tổng hợp báo cáo bảo hành

```text
QUICK PROBLEM CARD #2

Bài toán:
Tự động tổng hợp phản hồi bảo hành từ nhiều đại lý để tạo báo cáo lỗi phổ biến.

Công ty thành viên:
[x] VinFast   [ ] Xanh SM   [ ] Vinhomes   [ ] Vinmec   [ ] Khác

Ai đang đau?

- Nhân viên bảo hành.
- Kỹ sư chất lượng.
- Quản lý dịch vụ.

Workflow thủ công hiện tại (4 bước):

-> 1. Thu thập phản hồi từ các đại lý
-> 2. Đọc từng báo cáo
-> 3. Phân nhóm các lỗi giống nhau
-> 4. Viết báo cáo tổng hợp

Bước nào tốn thời gian/lỗi nhất?

Bước 2-4 (~20 phút/lượt)

AI có thể nhảy vào hỗ trợ bước nào?

Đọc, tóm tắt và gom nhóm các lỗi giống nhau.

Đo thành công bằng gì (Metric)?

- Giảm thời gian tạo báo cáo từ 20 phút xuống dưới 5 phút.
- Giảm lỗi bỏ sót vấn đề phổ biến.

Quick Architecture:

[ ] No AI   [ ] Rule   [x] LLM   [ ] Agent

LLM đọc báo cáo, tóm tắt và gom nhóm lỗi theo chủ đề.
```

---

## Thẻ bài toán tiêu biểu: Card #3 - Vinpearl phân tích review khách sạn

```text
QUICK PROBLEM CARD #3

Bài toán:
Phân tích đánh giá khách hàng để phát hiện các vấn đề dịch vụ nổi bật.

Công ty thành viên:
[ ] VinFast   [ ] Xanh SM   [ ] Vinhomes   [ ] Vinmec   [x] Khác (Vinpearl)

Ai đang đau?

- Quản lý khách sạn.
- Bộ phận CSKH.

Workflow thủ công hiện tại (4 bước):

-> 1. Thu thập review từ Booking, Agoda và Google
-> 2. Đọc từng đánh giá
-> 3. Phân loại theo từng chủ đề
-> 4. Tổng hợp các vấn đề nổi bật

Bước nào tốn thời gian/lỗi nhất?

Bước 2-4 (~15 phút/lượt)

AI có thể nhảy vào hỗ trợ bước nào?

Phân tích cảm xúc, phân loại chủ đề và tóm tắt các vấn đề nổi bật.

Đo thành công bằng gì (Metric)?

- Giảm thời gian tổng hợp từ 15 phút xuống dưới 3 phút.
- Phát hiện trên 95% các chủ đề được khách phản ánh.

Quick Architecture:

[ ] No AI   [ ] Rule   [x] LLM   [ ] Agent

LLM phân tích review, phân loại chủ đề và sinh báo cáo tóm tắt.
```