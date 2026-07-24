# Lab 02 — Worksheet: AI Product Scoping (Vin Smart Future)

---

## 🏛️ 1. Bối cảnh thực tế: Vin Smart Future (Vingroup)

**Vingroup** — Tập đoàn tư nhân lớn nhất Việt Nam — vừa sáp nhập toàn bộ các phòng ban công nghệ thuộc các công ty thành viên thành một đơn vị công nghệ thống nhất mang tên **Vin Smart Future**. 

Nhiệm vụ của **Vin Smart Future** là xây dựng các giải pháp AI, số hóa, và tự động hóa cốt lõi để nâng cao hiệu suất vận hành và trải nghiệm khách hàng xuyên suốt các công ty thành viên:
* 🚗 **VinFast:** Hệ thống xe điện thông minh (EV), trợ lý AI ảo trong xe, dự đoán bảo trì pin, và quản lý chuỗi cung ứng sản xuất.
* 🚕 **Xanh SM (GSM):** Vận hành đội xe taxi/xe máy điện thông minh, điều vận thông minh (Smart Dispatching), tối ưu hóa lộ trình di chuyển.
* 🏢 **Vinhomes:** Quản lý đô thị thông minh (Smart Cities), trợ lý cư dân thông minh, tối ưu hóa mức tiêu thụ năng lượng.
* 🏥 **Vinmec:** Y tế thông minh, chẩn đoán hình ảnh bằng AI, tối ưu hóa quản lý hồ sơ bệnh án.
* 🎢 **Vinpearl / VinWonders:** Trải nghiệm du lịch số hóa, quản lý phòng và luồng khách thông minh tại các khu vui chơi.

Trong buổi Lab hôm nay, nhóm của bạn sẽ đóng vai trò là **AI Product Engineer** tại **Vin Smart Future**, tiến hành tìm kiếm, scoping, phân tích độ khả thi, thiết lập ranh giới vận hành, và xây dựng một **bản mẫu kỹ thuật (prompt prototype)** cho một bài toán cụ thể thuộc một trong những mảng kinh doanh trên.

---

## 📊 2. Cơ cấu tính điểm bài lab

### 👥 Điểm nhóm (60 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **G1. Workflow Mapping** | 20 | Problem Deep-Dive | Vẽ chi tiết quy trình hiện tại: các bước, handoff, thời gian, bottleneck |
| **G2. Problem Statement** | 20 | Problem Deep-Dive | Problem Statement 6-field bám sát thực tế, metric có số và ranh giới rõ ràng |
| **G3. AI Fit & Future Flow** | 10 | Problem Deep-Dive | So sánh Rule vs LLM vs Agent, future flow có bước AI, ranh giới và Fallback |
| **G4. Decision Quality** | 10 | Problem Deep-Dive | Quyết định Go/Not Yet/No-Go trung thực và có chứng cứ rõ ràng |

### 👤 Điểm cá nhân (40 điểm)

| Gate | Điểm | Deliverable | Tiêu chí chấm |
|---|---:|---|---|
| **I1. Scan & Cards** | 15 | Quick Cards | Liệt kê 5 problems sử dụng 3 lenses, hoàn thiện 3 quick cards chất lượng |
| **I2. Prototyping** | 10 | 02-lab/ | Chạy thử nghiệm programmatic prompt prototype thành công |
| **I3. AI Log & Reflection** | 15 | 03-ai-log.md | Phản ánh trung thực về việc dùng AI làm thought-partner (giúp gì, sai gì, sửa gì) |

---

# 🚀 Phase 0 — worked Example: Xanh SM Intelligent Dispatcher (15 min)

*Giảng viên walk-through ví dụ thực tế từ Vin Smart Future để bạn hiểu rõ cách scoping một bài toán AI.*
Đọc chi tiết worked example tại file [02-deliverable-example.md](02-deliverable-example.md).

---

# 🔍 Phase 1 — SCAN (Cá nhân, 20 min)

Hãy sử dụng **4 Lenses** dưới đây để quét qua hoạt động vận hành của các công ty thành viên Vingroup. Ghi lại **ít nhất 5 bài toán/bottleneck** thực tế.

