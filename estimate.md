# Ước lượng: skill chấm SWP, quy đổi ra giờ bằng một hệ số

Báo cáo HTML của skill `estimate-swp`: [`reports/estimate-swp-hoangndn-1456-project-3-20261023-152239.html`](reports/estimate-swp-hoangndn-1456-project-3-20261023-152239.html)

Trang GitHub của file này hiện mã nguồn HTML; muốn xem giao diện thì tải file về rồi mở bằng trình duyệt. Chế độ xem Giờ trong trang dùng hệ số mặc định 1 giờ/SWP (ra 1.400 giờ), nên giờ chính thức là số ở mục 2 và mục 3 bên dưới (hệ số 3,625).

Skill chấm 276 issue lá trên chính Project này ở mức `--level max` với hai assessor độc lập A và B. Điểm của issue cha là tổng điểm các issue con. Skill chỉ xuất báo cáo. Script ghi SWP đã chốt vào field `Point (SWP)`; cách làm được mô tả trong `AI-report.md`.

## 1. Issue mẫu skill chọn để kiểm tra

Skill tự chọn các issue đại diện: nhỏ nhất (#120), mức trung vị (#12), lớn nhất (#286), ngoại lai (#48) và một issue hai assessor chấm khác nhau (#8).

| Issue | Skill chấm (Scope × Complexity → SWP) | Bạn chốt | Lý do |
|---|---|---|---|
| #120 — [Dev Task] FUNC106 · Đánh dấu bản ghi hết thời hạn lưu trữ | 1 × 1 → 1 | 1 (giữ nguyên) | Một logic đánh dấu theo hạn 7 năm, không xóa bản ghi, không có luồng phê duyệt xóa (ngoài phạm vi). DoD có ba dòng, gồm một ca ranh giới. Đây là việc nhỏ nhất của backlog nên 1 là hợp lý. |
| #12 — [Dev Task] SCR030 · Màn form chốt giao dịch (B-3 đến B-9) | 3 × 2 → 5 | 5 (giữ nguyên) | Một màn FE (form B-3 đến B-9, kiểm tra phía client, quản lý khóa chống gửi lặp). Điểm khó duy nhất là sinh khóa mới khi đổi một trong bốn ô, nên độ phức tạp ở mức vừa. Scope 3 cho một màn. |
| #286 — [Dev Task] SCR160 · API-150 nhập và kiểm tệp xác nhận thanh toán | 5 × 3 → 10 | 10 (giữ nguyên) | Một API phải làm bốn việc: kiểm tra quyền, kiểm tra định dạng tệp, phát hiện trùng trước khi nhận, ghi hai bảng. Ngoài ra phải thêm migration và viết tài liệu định dạng tệp đầu vào vì chiều vào chưa có định dạng. DoD có năm dòng nên Scope 5, Complexity 3. |
| #48 — [Dev Task] SCR002 · Xác thực hai bước (MFA) cho vai quản trị và phê duyệt | 5 × 3 → 10 | 10 (giữ nguyên) | Phạm vi xác thực gồm màn FE, kiểm tra mã qua server action, xác định tài khoản thuộc diện MFA, chặn truy cập trước bước hai. DoD có sáu dòng. Lỗi ở bước xác thực ảnh hưởng mọi vai nên Complexity 3. |
| #8 — [Dev Task] SCR030 · Migration: CHECK đơn giá và chỗ lưu 参加上限 | 2 × 2 → 3 | 3 (giữ nguyên) | Hai assessor chấm lệch nhau (A 3, B 5). Tôi chốt 3: phần làm được ngay là CHECK đơn giá; phần cột lưu 参加上限 và kiểm khi chốt chỉ làm sau khi khách trả lời SCR030-Q7 (DoD ghi: chưa có đáp án thì item dừng chờ). Rủi ro đã biết: #146 cũng tạo cột lưu 参加上限 (bước 2 là migration thêm cột), nên phần cột có thể bị tính hai lần giữa #8 và #146. #146 còn yêu cầu ghi câu trả lời của khách trước khi viết migration, nhưng #8 đã vào Sprint 1 còn #146 chưa làm. Tôi chưa chấm lại #8, vì đổi #8 kéo theo tổng của Sprint 1 và các tổng epic. |

Tôi giữ nguyên điểm của skill cho cả năm mẫu (hai vòng hỏi trong skill, cả hai vòng đều chọn đề xuất của skill). Agent soạn lý do trong bảng từ phạm vi và DoD của từng issue, tôi duyệt. Bước này chưa chứng minh tôi đã phản biện skill. Phép kiểm tra độc lập nằm ở bộ đáp án mẫu (`AI-report.md` mục 2.3).

## 2. Cách quy ra giờ

- **Cách chọn:** quy ước đổi SWP ra giờ bằng một hệ số `r` (giờ trên một SWP), không ước lượng trực tiếp từng issue.
- **Vì sao:** SWP đo khối lượng việc, không phụ thuộc người làm. Dùng chung một hệ số cho mọi lá giúp giờ nhất quán giữa các issue. Khi đổi bối cảnh (ví dụ đội dùng AIDD), chỉ cần đổi `r`. Ước lượng trực tiếp hàng trăm issue thì mỗi issue một kiểu suy đoán, không kiểm tra lại được.
- **Neo:** dùng các lá của bộ đáp án mẫu (10/10 lá có giờ neo), chọn theo tầng loại việc. Một agent độc lập (không thấy điểm của skill) ước lượng giờ từng lá từ dưới lên, liệt kê việc nhỏ kèm giờ.
- **Bối cảnh giờ neo:** dev mid 3 năm, đội **không dùng AIDD**, giờ gồm code, unit test, review và sửa lỗi. Một neo là việc BrSE hỏi khách, ước lượng theo giờ BrSE. Đổi sang đội dùng AIDD thì phải đo lại `r`, không dùng chung số này.
- **Quy tắc:**
  - `r` = trung vị của (giờ neo ÷ SWP skill chốt) trên 10/10 neo = **3,625 giờ/SWP**; khoảng P25–P75 = 3,25–3,94. Dùng trung vị vì số neo ít, một neo lệch không kéo lệch cả hệ số.
  - Giờ của lá = SWP × `r`, làm tròn theo bước 0,5 giờ (nửa bước, tức 0,25 giờ, làm tròn lên; ví dụ 2 SWP × 3,625 = 7,25 giờ → 7,5 giờ), tối thiểu 0,5 giờ.
  - Giờ của issue cha = tổng giờ con, không làm tròn lại.
- **Áp dụng nhất quán:** script tính giờ cho mọi lá từ cùng một `r`, rồi ghi vào field `Estimated time`; không sửa tay giờ của issue nào.

## 3. Tổng theo epic

Số issue chỉ tính các lá; SWP và giờ lấy từ field của Project rồi cộng trên các lá.

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

Chỉ so sánh phần giao nhau: chức năng (FUNC) × vai BE, FE, QA, cùng bối cảnh không AIDD, trước buffer. LAB-1 đổi từ người-ngày theo 7 giờ/người-ngày. Phạm vi so sánh được là 134/146 FUNC, 121/276 lá LAB-5. Phần còn lại không ghép được một-một nên không đem so sánh, không chia đều. Ngưỡng được ghi trước khi so sánh: tỉ số LAB-5/LAB-1 trong khoảng [0.7; 1.5].

| Phần (epic) | LAB-1 (giờ) | LAB-5 (giờ) | Chênh (giờ) | Vì sao |
|---|---|---|---|---|
| aitai-trades | 160,2 | 138,5 | -21,7 | Tỉ số 0,86, đạt. Lá chuyển trạng thái và lá test SCR032 chịu P5-S01, P5-S12, P5-A01 (36 giờ trong 138,5); LAB-5 vẫn thấp hơn LAB-1 nên không tìm thêm nguyên nhân. |
| audit | 47,3 | 72,5 | 25,2 | Tỉ số 1,53, LỆCH, vượt ngưỡng 0,03. Phạm vi khác: SCR120-LOG là hàm ghi log chung cho mọi route ghi. |
| auth-accounts | 159,9 | 153 | -6,9 | Tỉ số 0,96, đạt. Không lá so được nào trỏ tới dòng P5-*; chênh nhỏ nên không tìm nguyên nhân riêng. |
| corrections | 111,6 | 102 | -9,6 | Tỉ số 0,91, đạt. Một lá chịu P5-S03 (kiểm hạn mức lô cho dòng sau đính chính, 36,5 giờ); các lá còn lại không trỏ tới dòng P5-*. |
| data-migration | 143,6 | 84 | -59,6 | Tỉ số 0,59, LỆCH. Phạm vi khác: LAB-1 đặt đều 33,6h BE cho mỗi công cụ. Schema lỗi migrate ở SCR170-BE không được đưa vào so sánh. P5-S18 (#128, #131): FUNC-122 và FUNC-126 là hai lá LAB-5 viết thiết kế mới, 33 giờ trong 84. |
| delivery | 113,7 | 163 | 49,3 | Tỉ số 1,43, đạt nhưng sát ngưỡng. Hai lá chịu dòng PREMISE: SCR091-BE (P5-S20, từ chối giao vượt số khả dụng của lô, 18 giờ) và SCR093 (P5-A05, định nghĩa giao hàng tồn đọng, 29 giờ), tổng 47 giờ trong 163. Phần chênh gần bằng con số này; tôi chưa tách riêng giờ của phần PREMISE thêm. |
| incentive-rates | 256,3 | 331 | 74,7 | Tỉ số 1,29, đạt. Bốn lá chịu dòng PREMISE: SCR080-BE-LIMIT, SCR080-TEST và SCR081 (P5-S08, đếm hạn mức đổi bảng theo GOV-RULE-01), cùng SCR080-FE (P5-S21, chú giải nhãn 交付率); tổng 109,5 giờ trong 331, lớn hơn phần chênh +74,7 giờ. |
| lot-intake | 149,1 | 207 | 57,9 | Tỉ số 1,39, đạt. Hai lá SCR020 (BE và test) chịu P5-S05 và P5-H05 (key chống ghi trùng ngay lần gửi online đầu), tổng 65,5 giờ trong 207. Phần chênh gần bằng con số này; tôi chưa tách riêng giờ của phần PREMISE thêm. |
| master-data | 76,7 | 149 | 72,3 | Tỉ số 1,94, LỆCH. Phạm vi khác: SCR140, SCR150 gộp FE+BE nhưng được so với FUNC×BE; LAB-1 để FE ở FUNC-111/115. Lá SCR141 tính lại hạn (#218) chịu P5-A04, 36,5 giờ. |
| notifications | 79,8 | 116,5 | 36,7 | Tỉ số 1,46, đạt nhưng sát ngưỡng 1,5. Không lá so được nào trỏ tới dòng P5-*; tôi chưa tìm ra nguyên nhân về phạm vi. |
| offline-sync | 41,9 | 69 | 27,1 | Tỉ số 1,65, LỆCH. Phạm vi khác: LAB-1 xếp SCR132 và FUNC-103 vào BE, LAB-5 xếp vào FE. |
| participants | 114,2 | 124,5 | 10,3 | Tỉ số 1,09, đạt. Không lá so được nào trỏ tới dòng P5-*. |
| privacy-appi | 155,1 | 152,5 | -2,6 | Tỉ số 0,98, đạt. Không lá so được nào trỏ tới dòng P5-*. |
| reports | 125,9 | 152,5 | 26,6 | Tỉ số 1,21, đạt. Không lá so được nào trỏ tới dòng P5-*. |
| seri-auction | 34,6 | 62 | 27,4 | Tỉ số 1,79, LỆCH. Phạm vi khác: SCR040-BE thêm người xác nhận, máy trạng thái, migration (LECH-SCR040-01/04/05). Mã PREMISE của hai lá SCR040: P5-S15, P5-H02 (BE) và P5-S02 (test). |
| settlement | 154,6 | 276 | 121,4 | Tỉ số 1,79, LỆCH. Phạm vi khác: SCR063 gộp FE+BE; SCR061-GUARD chặn nhiều route; LAB-1 xếp SCR062 vào BE. Lá SCR131 chịu P5-S11, 29 giờ. |
| **Tổng** | 1.924,4 | 2.353 | 428,6 | Tỉ số 1,22, đạt |

Các dòng được làm tròn một chữ số thập phân, còn tổng tính trên số chưa làm tròn; cộng các dòng sẽ ra 1.924,5 thay vì 1.924,4 (chênh 428,5 thay vì 428,6).

Hạn chế của phép so sánh:

- Lá gộp FE+BE của màn tầng 3 chỉ gắn một vai, trong khi LAB-1 chia FUNC theo BE, FE, QA. Vì vậy, phép so sánh theo vai đẩy tỉ số của master-data và settlement lên.
- `P5-S18` (#128, #131) và `P5-A04` (#218) có issue trỏ tới và các issue đó nằm trong phần so được, nên đã ghi ở dòng data-migration và master-data. `P5-S19` (#6, #83, #149) cũng có issue trỏ tới, nhưng các issue đó không thuộc phần so được, nên không giải thích được phần chênh của epic nào ở bảng trên.
