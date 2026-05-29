# Phase 1 — SCAN: Tìm kiếm cơ hội

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
| 1 | **VinBus** | AI Upgrade | Hệ thống AI được tích hợp qua camera để đánh giá cảm xúc và phân loại mức độ hài lòng của khách hàng. |
| 2 | **VinFast** | AI Upgrade | Hệ thống nhận diện khách hàng, thu thập thông tin khách hàng, nhằm cung cấp cho nhân viên tư vấn bán hàng thông tin về khách hàng => Customer Centric . |
| 3 | **VFilms** | Lặp lại | Xây dựng kịch bản cho những video ngắn (khoảng 3 giờ/video). |
| 4 | **VFilms** | AI-upgrade | Hệ thống AI tăng khả năng sử lý đồ hoạ kỹ xảo phim| 
| 5 | **VinBus** | Pain từ người khác | Hệ thống AI sử dụng dữ liệu từ camera và cảm biến để đưa ra số lượng người trên xe bus. Nhằm tránh việc quá tải |
| 6 | **Xanh SM** | Pain từ người khác | Hệ thống map hoạt động không hiệu quả trên app. Làm giảm trải nhiệm của khách hàng và tài xế |

-----------------------

Chọn top 3 từ danh sách SCAN: **#1 (VinBus Đánh giá mức độ hài lòng), #3 (VFilms Xây dựng kịch bản ngắn), #6 (Xanh SM Hệ thống Map).**

## Thẻ bài toán tiêu biểu: Card #1 — VinBus Đánh giá mức độ hài lòng khi di chuyển trên Bus

## QUICK PROBLEM CARD #1 — VinBus: AI đánh giá mức độ hài lòng của khách hàng

```text id="mrm3ci"
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #1                                       │
│                                                             │
│ Bài toán: Đánh giá mức độ hài lòng của khách hàng           │
│ trên xe VinBus nhằm phát hiện sớm trải nghiệm tiêu cực      │
│ và cải thiện chất lượng dịch vụ.                            │
│                                                             │
│ Công ty thành viên: [x] VinBus                              │
│                                                             │
│ Ai đang đau?                                                │
│ Team vận hành VinBus, Customer Experience Team,             │
│ Hành khách                                                   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│ 1. Khách hàng trải nghiệm chuyến xe                         │
│ → 2. Khách phản hồi qua survey/app hoặc hotline             │
│ → 3. Team CSKH tổng hợp phản hồi                            │
│ → 4. Team vận hành đọc dữ liệu và xác định vấn đề           │
│ → 5. Đưa ra hành động cải thiện dịch vụ                     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-4 (⏱ ~20 phút/chuyến xe cần review) 🔴               │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-4                                                     │
│ (Computer Vision + sentiment analysis để phân tích          │
│ mật độ hành khách, biểu cảm tổng quát và phản hồi text)     │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian phân tích phản hồi từ 20 phút → dưới 3 phút  │
│ Phát hiện ≥ 85% chuyến xe có trải nghiệm tiêu cực           │
│                                                             │
│ Quick Architecture: [x] LLM + Computer Vision               │
└─────────────────────────────────────────────────────────────┘
```

## QUICK PROBLEM CARD #2 — VFilms: AI hỗ trợ xây dựng kịch bản video ngắn

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #2                                       │
│                                                             │
│ Bài toán: Hỗ trợ xây dựng kịch bản cho video ngắn           │
│ (short-form content) nhằm giảm thời gian sản xuất nội dung. │
│                                                             │
│ Công ty thành viên: [x] VFilms                              │
│                                                             │
│ Ai đang đau?                                                │
│ Scriptwriter, Creative Team, Video Producer                │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│ 1. Nhận brief nội dung từ team marketing                    │
│ → 2. Research trend và insight người xem                   │
│ → 3. Brainstorm ý tưởng video                               │
│ → 4. Viết kịch bản chi tiết                                 │
│ → 5. Team review & chỉnh sửa                                │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-4 (⏱ ~3 giờ/video)                                   │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-4                                                     │
│ (Trend analysis → brainstorm → draft script)                │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm thời gian viết kịch bản từ 3 giờ → dưới 30 phút/video  │
│ 80% script draft được team creative approve để chỉnh sửa    │
│                                                             │
│ Quick Architecture: [x] LLM Feature                         │
└─────────────────────────────────────────────────────────────┘
```

## QUICK PROBLEM CARD #3 — Xanh SM: Hệ thống map hoạt động không hiệu quả

```text
┌─────────────────────────────────────────────────────────────┐
│ QUICK PROBLEM CARD #3                                       │
│                                                             │
│ Bài toán: Hệ thống map trên app Xanh SM hoạt động           │
│ không hiệu quả, gây khó khăn cho tài xế và khách hàng.      │
│                                                             │
│ Công ty thành viên: [x] Xanh SM                             │
│                                                             │
│ Ai đang đau?                                                │
│ Tài xế Xanh SM, Khách hàng, Team vận hành                   │
│                                                             │
│ Workflow thủ công hiện tại (5 bước):                        │
│ 1. Khách đặt chuyến trên app                                │
│ → 2. Hệ thống map xác định điểm đón/trả                     │
│ → 3. Driver nhận chuyến và di chuyển                        │
│ → 4. Driver gọi điện xác nhận vị trí khách                  │
│ → 5. Hủy chuyến hoặc điều chỉnh thủ công nếu sai vị trí     │
│                                                             │
│ Bước nào tốn thời gian/lỗi nhất?                            │
│ Bước 2-4 (⏱ 8–15 phút/chuyến lỗi) 🔴                        │
│                                                             │
│ AI có thể nhảy vào hỗ trợ ở bước nào?                       │
│ Bước 2-4                                                     │
│ (Context-aware pickup suggestion + route optimization)      │
│                                                             │
│ Đo thành công bằng gì (Metric có số)?                       │
│ Giảm tỉ lệ hủy chuyến do sai vị trí từ X% → dưới 30%        │
│ Giảm thời gian xác định điểm đón từ 5 phút → dưới 1 phút    │
│                                                             │
│ Quick Architecture: [x] Agent                               │
└─────────────────────────────────────────────────────────────┘
```
