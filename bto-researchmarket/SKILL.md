---
name: bto-researchmarket
description: Research sâu một thị trường bằng nhiều agent chạy song song, ra một bản research đã kiểm chứng, mọi nhận định gắn nhãn độ tin, số phải tự tính chứ không trích lại, bắt buộc có TAM SAM SOM. Dùng khi cần biết một thị trường có những ai, giá bao nhiêu, còn khoảng trống nào, trước khi build. Kích hoạt khi nói "research market", "research thị trường", "làm research về", "so sánh thị trường".
---

# /bto-researchmarket

Từ một câu hỏi ra một bản research đáng tin, agent làm phần nặng, bạn giữ hai
việc không giao được: đặt mục tiêu, và sàng lọc kết quả.

## Bước 0 — Viết mục tiêu một câu

Bản research trả lời một quyết định, không phải "mọi thứ về X". Viết trước:

```
Tôi cần biết <điều gì> về thị trường <X> để quyết định <build hay không / giá bao nhiêu / vào bằng đường nào>.
```

Không có câu này thì agent trả về một bản tóm tắt chung chung không dùng vào
việc gì.

## Bước 1 — Thả 2 tới 3 agent research chạy song song

Chia việc: (1) đối thủ + giá, đọc từ chính trang pricing của họ; (2) người dùng
đang khen gì chửi gì, từ review và cộng đồng; (3) kích thước thị trường + tiền
đang đổ vào đâu. Dán nguyên đoạn hợp đồng này vào prompt của TỪNG agent:

> Gắn nhãn mọi dữ kiện: **[CONFIRMED — kèm URL]** nếu bạn đã mở đúng trang gốc
> (trang pricing, docs, công bố của chính hãng), hoặc **[UNVERIFIED — lý do]**.
> Ưu tiên nguồn gốc hơn trang tổng hợp. Ghi ngày "last updated" nếu trang có.
> Con số nào được trích khắp nơi mà không truy được nguồn gốc thì nói thẳng:
> số không truy được nguồn là một PHÁT HIỆN, không phải một trích dẫn.
> Mọi phép quy đổi phải ghi rõ giả định. Trả về markdown thô, giữ nguyên chi
> tiết, không tự tóm tắt gọn. KHÔNG tự dựng trang, KHÔNG tự publish gì cả,
> phiên chính sẽ tổng hợp.

Dữ kiện GitHub (sao, license, lần push cuối) lấy bằng `gh api`, không lấy từ
bài blog.

## Bước 2 — Tổng hợp, đây là phần làm bản research đáng tin

- **Ba nhãn trên mọi con số:** `confirmed` / `secondary` / `vendor-claimed`.
  Hãng tự nói về mình thì là vendor-claimed, dù nghe hay tới đâu.
- **TAM SAM SOM bắt buộc**, tính bằng chuỗi phép nhân với giả định in ra:
  ```
  TAM = <số người có nhu cầu> × <giá năm>
  SAM = TAM × <% đúng phân khúc, đúng kênh, đúng ngôn ngữ>
  SOM = SAM × <% thực tế với nguồn lực của bạn trong 12 tháng>
  ```
  Số của hãng phân tích là kích thước của thị trường; chuỗi này mới là kích
  thước CỦA BẠN. Người đọc được phép cãi giả định, không cãi được số học.
- **Số tự tính, không trích lại.** Chi phí, đơn giá quy đổi về cùng một đơn vị
  (ví dụ $ trên 1,000 lượt dùng), kèm giả định quy đổi.
- **Mục "số bị từ chối in":** liệt kê những con số lan truyền mà không truy
  được nguồn, và vì sao. Mục này tạo niềm tin hơn mọi trích dẫn.
- Số liệu thị trường ghi rõ theo định nghĩa phân khúc nào, không trộn.

## Bước 3 — Đổ vào template và tự kiểm

Điền kết quả vào template bản research một trang phát kèm Buổi 3. Không có
template thì cứ theo đúng thứ tự các bước trên, mỗi mục vài dòng. Trước khi nộp:

- [ ] Mọi con số có nhãn, có nguồn kèm ngày đọc
- [ ] Có TAM SAM SOM với giả định in ra
- [ ] Có cột giá của từng đối thủ
- [ ] Có mục số bị từ chối in (không có số nào bị từ chối cũng là một câu trả lời)
- [ ] Bạn đã đọc hết và sửa ít nhất một chỗ agent nói sai. Chưa tìm thấy chỗ
      sai nào thì gần như chắc chắn là chưa đọc kỹ

## Bước 4 — Muốn khoe thì dựng thành trang

Bản một trang là bài nộp. Muốn một trang web đẹp kiểu
[promptwatch](https://promptwatch.com/best-geo-and-ai-visibility-platforms-compared-2026)
thì đưa bản research cộng link đó cho agent, yêu cầu một file HTML tự chứa,
rồi **mở ra nhìn bằng mắt trước khi gửi ai**: bảng có tràn không, số có đúng
với bản research không. Agent dựng trang rất nhanh và sai số rất im lặng.
