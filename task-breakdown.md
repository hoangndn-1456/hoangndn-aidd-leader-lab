# Chia task: từ spec LAB-4 tới backlog trên GitHub Project

Task được chia từ bộ spec LAB-4 bản nộp 12/10/2026 và các dòng `P5-*` trong `PREMISE.md`. Số liệu trong file này lấy từ dump Project và backlog đã khoá, không nhập tay.

## 1. Nguyên tắc chia task

### 1.1 Luật chia issue

Một luật chung, với ngoại lệ theo tầng của màn:

- Cấp 1, epic (`type:epic`) = một feature của LAB-4.
- Cấp 2 = một màn, một luồng TECH, một nhóm DB/API hoặc một hạng mục ràng buộc. Issue đó là **lá** (`type:devtask`, `type:testdesign`, `type:testexecution`) khi có một discipline chính và nằm gọn trong một lớp, hoặc một luồng hai lớp có giới hạn (Scope dự kiến không quá 5).
- Vượt ngưỡng đó thì issue thành **cha** `type:story` và tách sub-issue cấp 3 theo lớp (API/BE, FE, test). Mọi issue cha đều có con.
- Độ hạt theo tầng, do script ghi vào registry (cột `tang`, cờ `sprint1`): màn tầng 1 và màn có trong Sprint 1 thành story kèm sub-issue theo lớp. Màn tầng 3 đơn giản là một lá `type:devtask` có DoD gồm FE, BE, test; đây là ngoại lệ được ghi rõ của luật một discipline chính, và Scope từ 8 trở lên vẫn phải tách. Màn tầng 2 theo luật chung. Mỗi epic có ít nhất một story có sub-issue.
- Dừng tách khi lá có DoD từ 2 mục kiểm tra được trong một lượt review. Sau lần chấm nháp, lá có Scope từ 8 hoặc SWP từ 16 phải tách hoặc ghi lý do.
- Phần kiểm tra của dòng ĐẶC THÙ nằm ở issue ràng buộc. Issue màn chỉ ghi "phụ thuộc #…", không lặp lại việc đó trong DoD, để SWP không bị tính hai lần.

"DT" là dòng có cờ ĐẶC THÙ ở mục 6.3 của spec màn; "tầng" là mức quan trọng của màn theo traceability LAB-4. Tôi đặt mục tiêu khoảng 200 item trước khi chạy. Thực tế là 380 item vì các lá nằm ngay dưới epic được bọc thêm story theo guideline (mục 1.4).

### 1.2 Tiêu chí hoàn thành

- Mỗi lá có mục DoD dạng checkbox, ít nhất 2 mục kiểm tra được trong một lượt review. Validator chặn lá thiếu DoD trước khi tạo issue.
- Story và epic hoàn thành khi mọi issue con đã đóng. DoD của cha nêu tiêu chí nghiệm thu ở mức story, không chép lại DoD của lá (SWP cha là tổng con).
- Quy ước Status: issue mới tạo ở `New`; trong sprint đi theo luồng của template Sun* (`In Progress` → `In Review` → `QA Testing` → `Closed`). Trạng thái thực tế sau Sprint 1 nằm trong `progress-report.md`.

### 1.3 Ba cấp trên Project

| Cấp | Tracker trên GitHub | Số item |
|---|---|---|
| Epic (một feature LAB-4, cộng epic Nền tảng chung) | `[Epic]`, nhãn `type:epic` | 17 |
| Story (một màn, một luồng TECH, hoặc nhóm epic × loại việc) | `[Story]`, nhãn `type:story` | 87 |
| Lá: việc lập trình | `[Dev Task]`, nhãn `type:devtask` + `team:*` | 224 |
| Lá: thiết kế test | `[Test Design]`, nhãn `type:testdesign` | 40 |
| Lá: chạy test | `[Test Execution]`, nhãn `type:testexecution` | 12 |

Quan hệ cha con dùng sub-issue thật của GitHub (field `Parent issue`), không dùng checklist trong body. Mỗi issue có khối "Mã spec" và "Registry" trong body để tra ngược về spec LAB-4.

