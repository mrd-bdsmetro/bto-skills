# bto-skills

**Ba skill rút từ Build to Own cohort 01, cài vào agent của bạn trong một phút.**

Một skill là một tệp hướng dẫn agent tự đọc khi gặp đúng loại việc. Bạn không
phải nhớ quy trình, không phải dán lại prompt mỗi lần. Agent thấy bạn chạm tới
đúng loại việc là nó tự mở hướng dẫn ra và làm theo.

Mọi luật trong ba skill này rút từ việc thật trong chương trình
[Build to Own](https://luma.com/6bc3oab0): bốn tuần, một sản phẩm có người trả
tiền. Không có luật nào lấy từ sách.

| Skill | Dùng khi | Nó ép agent làm gì |
|---|---|---|
| `giu-khoa` | Chạm tới API key, `.env`, trước khi commit hoặc push | Đưa tên biến thay vì giá trị, quét secret trước khi push, lộ key thì xoay chứ không xoá commit |
| `research-market` | Cần biết một thị trường có những ai, giá bao nhiêu, còn khoảng trống nào | Nhiều agent quét song song, mọi con số gắn nhãn nguồn, bắt buộc TAM SAM SOM, số không truy được nguồn thì từ chối in |
| `teardown` | Muốn build một sản phẩm tương tự thứ đã có trên thị trường | Phân rã ra spec sạch, build ở phiên riêng chỉ đọc spec, cấm chép code, cấm tên kiểu X-clone |

## Cài

Mở Claude Code và dán câu này, agent tự làm phần còn lại:

> Cài bto-skills: chạy `git clone https://github.com/sonpiaz/bto-skills.git ~/.claude/skills/bto-skills && ~/.claude/skills/bto-skills/setup` rồi xác nhận ba skill giu-khoa, research-market, teardown đã nhận.

Hoặc tự chạy hai lệnh:

```bash
git clone https://github.com/sonpiaz/bto-skills.git ~/.claude/skills/bto-skills
~/.claude/skills/bto-skills/setup
```

Chỉ cần một skill thì tải đúng một tệp, ví dụ teardown:

```bash
mkdir -p ~/.claude/skills/teardown
curl -o ~/.claude/skills/teardown/SKILL.md \
  https://raw.githubusercontent.com/sonpiaz/bto-skills/main/teardown/SKILL.md
```

Dùng Codex hay agent khác thì vẫn dùng được, chỉ khác chỗ đặt tệp. Hỏi agent
của bạn "skill hoặc hướng dẫn của tôi đặt ở đâu" là nó chỉ cho.

## Kiểm đã ăn chưa

Mở một phiên agent mới và thử từng câu:

```
Tôi sắp nối một API mới vào dự án. Có luật nào tôi phải theo không?
Research thị trường công cụ đặt lịch cho tiệm làm đẹp giúp tôi.
Tôi muốn build một sản phẩm tương tự Calendly.
```

Câu một nó nhắc tên biến thay vì giá trị. Câu hai nó hỏi ngược mục tiêu một
câu. Câu ba nó nhắc phân rã trước khi build. Đủ ba là xong.

## Skill không thay bạn chịu trách nhiệm

Skill làm agent nhớ luật và đi đúng quy trình. Nó không làm con số thành
đúng, không làm key hết lộ, không làm sản phẩm của bạn hết giống bản gốc.
Ba việc vẫn là của bạn: đặt mục tiêu trước khi giao, đọc kết quả rồi sửa chỗ
sai trước khi tin, và duyệt trước khi thứ gì đó rời khỏi máy.

---

Viết bởi [Son Piaz](https://github.com/sonpiaz) cho người tham gia Build to
Own cohort 01, tháng 8/2026. Ai không trong chương trình dùng cũng được, đó
là lý do repo này public.
