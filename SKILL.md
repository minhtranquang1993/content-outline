---
name: seo-outline
description: >
  Tạo dàn bài SEO chuẩn AEO/GEO cho một keyword bất kỳ — có research SERP thật,
  phân tích intent, structured output với H1/H2/H3/FAQ/AIO Notes/SEO Meta và auto-review ngay sau khi tạo outline.
  Trigger khi user nói: "/seo-outline", "viết outline cho keyword", "lên outline seo",
  "lên dàn bài seo", "tạo outline", "tạo dàn bài SEO chuẩn AEO", "outline keyword",
  "dàn bài seo chuẩn", "lên outline deep", "tạo outline cho bài blog", "outline landing page".
version: 1.0.0
tags: [seo, outline, aeo, geo, keyword, serp, dàn-bài, blog, landing-page]
---

# SEO Outline Skill

Tạo dàn bài SEO chuẩn AEO/GEO cho một keyword — research SERP thật, phân tích intent, output có cấu trúc sẵn sàng cho writer, kèm auto-review chất lượng.

## Khi nào dùng skill này?

- Lên dàn bài SEO cho bài blog / landing page / bài tư vấn
- Tạo outline chuẩn AEO/GEO để dễ được AI Overview, featured snippet hoặc các AI search engine trích dẫn
- Phân tích intent keyword trước khi viết bài
- Chuẩn hóa cấu trúc bài trước khi giao writer viết

---

## Input

| Tham số | Bắt buộc | Giá trị | Ghi chú |
|---|---:|---|---|
| `keyword` | Có | Từ khóa chính | Keyword cần tạo outline |
| `mode` | Không | `lite`, `standard`, `deep` | Mặc định `lite` nếu không chỉ định |

**Ví dụ trigger hợp lệ:**
```
/seo-outline keyword="mổ cận lasik có đau không" mode=standard
/seo-outline keyword="các loại lens cận"
viết outline cho keyword "mắt cận thị khi về già"
lên outline deep cho keyword "hướng dẫn chăm sóc mắt sau phẫu thuật"
```

**Auto-chọn mode nếu user không chỉ định:**
- Keyword dạng "là gì", "có nên không", "có đau không" → `lite` hoặc `standard`
- Keyword dạng "các loại", "hướng dẫn toàn diện", "so sánh chi tiết" → `deep`
- Không chắc → `lite`

---

## Mode Budget

| Mode | Số H2 | Tổng H3 (gồm FAQ) | FAQ H3 | Dùng khi |
|---|---:|---:|---:|---|
| `lite` | 4–6 | 6–12 | 2–3 | Keyword hẹp, Q&A ngắn, cần viết nhanh |
| `standard` | 6–8 | 12–20 | 3–5 | Cần sâu hơn mặt bằng đối thủ |
| `deep` | 8–12 | 20–36 | 5–8 | Pillar content, chủ đề rộng, cạnh tranh cao |

---

## Workflow bắt buộc (3 bước — không bỏ bước nào)

```
1. Research SERP  →  2. Tạo outline  →  3. Review outline ngay
```

Chưa có review thì task **chưa hoàn tất**.

---

## Bước 1 — Research SERP

### 1.1. Tìm kết quả SERP

Dùng `WebSearch` để search keyword:
- `{keyword}` — kết quả chính
- `{keyword} câu hỏi thường gặp` — tìm PAA (People Also Ask)
- `{keyword} [năm hiện tại]` — tìm nội dung mới
- Nếu keyword có local intent: `{keyword} [thành phố]`

Fetch nội dung top 3–5 URL bằng `WebFetch` để phân tích cấu trúc H2/H3.

### 1.2. Phân tích SERP

Xác định:
- **Primary intent**: `informational` | `commercial` | `transactional` | `navigational`
- **Modifier**: `local` | `non-local`
- **SERP format chính**: listicle, comparison, pricing, how-to, local pack
- **Cấu trúc H2/H3** của top 1–3 kết quả
- **Độ sâu trung bình** của đối thủ (số H2/H3)
- **People Also Ask** và related queries thật sự liên quan

### 1.3. Xác định đặc thù nội dung

