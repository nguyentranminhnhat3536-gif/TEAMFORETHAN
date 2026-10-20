---
id: k/shared/approval-flow
type: policy
title: Quy trình duyệt trước khi đăng
tags: [duyệt, n8n, an toàn]
links: [k/shared/content-package-format]
scope: shared
author: master
confidence: 1
pinned: true
---

nháp (người viết) → đã soát (brand-reviewer chấm ĐẠT) → đã duyệt (CHỈ người dùng đổi) → n8n-operator gửi sang n8n.
Không ai trong văn phòng được tự đổi trạng thái thành "đã duyệt".
Không ai tự đăng lên mạng, tự bật quảng cáo, tự nhắn khách.
n8n chỉ nhận gói "đã duyệt" và đưa vào hàng chờ. Người dùng bấm đăng hoặc hẹn giờ trong n8n.