### 4 Lenses tìm bài toán AI cho Vingroup:
1. **Lặp lại (Repetitive):** Tác vụ lặp đi lặp lại nhiều lần hằng ngày. (Ví dụ: So khớp hóa đơn sạc điện tại VinFast, route lại chuyến taxi tại Xanh SM).
2. **Tốn thời gian (Time-consuming):** Tác vụ ngốn thời gian xử lý thủ công của nhân viên. (Ví dụ: Soạn thảo phản hồi đánh giá 1-star của cư dân Vinhomes).
3. **AI có thể tốt hơn (AI-upgrade):** Dịch vụ khách hàng hiện tại còn chậm hoặc phản hồi rập khuôn. (Ví dụ: Chatbot CSKH Vinpearl hỗ trợ đặt vé vui chơi).
4. **Pain từ người khác (Stakeholder Pain):** Bottleneck khiến khách hàng hoặc nhân viên thực địa phàn nàn. (Ví dụ: Tài xế Xanh SM phàn nàn về việc hệ thống gợi ý điểm đón khách không chính xác).

> [!TIP]
> **🤖 AI Prompts — Partner brainstorm:**
> Hãy sử dụng prompt sau để brainstorm các bài toán thực tế nếu bạn chưa có ý tưởng:
> *"Tôi là AI Engineer tại Vin Smart Future (Vingroup). Tôi đang tìm kiếm các pain point vận hành cụ thể có thể tối ưu bằng AI cho mảng [Chọn một: VinFast / Xanh SM / Vinhomes / Vinmec]. Hãy gợi ý cho tôi 5 quy trình nghiệp vụ thủ công, tốn nhiều thời gian và gây rò rỉ hiệu suất kèm con số thống kê ước tính về tổn thất."*

### 📝 List bài toán của tôi:
| # | Subsidiary (VinFast/Xanh SM...) | Lens | Mô tả ngắn bài toán |
|---|----------------------------------|------|---------------------|
| 1 |Vinmec |Tốn thời gian |Bác sĩ phải đọc nhiều phần trong hồ sơ bệnh án để viết bản tóm tắt xuất viện cho từng bệnh nhân. |
| 2 |Vinhomes |AI-upgrade |Yêu cầu và khiếu nại của cư dân được phân loại thủ công, khiến phản hồi chậm hoặc bị chuyển sai bộ phận. |
| 3 |Vinpearl |Nhân viên phải đọc hàng trăm đánh giá của khách hàng mỗi ngày để phát hiện các sự cố nghiêm trọng cần xử lý sớm.|
| 4 |VinFast |Lặp lại |Nhân viên chất lượng phải tổng hợp báo cáo lỗi từ nhiều nhà cung cấp với cách diễn đạt và định dạng khác nhau. |
| 5 |XanhSM| Tốn thời gian|Nhân viên vận hành phải đọc ghi chú của tài xế và tổng đài để tổng hợp nguyên nhân khách hàng hủy chuyến. |

---

# 🃏 Phase 2 — QUICK-ASSESS (Cá nhân, 30 min)

Chọn **top 3 bài toán** từ danh sách trên và hoàn thiện **3 Quick Problem Cards** dưới đây (10 phút/card).

