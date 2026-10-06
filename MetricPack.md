# Day 20: Product Metrics - Retention & Engagement
**Thông tin cá nhân**

**Họ tên**: Lê Duy Bảo

**Mã học viên:** 2A202602749

## Phase 0 - Phạm vi

### Ghi phạm vi, mỗi mục một dòng

**Dự án:** AI gateway

**Persona:** người quản lý hạ tầng và tài nguyên AI

**Core job:** quản lý routing tập trung đến đúng model/provider cho từng request của các team để tối ưu chi phí và latency, đồng thời đáp ứng yêu cầu chất lượng và ngân sách.

## Phase 1 - Core Action

### Phân biệt bốn khái niệm

| Thành phần | Câu trả lời |
|---|---|
| Core job | Quản lý routing và tài nguyên AI tập trung cho các team. |
| Core action | Kiểm tra kết quả vận hành của một routing plan và quyết định giữ nguyên hoặc điều chỉnh. |
| Core value | Kiểm soát được routing, chi phí và latency theo yêu cầu của từng team. |
| Core value event | Hoàn tất một lần kiểm tra có dữ liệu request thực tế và ghi nhận quyết định routing. |

### Điền Core Action Card

| Thành phần | Câu trả lời |
|---|---|
| Target user | Nhân viên quản lý hạ tầng và tài nguyên AI. |
| Core job | Đảm bảo request được routing phù hợp trong giới hạn chất lượng, chi phí và latency. |
| Core action | Kiểm tra kết quả policies đang vận hành và quyết định giữ nguyên hoặc điều chỉnh. |
| Object | Routing policies và dữ liệu vận hành của một team/project. |
| Preconditions | Policies đã có hiệu lực, có request thực tế, có dữ liệu model/provider, chi phí, latency, error logs , fallback về baseline  và kết quả đánh giá chất lượng khi cần. |
| Completion rule | Người quản lý đối chiếu kết quả với các ngưỡng đã thống nhất, ghi nhận quyết định; nếu điều chỉnh thì policy mới phải được áp dụng thành công. |
| Core value | Biết tài nguyên AI đang được sử dụng thế nào và kiểm soát được các sai lệch cần xử lý. |
| Evidence of value | Dữ liệu request, kết quả đối chiếu ngưỡng và quyết định gắn với policy version. |
| Candidate event | `routing_completed` |

### Tự kiểm 5 tiêu chí

- [x] Gần core value: hành vi xảy ra là người dùng đã tới gần giá trị rõ rệt
- [x] Lặp lại được: hành vi xuất hiện lại khi nhu cầu quay lại
- [x] Quan sát được: biết chính xác khi nào nó hoàn tất
- [x] Có ý nghĩa: hành vi tăng thật sự nghĩa là sản phẩm tốt hơn
- [x] Tác động được: team cải thiện được khả năng nó xảy ra


## Phase 2 - Nature & cadence

### Điền Action Nature Card

| Thành phần | Câu trả lời |
|---|---|
| Actor | Nhân viên quản lý hạ tầng và tài nguyên AI. |
| Intent | Xác nhận routing đang đáp ứng yêu cầu và xử lý sai lệch về tài nguyên AI. |
| Trigger | Đến kỳ kiểm tra; onboard team; thay đổi budget/model/provider; phát hiện chi phí, latency hoặc lỗi bất thường. |
| Effort | Xem dashboard, đối chiếu policy và ra quyết định; tăng effort khi cần điều tra hoặc điều chỉnh. |
| Value timing | Khi hoàn tất kiểm tra và quyết định vận hành; hiệu quả điều chỉnh cần quan sát ở các request tiếp theo. |
| State | Policy đang chạy → chạm budget hoặc phát hiện bất thường → kiểm tra → giữ nguyên hoặc điều chỉnh → tiếp tục theo dõi. |
| Dependency | Dữ liệu đủ và chính xác; quyền quản lý; ngưỡng đã cấu hình; workload thực tế. |
| Repeat condition | Xuất hiện kỳ kiểm tra tiếp theo hoặc thay đổi/sai lệch cần xử lý. |

### Kết luận cadence

**Dạng hành vi:** Kiểm tra định kỳ kết hợp xử lý theo sự kiện vận hành.

**Kết luận:** Đối với **nhân viên quản lý hạ tầng và tài nguyên AI**, core action **kiểm tra kết qu ả policy và quyết định vận hành** thường xuất hiện **theo phiên kiểm tra hoặc khi có bất thường** vì **nhu cầu quản lý phụ thuộc vào lịch vận hành và thay đổi tài nguyên AI**. Do đó, nhịp đo phù hợp là **theo chu kỳ kiểm tra đã thống nhất.


## Phase 3 - Metric System + Retention Definition

### Activation metric

| Thành phần | Câu trả lời |
|---|---|
| Start event | `routing_setup_started`: người quản lý bắt đầu thiết lập policies routing và config riêng cho các team/project nếu có. |
| Activation event | `routing_completed` đầu tiên sau khi policy có hiệu lực và có request thực tế. |
| Time window | Activation rate = người quản lý activated trong 7 ngày / người bắt đầu thiết lập đã có đủ 7 ngày quan sát. |

### Engagement metric

**Góc đo:** Mức độ hoàn thành kiểm tra; phạm vi quản lý.

**Engagement metric của bạn:** Review completion rate = lượt kiểm tra hoàn tất / lượt kiểm tra đến hạn hoặc phát sinh cần xử lý; management coverage = team/project được kiểm tra trong kỳ / team/project có nhu cầu kiểm tra thuộc phạm vi phụ trách. Không tính lượt kiểm tra lặp lại không có dữ liệu hoặc nhu cầu mới.

