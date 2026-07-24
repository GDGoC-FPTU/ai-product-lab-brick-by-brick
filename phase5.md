# 🏁 Phase 5 — EVALUATE: Vinhomes Intelligent Resident Ticket Router

> **Dự án:** Tự động hóa phân loại, đánh giá độ khẩn cấp và điều hướng phản ánh cư dân trên App Vinhomes Resident  
> **Đơn vị phát triển:** Vin Smart Future (Vingroup)  
> **Công ty thành viên thụ hưởng:** Vinhomes (Khối Vận hành & Ban Quản lý Đại đô thị)

---

## 5.1. AI Readiness Checklist (Đánh giá mức độ sẵn sàng triển khai AI)

| # | Tiêu chí đánh giá | Trạng thái | Chi tiết bằng chứng & Hiện trạng |
|---|-------------------|:----------:|-----------------------------------|
| **1** | **Dữ liệu mẫu & Logs sạch (Clean Data)** | ✅ **ĐẠT** | Đã thu thập và làm sạch log lịch sử của **10.000+ ticket phản ánh** từ App Vinhomes Resident trong 6 tháng gần nhất tại Vinhomes Ocean Park 1. Dữ liệu đã được gán nhãn chuẩn theo 4 danh mục chính (Kỹ thuật, Vệ sinh, An ninh, Ban Quản lý). |
| **2** | **Kiểm soát rủi ro khi AI sai (Risk Containment)** | ✅ **ĐẠT** | Rủi ro được cô lập hoàn toàn nhờ mô hình **Human-in-the-Loop (Lễ tân 1-Click Duyệt)**. Mọi đề xuất của AI đều ở dạng nháp (`DRAFT_ONLY`), không tự phát hành tin nhắn hay gán ticket tự động nếu chưa có sự phê duyệt của con người. |
| **3** | **Cơ chế dự phòng (Fallback Mechanism)** | ✅ **ĐẠT** | Khi điểm tin cậy (Confidence Score) của LLM < 80% hoặc hệ thống gặp sự cố kết nối API, ticket tự động đẩy về luồng tiếp nhận thủ công truyền thống của Lễ tân mà không gián đoạn vận hành. |
| **4** | **Sự sẵn sàng của Stakeholders (Sponsorship)** | ✅ **ĐẠT** | Ban Quản lý Đại đô thị và Đội ngũ Lễ tân sảnh hoàn toàn ủng hộ dự án vì giúp họ giảm **80% khối lượng thao tác gõ máy**, cho phép tập trung nâng cao trải nghiệm đón khách trực tiếp. |

---

## 5.2. Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future

- [x] **GO (Bắt đầu xây dựng Prototype & Triển khai Pilot):** Bắt đầu phát triển với scope hẹp tại 1 phân khu đại đô thị.
- [ ] **NOT YET (Cần tích lũy thêm dữ liệu / xác lập baseline):** Trì hoãn để chuẩn bị thêm.
- [ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

---

## 5.3. Justification (Lý giải quyết định dựa trên Bằng chứng Kỹ thuật & Chi phí)

### 📊 1. Hiệu quả kinh tế & ROI (Return on Investment)
* **Tiết kiệm thời gian vận hành:** Giảm tổng thời gian tiếp nhận và gán ticket từ **45-60 phút xuống dưới 1 phút/ticket** (giảm 98% thời gian chờ).
* **Cải thiện chỉ số SLA & CSAT:** Giảm tỷ lệ trễ SLA phản hồi từ **22% xuống dưới 2%**, kỳ vọng nâng chỉ số hài lòng cư dân (CSAT) từ **78% lên trên 92%**.
* **Chi phí vận hành tối ưu (OPEX):** Sử dụng mô hình **Gemini 2.5 Flash** với chi phí ước tính chỉ khoảng **~0,0005 USD/ticket** (~12 VNĐ/ticket). Tổng chi phí API cho 10.000 ticket/tháng chỉ khoảng **5 USD/tháng** (~120.000 VNĐ), cực kỳ rẻ so với giá trị tiết kiệm hàng trăm giờ làm việc của nhân sự.

### 🛡️ 2. Bằng chứng kiểm thử Ranh giới An toàn (Prompt Safety Verification)
* Kết quả chạy thực nghiệm programmatic stress-test tại Phase 4 ([starter-code/prompt_prototype.py](starter-code/prompt_prototype.py)) cho thấy mô hình đạt **100% tuân thủ ranh giới an toàn**:
  1. Luôn giữ thuộc tính nháp `status: "DRAFT_ONLY"` kể cả khi bị người dùng dụ dỗ bỏ qua bước duyệt.
  2. Tự động nhận diện chính xác các từ khóa rủi ro pháp lý/tài chính và chuyển tiếp cho `BAN_PHAP_LY` thay vì gán nhầm cho Kỹ thuật sảnh.

### ⚙️ 3. Phân định ranh giới giữa Rule-Based và AI (Hybrid Design)
* Nhóm đã tiếp thu toàn bộ phản biện khắt khe từ CFO & Trưởng phòng Vận hành tại Phase 2: Không lạm dụng LLM vào các tác vụ bảng số liệu cứng. Hệ thống ứng dụng mô hình **Hybrid**: Dùng Form danh mục cứng (Rule-based) ở giao diện App cư dân, và chỉ dùng LLM ở khâu **Đọc hiểu đoạn văn tự do + Trích xuất mức độ khẩn cấp (Urgency Analysis)**.

---

## 5.4. Lộ trình triển khai Pilot & Scaling (Implementation Roadmap)

```text
 ┌──────────────────────┐      ┌──────────────────────┐      ┌──────────────────────┐
 │  GIAI ĐOẠN 1 (4 Tuần) │      │  GIAI ĐOẠN 2 (6 Tuần) │      │  GIAI ĐOẠN 3 (8 Tuần) │
 │  PILOT SCOPE HẸP     │ ───► │  ĐÁNH GIÁ & TỐI ƯU   │ ───► │  SCALING TOÀN BỘ     │
 └──────────────────────┘      └──────────────────────┘      └──────────────────────┘
  • Triển khai thử nghiệm       • Đo lường CSAT thực tế       • Mở rộng cho 100%
    tại Phân khu Sapphire         và Tỷ lệ Lễ tân duyệt         các khu đô thị Vinhomes
    Vinhomes Ocean Park 1.        1-Click thành công.           toàn quốc.
  • Tối đa 500 ticket/ngày.     • Fine-tune Few-shot prompt   • Tích hợp hệ thống tổng
                                  dựa trên feedback thực tế.    đài AI thoại tự động.
```
