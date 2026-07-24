# 🏗️ Phase 3 — DEEP-DIVE: Vinhomes Intelligent Resident Ticket Router

> **Dự án:** Tự động hóa phân loại, đánh giá độ khẩn cấp và điều hướng phản ánh cư dân trên App Vinhomes Resident  
> **Đơn vị phát triển:** Vin Smart Future (Vingroup)  
> **Công ty thành viên thụ hưởng:** Vinhomes (Khối Vận hành & Ban Quản lý Đại đô thị)

---

## 3.1. Current-State Workflow Mapping (Quy trình thủ công hiện tại)

Dưới đây là sơ đồ chi tiết quy trình tiếp nhận, xử lý và điều hướng tin nhắn phản ánh của cư dân hiện tại tại Ban Quản lý Tòa nhà Vinhomes:

```text
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                                CURRENT-STATE WORKFLOW                                   │
└─────────────────────────────────────────────────────────────────────────────────────────┘

 ┌─────────────────┐
 │   CƯ DÂN        │
 └────────┬────────┘
          │ (1) Gửi phản ánh (Văn bản tự do / Ghi chú / Hình ảnh qua App Vinhomes Resident)
          ▼
 ┌─────────────────┐
 │ BƯỚC 1: NHẬN    │ ⏱ 2 phút/lượt
 │ TIN PHẢN ÁNH    │ 📥 Input: Raw Text, User ID, Căn hộ ID
 └────────┬────────┘ 📤 Output: Record phản ánh mới trên CRM
          │
          │ 🔄 Handoff 1: Hệ thống đẩy thông báo về màn hình Lễ tân sảnh tòa nhà
          ▼
 ┌─────────────────┐
 │ BƯỚC 2: ĐỌC &   │ ⏱ 15 phút/lượt 🔴 [BOTTLENECK 1]
 │ TỔNG HỢP TIN    │ 👤 Actor: Lễ tân sảnh (Thủ công)
 └────────┬────────┘ ⚠️ Lý do tắc nghẽn: Lễ tân bị quá tải giờ cao điểm (bận đón khách/nhận thư)
          │
          ▼
 ┌─────────────────┐
 │ BƯỚC 3: PHÂN    │ ⏱ 15 phút/lượt 🔴 [BOTTLENECK 2]
 │ LOẠI SỰ CỐ      │ 👤 Actor: Lễ tân sảnh (Thủ công)
 └────────┬────────┘ 📥 Input: Nội dung văn bản tự do
          │          📤 Output: Mã nhóm sự cố (Kỹ thuật / Vệ sinh / An ninh / Luật)
          │ 🔄 Handoff 2: Lễ tân tra cứu danh sách nhân sự trực ca của từng đội
          ▼
 ┌─────────────────┐
 │ BƯỚC 4: TẠO     │ ⏱ 15 phút/lượt 🔴 [BOTTLENECK 3]
 │ TICKET & GÁN    │ 👤 Actor: Lễ tân sảnh (Thủ công)
 └────────┬────────┘ 📤 Output: Ticket ID gán cho Trưởng đội Kỹ thuật/Vệ sinh
          │
          ▼
 ┌─────────────────┐
 │ BƯỚC 5: SOẠN    │ ⏱ 3 phút/lượt
 │ TIN XÁC NHẬN    │ 👤 Actor: Lễ tân sảnh (Soạn mẫu tin nhắn thủ công)
 └────────┬────────┘ 📤 Output: Notification gửi về App cư dân
          │
          ▼
 ┌─────────────────┐
 │ KỸ THUẬT/BQL    │ ⏱ Tổng thời gian tiếp nhận & gán ticket ban đầu: 45 - 60 phút/ticket
 │ XỬ LÝ THỰC ĐỊA  │ ❌ Tỷ lệ trễ SLA phản hồi ban đầu: 22%
 └─────────────────┘ ❌ Tỷ lệ gán nhầm bộ phận: 12%
```

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Lễ tân Tòa nhà và Chuyên viên Ban Quản lý Khu đô thị Vinhomes. |
| **2. Current Workflow** | Khi cư dân gặp sự cố (mất nước, hỏng điều hòa sảnh, tiếng ồn, dột nước), họ gửi phản ánh dạng văn bản tự do qua App Vinhomes Resident. Lễ tân đọc từng tin nhắn, đọc hiểu ngữ nghĩa, tra cứu sổ tay để phân loại sự cố và tạo ticket thủ công gán cho bộ phận chuyên trách (Kỹ thuật, An ninh, Vệ sinh, Pháp lý). Quy trình gồm 5 bước thủ công kéo dài **45-60 phút/ticket**. |
| **3. Bottleneck** | **Bước 2, 3 & 4 (mất 45 phút):** Lễ tân bận rộn tiếp đón khách hàng và cư dân trực tiếp tại sảnh khiến tin nhắn bị tích tụ. Việc đọc hiểu văn bản không cấu trúc và phân loại thủ công tốn nhiều thời gian, dẫn tới tỷ lệ phân loại nhầm bộ phận lên đến **12%**. |
| **4. Business Impact** | Tỷ lệ trễ SLA phản hồi ban đầu đạt **22%** vào các khung giờ cao điểm (7h-9h, 17h-19h). Chỉ số hài lòng của cư dân (CSAT) giảm xuống dưới **80%**, gia tăng mâu thuẫn bức xúc giữa cư dân và Ban Quản lý đại đô thị. |
| **5. Success Metric** | 1. **Giảm thời gian phân loại & gán ticket:** Từ 45-60 phút xuống **< 1 phút/ticket**.<br>2. **Chính xác điều hướng:** Tỷ lệ phân loại đúng bộ phận đạt **≥ 95%**.<br>3. **Nâng cao CSAT:** Tăng chỉ số CSAT phản hồi dịch vụ cư dân lên **> 95%**. |
| **6. Operational Boundary** | **ĐƯỢC PHÉP:** AI phân loại ngữ nghĩa, trích xuất mức độ khẩn cấp (Urgency Level), tạo bản nháp (Draft) ticket và draft tin nhắn phản hồi.<br>**TUYỆT ĐỐI CẤM:**<br>1. AI không được tự động gán hoặc xử lý các tin nhắn có dấu hiệu **Tranh chấp pháp lý, khiếu nại tài chính, sổ đỏ** (bắt buộc chuyển ngay cho Ban Pháp lý BQL).<br>2. AI không được tự động phát hành tin nhắn cam kết mốc thời gian hoàn thành sửa chữa cho cư dân khi chưa được Lễ tân bấm duyệt (Bắt buộc Human-in-the-Loop). |

