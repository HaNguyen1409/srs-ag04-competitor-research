# srs-ag04-competitor-research

**AG-04** · Agent Node · phiên bản **2.0.0** · giấy phép MIT

> Vietnamese-language Claude skill — one independent, reusable service of the SRS-SOP agent pipeline. Machine-readable contract: [`skill.json`](skill.json).

[Bước tuỳ chọn] Agent Node AG-04 (Bước B7 SOP viết SRS): nghiên cứu sản phẩm tương tự/đối thủ qua tìm kiếm web có nguồn, lập hồ sơ tính năng/luồng/mẫu UI (T1/T2/T3) và ánh xạ REQ; làm sạch truy vấn để không lộ thông tin khách hàng. Chấm điểm nguyên.

## Hợp đồng giao tiếp

Skill là một dịch vụ độc lập, ghép lỏng: nhận đầu vào và trả đầu ra dưới dạng tài liệu/JSON mô tả trong [`SKILL.md`](SKILL.md), không gọi trực tiếp skill khác và không gắn với dự án cụ thể. Dùng riêng lẻ, hoặc ghép qua bộ điều phối [`srs-sop-pipeline`](https://github.com/HaNguyen1409/srs-sop-pipeline).

| Bước SOP | Việc | Loại | Nhận từ | Chuyển tới |
|---|---|---|---|---|
| 7 | (Tuỳ chọn) Nghiên cứu sản phẩm tương tự & đối thủ | Agent | B1, B5 | B8, B12 |

**Sản phẩm đầu ra:** none (competitor profiles + ui_references)

**Skill phía sau (dùng đầu ra):** [`srs-ag05-feature-matrix`](https://github.com/HaNguyen1409/srs-ag05-feature-matrix) `^2.0.0` · [`srs-ag07-screen-flow-design`](https://github.com/HaNguyen1409/srs-ag07-screen-flow-design) `^1.0.0`

## Cài đặt

**Claude Code** — clone đúng phiên bản vào thư mục skill:

```bash
git clone --branch v2.0.0 https://github.com/HaNguyen1409/srs-ag04-competitor-research.git ~/.claude/skills/srs-ag04-competitor-research
```

Nâng cấp: `git -C ~/.claude/skills/srs-ag04-competitor-research fetch --tags && git -C ~/.claude/skills/srs-ag04-competitor-research checkout v<phiên-bản-mới>`.

**claude.ai / Claude Desktop** — tải `srs-ag04-competitor-research-v2.0.0.zip` ở trang [Releases](https://github.com/HaNguyen1409/srs-ag04-competitor-research/releases) rồi tải lên ở phần Skills trong cài đặt.

**Cả bộ** — xem [`srs-sop-skills`](https://github.com/HaNguyen1409/srs-sop-skills) (cài toàn bộ skill theo phiên bản đã khoá).

## Quản lý phiên bản

Theo [SemVer](https://semver.org/lang/vi/), áp cho hợp đồng giao tiếp của skill:

| Tăng | Khi |
|---|---|
| MAJOR | Đổi hợp đồng làm vỡ skill phía sau: đổi/bỏ trường JSON, đổi hệ mã ID, đổi bố cục tài liệu đầu ra |
| MINOR | Thêm khả năng tương thích ngược: trường tuỳ chọn, mục mới, chế độ mới |
| PATCH | Sửa câu chữ, sửa lỗi, làm rõ luật mà không đổi đầu ra |

Phát hành: sửa `SKILL.md` → tăng `version` trong frontmatter, `VERSION`, `skill.json` → thêm mục vào [`CHANGELOG.md`](CHANGELOG.md) → `python tools/check_skill.py` → commit → `git tag -a vX.Y.Z -m "vX.Y.Z"` → `git push --follow-tags`. GitHub Actions kiểm lại, chạy test và đính kèm zip vào Release.

## Giấy phép

MIT — xem [`LICENSE`](LICENSE).
