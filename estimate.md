# Ước lượng: SWP do skill chấm, giờ quy theo một hệ số

Báo cáo HTML của skill `estimate-swp`: [`reports/estimate-swp-hoangndn-1456-project-3-20261023-152239.html`](reports/estimate-swp-hoangndn-1456-project-3-20261023-152239.html)

Skill chấm 276 lá trên chính Project này ở mức `--level max` (hai assessor độc lập A và B), issue cha lấy tổng của issue con. Skill chỉ xuất báo cáo; SWP đã chốt được ghi vào field `Point (SWP)` bằng script, cách làm kể ở `AI-report.md`.

## 1. Issue mẫu skill chọn để kiểm

Skill tự chọn các issue đại diện: nhỏ nhất (#120), mức trung vị (#12), lớn nhất (#286), ngoại lai (#48) và một issue hai assessor chấm khác nhau (#8).

| Issue | Skill chấm (Scope × Complexity → SWP) | Bạn chốt | Lý do |
|---|---|---|---|
| #120 — [Dev Task] FUNC106 · Đánh dấu bản ghi hết thời hạn lưu trữ | 1 × 1 → 1 | 1 (giữ nguyên) | Một logic đánh dấu theo hạn 7 năm, không xóa bản ghi, không có luồng phê duyệt xóa (ngoài phạm vi); DoD ba dòng gồm một ca ranh giới. Là việc nhỏ nhất của backlog nên 1 là hợp lý. |
| #12 — [Dev Task] SCR030 · Màn form chốt giao dịch (B-3 đến B-9) | 3 × 2 → 5 | 5 (giữ nguyên) | Một màn FE (form B-3 đến B-9, kiểm phía client, quản lý khóa chống gửi lặp). Điểm khó duy nhất là sinh khóa mới khi đổi một trong bốn ô, nên phức tạp ở mức vừa; Scope 3 cho một màn. |
| #286 — [Dev Task] SCR160 · API-150 nhập và kiểm tệp xác nhận thanh toán | 5 × 3 → 10 | 10 (giữ nguyên) | Một API phải làm bốn việc: kiểm quyền, kiểm định dạng tệp, phát hiện trùng trước khi nhận, ghi hai bảng; thêm migration và tài liệu định dạng tệp chiều vào chưa có. DoD năm dòng nên Scope 5, Complexity 3. |
| #48 — [Dev Task] SCR002 · Xác thực hai bước (MFA) cho vai quản trị và phê duyệt | 5 × 3 → 10 | 10 (giữ nguyên) | Đụng xác thực: màn FE, kiểm mã qua server action, xác định tài khoản thuộc diện MFA, chặn đường vào khi chưa qua bước hai; DoD sáu dòng. Lỗi ở bước xác thực ảnh hưởng mọi vai nên Complexity 3. |
| #8 — [Dev Task] SCR030 · Migration: CHECK đơn giá và chỗ lưu 参加上限 | 2 × 2 → 3 | 3 (giữ nguyên) | Hai assessor lệch (A 3, B 5). Tôi chốt 3: phần làm được chỉ là CHECK đơn giá và một cột lưu; phần kiểm 参加上限 phải chờ khách trả lời SCR030-Q7 và đã có việc riêng (#146). |

Tôi giữ nguyên điểm của skill cho cả năm mẫu (hai vòng hỏi trong skill, cả hai vòng đều chọn đề xuất của skill). Lý do trong bảng do agent soạn từ phạm vi và DoD của từng issue, tôi duyệt. Cổng này chưa chứng minh tôi phản biện skill; phép kiểm độc lập nằm ở bộ đáp án mẫu (`AI-report.md` mục 2.3).

## 2. Cách quy ra giờ

- **Cách chọn:** quy ước đổi SWP ra giờ bằng một hệ số `r` (giờ trên một SWP), không ước trực tiếp từng issue.
- **Vì sao:** SWP đo khối lượng việc, không phụ thuộc người làm. Một hệ số áp cho mọi lá thì giờ nhất quán giữa các issue và đổi bối cảnh (ví dụ đội dùng AIDD) chỉ cần đổi `r`. Ước trực tiếp hàng trăm issue thì mỗi issue một kiểu suy đoán, không kiểm lại được.
- **Neo:** các lá của bộ đáp án mẫu (10/10 lá có giờ neo), chọn theo tầng loại việc. Một agent độc lập (không thấy điểm của skill) ước giờ từng lá từ dưới lên, liệt kê việc nhỏ kèm giờ.
- **Bối cảnh giờ neo:** dev mid 3 năm, đội **không dùng AIDD**, giờ gồm code, unit test, review và sửa lỗi. Một neo là việc BrSE hỏi khách, ước theo giờ BrSE. Đổi sang đội dùng AIDD thì phải đo lại `r`, không dùng chung số này.
- **Quy tắc:**
  - `r` = trung vị của (giờ neo ÷ SWP skill chốt) trên 10/10 neo = **3,625 giờ/SWP**; khoảng P25–P75 = 3,25–3,94. Dùng trung vị vì neo ít, một neo lệch không kéo cả hệ số.
  - Giờ của lá = SWP × `r`, làm tròn tới bước 0,5 giờ, sàn 0,5 giờ.
  - Giờ của issue cha = tổng giờ con, không làm tròn lại.
- **Áp dụng nhất quán:** script tính giờ cho mọi lá từ cùng một `r`, rồi ghi vào field `Estimated time`; không sửa tay giờ của issue nào.

## 3. Tổng theo epic

Số issue đếm lá; SWP và giờ cộng trên lá, đọc từ field của Project.

| Epic | Số issue | Tổng SWP | Tổng giờ | Ghi chú |
|---|---|---|---|---|
| #27 — Xác thực và quản lý tài khoản nội bộ | 11 | 62 | 226 | 17 item kể cả issue cha |
| #28 — Quản lý bên tham gia | 20 | 87 | 316,5 | 30 item kể cả issue cha |
| #29 — Dữ liệu chủ: lịch chợ và danh mục mặt hàng | 9 | 54 | 196 | 13 item kể cả issue cha |
| #30 — Tiếp nhận lô hàng | 14 | 90 | 326,5 | 20 item kể cả issue cha |
| #1 — Giao dịch thỏa thuận (相対取引): chốt và hủy | 21 | 86 | 313 | 25 item kể cả issue cha |
| #31 — Nhập hàng loạt và tra cứu kết quả đấu giá (せり) | 9 | 40 | 145,5 | 12 item kể cả issue cha |
| #32 — Đính chính giao dịch đã chốt | 13 | 70 | 254 | 17 item kể cả issue cha |
| #33 — Quyết toán và khóa ngày nghiệp vụ (nửa A: đối chiếu, khóa ngày, tranh chấp) | 27 | 153 | 555,5 | 35 item kể cả issue cha |
| #34 — Thưởng hoàn thành nộp đủ và version tỷ lệ thưởng | 22 | 144 | 523,5 | 30 item kể cả issue cha |
| #35 — Giao hàng | 16 | 74 | 268,5 | 21 item kể cả issue cha |
| #36 — Đồng bộ ngoại tuyến và giải quyết xung đột | 6 | 31 | 113 | 9 item kể cả issue cha |
| #37 — Thông báo: gửi, thử lại, nhật ký và cấu hình | 7 | 40 | 145,5 | 10 item kể cả issue cha |
| #38 — Báo cáo và theo dõi KPI nghiệm thu | 7 | 42 | 152,5 | 10 item kể cả issue cha |
| #39 — Nhật ký kiểm toán | 6 | 30 | 109 | 7 item kể cả issue cha |
| #40 — Bảo vệ thông tin cá nhân theo APPI | 13 | 68 | 247 | 18 item kể cả issue cha |
| #41 — Chuyển đổi dữ liệu | 8 | 33 | 120,5 | 10 item kể cả issue cha |
| #42 — Nền tảng chung | 67 | 296 | 1.077,5 | 79 item kể cả issue cha |
| **Tổng** | 276 | 1.400 | 5.090 | 380 item |

## 4. So với estimate LAB-1

Chỉ so phần giao nhau: chức năng (FUNC) × vai BE, FE, QA, cùng bối cảnh không AIDD, trước buffer; LAB-1 đổi từ người-ngày theo 7 giờ/người-ngày. Phạm vi so được: 134/146 FUNC, 121/276 lá LAB-5; phần còn lại không ghép được một-một nên không đem so, không chia đều. Cổng ghi trước khi so: tỉ số LAB-5/LAB-1 trong khoảng [0.7; 1.5].

| Phần (epic) | LAB-1 (giờ) | LAB-5 (giờ) | Chênh (giờ) | Vì sao |
|---|---|---|---|---|
| aitai-trades | 160,2 | 138,5 | -21,7 | Tỉ số 0,86, đạt. — |
| audit | 47,3 | 72,5 | 25,2 | Tỉ số 1,53, LỆCH. phạm vi khác: SCR120-LOG là hàm ghi log chung cho mọi route ghi; vượt cổng 0,03 |
| auth-accounts | 159,9 | 153 | -6,9 | Tỉ số 0,96, đạt. — |
| corrections | 111,6 | 102 | -9,6 | Tỉ số 0,91, đạt. — |
| data-migration | 143,6 | 84 | -59,6 | Tỉ số 0,59, LỆCH. phạm vi khác: LAB-1 đặt đều 33,6h BE mỗi công cụ; schema lỗi migrate ở SCR170-BE, không đem so |
| delivery | 113,7 | 163 | 49,3 | Tỉ số 1,43, đạt. — |
| incentive-rates | 256,3 | 331 | 74,7 | Tỉ số 1,29, đạt. — |
| lot-intake | 149,1 | 207 | 57,9 | Tỉ số 1,39, đạt. — |
| master-data | 76,7 | 149 | 72,3 | Tỉ số 1,94, LỆCH. phạm vi khác: SCR140, SCR150 gộp FE+BE, so với FUNC×BE; LAB-1 để FE ở FUNC-111/115 |
| notifications | 79,8 | 116,5 | 36,7 | Tỉ số 1,46, đạt. — |
| offline-sync | 41,9 | 69 | 27,1 | Tỉ số 1,65, LỆCH. phạm vi khác: LAB-1 xếp SCR132 và FUNC-103 vào BE, LAB-5 xếp FE |
| participants | 114,2 | 124,5 | 10,3 | Tỉ số 1,09, đạt. — |
| privacy-appi | 155,1 | 152,5 | -2,6 | Tỉ số 0,98, đạt. — |
| reports | 125,9 | 152,5 | 26,6 | Tỉ số 1,21, đạt. — |
| seri-auction | 34,6 | 62 | 27,4 | Tỉ số 1,79, LỆCH. phạm vi khác: SCR040-BE thêm người xác nhận, máy trạng thái, migration (LECH-SCR040-01/04/05) |
| settlement | 154,6 | 276 | 121,4 | Tỉ số 1,79, LỆCH. phạm vi khác: SCR063 gộp FE+BE; SCR061-GUARD chặn nhiều route; SCR062 LAB-1 xếp BE |
| **Tổng** | 1.924,4 | 2.353 | 428,6 | Tỉ số 1,22, đạt |

Hạn chế của phép so:
- Lá gộp FE+BE của màn tầng 3 chỉ gắn một vai, trong khi LAB-1 chia FUNC theo BE, FE, QA; phép so theo vai vì vậy đẩy tỉ số của master-data và settlement lên.
- `P5-S18`, `P5-S19`, `P5-A04` mô tả phạm vi của dữ liệu chủ và chuyển đổi dữ liệu nhưng chưa issue nào trỏ tới trong backlog, nên phần chênh của hai epic này chưa trỏ được về dòng PREMISE.
