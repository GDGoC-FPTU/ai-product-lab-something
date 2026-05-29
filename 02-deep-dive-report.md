# Phase 2 — QUICK-ASSESS: 3 Quick Problem Cards

# 🏗️ Phase 3 — DEEP-DIVE (Nhóm)

## 3.1. Current-State Workflow

Quy trình xử lý hiện tại khi hệ thống map trên app Xanh SM xác định sai vị trí đón khách:

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách đặt    │     │ Hệ thống map │     │ Tài xế đến   │     │ Tài xế gọi   │
│ chuyến trên  │ ──→ │ xác định sai │ ──→ │ sai điểm đón │ ──→ │ điện xác nhận│
│ ứng dụng     │     │ điểm pickup  │     │ hoặc khó tìm │     │ lại vị trí   │
│              │     │              │     │ khách        │     │ khách hàng   │
│ Ai: Customer │     │ Ai: System   │     │ Ai: Driver   │     │ Ai: Driver   │
│ ⏱ 1 phút     │     │ ⏱ 1 phút     │     │ ⏱ 5 phút 🔴  │     │ ⏱ 5 phút 🔴  │
│ In: GPS      │     │ In: GPS      │     │ In: Route    │     │ In: Hotline  │
│ Out: Booking │     │ Out: Pickup  │     │ Out: Delay   │     │ Out: New GPS │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Bước 5       │
                                                               │ Hủy chuyến   │
                                                               │ hoặc điều    │
                                                               │ chỉnh thủ công│
                                                               │ Ai: Driver / │
                                                               │ Customer     │
                                                               │ ⏱ 3 phút 🔴  │
                                                               └──────────────┘

🔴 = Bottlenecks  
⏱ Tổng thời gian xử lý thủ công: ~15 phút/chuyến lỗi.
```

---

## 3.2. Problem Statement (6-field) — Vin Smart Future Standard

| Field                       | Nội dung                                                                                                                                                                                                                                                                                                                                                                                              |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Actor / Operator**     | Tài xế Xanh SM, Khách hàng và Team vận hành Xanh SM.                                                                                                                                                                                                                                                                                                                                                  |
| **2. Current Workflow**     | Khi khách hàng đặt xe tại khu vực đông người (trung tâm thương mại, bệnh viện, chung cư lớn), hệ thống map thường xác định sai điểm đón (pickup point). Tài xế phải gọi điện xác nhận lại vị trí khách, mất thời gian tìm kiếm hoặc phải hủy chuyến nếu không thể xác định đúng vị trí. Quy trình hiện tại phụ thuộc nhiều vào trao đổi thủ công giữa khách và tài xế.                                |
| **3. Bottleneck**           | Bước 3 & 4 (mất ~10 phút/chuyến lỗi): tài xế phải tự tìm khách hoặc gọi điện xác nhận vị trí thực tế do GPS/map không đủ ngữ cảnh địa điểm (nhiều cổng ra vào, nhiều block, nhiều điểm pickup gần nhau).                                                                                                                                                                                              |
| **4. Business Impact**      | Trung bình mỗi ngày có hàng nghìn chuyến ở khu vực đông người. Sai điểm đón làm tăng tỷ lệ hủy chuyến, tăng thời gian chờ của khách hàng, giảm trải nghiệm người dùng và gây thất thoát doanh thu cho Xanh SM. Ngoài ra, tài xế bị giảm hiệu suất nhận cuốc và dễ bị đánh giá thấp từ khách hàng.                                                                                                     |
| **5. Success Metric**       | 1. Giảm thời gian xác định điểm đón từ ~5 phút xuống dưới 1 phút (Efficiency). <br>2. Giảm tỷ lệ hủy chuyến do sai vị trí đón ≥ 30% (Business KPI). <br>3. Độ chính xác gợi ý điểm đón đúng đạt ≥ 90% (Quality).                                                                                                                                                                                      |
| **6. Operational Boundary** | AI được phép truy xuất dữ liệu GPS, lịch sử điểm đón phổ biến, dữ liệu bản đồ nội bộ và ngữ cảnh địa điểm (mall, bệnh viện, chung cư) để gợi ý điểm đón tối ưu dưới dạng recommendation. **CẤM:** AI không được tự ý thay đổi điểm đón cuối cùng mà không có xác nhận từ khách hàng hoặc tài xế; không được tự động hủy chuyến; các trường hợp confidence thấp phải yêu cầu xác nhận thủ công (HITL). |

---

## 3.3. Future-State Flow & AI Fit

### AI Fit:

**Agentic Feature + LLM Support**

Lý do:

* Không chỉ đơn thuần summarize text.
* Hệ thống cần kết hợp nhiều nguồn dữ liệu:

  * GPS
  * lịch sử điểm đón
  * context địa điểm
  * traffic & road access
* AI cần liên tục đề xuất tối ưu theo thời gian thực nhưng vẫn cần Human-in-the-loop.

### Quy trình tương lai (Future-State):

```text
┌──────────────┐     ┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ Bước 1       │     │ Bước 2       │     │ Bước 3       │     │ Bước 4       │
│ Khách đặt    │     │ 🔵 AI phân   │     │ 🔵 AI gợi ý  │     │ 🟢 Khách /   │
│ chuyến       │ ──→ │ tích context │ ──→ │ điểm pickup  │ ──→ │ Driver xác   │
│ trên app     │     │ địa điểm     │     │ tối ưu       │     │ nhận lại     │
└──────────────┘     └──────────────┘     └──────────────┘     └──────────────┘
                                                                      │
                                                                      ▼
                                                               ┌──────────────┐
                                                               │ Driver đến   │
                                                               │ đúng điểm đón│
                                                               └──────────────┘

↩️ Fallback:
Nếu confidence thấp hoặc nhiều điểm pickup khả thi,
AI yêu cầu khách chọn thủ công điểm đón trên app.
```