```
┌──────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                                        │
│                                                                              │
│ Bài toán (1 câu): Hỗ trợ bác sĩ Vinmec tạo bản nháp tóm tắt hồ sơ xuất viện.│
│                                                                              │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes                 │
│                     [x] Vinmec    [ ] Khác (Ghi rõ): __________              │
│                                                                              │
│ Ai đang đau (Actor)?                                                         │
│ Bác sĩ điều trị, điều dưỡng hỗ trợ hồ sơ và bệnh nhân chờ xuất viện.         │
│                                                                              │
│ Workflow thủ công hiện tại (3–5 bước):                                       │
│   1. Bác sĩ mở và đọc toàn bộ hồ sơ bệnh án của bệnh nhân.                   │
│   2. Kiểm tra chẩn đoán, kết quả xét nghiệm và diễn biến điều trị.           │
│   3. Tổng hợp thuốc, thủ thuật và phương pháp điều trị đã thực hiện.          │
│   4. Viết bản tóm tắt xuất viện theo biểu mẫu của bệnh viện.                 │
│   5. Kiểm tra, chỉnh sửa và ký xác nhận trước khi trả hồ sơ cho bệnh nhân.   │
│                                                                              │
│ Bước nào tốn thời gian/lỗi nhất?                                              │
│ Bước 2, 3 và 4 — đọc, tổng hợp và viết nội dung                              │
│ (⏱ khoảng 20–30 phút/bệnh nhân).                                            │
│                                                                              │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                        │
│ AI hỗ trợ tại bước 2, 3 và 4: trích xuất thông tin quan trọng, sắp xếp dữ    │
│ liệu theo biểu mẫu và tạo bản nháp tóm tắt để bác sĩ kiểm tra, chỉnh sửa.   │
│                                                                              │
│ Đo thành công bằng gì (Metric có số)?                                        │
│ Giảm thời gian tạo bản nháp từ khoảng 25 phút xuống dưới 5 phút/bệnh nhân.  │
│ Ít nhất 95% trường thông tin bắt buộc được trích xuất đầy đủ.                │
│ 100% bản tóm tắt phải được bác sĩ kiểm tra và ký xác nhận trước khi sử dụng.│
│                                                                              │
│ Quick Architecture: [ ] No AI   [x] Rule   [x] LLM   [ ] Agent              │
└──────────────────────────────────────────────────────────────────────────────┘


┌──────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                                        │
│                                                                              │
│ Bài toán (1 câu): Hỗ trợ Vinmec phân loại và ưu tiên yêu cầu đặt lịch khám. │
│                                                                              │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes                 │
│                     [x] Vinmec    [ ] Khác (Ghi rõ): __________              │
│                                                                              │
│ Ai đang đau (Actor)?                                                         │
│ Nhân viên tổng đài, nhân viên tiếp nhận, bác sĩ và bệnh nhân cần đặt lịch.   │
│                                                                              │
│ Workflow thủ công hiện tại (3–5 bước):                                       │
│   1. Bệnh nhân gọi điện hoặc gửi yêu cầu đặt lịch khám.                      │
│   2. Nhân viên đọc nội dung và hỏi thêm triệu chứng, thời gian mong muốn.    │
│   3. Nhân viên xác định chuyên khoa và mức độ ưu tiên phù hợp.                │
│   4. Kiểm tra lịch trống của bác sĩ và đề xuất khung giờ khám.               │
│   5. Xác nhận lịch hẹn và hướng dẫn bệnh nhân chuẩn bị giấy tờ cần thiết.    │
│                                                                              │
│ Bước nào tốn thời gian/lỗi nhất?                                              │
│ Bước 2, 3 và 4 — thu thập thông tin, chọn chuyên khoa và kiểm tra lịch       │
│ (⏱ khoảng 8–12 phút/yêu cầu).                                               │
│                                                                              │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                        │
│ AI hỗ trợ tại bước 2 và 3: tóm tắt yêu cầu, phát hiện thông tin còn thiếu,  │
│ đề xuất chuyên khoa và mức độ ưu tiên để nhân viên tiếp nhận kiểm tra.       │
│ Rule-based được dùng để kiểm tra các dấu hiệu khẩn cấp và dữ liệu bắt buộc.  │
│                                                                              │
│ Đo thành công bằng gì (Metric có số)?                                        │
│ Giảm thời gian xử lý yêu cầu từ khoảng 10 phút xuống dưới 3 phút/yêu cầu.   │
│ Ít nhất 90% yêu cầu thông thường được phân loại đúng chuyên khoa.            │
│ 100% trường hợp có dấu hiệu khẩn cấp phải được chuyển cho nhân viên xử lý.  │
│                                                                              │
│ Quick Architecture: [ ] No AI   [x] Rule   [x] LLM   [ ] Agent              │
└──────────────────────────────────────────────────────────────────────────────┘


┌──────────────────────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                                        │
│                                                                              │
│ Bài toán (1 câu): Hỗ trợ Vinmec tổng hợp phản hồi của bệnh nhân sau khám.   │
│                                                                              │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes                 │
│                     [x] Vinmec    [ ] Khác (Ghi rõ): __________              │
│                                                                              │
│ Ai đang đau (Actor)?                                                         │
│ Nhân viên chăm sóc khách hàng, quản lý bệnh viện và bệnh nhân sau khám.      │
│                                                                              │
│ Workflow thủ công hiện tại (3–5 bước):                                       │
│   1. Bệnh nhân gửi đánh giá qua ứng dụng, email hoặc cuộc gọi.               │
│   2. Nhân viên đọc từng phản hồi và ghi lại nội dung chính.                  │
│   3. Phân loại phản hồi theo chuyên môn, dịch vụ, chi phí hoặc cơ sở vật chất.│
│   4. Xác định mức độ nghiêm trọng và chuyển đến bộ phận phụ trách.           │
│   5. Soạn phản hồi ban đầu và theo dõi tình trạng xử lý.                     │
│                                                                              │
│ Bước nào tốn thời gian/lỗi nhất?                                              │
│ Bước 2, 3 và 4 — đọc, phân loại và xác định mức độ ưu tiên                   │
│ (⏱ khoảng 5–8 phút/phản hồi).                                               │
│                                                                              │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                                        │
│ AI hỗ trợ tại bước 2, 3 và 4: tóm tắt phản hồi, phân loại chủ đề, phát hiện │
│ nội dung tiêu cực hoặc nghiêm trọng và tạo bản nháp phản hồi ban đầu.        │
│ Các phản hồi liên quan đến an toàn, điều trị hoặc tranh chấp phải được       │
│ chuyển cho nhân viên có thẩm quyền kiểm tra.                                 │
│                                                                              │
│ Đo thành công bằng gì (Metric có số)?                                        │
│ Giảm thời gian phân loại từ khoảng 6 phút xuống dưới 1 phút/phản hồi.       │
│ Ít nhất 90% phản hồi được phân loại đúng nhóm vấn đề.                        │
│ 100% phản hồi liên quan đến an toàn hoặc chuyên môn y tế phải được người    │
│ phụ trách kiểm tra trước khi trả lời bệnh nhân.                              │
│                                                                              │
│ Quick Architecture: [ ] No AI   [x] Rule   [x] LLM   [ ] Agent              │
└──────────────────────────────────────────────────────────────────────────────┘
```