- **YMYL?** (y tế, tài chính, pháp lý, an toàn) → bắt buộc có trust block
- **Local intent?** → bắt buộc thêm Local block
- **Cạnh tranh cao?** → tăng độ sâu H3

---

## Bước 2 — Tạo Outline

### 2.1. Quy tắc H1

- Dạng câu hỏi hoặc benefit-driven
- Có keyword chính tự nhiên

**Ví dụ tốt:**
```
H1: Mổ cận LASIK có đau không? Quy trình và cảm giác thực tế
```

### 2.2. Quy tắc H2

- Mỗi H2 xử lý **1 intent** duy nhất
- Viết như câu hỏi người dùng thật sự search
- Có khả năng trả lời dạng AI snippet

**Ví dụ tốt:**
```
H2: Mổ cận LASIK có đau không?
H2: Những ai không nên mổ cận LASIK?
```

### 2.3. Quy tắc H3

- Cụ thể, granular — dùng để bắt long-tail queries
- Gắn tag `[cần dẫn chứng]` nếu heading cần số liệu, nghiên cứu, khuyến cáo chuyên gia, claim y tế/tài chính/pháp lý

**Ví dụ:**
```
H3: Cảm giác trong 24 giờ đầu sau phẫu thuật LASIK
H3: Khi nào đau mắt sau LASIK là dấu hiệu bất thường? [cần dẫn chứng]
```

### 2.4. Block Local / Địa phương (chỉ khi keyword có local intent)

```
H2: [Dịch vụ] tại [khu vực] — Thông tin địa phương
  H3: Khu vực phục vụ cụ thể
  H3: Mức giá tham khảo tại [thành phố] [cần dẫn chứng]
  H3: Câu hỏi thường gặp theo địa điểm
  H3: CTA địa phương
```

### 2.5. Trust block E-E-A-T (chỉ khi YMYL)

Outline bắt buộc có ≥ 1 trong số:
- Khi nào cần gặp chuyên gia
- Rủi ro / tiêu chí an toàn
- Chuẩn chuyên môn / quy định liên quan
- Cảnh báo không tự xử lý tại nhà

**Ví dụ:**
```
H2: Khi nào cần gặp bác sĩ thay vì tự theo dõi tại nhà?
H2: Những rủi ro cần biết trước khi mổ cận LASIK [cần dẫn chứng]
```

---

## Output Contract — Format bắt buộc

Output phải theo **đúng thứ tự** sau, không thêm intro/outro ngoài format:

```
Keyword chính: {keyword}
Intent: {informational | commercial | transactional | navigational} [local | non-local]

H1: {title — dạng câu hỏi hoặc benefit-driven}
H2: {section}
  H3: {subsection}
  H3: {subsection} [cần dẫn chứng]
H2: {section}
...
H2: FAQ
  H3: {câu hỏi 1}
  H3: {câu hỏi 2}
  ...

AIO Notes:
- Entity definitions: {thuật ngữ 1}, {thuật ngữ 2}, {thuật ngữ 3}
- Decision factors: {tiêu chí 1}, {tiêu chí 2}, {tiêu chí 3}

SEO Meta:
- Slug: {slug-lowercase-khong-dau-dung-gach-ngang}
- Meta title: {<60 ký tự, có keyword}
- Meta description: {120–155 ký tự, có keyword + CTA nhẹ}

Tham khảo bài viết:
https://...
https://...
https://...

Review:
- Điểm số: x/10
- Lý do:
  - ...
  - ...
- Gợi ý 10/10:
  - ...
```

### SEO Meta Rules

**Slug:**
- Lowercase, không dấu, dùng dấu gạch ngang
- Bỏ ký tự đặc biệt và stopword thừa

**Meta title:** < 60 ký tự, có keyword chính, tự nhiên

**Meta description:** 120–155 ký tự, có keyword + CTA nhẹ

---

## Bước 3 — Auto-Review (bắt buộc)

Sau khi tạo outline, review ngay trước khi trả output. Tự review bằng model hiện tại và ghi:

```
[review degraded mode]
```

nếu không dùng được model review riêng biệt.