### 1.4 So với Sun* GitHub Project Guideline v1.2

Đề không bắt buộc theo guideline này. Tôi chọn theo vì đây là chuẩn vận hành của Sun*.

| Mục guideline | Cách làm ở Project này | Đánh giá |
|---|---|---|
| Tracker và nhãn `type:*` (mục 3.1) | Có đủ 5 tracker đang dùng: Epic, Story, Dev Task, Test Design, Test Execution | Theo |
| Cấu trúc Epic → Story → Task (mục 4.1) | Các lá nằm trực tiếp dưới epic đã được bọc bằng story ngày 22–23/10; không còn lá nào nằm ngay dưới epic | Theo |
| Tiêu đề `[Tracker] Tên công việc` (mục 5.3) | Mọi tiêu đề có tiền tố tracker. Mã màn hoặc mã luật đứng sau tiền tố (`[Dev Task] SCR030 · …`). Trước 22/10, tôi giữ tiêu đề không có tiền tố để tra ngược về spec. Các tiêu đề đã đổi sang `[Tracker]`, nên không còn lệch guideline | Theo |
| Dev Task gắn `team:frontend` / `team:backend` | Dev Task của BE-1, BE-2 gắn `team:backend`, của FE-1 gắn `team:frontend`, màn tầng 3 gộp FE+BE gắn cả hai | Theo; Dev Task của BrSE (hỏi khách) không gắn team vì không phải việc lập trình |
| Field `Estimated time` (giờ) | Ghi số giờ ước lượng cho từng issue (đổi tên từ `Giờ ước` ngày 22/10) | Theo |
| Field `Priority`: Critical, High, Medium, Low | 380/380 item có giá trị. Agent đề xuất mức theo 4 tiêu chí (chặn Sprint 1 hoặc ràng buộc pháp lý; luồng chính; việc thường; màn tầng 3 và việc làm rõ không chặn). Mỗi item có một dòng lý do. Tôi duyệt phân bố và ngoại lệ; script ghi sau câu "go priority" | Theo |
| Field `Story Point` | Dùng field `Point (SWP)` thay cho Story Point | Lệch có lý do: đề bắt buộc trường point chỉ ghi SWP |
| Assignee bắt buộc (mục 5.3) | Dùng field `Người phụ trách (giả định)`: BE-1, BE-2, FE-1, QA-1, BrSE | Lệch có lý do: repo public, không gán tài khoản thật |
| Milestone cho Sprint và burn-down (mục 5.5) | Dùng field `Iteration` cho sprint, không tạo Milestone | Lệch tự chọn: đề bắt buộc dùng Iteration; chỉ xếp sprint ở một nơi để tránh hai nguồn lệch nhau |
| Target Version | Chưa dùng | Lệch có lý do: backlog chưa chia bản phát hành |

### 1.5 Lệch so với kế hoạch ban đầu

Kế hoạch ban đầu có một bản chụp SWP, giờ, Iteration và người phụ trách của mọi item, lưu trước khi đổi trạng thái cho Sprint giả lập. Bản chụp này không được tạo: lần áp đầu của Sprint 1 chạy sáng 24/10, trong lúc phần ghi Priority còn đang chạy, nên bản chụp sau đó sẽ chứa trạng thái giả lập và sai ý nghĩa. Thay vào đó tôi giữ bản dump Project chụp trước Sprint 1 (đủ SWP và giờ, mọi item còn `New`) và bản lưu giá trị cũ của các lệnh ghi, để khôi phục khi cần. Các file này nằm ngoài repo nộp.

## 2. Spec → issue

Bảng bao phủ mọi spec màn, TECH, DB, ADR, nhóm API, dòng hẹn và dòng bỏ qua trong registry. Số lượng gồm 59 SCR, 6 TECH, 12 DB, 5 ADR, 5 nhóm API. Các dòng LỆCH (262), FUNC (146) và ĐẶC THÙ (86) cũng nằm trong registry. Validator kiểm tra mỗi dòng thuộc đúng một issue hoặc nằm trong danh sách chưa thành issue.