```

```



> [!TIP]
> **🤖 AI Prompts — Stress-Test thẻ bài toán:**
> Hãy dán nội dung thẻ bài toán của bạn vào LLM để nhận phản biện:
> *"Đây là một thẻ bài toán vận hành tôi đề xuất cho Vin Smart Future: [Dán nội dung]. Hãy đóng vai trò là một CFO và Trưởng phòng Vận hành cực kỳ khắt khe, chỉ ra cho tôi 3 điểm yếu về logic, metric, và giải thích vì sao rule-based code thông thường có thể giải quyết bài toán này tốt hơn là dùng AI."*

---

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm, 85 min)

## 3.1. Current-State Workflow Mapping (25 min)
**Vẽ quy trình hiện tại lên bảng/giấy A3.** Sử dụng các ký hiệu:
* 🔴 **Bottleneck:** Bước gây tắc nghẽn, tốn thời gian, hoặc sai sót nhiều nhất.
* 🔄 **Handoff:** Điểm chuyển giao thông tin giữa người và hệ thống, hoặc giữa các bộ phận.
* Ghi rõ thời gian vận hành trung bình: **Tổng cộng = ____ phút/lượt**.

## 3.2. Problem Statement (6-field) & Metrics (15 min)
Điền đầy đủ 6 trường thông tin của bài toán:

| Field | Nội dung chi tiết |
|---|---|
| **1. Actor / Operator** | Ai đang thực hiện tác vụ hằng ngày? |
| **2. Current Workflow** | Mô tả tóm tắt quy trình thủ công hiện tại và công cụ sử dụng. |
| **3. Bottleneck** | Bước nào chậm, lỗi, hoặc cần xử lý ngôn ngữ tự động nhiều nhất? |
| **4. Business Impact** | Tổn thất thực tế đo bằng thời gian, chi phí, hoặc SLA của Vingroup. |
| **5. Success Metric** | AI giải quyết được thì đạt ngưỡng số mấy? (Ví dụ: *"85% vé được phân loại dưới 10s"*). |
| **6. Operational Boundary** | AI được phép làm gì, TUYỆT ĐỐI không được làm gì, điểm nào cần duyệt? |

## 3.3. Future-State Flow & AI Fit (25 min)
* **Xác định mức AI Fit (AI-Fit Matrix):** Giải pháp thuộc nhóm nào? [ ] Rule / State-Machine [ ] LLM Feature [ ] Agentic Loop.
* **Vẽ Future-State Flow:** Đánh dấu rõ:
  * 🔵 **AI Step:** Tác vụ LLM xử lý.
  * 🟢 **Human Step (HITL):** Bước con người phê duyệt/review (Human-in-the-loop).
  * ↩️ **Fallback:** Kế hoạch dự phòng khi LLM trả về kết quả lỗi hoặc không tự tin.

---

# 💻 Phase 4 — TECHNICAL PROMPT PROTOTYPE (Nhóm, 30 min)

Để đảm bảo kỹ sư của Vin Smart Future luôn giữ vững năng lực lập trình, nhóm của bạn sẽ tiến hành **lập trình bản mẫu prompt** trực tiếp trên **Gemini 2.5 Flash** bằng Python để stress-test hệ thống.

### Hướng dẫn thực hiện:
1. Mở file [starter-code/prompt_prototype.py](starter-code/prompt_prototype.py) bằng VS Code/Cursor.
2. Hoàn thiện các nội dung sau:
   * **System Prompt:** Viết chỉ thị cực kỳ nghiêm ngặt quy định vai trò, nhiệm vụ, định dạng output và **Operational Boundary (Ranh giới cấm)** của mô hình.
   * **Structured Output:** Định nghĩa định dạng JSON output rõ ràng.
   * **Adversarial Test Cases:** Viết ít nhất 3 prompts "tấn công" (Adversarial inputs) cố tình dụ AI vượt ranh giới hoặc đưa ra câu trả lời không được phép để kiểm tra xem ranh giới của bạn có thực sự vững chắc.
3. Chạy file python:
   ```bash
   python3 prompt_prototype.py
   ```
4. Kiểm tra xem các ranh giới an toàn có bị LLM phá vỡ hay không và ghi lại kết quả vào worksheet.

---

# 🏁 Phase 5 — EVALUATE (Nhóm, 20 min)

### AI Readiness Checklist:
1. [ ] Chúng tôi có sẵn dữ liệu mẫu/logs sạch để test?
2. [ ] Rủi ro khi AI sai có nằm trong tầm kiểm soát (qua HITL hoặc Fallback)?
3. [ ] Stakeholders sẵn sàng thay đổi quy trình làm việc cũ?

### Quyết định cuối cùng của Ban Giám Đốc Vin Smart Future:
[ ] **GO (Bắt đầu xây dựng Prototype):** Bắt đầu phát triển với scope hẹp.
[ ] **NOT YET (Cần tích lũy thêm dữ liệu/xác lập baseline):** Trì hoãn để chuẩn bị thêm.
[ ] **NO-GO (Không khả thi / Rule-based tốt hơn):** Hủy bỏ dự án AI này.

**Justification (Lý giải quyết định dựa trên bằng chứng kỹ thuật và chi phí):**
> *Viết lý giải chi tiết tại đây*

---

# 📝 Phase 6 — REFLECTION (Cá nhân)
*Ghi nhận phản ánh của cá nhân bạn về việc phối hợp với AI trong buổi học hôm nay vào file `03-ai-log.md`.*
