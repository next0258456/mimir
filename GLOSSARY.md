# Domain Glossary (Từ Điển Khái Niệm Nghiệp Vụ)

Tài liệu này định nghĩa ngôn ngữ chung (Ubiquitous Language) cho Tầng 4 (Knowledge & Semantic Layer) và Tầng 5 (AI Gateway & Orchestration Layer) trong hệ sinh thái **Yggdrasil**.

---

## 1. Kiến Trúc Kho Tri Thức & Bộ Nhớ (Knowledge & Memory)

- **Library (RAG Library)**: Thực thể quản trị tri thức và bộ nhớ tập trung, bao gồm bốn thành phần cốt lõi: `Librarian`, `DNS Semantic Tree`, `STM` và `LTM`.
- **Librarian**: Tác nhân điều hướng ngữ nghĩa bên trong `Library`, vận hành theo cơ chế ra quyết định (Decision-driven Semantic Router) dựa trên các `Decision Table` để định vị chính xác tọa độ tài liệu hoặc xác nhận sự vắng mặt của tri thức.
- **DNS Semantic Tree**: Cây phân loại tri thức phân tầng sử dụng hệ quy chiếu tọa độ 4 bậc dạng IPv4 (mỗi bậc từ `1` đến `255` ánh xạ trực tiếp tới tài liệu nguyên tử, trong khi giá trị `0` được dành riêng cho các mã điều khiển kỹ thuật như báo lỗi không tồn tại hoặc cấp phát nhánh mới).
- **Decision Table (Bảng Quyết Định)**: Bảng mục lục ngữ nghĩa (định danh riêng bằng hậu tố `.dt`) đặt tại mỗi nút nhánh của `DNS Semantic Tree`, mô tả phạm vi ý nghĩa của các nhánh con trực thuộc để `Librarian` ra quyết định rẽ nhánh hoặc mở rộng cây.
- **Split Domain**: Cơ chế phân nhánh leo thang tự động kích hoạt khi một nhánh lá chạm trần sức chứa (`255` tài liệu), nhằm chia nhỏ không gian tri thức và giữ mật độ lựa chọn tại mỗi nút luôn trong ngưỡng an toàn.
- **Merge-Split Rebalancing (Gộp – Tách Cân Bằng)**: Thao tác quy hoạch lại cây tri thức dưới quyền kiểm soát chủ động của kỹ sư dựa trên hai chỉ số **`Semantic Density` (Mật độ ngữ nghĩa)** và **`Semantic Diversity` (Độ đa dạng/phân tán ngữ nghĩa)**, bằng cách gộp các nhánh lệch hoặc thưa thớt rồi tái phân chia thành các nhánh mới có độ phủ cân bằng, đồng thời cập nhật tức thời mọi liên kết chéo trong toàn hệ thống.
- **STM (Short-Term Memory)**: Bộ nhớ ngắn hạn theo từng chu kỳ ngày, lưu giữ cặp *[Bản tóm tắt + Tọa độ tài liệu]* của các truy vấn vừa phát sinh và luôn được ưu tiên tra cứu cao hơn `LTM`.
- **LTM (Long-Term Memory)**: Sổ ghi tri thức dài hạn được tích lũy bền vững qua nhiều chu kỳ vận hành.
- **Dreaming**: Chu trình chắt lọc tri thức chạy trên cửa sổ các `STM` gần nhất kết hợp với nhật ký `Split/Merge` để đo tần suất truy cập, đồng bộ tọa độ mới và kết tinh tri thức vào `LTM`, sau đó đào thải `STM` cũ nhất và mở `STM` mới cho chu kỳ tiếp theo.
- **Unroutable Sentinel (`0.0.0.0`)**: Tín hiệu trả về mang tính tất định khẳng định yêu cầu truy vấn không tồn tại trong phạm vi tri thức của `Library`, buộc tác nhân gọi phải dừng suy luận thay vì đoán mò.

---

## 2. Vật Lý Ngữ Cảnh & Ngữ Nghĩa Nghiệp Vụ (Context Physics & Semantics)

- **Prompt Entropy**: Mức độ nhiễu loạn, phân mảnh ngữ cảnh hoặc xung đột ràng buộc bên trong một khối thông tin nạp vào mô hình (thường bị đẩy cao bởi việc băm nhỏ tài liệu, lặp đoạn gối đầu `overlap`, hoặc nhồi nhét tài liệu dư thừa).
- **Attention Collapse**: Trạng thái suy sụp khả năng tập trung của mô hình ngôn ngữ khi `Prompt Entropy` vượt ngưỡng chịu đựng, khiến mô hình bỏ qua các quy tắc bắt buộc hoặc thông tin trọng yếu dù dung lượng văn bản chưa vượt giới hạn bộ nhớ (Context Window).
- **Vector Density Collapse (Sụp đổ Mật độ Vector)**: Hiện tượng không gian nhúng bị lấp đầy quá dày đặc ở quy mô hàng triệu phân đoạn, khiến điểm tương đồng ngữ nghĩa giữa hàng ngàn tài liệu khác nhau tiệm cận mức ngang bằng và làm tê liệt khả năng phân biệt ngữ cảnh của tìm kiếm Vector.
- **Data-Blind AI**: Nguyên tắc cô lập dữ liệu tuyệt đối quy định mô hình ngôn ngữ chỉ được phép tiếp cận siêu dữ liệu (định nghĩa nghiệp vụ, lược đồ cấu trúc, quy tắc) để hiểu ý định và lập kế hoạch truy vấn; kết quả dữ liệu thực thi được chuyển thẳng tới người dùng cuối mà không bao giờ quay ngược lại qua mô hình.
- **Data Trap**: Quy tắc cảnh báo gắn trực tiếp vào thực thể dữ liệu nhằm phơi bày các dị biệt lịch sử, trường dữ liệu lỗi hoặc công thức bắt buộc, giúp AI tránh sinh ra truy vấn sai bản chất nghiệp vụ.

---

## 3. Điều Phối Truy Vấn & Kiểm Soát Vòng Lặp (Orchestration & Control)

- **Dual-Track Routing (Định tuyến Luồng Kép)**: Cơ chế phân tách yêu cầu đầu vào thành hai đường ray độc lập: luồng tra cứu văn bản/quy trình nhẹ được phép lặp qua mô hình tự nhiên, và luồng truy xuất dữ liệu nghiệp vụ nặng bị cắt vòng lặp để bảo vệ tài nguyên hạ tầng.
- **Single-Hop Execution (Thực thi Một Nhịp)**: Ràng buộc trên luồng dữ liệu cưỡng chế mô hình ngôn ngữ chỉ thực hiện đúng một nhịp sinh truy vấn từ siêu dữ liệu, sau đó tầng thực thi trả thẳng kết quả (hoặc thông báo từ chối truy cập/không có dữ liệu) về cho người dùng mà không vòng ngược lại qua mô hình, triệt tiêu hoàn toàn hành vi tự lặp sửa lỗi truy vấn và rò rỉ dữ liệu thô.