| Spec (mã LAB-4) | Epic | Issue/sub-issue | Phần spec chưa thành issue và vì sao |
|---|---|---|---|
| SCR030 | #1 | #2, #6, #7, #8, #9, #10, #11, #12, #13, #14 | — |
| SCR031 | #1 | #3, #15, #16, #17, #18 | — |
| SCR032 | #1 | #4, #19, #20, #21, #22, #23, #24 | — |
| SCR120 | #39 | #118, #317, #318, #319, #320, #321, #322 | — |
| SCR000 | #27 | #46, #334 | — |
| SCR001 | #27 | #47, #335 | — |
| SCR002 | #27 | #48, #336 | — |
| SCR003 | #27 | #49, #50, #337 | — |
| SCR004 | #27 | #51, #200, #201, #202 | — |
| SCR050 | #32 | #80, #242, #243, #244 | — |
| SCR051 | #32 | #81, #245, #246, #247, #248 | — |
| SCR052 | #32 | #82, #249, #250, #251 | — |
| SCR170 | #41 | #132, #326, #327, #328, #329 | — |
| SCR090 | #35 | #101, #291, #292, #293, #294 | — |
| SCR091 | #35 | #102, #295, #296, #297 | — |
| SCR092 | #35 | #103, #298, #299, #300, #301 | — |
| SCR093 | #35 | #104, #358 | — |
| SCR094 | #35 | #105, #302, #303, #304, #305 | — |
| SCR070 | #34 | #95, #277, #278, #279, #280 | — |
| SCR071 | #34 | #96, #355 | — |
| SCR080 | #34 | #97, #281, #282, #283, #284, #285 | — |
| SCR081 | #34 | #98, #356 | — |
| SCR121 | #34 | #99, #357 | — |
| SCR160 | #34 | #100, #286, #287, #288, #289, #290 | — |
| SCR020 | #30 | #69, #221, #222, #223 | — |
| SCR021 | #30 | #70, #346 | — |
| SCR022 | #30 | #71, #224, #225, #226 | — |
| SCR023 | #30 | #72, #73, #347 | — |
| SCR024 | #30 | #74, #227, #228, #229, #230 | — |
| SCR130 | #30 | #75, #348 | — |
| SCR140 | #29 | #66, #344 | — |
| SCR141 | #29 | #67, #216, #217, #218, #219, #220 | — |
| SCR150 | #29 | #68, #345 | — |
| SCR100 | #37 | #111, #361 | — |
| SCR101 | #37 | #112, #362 | — |
| SCR132 | #36 | #109, #306, #307, #308 | — |
| SCR010 | #28 | #54, #339 | — |
| SCR011 | #28 | #55, #56, #340 | — |
| SCR012 | #28 | #57, #203, #204, #205 | — |
| SCR013 | #28 | #58, #206, #207, #208 | — |
| SCR014 | #28 | #59, #209, #210, #211 | — |
| SCR015 | #28 | #60, #341 | — |
| SCR016 | #28 | #61, #342 | — |
| SCR017 | #28 | #62, #212, #213 | — |
| SCR018 | #28 | #63, #214, #215 | — |
| SCR133 | #40 | #124, #366 | — |
| SCR134 | #40 | #125, #323, #324, #325 | — |
| SCR180 | #40 | #126, #330, #331, #332 | — |
| SCR181 | #40 | #127, #367 | — |
| SCR110 | #38 | #116, #314, #315, #316 | — |
| SCR111 | #38 | #117, #364 | — |
| SCR040 | #31 | #76, #231, #232, #233, #234 | — |
| SCR041 | #31 | #77, #235, #236, #237, #238 | — |
| SCR060 | #33 | #86, #252, #253, #254, #255, #256, #257 | — |
| SCR061 | #33 | #87, #258, #259, #260, #261, #262 | — |
| SCR062 | #33 | #88, #263, #264, #265, #266, #267 | — |
| SCR063 | #33 | #89, #351 | — |
| SCR064 | #33 | #90, #268, #269, #270, #271, #272, #273 | — |
| SCR131 | #33 | #91, #352 | — |
| AITAI_CONFIRM_TECH | #1 | #5 | — |
| CORRECTION_APPROVE_TECH | #32 | #79 | — |
| INCENTIVE_CARRYOVER_TECH | #34 | #92 | — |
| NOTIFY_RETRY_TECH | #37 | #110 | — |
| OFFLINE_REPLAY_TECH | #36 | #108 | — |
| DAY_LOCK_TECH | #33 | #259 | — |
| AUDIT_DB | #42 | #144 | — |
| DELIVERY_DB | #42 | #145 | — |
| INCENTIVE_DB | #42 | #147 | — |
| LOT_DB | #42 | #148 | — |
| MARKET_CALENDAR_DB | #42 | #149 | — |
| PARTY_DB | #42 | #152 | — |
| PLATFORM_DB | #42 | #154 | — |
| SETTLE_DB | #42 | #197 | — |
| TRADE_DB | #42 | #199 | — |
| MIGRATION_DB | #42 | #150 | — |
| NOTIFY_DB | #42 | #151 | — |
| PRIVACY_DB | #42 | #155 | — |
| ADR-01 | #42 | #133 | — |
| ADR-02 | #42 | #134 | — |
| ADR-03 | #42 | #135 | — |
| ADR-04 | #42 | #136 | — |
| ADR-05 | #42 | #137 | — |
| API-G1 | #42 | #139 | — |
| API-G2 | #42 | #140 | — |
| API-G3 | #42 | #141 | — |
| API-G4 | #42 | #142 | — |
| API-G5 | #42 | #143 | — |
| SKIP-1 | #42 | #138 | — |
| SKIP-2 | #42 | #153 | — |
| SKIP-3 | #42 | #196 | — |
| SKIP-4 | #42 | #146 | — |
| HEN-BM52 | — | — | P5-S06 đã chốt: LAB-5 không viết tài liệu BM-2-901-52. Hợp đồng API nằm trong DoD của từng issue API (E17-APIG1 đến E17-APIG5) và ở epic sở hữu API. |
| HEN-BM54 | — | — | BM-2-901-54 là tài liệu mức hàm, không phải việc phát triển của nền tảng chung. P5-S07 đã chốt: không viết ở LAB-5. Đặc tả hàm nằm trong tiêu chí hoàn thành của issue code liên quan, không tách issue riêng. |
| HEN-TOKYO | #42 | #198 | — |

