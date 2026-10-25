# Sakura Market: backlog LAB-5 · Mã học viên: Ngô Đinh Nhật Hoàng · Đề: Product A

Đề Product A: phần mềm cho ban quản lý một chợ thủy sản giả lập. Repo này chứa backlog LAB-5 break từ bản thiết kế LAB-4 của chính tôi, cùng báo cáo chấm SWP, quy giờ và tiến độ.

## 1. Tổng quan

- **Bản LAB-4 làm mốc:** bản nộp ngày 12/10/2026 (commit `074467c` của repo prototype, thư mục `specs` đã nộp lên Drive). Mã spec LAB-4 trong repo này ghi dạng chữ, ví dụ `SCR030_AITAI_CONFIRM_SPEC.md`.
- **PREMISE.md có thay đổi** so với LAB-4: ba bảng spec sửa, giả định bổ sung và hướng đã chốt. Backlog break theo bản đã sửa.
- **Quy mô backlog trên Project:** 17 epic, 380 item, trong đó 276 lá (issue không có con) và 104 issue cha.
- **Sprint giả lập đã chạy:** Iteration `Sprint 1` (12 item cam kết theo năng lực, 6 việc xong). Việc chưa cam kết ở lại backlog, chưa gán Iteration; `Sprint 2` lập kế hoạch ngày 26/10/2026. Trạng thái, burndown và rủi ro ở `progress-report.md`.
- **Người phụ trách là vai giả định.** Field `Người phụ trách (giả định)` có 4 người nhận lá (BE-1, BE-2, FE-1, QA-1) và BrSE điều phối. Tôi không gán tài khoản GitHub thật vì repo và Project public.
- **Field `Point (SWP)` chỉ ghi SWP**, đúng chữ đề. Giờ ước lượng nằm ở field riêng `Estimated time`.

## 2. Link

| Mục | Link |
|---|---|
| Repo | https://github.com/hoangndn-1456/hoangndn-aidd-leader-lab |
| GitHub Project (view mặc định) | https://github.com/users/hoangndn-1456/projects/3 |
| Báo cáo HTML của skill chấm SWP | `reports/estimate-swp-hoangndn-1456-project-3-20261023-152239.html` |
| Bộ spec LAB-4 đã nộp (thư mục Drive) | https://drive.google.com/drive/folders/19pAtpeGNUPFsqRI2sa_7fz8qGyCpN5Gi (cần tài khoản Sun*; đã chia sẻ cho L&D và trainer) |

Đã mở thử bằng cửa sổ ẩn danh: {{hoang.an_danh}}

## 3. Cấu trúc repo

| File/thư mục | Nội dung |
|---|---|
| `README.md` | Trang này |
| `PREMISE.md` | Khác biệt so với LAB-4: spec sửa, giả định, hướng đã chốt |
| `task-breakdown.md` | Luật chia task, spec → issue, hạng mục ràng buộc đặc thù, chỗ hở của spec |
| `estimate.md` | Issue mẫu đã kiểm, cách quy giờ, tổng theo epic, so với LAB-1 |
| `progress-report.md` | Báo cáo tiến độ Sprint 1 giả lập |
| `AI-report.md` | Skill, agent, prompt đã dùng; cách review output AI; điểm đặc biệt và chỗ chưa tốt |
| `reports/` | Báo cáo HTML của skill `estimate-swp` và biểu đồ burndown Sprint 1 (SVG) |
| `skills/` | Định nghĩa 3 subagent tự viết cho pipeline break task |

## 4. Spec → epic

| Spec LAB-4 | Epic trên Project | Ghi chú (ràng buộc đặc thù liên quan) |
|---|---|---|
| specs/auth-accounts/README.md | #27 — Xác thực và quản lý tài khoản nội bộ | — |
| specs/participants/README.md | #28 — Quản lý bên tham gia | tu-cach-giao-dich |
| specs/master-data/README.md | #29 — Dữ liệu chủ: lịch chợ và danh mục mặt hàng | — |
| specs/lot-intake/README.md | #30 — Tiếp nhận lô hàng | — |
| specs/aitai-trades/README.md | #1 — Giao dịch thỏa thuận (相対取引): chốt và hủy | han-muc-lo, khoa-ngay, tu-cach-giao-dich |
| specs/seri-auction/README.md | #31 — Nhập hàng loạt và tra cứu kết quả đấu giá (せり) | — |
| specs/corrections/README.md | #32 — Đính chính giao dịch đã chốt | han-muc-lo, hoan-nap-khen-thuong |
| specs/settlement/README.md | #33 — Quyết toán và khóa ngày nghiệp vụ (nửa A: đối chiếu, khóa ngày, tranh chấp) | — |
| specs/incentive-rates/README.md | #34 — Thưởng hoàn thành nộp đủ và version tỷ lệ thưởng | — |
| specs/delivery/README.md | #35 — Giao hàng | han-muc-lo, hoan-tat-giao-hang |
| specs/offline-sync/README.md | #36 — Đồng bộ ngoại tuyến và giải quyết xung đột | — |
| specs/notifications/README.md | #37 — Thông báo: gửi, thử lại, nhật ký và cấu hình | — |
| specs/reports/README.md, specs/reports/screen-specification/SCR110_REPORT_CATALOG_SPEC.md#3, specs/reports/screen-specification/SCR111_KPI_TRACKING_SPEC.md#3 | #38 — Báo cáo và theo dõi KPI nghiệm thu | — |
| specs/audit/README.md, specs/audit/screen-specification/SCR120_AUDIT_SEARCH_SPEC.md#3 | #39 — Nhật ký kiểm toán | — |
| specs/privacy-appi/README.md | #40 — Bảo vệ thông tin cá nhân theo APPI | — |
| specs/data-migration/README.md | #41 — Chuyển đổi dữ liệu | — |
| PREMISE.md#12, specs/_common/api-list.md, README.md#7 | #42 — Nền tảng chung | cong-rong-dinh-chinh, han-muc-lo, hoan-nap-khen-thuong, hoan-tat-giao-hang, khoa-ngay, lo-trong-ngay, nguoi-trong-vong-lap, thong-bao, tu-cach-giao-dich |

Epic Nền tảng chung chứa mọi issue ràng buộc đặc thù (nhãn `constraint:*`), TECH dùng chung, DB, ADR, nhóm API và dòng PREMISE không thuộc riêng feature nào. Bảng spec → issue chi tiết ở `task-breakdown.md` mục 2.
