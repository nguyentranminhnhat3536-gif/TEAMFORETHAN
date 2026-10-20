# TEAMFORETHAN: đội AI cho ETHAN STUDIO

> **Bạn lo bán hàng. Phần mềm lo phần còn lại.**

Repo này dựng **hai đội AI** cho ETHAN STUDIO, chạy trên [agentco](https://github.com/minhvq36/agentco) (một "công ty ảo" của các nhân viên AI chạy trên máy anh, dùng gói Claude sẵn có):

| Đội | Trạng thái | Nhiệm vụ |
|---|---|---|
| 📣 **Marketing** | ✅ **Đã dựng**: `company/offices/marketing/` | Tăng nhận diện thương hiệu, kéo follow, bán phần mềm |
| 💻 **Code** | ⏳ Giai đoạn 2 | Website `/links`, template cho nhóm Telegram, phần mềm cho quán |

**Mục tiêu trước 01/01/2027:** mỗi kênh social ≥ 1.000 người theo dõi, doanh thu phần mềm ≥ 1.000 USD. Mục tiêu phụ: kéo người vào nhóm Telegram.

---

## Đọc gì trước

| # | Tài liệu | Dùng để |
|---|---|---|
| 1 | [Sổ tay thương hiệu](docs/marketing/01-so-tay-thuong-hieu.md) | Tên, slogan, giọng nói, màu, khán giả. Mọi thứ phải khớp file này |
| 2 | [Thiết kế lại kênh social](docs/marketing/02-thiet-ke-lai-kenh-social.md) | **Làm ngay hôm nay:** tên, handle, bio (đã đếm ký tự), ảnh bìa, ghim, 2FA cho từng kênh |
| 3 | [Kế hoạch 10 tuần](docs/marketing/03-ke-hoach-10-tuan.md) | Series "Hành trình 0 → 1.000", nhịp đăng, lộ trình theo tuần, đường tới 1.000 USD |
| 4 | [Nối với n8n](integrations/n8n/README.md) | Cho đội AI gọi các workflow n8n anh đang có |

---

## Đội Marketing gồm ai

Một **Trưởng phòng** (agentco gọi là Assistant) nhận lời anh nói, chia việc, giao cho 10 nhân viên chạy song song:

| Vai | Làm gì | Model |
|---|---|---|
| 🧭 Chiến lược thương hiệu | Lịch nội dung tuần, kế hoạch chiến dịch | standard |
| 🔎 Săn xu hướng | Trend, đối thủ, nỗi đau chủ quán (có nguồn) | standard |
| ✍️ Copywriter | Caption, bài FB/LinkedIn/Threads, bio, tin Telegram | standard |
| 🎬 Biên kịch video | Kịch bản video ngắn, video dài, video ads, chữ thumbnail | standard |
| 🎨 Thiết kế sáng tạo | Brief Canva, prompt ảnh AI, bố cục thumbnail và carousel | standard |
| 🎯 Chuyên viên quảng cáo | Kế hoạch ads Meta/TikTok, bản chữ A/B test | standard |
| 💬 Cộng đồng & chốt đơn | Kịch bản inbox MOCKUP, trả lời bình luận, nhóm Telegram | standard |
| 📊 Phân tích tăng trưởng | Báo cáo tuần, tiến độ tới mốc 1.000 | standard |
| 🔍 Soát thương hiệu | Chấm ĐẠT/CHƯA ĐẠT theo sổ tay trước khi trình anh | eco (rẻ) |
| 🔗 Điều phối n8n | Đẩy nội dung **đã được anh duyệt** sang n8n | eco (rẻ) |

**Quy trình duyệt:** nháp → *Soát thương hiệu* chấm ĐẠT → **anh duyệt** → *Điều phối n8n* đẩy sang hàng chờ. Không vai nào tự đăng, tự bật ads hay tự nhắn khách.

Đội "nhớ" thương hiệu qua `company/offices/marketing/knowledge/shared/`. Đó là bản rút gọn của sổ tay, mỗi mục dưới 250 token để chạy rẻ.

---

## Chạy lần đầu

Cần: **Node.js 22+** và một **gói Claude** (không cần API key).

```bash
# 1. Cài agentco
npm i -g @agent-co-app/cli

# 2. Ở thư mục gốc repo này, tạo file cấu hình công ty.
#    agentco tự nhận thư mục ./company và giữ nguyên văn phòng Marketing có sẵn.
cd TEAMFORETHAN
agentco init
agentco login

# 3. Kiểm tra rồi chạy
agentco doctor
agentco start          # mở http://127.0.0.1:7317
```

Mở giao diện, chọn văn phòng **Marketing ETHAN STUDIO**, rồi nói chuyện với Trưởng phòng.

**Nên làm thêm:**

- Bỏ mẫu thumbnail, video ads, video hằng ngày (ảnh chụp, file video) và bản CSV của bảng `ethansocial` vào **Thư viện tài liệu** trong giao diện. Hoặc chép thẳng vào `company/offices/marketing/library/files/`. Đội sẽ bám theo mẫu thật thay vì bộ màu đề xuất.
- Nối n8n theo [hướng dẫn](integrations/n8n/README.md).

---

## Câu lệnh mẫu cho Trưởng phòng

```text
Lên lịch nội dung tuần 27/10–02/11 cho series Hành trình 0 → 1.000, ưu tiên TikTok và Facebook.
```
```text
Viết kịch bản 3 video đầu tiên: Ngày 1 "ETHAN STUDIO là ai", Ngày 2 demo web quán café, Ngày 3 mẹo chốt sổ cuối ngày.
```
```text
Viết brief Canva cho ảnh đại diện, bìa Facebook, banner YouTube và banner LinkedIn theo sổ tay thương hiệu.
```
```text
Soạn kịch bản inbox cho quy trình MOCKUP và tin chào nhóm Telegram.
```
```text
Lên kế hoạch quảng cáo Facebook tăng lượt theo dõi trang, ngân sách 100.000đ/ngày, chạy 7 ngày.
```
```text
Đây là CSV số liệu tuần này (trong thư viện). Viết báo cáo tuần và đề xuất tuần sau.
```
```text
Gói MKT-20261027-01 và MKT-20261027-02 tôi đã duyệt. Nhờ n8n-operator đưa vào hàng chờ đăng.
```

---

## Cấu trúc repo

```
README.md
docs/marketing/
  01-so-tay-thuong-hieu.md        sổ tay thương hiệu
  02-thiet-ke-lai-kenh-social.md  checklist + bio dán dùng ngay cho 7 kênh + Telegram
  03-ke-hoach-10-tuan.md          kế hoạch 20/10 → 31/12/2026
integrations/n8n/README.md        nối agentco ↔ n8n qua MCP
company/                          thư mục công ty agentco (company.yaml do `agentco init` tạo)
  offices/marketing/
    office.yaml                   cấu hình văn phòng + Trưởng phòng
    charter.md                    điều lệ: mục tiêu + 7 luật làm việc
    roles/*.yaml                  10 nhân viên
    skills/*.md                   cách làm việc của từng người (sửa thoải mái)
    knowledge/shared/*.md         trí nhớ chung: thương hiệu, khán giả, mục tiêu, kênh…
    library/files/                mẫu và số liệu anh bỏ vào
```

**Sửa đội thế nào:** sửa `skills/<vai>.medium.md` để đổi cách làm việc, `knowledge/shared/*.md` để đổi thông tin thương hiệu. Sau khi sửa skill, tăng `version` trong `roles/<vai>.yaml` để agentco nạp bản mới.

---

## Giai đoạn 2: Đội Code

Đội Marketing đã ghi sẵn các việc cần đội Code làm:

1. Trang **`/links`** trên website (link-in-bio chung cho mọi kênh) và đổi tên website thành ETHAN STUDIO
2. **Bộ 3 template Google Sheets** cho quán (doanh thu ngày, kho nguyên liệu, lịch ca), làm mồi kéo vào nhóm Telegram
3. Form **"Nhận mockup miễn phí"** nối về n8n
4. Phần mềm quản lý cho quán (sản phẩm chính để đạt 1.000 USD)