Có 13 dòng registry chưa thành issue; lý do ghi bên dưới:

| Dòng registry | Vì sao chưa thành issue |
|---|---|
| FUNC-023 | Spec của màn nhập lô chưa mô tả máy trạng thái vòng đời lô: SCR020, SCR021, SCR022 không có trạng thái lô, nên chưa đủ cơ sở viết DoD kiểm tra được. Để mở; cần bổ sung spec trước, chưa xếp vào issue nào. |
| FUNC-027 | Việc ghi trước/sau và lý do khi điều chỉnh lô thuộc màn SCR024 (Điều chỉnh thuộc tính lô). Spec SCR024 nằm ngoài phần đã chia nên chưa có issue; để mở, chưa gắn vào issue SCR024. |
| FUNC-037 | FUNC-037 là ràng buộc CAP-HUMAN-01 (chặn đường nhập tự động); spec đánh dấu ĐẶC THÙ ở L10 và phần truy vết. Issue ràng buộc đặc thù đã phụ trách phần kiểm tra; tách thêm một issue ở đây sẽ tính SWP hai lần. |
| FUNC-045 | Chặn sửa trực tiếp ngày đã khóa là ràng buộc BR-CLOSE-01 (dòng ĐẶC THÙ), do issue ràng buộc xử lý. Phần spec đã chia không có route nào thực hiện việc chặn, và TECH ghi rõ không kiểm tra ngày khóa. |
| FUNC-096 | Tích hợp máy in nhiệt thuộc nhóm in ấn FG-14; đặc tả ở SCR130, ngoài phần đã chia. SCR020-Q8 (in phiếu ngay sau đăng ký) còn mở nên chưa có cơ sở viết DoD. |
| FUNC-098 | Thiết kế bố cục chứng từ in thuộc nhóm FG-14; đặc tả ở SCR130, ngoài phần đã chia. Để mở, chưa gắn vào issue SCR130. |
| FUNC-099 | Xuất PDF cho 4 biểu mẫu còn lại thuộc nhóm FG-14; phần spec đã chia không có màn hay mục spec tương ứng. Để mở; việc viết spec này ghi ở P5-S17, chưa có issue riêng. |
| HEN-BM52 | P5-S06 đã chốt: LAB-5 không viết tài liệu BM-2-901-52. Hợp đồng API nằm trong DoD của từng issue API (E17-APIG1 đến E17-APIG5) và ở epic sở hữu API. |
| HEN-BM54 | BM-2-901-54 là tài liệu mức hàm, không phải việc phát triển của nền tảng chung. P5-S07 đã chốt: không viết ở LAB-5. Đặc tả hàm nằm trong tiêu chí hoàn thành của issue code liên quan, không tách issue riêng. |
| LECH-SCR060-02 | CSV của RPT-05 đặt ở SCR110 thuộc epic báo cáo; vị trí còn chờ SCR060-Q15. SCR060 chỉ giữ bản màn hình nên không có việc ở epic quyết toán. |
| LECH-SCR060-03 | Bản in A4 theo FORM-SETTLE-01 thuộc SCR131, có spec riêng trong cùng epic. SCR060-Q7 đã đóng ngày 08/10, xác định E-1 không thay được SCR131. Liên kết sang SCR131 nằm ở E08-SCR060-FE-NAV. |
| LECH-SCR060-06 | Phần thiếu gồm CSV và các trường của bản in A4 (số chênh lệch, 備考, 確認者, 出力日時, 出力者), thuộc SCR131 và SCR110. E-1 giữ nguyên là bản in tạm. |
| LECH-SCR060-15 | Ngày nghiệp vụ theo lịch chợ cần bảng lịch của SCR140, SCR141 (tầng 3, epic khác). Nguồn cấp lịch chưa chốt (SCR060-Q9, câu QA Q21), nên chưa có đầu vào để làm. |

