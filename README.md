# Sakura Market: backlog LAB-5 · Mã học viên: Ngô Đinh Nhật Hoàng · Đề: Product A

Đề Product A: phần mềm cho ban quản lý một chợ thủy sản giả lập. Repo này chứa backlog LAB-5 được chia từ bản thiết kế LAB-4 của chính tôi, cùng báo cáo chấm SWP, quy giờ và tiến độ.

## 1. Tổng quan

- **Bản LAB-4 làm mốc:** bản nộp ngày 12/10/2026 (commit `074467c` của repo prototype, thư mục `specs` đã nộp lên Drive). Mã spec LAB-4 trong repo này ghi dạng chữ, ví dụ `SCR030_AITAI_CONFIRM_SPEC.md`.
- **PREMISE.md có thay đổi** so với LAB-4: ba bảng spec đã sửa, giả định bổ sung và hướng đã chốt. Backlog được chia theo bản đã sửa.
- **Quy mô backlog trên Project:** 17 epic, 380 item, trong đó 276 lá (issue không có con) và 104 issue cha.
- **Sprint giả lập đã chạy:** Iteration `Sprint 1` (12 item cam kết theo năng lực, 6 việc đã xong). Việc chưa cam kết vẫn ở backlog, chưa gán Iteration; `Sprint 2` được lập kế hoạch ngày 26/10/2026. Trạng thái, burndown và rủi ro ở `progress-report.md`.
- **Người phụ trách là vai giả định.** Field `Người phụ trách (giả định)` có 4 người nhận issue lá (BE-1, BE-2, FE-1, QA-1) và BrSE điều phối. Tôi không gán tài khoản GitHub thật vì repo và Project public.
- **Field `Point (SWP)` chỉ ghi SWP**, đúng tên trong đề. Giờ ước lượng nằm ở field riêng `Estimated time`.

## 2. Link

| Mục | Link |
|---|---|
| Repo | https://github.com/hoangndn-1456/hoangndn-aidd-leader-lab |
| GitHub Project (view mặc định: LAB-5 Backlog) | https://github.com/users/hoangndn-1456/projects/3 |
| View "LAB-5 Backlog": bảng đủ SWP, giờ, người phụ trách giả định, nhóm theo issue cha | https://github.com/users/hoangndn-1456/projects/3/views/16 |
| View "Sprint 1": các item của sprint giả lập | https://github.com/users/hoangndn-1456/projects/3/views/17 |
| Báo cáo HTML của skill chấm SWP | `reports/estimate-swp-hoangndn-1456-project-3-20261023-152239.html` (GitHub chỉ hiện mã nguồn; tải file về rồi mở bằng trình duyệt) |
| Bộ spec LAB-4 đã nộp (thư mục Drive) | https://drive.google.com/drive/folders/19pAtpeGNUPFsqRI2sa_7fz8qGyCpN5Gi (cần tài khoản Sun*; đã chia sẻ cho L&D và trainer) |

Ngày 25/10/2026, tôi đã mở thử repo, Project và báo cáo HTML bằng cửa sổ ẩn danh; cả ba mở được, không cần đăng nhập. Trang GitHub của file HTML hiện mã nguồn, nên cần tải file về để xem giao diện.

## 3. Cấu trúc repo

| File/thư mục | Nội dung |
|---|---|
| `README.md` | Trang này |
| `PREMISE.md` | Khác biệt so với LAB-4: spec đã sửa, giả định, hướng đã chốt |
| `task-breakdown.md` | Quy tắc chia task, spec → issue, hạng mục ràng buộc đặc thù, chỗ hở của spec |
| `estimate.md` | Issue mẫu đã kiểm tra, cách quy giờ, tổng theo epic, so sánh với LAB-1 |
| `progress-report.md` | Báo cáo tiến độ Sprint 1 giả lập |
| `AI-report.md` | Skill, agent, prompt đã dùng; cách review output AI; điểm đặc biệt và chỗ chưa tốt |
| `reports/` | Báo cáo HTML của skill `estimate-swp` và biểu đồ burndown Sprint 1 (SVG) |
| `skills/` | Định nghĩa 3 subagent tự viết cho pipeline break task |