### Retention Definition

| Thành phần | Câu trả lời |
|---|---|
| Unit | Một người quản lý, xác định bằng user ID. |
| Cohort entry | Tuần người quản lý hoàn thành activation lần đầu. |
| Return event | Hoàn tất ít nhất một `routing_completed` cho nhu cầu kiểm tra mới. |
| Window | Tuần W1, W2, W3… sau tuần activation W0; đề xuất cho pilot có lịch kiểm tra hàng tuần. |
| Threshold | Ít nhất một lượt kiểm tra hợp lệ trong tuần; chưa dùng ngưỡng này để xác định core user. |
| Segment | Theo số team/project phụ trách, workload và lịch kiểm tra; báo riêng người không có nhu cầu kiểm tra trong kỳ. |

### North Star, leading, counter

**North Star Metric:** **Số team/project được quản lý routing** đạt **kiểm tra đúng hạn, có dữ liệu request thực tế và quyết định vận hành được ghi nhận theo tiêu chí đã thống nhất** mỗi **tuần**

**Leading indicators :**

- Activation rate trong 7 ngày.
- Tỷ lệ team/project có đủ dữ liệu để kiểm tra.
- Review completion rate trong kỳ.

**Counter-metric:**

- Tỷ lệ vi phạm policy và vượt budget trên request thực tế.
- Tỷ lệ request vượt giới hạn latency hoặc output không đạt chất lượng trên mẫu được đánh giá.
- Thời gian người quản lý cần để hoàn tất một lượt kiểm tra, tránh tăng metric bằng cách tăng việc thủ công.


## Phase 4:Product Loop + Tracking nhanh

### Product Loop

**Chu kỳ 1:** Người quản lý thiết lập policy → request thực tế chạy qua Gateway → dữ liệu vận hành được tổng hợp → người quản lý kiểm tra và quyết định giữ nguyên hoặc điều chỉnh.

**Chu kỳ 2:** Policy tiếp tục vận hành hoặc bản điều chỉnh có hiệu lực → request mới tạo dữ liệu mới → đến kỳ kiểm tra hoặc xuất hiện bất thường → người quản lý đánh giá lại kết quả và ra quyết định tiếp theo.

**Loại loop chính:** habit

**Metric hypothesis (bắt buộc):** Nếu loop này hoạt động, metric **review completion rate** sẽ thay đổi theo hướng **tăng** trong **4 tuần pilot**, vì **dữ liệu tập trung giúp người quản lý hoàn tất việc kiểm tra và ra quyết định dễ hơn**. Habit là giả thuyết về việc kiểm tra định kỳ, cần xác nhận bằng hành vi thực tế.

### Tracking nhanh

| Tên event | Ý nghĩa | Ghi nhận lúc | Metric dùng |
|---|---|---|---|
| `routing_setup_started` | Bắt đầu thiết lập routing cho team/project | Khi cấu hình đầu tiên được lưu | Activation rate |
| `routing_review_due` | Một nhu cầu kiểm tra đến hạn hoặc được tạo từ bất thường | Khi hệ thống xác định một lượt kiểm tra cần thực hiện | Mẫu số review completion rate; management coverage |
| `routing_review_data_ready` | Đủ dữ liệu bắt buộc cho lượt kiểm tra | Khi dữ liệu đáp ứng điều kiện kiểm tra | Tỷ lệ team/project có đủ dữ liệu |
| `routing_review_started` | Người quản lý bắt đầu lượt kiểm tra | Khi mở và bắt đầu xử lý một review cụ thể | Thời gian hoàn tất kiểm tra |
| `routing_completed` | Đã đối chiếu dữ liệu và ghi nhận quyết định hợp lệ | Khi quyết định được lưu; nếu thay đổi, policy mới đã áp dụng thành công | Activation; engagement; retention; North Star; thời gian kiểm tra |
| `gateway_request_completed` | Request kết thúc với response hoặc lỗi | Khi request hoàn tất hoặc bị chặn/thất bại | Policy/budget compliance; latency violation |
| `output_quality_evaluated` | Output trong mẫu đã được chấm chất lượng | Khi validator hoặc người chấm hoàn tất | Tỷ lệ output không đạt chất lượng |

**Tiêu chí nghiệm thu:**

- Mỗi review có review ID, user ID, team/project ID, kỳ dữ liệu và policy version; không đếm trùng khi tải lại trang hoặc lưu lại.
- Chỉ ghi `routing_completed` khi có dữ liệu thực tế, kết quả đối chiếu và quyết định; mở dashboard chưa được tính hoàn tất.
- Team/project chỉ được tính một lần trong North Star mỗi tuần và phải hoàn tất các lượt kiểm tra đến hạn trong tuần đó.
- Phân biệt dữ liệu thiếu với kết quả đạt; kiểm tra thủ công event, trace và quyết định trên ít nhất 5 lượt kiểm tra.

## Phase 5-Tự soi lỗi

### Đối chiếu bảy câu, sửa ngay chỗ mắc

- [x] Core action không phải thao tác giao diện hay output của hệ thống
- [x] Activation không phải "xem hết hướng dẫn" hay "đăng nhập"
- [x] Tần suất không cao hơn nhu cầu thật
- [x] Loop có lý do quay lại ngoài thông báo
- [x] Retention không dùng chung một window cho mọi cadence
- [x] Mọi event đều dùng để tính một metric
- [x] Metric nào cũng có event để tính