## 3. Hạng mục chịu ràng buộc đặc thù

Mọi dòng ĐẶC THÙ (86 dòng) thuộc issue ràng buộc riêng trong epic Nền tảng chung, nhãn `constraint:*`. Issue màn chỉ ghi phụ thuộc tới issue ràng buộc, không lặp lại việc đó trong DoD, nên SWP không bị tính hai lần. 完納奨励金 đứng đầu bảng.

| Ràng buộc | Nhóm (nhãn) | Số dòng ĐẶC THÙ | Issue | Vì sao tách riêng |
|---|---|---|---|---|
| 完納奨励金 (thưởng hoàn thành nộp đủ): BR-INC-01, GOV-RULE-01 | hoan-nap-khen-thuong | 9 | #161, #162, #163, #164, #165 | Quy tắc riêng của chợ này: bảng tỷ lệ có phiên bản, maker-checker, hạn mức đổi bảng mỗi năm, làm tròn theo JPY. Tính sai sẽ trả sai tiền cho bên mua; vẫn còn điểm phải hỏi khách |
| Tư cách giao dịch 2 cấp 許可 / 承認: BR-PERM-01 | tu-cach-giao-dich | 28 | #182, #183, #184, #185, #186, #187, #188, #189, #190, #191, #192, #193, #194 | Hai cấp quyền pháp lý khác nhau theo loại bên. Một bộ kiểm tra dùng chung cho màn quản lý bên, giao dịch 相対 và nhập kết quả せり. 許可 và 承認 tách thành issue riêng |
| Khoá ngày nghiệp vụ: BR-CLOSE-01 | khoa-ngay | 21 | #166, #167, #168, #169, #170, #171, #172, #173 | Mọi route ghi phải chặn ngày đã khoá. Bước kiểm tra và ghi phải nằm trong cùng transaction, nên triển khai và test một lần ở tầng chung |
| Hạn mức số lượng lô: BR-LOT-02 | han-muc-lo | 14 | #174, #175, #176, #177, #178 | Ba luồng (相対, せり, đính chính) cùng trừ số khả dụng của lô. Tách riêng để kiểm tra tính nguyên tử và chống bán vượt ở một chỗ |
| Hoàn tất giao hàng: BR-DEL-03 | hoan-tat-giao-hang | 8 | #157, #158, #159, #160 | Chỉ thị giao hàng sinh từ giao dịch và chặn khoá ngày; liên quan cả giao dịch, giao hàng và quyết toán |
| Giữ người trong vòng lặp: CAP-HUMAN-01 | nguoi-trong-vong-lap | 2 | #180, #181 | Kết quả せり phải do người nhập. Đặc thù này không thể số hoá toàn bộ, cần hỏi khách cách chặn |
| Thông báo: BR-NOTIFY-01 | thong-bao | 2 | #195 | Quy tắc thử lại dùng chung cho mọi thông báo |
| Đối soát cộng ròng đính chính: PRE-12 | cong-rong-dinh-chinh | 1 | #156 | 反対仕訳 và 訂正後 phải cộng ròng đúng trong ngày; ảnh hưởng quyết toán |
| Lô chỉ bán trong ngày của lô: PRE-31 | lo-trong-ngay | 1 | #179 | Luật lô theo ngày nghiệp vụ dùng chung cho mọi luồng bán |

