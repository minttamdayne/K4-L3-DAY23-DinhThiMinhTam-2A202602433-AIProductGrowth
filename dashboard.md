# OPERATING DASHBOARD — TRIPLAN AI TRAVEL PLANNER

**B2C** · 10/10/2026 · **Đinh Thị Minh Tâm — 2A202602433**  
**North Star:** Weekly Qualified Itinerary Exports (WQIE) = số `itinerary_id` duy nhất được người dùng thật xuất thành công/tuần (loại trừ nháp, lỗi, xuất lặp, test). **Hiện tại:** chưa đo · **Mục tiêu:** ≥1,2B sau baseline.

> **Trạng thái toàn bảng: CHƯA CÓ DỮ LIỆU THỰC TẾ.** B = baseline 2 cohort tuần đã đo; không tô xanh/vàng/đỏ cho chỉ số chưa quan sát. [MH] = mô hình dự phóng; [TB] = ngưỡng tạm đợi đo baseline.

### LEADING · Hằng ngày/tuần
| Đèn | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn · Báo trước cho |
|---|---|---|---|---|---|
| **L1 Activation 24h** = new user có ≥1 qualified export/ new user đủ 24h | Chưa đo | ≥1,2B | 0,8B–<1,2B | <0,8B | [TB] · O1 |
| **L2 WQIE** = distinct qualified exported itinerary/tuần | Chưa đo | ≥1,2B | 0,8B–<1,2B | <0,8B | [TB] · O1 |
| **L3 p95 AI cost/job ÷ $2,49** (completed job, không lấy trung bình) | Chưa đo | ≤21,33% | >21,33–40% | >40% | [MH] · O2→G1 |

### OPERATING · Hằng tuần/tháng
| Đèn | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn · Báo trước cho |
|---|---|---|---|---|---|
| **O1 Trial→Paid** = trial user trả phí lần đầu / trial đủ thời gian quan sát | Chưa đo | ≥1,2B | 0,8B–<1,2B | <0,8B | [TB] · G2 |
| **O2 AI cost/paid revenue** = inference cost paid jobs / doanh thu thuần paid jobs | Chưa đo | ≤21,33% | >21,33–40% | >40% | [MH] · G1 |
| **O3 Free-tier cost share** = free inference cost / tổng COGS | Chưa đo | <20% | 20–40% | >40% | [TB] · G1 |

### LAGGING · Hằng tháng/quý
| Đèn | Hiện tại | 🟢 | 🟡 | 🔴 | Nguồn |
|---|---|---|---|---|---|
| **G1 Gross margin** = (net revenue−COGS)/net revenue | Chưa đo | ≥78,67% | 60–<78,67% | <60% | [MH] |
| **G2 CAC payback** = CAC / gross profit per payer per month | Chưa đo | ≤1,27 tháng | >1,27–3 | >3 | [MH] |

**Nguồn ngưỡng & lý do:** [MH] $0,531/$2,49 = **21,33%** (mốc chi phí AI cơ sở); sàn GM 60% ⇒ trần cost/job $0,996 = **40%** giá; ($2,49−$0,531)/$2,49 = **78,67%** GM *nếu* $0,531 là toàn bộ COGS. CAC giả định $7,053 / ($7,053 ARPU × 78,68% GM) = **1,27 tháng**; trần mục tiêu **3 tháng**. [TB] các biên ±20% quanh B và free-tier 20/40% là **chính sách thử nghiệm**, không phải benchmark; phải hiệu chuẩn sau ≥2 cohort. Giá trị [MH] là dự phóng, **không phải phép đo p95**.

### 5 LUẬT QUYẾT ĐỊNH · ⏹ = DỪNG
1. **⏹ R1 — L1:** **NẾU** activation <0,8B **TRONG** 2 cohort tuần, **VÀ** mỗi cohort ≥100 new users, **THÌ** Growth Lead **đóng băng tăng ngân sách ads 14 ngày**, Product Lead sửa một bước onboarding; **KHÔNG THÌ** không tăng ads để bù conversion.
2. **R2 — L2:** **NẾU** WQIE <0,8B **TRONG** 2 tuần, **VÀ** ≥100 active users/tuần, **THÌ** Product Lead phân tích funnel và sửa bước rơi lớn nhất trong 7 ngày; **KHÔNG THÌ** không thêm tính năng chỉ để tăng số lượt tạo.
3. **⏹ R3 — L3:** **NẾU** p95 cost/job/price >40% **TRONG** 2 tuần, **VÀ** ≥100 completed jobs/tuần, **THÌ** AI Lead **dừng tăng quota**, đặt giới hạn regenerate và tối ưu model; **KHÔNG THÌ** không tăng giá đại trà hay bỏ kiểm thử chất lượng.
4. **⏹ R4 — O2:** **NẾU** AI cost/paid revenue >40% **TRONG** 2 tuần, **VÀ** ≥30 giao dịch trả tiền đã đối soát/kỳ, **THÌ** AI Lead **dừng tác vụ AI tự động không thiết yếu**, áp quota trong sprint tới; **KHÔNG THÌ** không mở rộng free tier.
5. **R5 — O1:** **NẾU** trial→paid <0,8B **TRONG** 2 cohort trial đủ hạn, **VÀ** mỗi cohort ≥100 users, **THÌ** Growth Lead thử một thay đổi paywall trong 14 ngày, giữ nguyên giá; **KHÔNG THÌ** không giảm giá hàng loạt.

### CỔNG GÁC 90 NGÀY
| Cổng | Một metric chính | Ngưỡng GO | Bằng chứng bắt buộc | Nếu trượt |
|---|---|---|---|---|
| **D30 · LEARN** | Số user đăng ký mới hợp lệ có tracking activation | **≥100** | File cohort activation D0–D30 + event log đối soát | **FIX** tracking/onboarding đúng 30 ngày, một lần |
| **D60 · VALUE** | Activation 24h (cohort gần nhất) | **≥1,2B** (B=baseline D30) | Cohort report, timestamps đăng ký/xuất | **FIX** một bước funnel nếu chưa FIX; **PIVOT** nếu giả định nhu cầu sai |
| **D90 · ECONOMICS** | AI Cost / Paid Revenue | **≤40%**, với ≥30 paid jobs đã đối soát | Cost ledger token/model + payment ledger | **KILL** nếu đã FIX cùng vấn đề mà vẫn >40%; nếu chưa FIX, FIX một lần |

**KILL CRITERIA:** Tại **ngày 90**, dừng mô hình trả tiền theo lịch trình hiện tại nếu AI Cost / Paid Revenue **>40%** trên **≥30 paid jobs**, **sau một chu kỳ FIX 30 ngày cho chính vấn đề này**; không được dùng FIX lần hai để trì hoãn PIVOT/KILL.

**CHƯA ĐO ĐƯỢC:** Activation, WQIE, trial→paid, p95 AI cost/job, free-tier COGS, GM thực, CAC/payback thực, runway. Cần event tracking (`user_signed_up`, `itinerary_exported`, `trial_started`, `payment_success`), token-cost logs và ledger doanh thu/chi phí. **Dự kiến baseline đầu tiên: 24/10/2026 nếu tracking chạy từ 10/10**; cohort D30 và chỉ số D60/D90 chỉ có khi đủ ngày. Nếu Triplan không có trial thật, đổi O1 thành *Free→First Paid* trước khi đo.