**Focus review vào 3 điểm:**
1. Search intent — outline có match đúng intent không?
2. AEO/SEO snippet readiness — heading có đủ cụ thể để trigger snippet không?
3. Tính chuyển đổi — có trust signal, CTA logic không?

Review không được dài hơn outline.

---

## QA Checklist trước khi trả output

Tự check 11 mục này, nếu fail → sửa trước khi trả:

| # | Tiêu chí | Pass khi |
|---|---|---|
| 1 | Mode budget | H2/H3/FAQ đúng giới hạn mode |
| 2 | Không trùng intent | Mỗi H2 xử lý 1 ý khác nhau |
| 3 | Heading rõ | Không có heading mơ hồ kiểu "Thông tin thêm" |
| 4 | Có nguồn thật | Có ít nhất 3 URL research |
| 5 | Đúng format | Có Keyword, Intent, H1, H2/H3, FAQ, AIO Notes, SEO Meta, nguồn |
| 6 | AIO Notes | Có Entity definitions và Decision factors |
| 7 | Evidence tags | Các claim cần nguồn có `[cần dẫn chứng]` |
| 8 | Local | Có local block nếu intent là local |
| 9 | E-E-A-T | Có trust block nếu là YMYL |
| 10 | SEO Meta | Slug, title, description đạt chuẩn |
| 11 | Review | Có điểm số + lý do + gợi ý cải thiện |

---

## Ví dụ Output (rút gọn)

```
Keyword chính: mổ cận lasik có đau không
Intent: informational [non-local]

H1: Mổ cận LASIK có đau không? Cảm giác và lưu ý trước khi phẫu thuật
H2: Mổ cận LASIK có đau không?
  H3: Cảm giác trong lúc chiếu laser
  H3: Cảm giác trong 24 giờ đầu sau mổ
H2: Vì sao một số người thấy cộm hoặc xốn mắt sau LASIK?
  H3: Khô mắt tạm thời sau phẫu thuật [cần dẫn chứng]
  H3: Phản ứng hồi phục bình thường của giác mạc
H2: Khi nào đau mắt sau LASIK là dấu hiệu cần đi khám?
  H3: Các dấu hiệu bất thường không nên bỏ qua [cần dẫn chứng]
H2: Ai phù hợp và không phù hợp để mổ LASIK?
  H3: Điều kiện độ cận, giác mạc và sức khỏe mắt [cần dẫn chứng]
H2: FAQ
  H3: Mổ LASIK bao lâu thì nhìn rõ?
  H3: Sau LASIK có bị cận lại không?
  H3: Mổ LASIK có cần nghỉ làm không?

AIO Notes:
- Entity definitions: LASIK, giác mạc, khúc xạ, khô mắt sau mổ
- Decision factors: mức độ đau, thời gian hồi phục, điều kiện phù hợp, rủi ro

SEO Meta:
- Slug: mo-can-lasik-co-dau-khong
- Meta title: Mổ cận LASIK có đau không? Lưu ý cần biết
- Meta description: Mổ cận LASIK có đau không? Tìm hiểu cảm giác thực tế, thời gian hồi phục và dấu hiệu cần đi khám trước khi quyết định.

Tham khảo bài viết:
https://...
https://...
https://...

Review:
- Điểm số: 8.5/10
- Lý do:
  - Đúng informational intent, có trust block cho chủ đề y tế
  - Heading đủ cụ thể để bắt snippet và PAA
  - Có thể tăng chuyển đổi bằng section tư vấn/đặt lịch nếu dùng cho website bệnh viện
- Gợi ý 10/10:
  - Thêm local/brand block nếu bài phục vụ dịch vụ LASIK tại TP.HCM
```

---

## Lưu ý quan trọng

- Không bỏ research nguồn thật — outline không có nguồn là outline không đủ tin cậy
- Không bỏ review — review là checkpoint quality tự động
- Không viết outline quá dài nếu mode là `lite` — ưu tiên bám mặt bằng top SERP
- Chủ đề y tế/tài chính/pháp lý phải có trust signal và tag `[cần dẫn chứng]` đúng chỗ
- Output phải sạch theo format cố định — writer cầm là dùng được ngay
