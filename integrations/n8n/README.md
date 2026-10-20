# Nối đội Marketing với n8n (ethanstudio.app.n8n.cloud)

Anh đã có sẵn các workflow n8n chạy tốt. **Không cần làm lại.** Ta cho đội Marketing AI *gọi* đúng những workflow đó qua MCP (giao thức để AI dùng công cụ bên ngoài). Chỉ vai **Điều phối n8n** (`n8n-operator`) được cầm chìa khoá.

```
Đội Marketing (agentco)                      n8n cloud của anh
─────────────────────────                    ─────────────────────────────
viết → soát → ANH DUYỆT  ──► n8n-operator ──► workflow "Available in MCP"
                                              (hàng chờ đăng, lịch đăng, số liệu…)
```

> 🔒 **Luật an toàn có sẵn trong đội:** n8n-operator chỉ gửi gói nội dung có trạng thái **"đã duyệt"**, và chỉ anh được đổi sang trạng thái đó. Không vai nào tự đăng, tự bật quảng cáo hay tự nhắn khách.

---

## Bước 1. Bật MCP cho n8n

1. Vào **ethanstudio.app.n8n.cloud** → **Settings** → **Instance-level MCP** → bật lên. Cần quyền owner hoặc admin.
2. Mở phần kết nối client (**Connect a client** / **Connection details**). Chép **địa chỉ server (URL)** và tạo **token** (tab *API key* hoặc *Access token*, tuỳ phiên bản n8n).
   Token chỉ hiện **một lần**. Chép ngay.
3. Mở từng workflow muốn đội dùng → **Settings** → bật **Available in MCP**. Chỉ bật cho workflow anh muốn AI gọi được.

Tài liệu gốc của n8n: <https://docs.n8n.io/connect/connect-to-n8n-mcp-server>

> Tên menu có thể hơi khác giữa các phiên bản n8n. Nếu không thấy, tìm chữ "MCP" trong Settings.

## Bước 2. Khai báo trong agentco

Mở `company/company.yaml`. File này do `agentco init` tạo ra. Thay dòng `mcpServers: {}` bằng:

```yaml
mcpServers:
  n8n:
    type: http
    url: "<DÁN URL Ở BƯỚC 1 VÀO ĐÂY>"
    headers:
      Authorization: "Bearer ${N8N_MCP_TOKEN}"
```

Để nguyên chữ `${N8N_MCP_TOKEN}`. agentco tự thay bằng token thật lúc chạy, và **chỉ** cho vai `n8n-operator` (vai này khai `secrets: [N8N_MCP_TOKEN]`).

## Bước 3. Cất token (không bao giờ commit lên git)

```bash
VALUE="<token n8n>" agentco secret set N8N_MCP_TOKEN
```

Token nằm trong `company/.state/secrets.json`. File này đã được `.gitignore` chặn, không lên GitHub.

## Bước 4. Thử

Nói với Trưởng phòng Marketing:

> Nhờ n8n-operator liệt kê các workflow n8n đang dùng được, chưa chạy gì cả.

Thấy danh sách là đã nối xong.

---

## Workflow nên có (nếu chưa có)

| Workflow | Nhận gì | Làm gì |
|---|---|---|
| **Hàng chờ đăng** | Gói nội dung "đã duyệt" | Ghi vào Google Sheet hoặc Data Table với trạng thái *chờ đăng*. Anh bấm đăng hoặc hẹn giờ |
| **Đăng chéo** | Link video gốc + caption từng kênh | Đăng hoặc hẹn giờ lên Facebook, Instagram, YouTube Shorts, Threads |
| **Số liệu tuần** | (không) | Lấy số người theo dõi từng kênh, ghi vào bảng `ethansocial` mỗi Chủ nhật |
| **Inbox MOCKUP** | Tin nhắn có chữ MOCKUP | Ghi tên quán, link vào bảng khách tiềm năng. Báo về Telegram của anh |

Dữ liệu gửi sang n8n theo **Gói nội dung** (xem `company/offices/marketing/knowledge/shared/content-package-format.md`). Các trường: `id`, `Ngày đăng`, `Kênh`, `Định dạng`, `Trụ cột`, `Câu móc`, `Nội dung`, `CTA`, `Hashtag`, `Trạng thái`.

> Mình chưa đọc được workflow hiện có của anh: n8n cloud cần đăng nhập. Nếu anh tạo **n8n API key** (Settings → n8n API) và đưa cho mình trong một phiên làm việc, mình đọc được workflow thật và nối khớp từng trường. Xong việc thì anh xoá key đó.
