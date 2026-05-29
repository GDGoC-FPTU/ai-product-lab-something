# Phase 1 — SCAN: Tìm kiếm cơ hội

Dùng **4 Lenses** quét qua vận hành của các công ty thành viên Vingroup.

| # | Subsidiary | Lens | Mô tả ngắn bài toán |
|---|------------|------|---------------------|
|1| **VinRobotics** | **AI Upgrade** | Hệ thống AI Vision tích hợp trực tiếp vào cánh tay robot công nghiệp tại nhà máy VinFast, tự động phát hiện sai sót mối hàn/lắp ráp siêu nhỏ theo thời gian thực để dừng dây chuyền kịp thời, giảm tỷ lệ hàng lỗi |
|2| **VinRobotics** | **Lặp lại**| Tự động hóa quy trình chạy hàng nghìn chu kỳ kiểm thử mô phỏng cho các dòng Robot tự hành (AGV) trong kho vận, giúp tối ưu hóa thuật toán né vật cản và hoạch định đường đi mà không cần thử nghiệm vật lý tốn kém. |
|3| **VinRobotics** | **Pain từ người khác** | Tích hợp dữ liệu từ hệ thống quản lý kho (WMS) của VinFast/Vinhomes vào Robot kiểm kho tự hành. Robot tự động lập lịch di chuyển, quét mã và đối chiếu tồn kho vào ban đêm để giải quyết nỗi đau kiểm kho thủ công sai sót và tốn nhân lực của bộ phận Vận hành Kho. |
|4| **Vinhomes** | **AI Upgrade** | Hệ thống AI Vision phân tích mật độ cư dân tại các tiện ích chung (bể bơi, sân bóng, lounge) để tự động điều phối lịch trực lễ tân/bảo vệ và tối ưu hóa lượng điện tiêu thụ của hệ thống chiếu sáng/điều hòa theo thời gian thực. |
|5| **Vinmec** | **AI Upgrade** | Hệ thống AI tự động nghe, bóc tách và ghi chép cuộc hội thoại giữa Bác sĩ - Bệnh nhân trong phòng khám (Medical Scribing) để tự động điền thông tin vào bệnh án điện tử, giúp bác sĩ giảm 80% thời gian gõ máy hành chính. |
|6| **Xanh SM** | **Pain từ người khác** | Hệ thống AI phân tích dữ liệu lịch sử đặt xe và thời tiết từ các ứng dụng giao thông công cộng để tự động điều phối, gợi ý tài xế di chuyển đón đầu trước tại các nút giao lớn, giảm thời gian chờ của khách và tăng hiệu suất cuốc của tài xế. |

-----------------------

Chọn top 3 từ danh sách SCAN: **#1 (VinBus Đánh giá mức độ hài lòng), #3 (VFilms Xây dựng kịch bản ngắn), #6 (Xanh SM Hệ thống Map).**


### CARD #1: VINROBOTICS (LENS: AI UPGRADE)
```
┌──────────────────────────────────────────────────────────────┐
│QUICK PROBLEM CARD #1                                                                                     │
│ 
|Bài toán: Tự động phát hiện sai sót mối hàn và lỗi lắp ráp siêu nhỏ theo     │
│                   thời gian thực trên dây chuyền sản xuất.                          │
│                                                                                     │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes                        │
│                     [ ] Vinmec    [x] Khác: VinRobotics                             │
│                                                                                     │
│ Ai đang đau (Actor)? Kỹ sư quản lý chất lượng (QA/QC) & Công nhân dây chuyền        │
│                                                                                     │
│ Workflow thủ công hiện tại (3-5 bước):                                              │
│   1. Robot hàn/lắp ráp hoàn thành sản phẩm ──> 2. Sản phẩm di chuyển qua băng tải   │
│   ──> 3. Kỹ sư QA dùng mắt thường hoặc kính lúp kiểm tra xác suất để phát hiện lỗi. │
│                                                                                     │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3: Kiểm tra thủ công (Dễ bỏ sót lỗi khuất,     │
│                                  phát hiện chậm khiến hàng lỗi bị lọt sang khâu sau)│
│                                                                                     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Hệ thống AI Vision quét liên tục bề mặt,      │
│ đối chiếu mô hình 3D chuẩn để phát hiện sai lệch và ra lệnh dừng robot hành lập tức.│
│                                                                                     │
│ Đo thành công bằng gì (Metric có số)?                                               │
│   - Giảm tỷ lệ sản phẩm lỗi (Defect rate) lọt qua khâu kiểm tra xuống dưới ──> 0.05%│
│   - Thời gian phát hiện và cảnh báo lỗi giảm từ vài phút xuống ──> dưới 0.5 giây.   │
│                                                                                     │
│ Quick Architecture: [ ] No AI   [ ] Rule   [ ] LLM   [x] Agent (Edge AI Vision)      │
└─────────────────────────────────────────────────────────────┘
```