---

## 3.3. Future-State Flow & AI Fit Analysis

### 📊 Phân tích AI Fit (AI-Fit Matrix)
* **Rule-based / State-Machine:** *Không đủ (Not Enough).* Ngôn ngữ tiếng Việt của cư dân rất phong phú, viết tắt, sai chính tả (ví dụ: *"nhà A3-1204 bị ngập lênh láng rồi"*), Rule-based không thể bao quát hết các ngữ cảnh.
* **LLM Feature (Được chọn):** *Rất phù hợp (Best Fit).* Sử dụng LLM để đọc hiểu tự nhiên, phân loại văn bản (Text Classification), trích xuất thực thể (Entity Extraction: Số căn, loại sự cố) và trích xuất mức độ khẩn cấp (Sentiment & Urgency Analysis).
* **Agentic Loop:** *Chưa cần thiết (Overkill).* Quy trình đã có các bước rõ ràng, việc dùng Agent tự trị có thể gây ra rủi ro chi phí API đắt đỏ và khó kiểm soát ranh giới an toàn.

---

### 🚀 Future-State Workflow (Quy trình tương lai ứng dụng AI)

```text
┌─────────────────────────────────────────────────────────────────────────────────────────┐
│                                FUTURE-STATE WORKFLOW                                    │
└─────────────────────────────────────────────────────────────────────────────────────────┘

 ┌─────────────────┐
 │   CƯ DÂN        │
 └────────┬────────┘
          │ (1) Gửi phản ánh (Văn bản tự do / Hình ảnh qua App Vinhomes Resident)
          ▼
 ┌─────────────────┐
 │ BƯỚC 1: NHẬN    │ ⏱ 1 giây
 │ TIN PHẢN ÁNH    │ 📥 Input: Raw Text, User ID, Căn hộ ID
 └────────┬────────┘ 📤 Output: Event Trigger gửi sang AI Module
          │
          ▼
 ┌─────────────────┐
 │ BƯỚC 2: 🔵 AI   │ ⏱ 3 giây ⚡ [AI STEP]
 │ CLASSIFY & RISK │ 🤖 Tech: Gemini 2.5 Flash / LLM Engine
 └────────┬────────┘ 📥 Input: Raw Text + Metadata căn hộ
          │          📤 Output: JSON { category, urgency, is_legal_risk }
          │
          ├────────────────────────────────────────┐
          │ (Nếu Confidence < 80% hoặc Risk == True)│
          ▼                                        ▼
 ┌─────────────────┐                      ┌─────────────────┐
 │ BƯỚC 3: 🔵 AI   │ ⏱ 2 giây              │ ↩️ FALLBACK     │ ⏱ 5 phút
 │ DRAFT TICKET    │ 🤖 Tech: LLM Generator │ CHUYỂN BQL/LUẬT │ 👤 Lễ tân / Pháp lý
 └────────┬────────┘ 📤 Output: Draft Form │ XỬ LÝ THỦ CÔNG  │    xử lý thủ công
          │          + Draft Confirmation └─────────────────┘    như quy trình cũ
          │
          │ 🔄 Handoff: Đẩy bản nháp lên Màn hình Lễ tân (1-Click Approval)
          ▼
 ┌─────────────────┐
 │ BƯỚC 4: 🟢 HUMAN│ ⏱ 10 - 30 giây 🛡️ [HUMAN-IN-THE-LOOP]
 │ CLICK DUYỆT     │ 👤 Actor: Lễ tân sảnh
 └────────┬────────┘ 📥 Input: Draft Ticket & Proposed Action
          │          👉 Lễ tân xem nhanh 3 giây -> Click [Duyệt & Gửi]
          ▼
 ┌─────────────────┐
 │ TỰ ĐỘNG PHÁT    │ ⏱ Tổng thời gian phản hồi & gán ticket: < 1 phút/ticket (Giảm 98%)
 │ TICKET & GỬI SMS│ 🎯 Tỷ lệ gán đúng: ≥ 95%
 └─────────────────┘ 🎯 Tỷ lệ trễ SLA: < 2%
```

---

## 🛠️ Tóm tắt các rào cản an toàn (Operational Boundaries) & Projekt Guardrails

1. **Guardrail 1 — Thẻ Nháp bắt buộc (`status: "DRAFT_ONLY"`):**
   Mọi output do LLM tạo ra bắt buộc phải mang nhãn nháp. Hệ thống Core CRM của Vinhomes sẽ từ chối gửi tin nếu thiếu chữ ký số xác nhận của Lễ tân.
2. **Guardrail 2 — Bộ lọc Rủi ro Pháp lý & Tranh chấp (`requires_legal_review`):**
   Khi LLM phát hiện các từ khóa mang tính rủi ro pháp lý cao (tranh chấp phí, kiện tụng, hợp đồng, sổ đỏ), ticket tự động bypass khỏi đội Lễ tân sảnh và chuyển thẳng cho Ban Pháp lý BQL xử lý theo luồng riêng.
3. **Guardrail 3 — Kế hoạch dự phòng (Fallback Mechanism):**
   Nếu điểm tin cậy (Confidence Score) của LLM dưới 80%, hệ thống tự động quay về quy trình tiếp nhận thủ công truyền thống, đảm bảo không làm gián đoạn vận hành.

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