## 4. Spec → epic

| Spec LAB-4 | Epic trên Project | Ghi chú (ràng buộc đặc thù liên quan) |
|---|---|---|
| specs/auth-accounts/README.md | #27 — Xác thực và quản lý tài khoản nội bộ | — |
| specs/participants/README.md | #28 — Quản lý bên tham gia | tư cách giao dịch 許可/承認 (BR-PERM-01) |
| specs/master-data/README.md | #29 — Dữ liệu chủ: lịch chợ và danh mục mặt hàng | — |
| specs/lot-intake/README.md | #30 — Tiếp nhận lô hàng | — |
| specs/aitai-trades/README.md | #1 — Giao dịch thỏa thuận (相対取引): chốt và hủy | hạn mức số lượng lô (BR-LOT-02), khoá ngày nghiệp vụ (BR-CLOSE-01), tư cách giao dịch 許可/承認 (BR-PERM-01) |
| specs/seri-auction/README.md | #31 — Nhập hàng loạt và tra cứu kết quả đấu giá (せり) | — |
| specs/corrections/README.md | #32 — Đính chính giao dịch đã chốt | hạn mức số lượng lô (BR-LOT-02), 完納奨励金 (BR-INC-01, GOV-RULE-01) |
| specs/settlement/README.md | #33 — Quyết toán và khóa ngày nghiệp vụ (nửa A: đối chiếu, khóa ngày, tranh chấp) | — |
| specs/incentive-rates/README.md | #34 — Thưởng hoàn thành nộp đủ và version tỷ lệ thưởng | 完納奨励金 (BR-INC-01, GOV-RULE-01): issue ràng buộc #161–#165 ở epic #42 |
| specs/delivery/README.md | #35 — Giao hàng | hạn mức số lượng lô (BR-LOT-02), hoàn tất giao hàng (BR-DEL-03) |
| specs/offline-sync/README.md | #36 — Đồng bộ ngoại tuyến và giải quyết xung đột | — |
| specs/notifications/README.md | #37 — Thông báo: gửi, thử lại, nhật ký và cấu hình | — |
| specs/reports/README.md, specs/reports/screen-specification/SCR110_REPORT_CATALOG_SPEC.md#3, specs/reports/screen-specification/SCR111_KPI_TRACKING_SPEC.md#3 | #38 — Báo cáo và theo dõi KPI nghiệm thu | — |
| specs/audit/README.md, specs/audit/screen-specification/SCR120_AUDIT_SEARCH_SPEC.md#3 | #39 — Nhật ký kiểm toán | — |
| specs/privacy-appi/README.md | #40 — Bảo vệ thông tin cá nhân theo APPI | — |
| specs/data-migration/README.md | #41 — Chuyển đổi dữ liệu | — |
| PREMISE LAB-4 §12, specs/_common/api-list.md, README LAB-4 §7 | #42 — Nền tảng chung | cộng ròng đính chính (PRE-12), hạn mức số lượng lô (BR-LOT-02), 完納奨励金 (BR-INC-01, GOV-RULE-01), hoàn tất giao hàng (BR-DEL-03), khoá ngày nghiệp vụ (BR-CLOSE-01), lô chỉ bán trong ngày (PRE-31), giữ người trong vòng lặp (CAP-HUMAN-01), thông báo (BR-NOTIFY-01), tư cách giao dịch 許可/承認 (BR-PERM-01) |

Epic Nền tảng chung chứa mọi issue ràng buộc đặc thù (nhãn `constraint:*`), TECH dùng chung, DB, ADR, nhóm API và dòng PREMISE không thuộc riêng feature nào. Bảng spec → issue chi tiết ở mục 2 của `task-breakdown.md`. Tên ràng buộc ở cột Ghi chú khớp nhãn `constraint:*` trên issue; số issue của từng ràng buộc ở mục 3 của `task-breakdown.md`.