```
┌──────────────────────────────────────────────────────────────┐
│QUICK PROBLEM CARD #2                                                                                     │
│ 
|Bài toán: Tự động hóa quy trình chạy thử nghiệm mô phỏng động học nhằm      │
│                   tối ưu thuật toán điều hướng cho Robot tự hành (AGV).             │
│                                                                                     │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes                        │
│                     [ ] Vinmec    [x] Khác: VinRobotics                             │
│                                                                                     │
│ Ai đang đau (Actor)? Đội ngũ R&D Phần mềm (Firmware Engineers)                      │
│                                                                                     │
│ Workflow thủ công hiện tại (3-5 bước):                                              │
│   1. Kỹ sư lập trình thuật toán né vật cản ──> 2. Nạp phần mềm vào robot thật       │
│   ──> 3. Thiết lập sa bàn vật lý và quan sát robot chạy để tìm lỗi (mất nhiều tuần).│
│                                                                                     │
│ Bước nào tốn thời gian/lỗi nhất? Bước 3: Thử nghiệm vật lý (Tốn thời gian setup,    │
│                                  không thể thử hết hàng nghìn góc cua, va chạm).    │
│                                                                                     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? AI tự động tạo và lặp lại hàng nghìn kịch     │
│ bản di chuyển ảo (Kinematic Simulation) trong môi trường số để ép thuật toán tìm lỗi│
│                                                                                     │
│ Đo thành công bằng gì (Metric có số)?                                               │
│   - Tăng số lượng kịch bản kiểm thử góc khuất từ 50 kịch bản/tuần ──> 10,000+/ngày. │
│   - Rút ngắn thời gian hoàn thiện 1 phiên bản firmware từ 1 tháng ──> dưới 3 ngày.  │
│                                                                                     │
│ Quick Architecture: [ ] No AI   [ ] Rule   [x] LLM/GenAI   [ ] Agent     │
└─────────────────────────────────────────────────────────────┘
```

```
┌──────────────────────────────────────────────────────────────┐
│QUICK PROBLEM CARD #3                                                                                     │
│ 
|Bài toán: Tự động hóa quy trình kiểm kê kho vận ban đêm bằng robot tự hành  │
│                   nhằm loại bỏ sai lệch dữ liệu tồn kho thực tế.                    │
│                                                                                     │
│ Công ty thành viên: [ ] VinFast   [ ] Xanh SM   [ ] Vinhomes                        │
│                     [ ] Vinmec    [x] Khác: VinRobotics (Giải quyết cho VinFast Kho)│
│                                                                                     │
│ Ai đang đau (Actor)? Bộ phận Quản lý Kho vật tư (Logistics/Supply Chain)            │
│                                                                                     │
│ Workflow thủ công hiện tại (3-5 bước):                                              │
│   1. Nhân viên cầm máy quét đi từng kệ hàng ──> 2. Trèo cao/bới hộp để tìm mã vạch  │
│   ──> 3. Nhập số lượng thủ công vào file Excel/WMS ──> 4. Đối chiếu lệch dòng tiền. │
│                                                                                     │
│ Bước nào tốn thời gian/lỗi nhất? Bước 1 & 2: Đi quét mã và đếm thủ công hàng hóa     │
│                                  (Tốn hàng chục giờ nhân công, dễ ghi sai số lượng).│
│                                                                                     │
│ AI có thể nhảy vào hỗ trợ ở bước nào? Robot quét map tự động chạy ban đêm, đọc dữ   │
│ liệu hệ thống WMS để tự đối chiếu, dùng AI Vision đếm số thùng hàng trên kệ.        │
│                                                                                     │
│ Đo thành công bằng gì (Metric có số)?                                               │
│   - Giảm thời gian kiểm kê định kỳ từ 24 giờ dừng kho ──> 0 giờ (chạy tự động đêm). │
│   - Độ chính xác dữ liệu tồn kho (Inventory Accuracy) tăng từ 92% ──> 99.9%.        │
│                                                                                     │
│ Quick Architecture: [ ] No AI   [ ] Rule   [ ] LLM   [x] Agent    │
└─────────────────────────────────────────────────────────────┘
```