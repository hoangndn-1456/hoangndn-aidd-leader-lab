# Định nghĩa subagent tự viết

Thư mục này chứa 3 định nghĩa **subagent** của Claude Code mà tôi viết cho pipeline break task LAB-5. Đây không phải Skill (gói `SKILL.md`); mỗi file là frontmatter (tên, model, tool được cấp) cộng thân prompt giữ luật ổn định của agent. Khi chạy, các file nằm ở `.claude/agents/` của thư mục làm việc.

| File | Vai | Model | Tool |
|---|---|---|---|
| `lab5-epic-worker.md` | Tách backlog cho một unit (một epic hoặc nửa epic) từ spec LAB-4, trả JSON theo schema | sonnet | Read, Glob, Grep |
| `lab5-constraint-worker.md` | Gom các dòng ràng buộc đặc thù thành issue riêng thuộc epic Nền tảng chung | opus | Read, Glob, Grep |
| `lab5-backlog-evaluator.md` | Soát ngữ nghĩa backlog theo rubric (vòng evaluator-optimizer), trả danh sách phát hiện | opus | Read |

Không agent nào có Bash, Write, Edit hay MCP: subagent chỉ đọc, mọi lệnh ghi GitHub đi qua script có dry-run. Cách dùng và lý do chọn model ở `AI-report.md` mục 1.