## 4. Chỗ hở của spec LAB-4 tìm thấy khi chia task

Cột "Xử lý" chỉ dùng một trong bốn cách của đề.

| Spec | Chỗ hở/mâu thuẫn | Xử lý |
|---|---|---|
| README LAB-4 §7.1 | README ghi 280 dòng LỆCH; registry đếm theo dòng bảng mục 6.3 ra số khác. Nhiều dòng ghi cờ kèm tham chiếu tới dòng khác | để mở vì không ép số cho khớp; registry nối nhóm tham chiếu, validator bắt buộc các dòng cùng nhóm thuộc một issue |
| CSV 146 FUNC (LAB-3) | Một phần FUNC ghi màn là `-` (việc nền), không thể bao phủ gián tiếp qua màn | để mở vì không có màn để gắn; registry bao phủ trực tiếp các FUNC này, gán epic theo epic chiếm đa số trong nhóm FG |
| SCR094 (P5-S20) | SCR094-Q3 ghi người trả lời là khách và còn mở; P5-S20 đóng nội bộ theo phương án A mà không hỏi khách | để mở vì đã chốt nội bộ, không tạo issue xác nhận; tiêu chí hoàn thành của issue code SCR094 có phần sửa câu hỏi đó |
| SCR093, SCR060, SCR061, SCR131 (P5-A05) | Ba nguồn nêu ba điều kiện "giao hàng tồn đọng" khác nhau | giả định (P5-A05); không tạo issue xác nhận riêng, câu hỏi nằm trong tiêu chí hoàn thành của #104 |
| `AITAI_CONFIRM_TECH.md` F-1; SCR030, SCR032 | Khi chuyển trạng thái giao dịch, hệ thống không kiểm tra lại tư cách bên mua | đã sửa thiết kế (P5-S01) |
| `AITAI_CONFIRM_TECH.md` F-2; SCR040 | Luồng nhập hàng loạt せり không đọc `Idempotency-Key`, gửi lại thì ghi trùng | đã sửa thiết kế (P5-S02) |
| `CORRECTION_APPROVE_TECH.md` F-1; SCR050, SCR052 | Bước kiểm tra hạn mức lô chỉ chạy với giao dịch thường, bỏ sót dòng sau đính chính | đã sửa thiết kế (P5-S03) |
| `OFFLINE_REPLAY_TECH.md` G-1 | Lỗi 400 không được xếp vào nhóm lỗi vĩnh viễn, làm chặn cả hàng đợi | đã sửa thiết kế (P5-S04) |
| `OFFLINE_REPLAY_TECH.md` G-2; SCR020 | Lần gửi online đầu không có key chống ghi trùng | đã sửa thiết kế (P5-S05) |
| BM-2-901-52 API Design | README LAB-4 hẹn tài liệu này cho LAB-5 | đã sửa thiết kế (P5-S06) |
| BM-2-901-54 Function Specifications | README LAB-4 hẹn tài liệu này cho LAB-5 | đã sửa thiết kế (P5-S07) |
| `INCENTIVE_CARRYOVER_TECH.md` F-1..F-3 | Cách đếm hạn mức đổi bảng tỷ lệ khác GOV-RULE-01; bước tạo version có race | đã sửa thiết kế (P5-S08) |
| SCR132 mục 6.3 L1 | API giải quyết xung đột đồng bộ chỉ kiểm tra đăng nhập, chưa kiểm tra vai trò | đã sửa thiết kế (P5-S09) |
| `_common/api-list.md` | Thiếu API cho màn tầng 3, chỉ liệt kê ở README | đã sửa thiết kế (P5-S10) |
| API-035 | Thiếu tham số ngày nghiệp vụ và schema phản hồi | đã sửa thiết kế (P5-S11) |
| `docs/permission-matrix.md` | Thứ tự kiểm tra của route chuyển trạng thái giao dịch chưa khớp TECH | đã sửa thiết kế (P5-S12) |
| `SERI_BULK_ENTRY` | Chưa có TECH riêng cho nhập hàng loạt せり | đã sửa thiết kế (P5-S13) |
| FUNC-136; SCR030 | 参加上限 chưa có cột lưu, chưa định nghĩa hạn mức | đã sửa thiết kế (P5-S14) |
| SCR040, SCR041; `TRADE_DB.md` | Kết quả せり không lưu người và thời điểm xác nhận | đã sửa thiết kế (P5-S15) |
| `_common/error-codes.md` | Mã lỗi nằm rải rác trong nhiều spec, không có danh mục chung | để mở vì danh mục mã lỗi chung (P5-S16) đã nêu ở PREMISE nhưng backlog chưa có issue riêng để viết; việc này chưa xếp vào sprint nào |
| FUNC-099 | Xuất PDF biểu mẫu chỉ có một câu trong PREMISE LAB-4 | để mở vì spec xuất PDF 4 biểu mẫu (P5-S17) đã nêu ở PREMISE nhưng backlog chưa có issue riêng; việc này chưa xếp vào sprint nào |
| FUNC-122, FUNC-126; SCR170 | Hai FUNC migrate chỉ là nhãn, chưa có thiết kế | đã sửa thiết kế (P5-S18) |
| `AITAI_CONFIRM_TECH.md` mục 4.2; `MARKET_CALENDAR_DB.md` | Ngày nghiệp vụ hiện tại tính từ 50 lô gần nhất, sai khi ngày mới nhất đã khoá | đã sửa thiết kế (P5-S19) |
| SCR094; SCR091, SCR092 | Giao vượt số chỉ thị vẫn xác nhận hoàn tất được | đã sửa thiết kế (P5-S20) |
| Nhãn 交付率 | Nhãn chưa có chú giải, dễ đọc nhầm thành tỷ lệ giao hàng | đã sửa thiết kế (P5-S21) |
| SCR032-Q6 | Chữ "chốt" trong BR-PERM-01 chưa rõ là tạo nháp hay đạt 確定 | giả định (P5-A01) |
| PREMISE LAB-4 "Nơi lưu dữ liệu"; ADR-05 | Chưa chọn region khi dựng môi trường | giả định (P5-A02) |
| SCR030-Q7 | 参加上限 chưa nêu đơn vị và chỗ lưu | giả định (P5-A03) |
| SCR141 | Chưa rõ có tính lại hạn khi lưu lịch chợ hay không, cũng chưa có cách làm | giả định (P5-A04) |
| SCR093-Q2 | Định nghĩa giao hàng tồn đọng | giả định (P5-A05) |
| SCR071 L10 | Chưa rõ 基準額 của thưởng lấy từ đâu | giả định (P5-A06) |
