# TRIPLAN · OPERATING DASHBOARD (B2C)
**Đinh Thị Minh Tâm · 2A202602433 · 10/10/2026**  
**NORTH STAR:** Weekly Qualified Itinerary Exports (WQIE) — số `itinerary_id` duy nhất xuất thành công/tuần bởi user thật; không tính nháp, xuất lỗi/lặp, test. **Hiện:** chưa đo · **Đích:** ≥1,2B.  
**Chú giải:** B = baseline đo trong 2 cohort tuần; [TB] ngưỡng tạm cần hiệu chuẩn; [MH] suy từ mô hình tài chính (chưa phải số đo). **Không có số thực → không gán màu.**

### 3 tầng · 8 đèn
| Tầng · Đèn (định nghĩa rút gọn) | Hiện | 🟢 | 🟡 | 🔴 | Nguồn · dẫn tới |
|---|---|---|---|---|---|
| **L1 Activation 24h** · new users xuất ≥1 lịch trình hợp lệ/ new users đủ 24h | N/A | ≥1,2B | 0,8B–<1,2B | <0,8B | [TB] → O1 |
| **L2 WQIE** · distinct qualified exported itinerary/tuần | N/A | ≥1,2B | 0,8B–<1,2B | <0,8B | [TB] → O1 |
| **L3 p95 AI cost/job ÷ giá/job** · job hoàn tất, không dùng trung bình | N/A | ≤21,33% | >21,33–40% | >40% | [MH] → O2 |
| **O1 Trial→Paid** · trial users trả phí lần đầu / trial users đủ thời hạn | N/A | ≥1,2B | 0,8B–<1,2B | <0,8B | [TB] → G2 |
| **O2 AI cost/paid revenue** · token cost paid jobs / net paid revenue | N/A | ≤21,33% | >21,33–40% | >40% | [MH] → G1 |
| **O3 Free-tier cost share** · free inference cost / COGS toàn bộ | N/A | <20% | 20–40% | >40% | [TB] → G1 |
| **G1 Gross margin** · (net revenue − total COGS)/net revenue | N/A | ≥78,67% | 60–<78,67% | <60% | [MH] · kết quả |
| **G2 CAC payback** · CAC / gross profit/payer/tháng | N/A | ≤1,27 tháng | >1,27–3 | >3 | [MH] · kết quả |

**Cơ sở ngưỡng:** [MH] $0,531 Cost/Job ÷ $2,49 Price/Job = **21,33%**; mốc quản trị GM 60% ⇒ trần cost/job **$0,996 (40%)** nếu chưa tính chi phí khác. ($2,49−$0,531)/$2,49 = **78,67%** GM *chỉ nếu* $0,531 là toàn bộ COGS. CAC giả định $7,053 ÷ ($7,053 ARPU × 78,68% GM) = **1,27 tháng**; mục tiêu ≤3. [TB] ±20% B, free-tier 20/40% là quy tắc thử nghiệm, **đo đủ hai chu kỳ rồi hiệu chuẩn**. Không suy p95 từ chi phí trung bình.

### 5 luật NẾU → TRONG/TRÊN → THÌ → KHÔNG THÌ (⏹ dừng)
1. **⏹ L1:** **NẾU** Activation <0,8B **TRONG** 2 cohort tuần (mỗi cohort ≥100 users), **THÌ** Growth Lead **đóng băng tăng ads 14 ngày**, Product Lead sửa một bước onboarding; **KHÔNG THÌ** không tăng ads bù activation.
2. **L2:** **NẾU** WQIE <0,8B **TRONG** 2 tuần (≥100 active users/tuần), **THÌ** Product Lead tìm bước rơi lớn nhất và sửa trong 7 ngày; **KHÔNG THÌ** không bổ sung tính năng để thổi phồng exports.
3. **⏹ L3:** **NẾU** p95 AI cost/job ÷ price >40% **TRONG** 2 tuần (≥100 completed jobs/tuần), **THÌ** AI Lead **dừng tăng quota**, giới hạn regenerate, tối ưu model; **KHÔNG THÌ** không tăng giá đồng loạt hoặc bỏ kiểm tra chất lượng.
4. **⏹ O2:** **NẾU** AI cost/paid revenue >40% **TRONG** 2 tuần (≥30 paid transactions đã đối soát/kỳ), **THÌ** AI Lead **dừng các request AI tự động không thiết yếu** ngay sprint tới; **KHÔNG THÌ** không mở rộng free tier.
5. **O1:** **NẾU** Trial→Paid <0,8B **TRONG** 2 cohort trial đủ hạn (mỗi cohort ≥100 users), **THÌ** Growth Lead thử một thay đổi paywall trong 14 ngày; **KHÔNG THÌ** không giảm giá hàng loạt.

### 3 cổng gác 90 ngày · một metric/cổng
| Cổng | Metric duy nhất | Ngưỡng GO | Bằng chứng | Nếu trượt |
|---|---|---|---|---|
| **D30 · Học** | New users có activation tracking hợp lệ | **≥100** | `cohort_D30.csv` + event log | **FIX** tracking/onboarding một lần, 30 ngày |
| **D60 · Giá trị** | Activation 24h | **≥1,2B** (B đo ở D30) | `activation_cohorts.csv` | **FIX** một lần nếu biết nút thắt; **PIVOT** nếu giả định sai |
| **D90 · Kinh tế** | AI cost/paid revenue | **≤40%** với ≥30 paid jobs | `ai_cost_ledger.csv` + payment ledger | **KILL** nếu đã FIX cùng lỗi 30 ngày vẫn đỏ; nếu chưa FIX, FIX một lần |

**KILL CRITERIA:** Đến **D90**, **KILL** hướng bán lịch trình hiện tại nếu AI cost/paid revenue vẫn **>40% trên ≥30 paid jobs**, sau **một FIX 30 ngày đã bắt đầu không muộn hơn D60**; nếu không thỏa điều kiện theo dõi/FIX thì chưa được tuyên bố KILL.

**CHƯA ĐO ĐƯỢC:** B, WQIE, activation, p95 AI costs, paid conversion, free COGS, GM thực, CAC/payback thực, runway. Cần `user_signed_up`, `itinerary_exported`, `trial_started`, `payment_success`, token-cost + payment logs; **mốc baseline dự kiến 24/10/2026** nếu tracking bắt đầu 10/10; D30/D60 cần đúng thời gian cohort. Nếu không có trial thực, đổi O1 thành **Free→First Paid** trước đo.
