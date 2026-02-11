📑 AI Prompt Engineering: Quy Hoạch Dashboard Generator

Repository này chứa Master Prompt và quy trình tư duy (Thinking Process) để chuyển đổi các văn bản hành chính khô khan (Quyết định phê duyệt, Nhiệm vụ quy hoạch dạng PDF) thành một Dashboard quản trị (Admin Dashboard) tương tác, trực quan, chạy trên một file HTML duy nhất.

🎯 Mục tiêu

Biến đổi dữ liệu phi cấu trúc (Unstructured Data - PDF văn bản) thành giao diện trực quan (Visual Data) giúp lãnh đạo ra quyết định nhanh chóng.

⚠️ Yêu cầu Tiên quyết (Prerequisites)

QUAN TRỌNG: Để sử dụng Prompt này hiệu quả, bạn bắt buộc phải đọc và hiểu rõ văn bản đầu vào. AI là công cụ hiển thị, nhưng tư duy logic và kiểm chứng dữ liệu thuộc về con người.

Trước khi chạy Prompt, hãy tự trả lời các câu hỏi sau về tài liệu gốc:

Pháp lý: Văn bản này là gì? (Quyết định phê duyệt, Nhiệm vụ quy hoạch, hay Điều chỉnh cục bộ?). Ai ký? Ngày ký?

Số liệu cốt lõi (KPIs): Đâu là những con số "sống còn"? (Diện tích quy hoạch, Dân số dự kiến, Tỷ lệ đất giao thông, Mật độ xây dựng).

Phạm vi không gian: Ranh giới Đông-Tây-Nam-Bắc giáp cái gì? (Cần biết để yêu cầu AI vẽ visual map).

Cấu trúc dữ liệu: Các bảng chỉ tiêu trong văn bản đang so sánh cái gì? (Quy chuẩn quốc gia vs Đề xuất của tỉnh).

Lưu ý: Nếu bạn nạp vào một văn bản rác hoặc không hiểu bối cảnh của các con số, Dashboard sinh ra sẽ chỉ đẹp về hình thức nhưng sai lệch về chuyên môn ("Garbage In, Garbage Out").

🛠️ Master Prompt Structure

Prompt được thiết kế theo tư duy Modular, chia làm 4 phần chính. Bạn có thể copy đoạn dưới đây vào ChatGPT/Claude/Gemini.

1. Định danh & Nhiệm vụ (Role & Task)

Đóng vai là một Senior UI/UX Designer và Frontend Developer chuyên về Tailwind CSS. 
Nhiệm vụ của bạn là phân tích dữ liệu từ văn bản được cung cấp và xây dựng một Dashboard quản trị (Admin Dashboard) hiện đại.
Output phải là một file HTML duy nhất (Single-file HTML), có thể chạy ngay trên trình duyệt mà không cần cài đặt môi trường.


2. Yêu cầu Kỹ thuật (Tech Stack)

- Core: HTML5 semantic.
- Styling: Tailwind CSS (Sử dụng CDN). Thiết kế theo phong cách "Clean & Corporate".
- Icons: FontAwesome 6 (CDN).
- Logic: Vanilla JavaScript (ES6+) để xử lý chuyển Tab, Modal. Không dùng React/Vue/jQuery để đảm bảo tính độc lập của file.
- Font: 'Inter' hoặc 'Be Vietnam Pro' (Google Fonts).
- Responsive: Tương thích hoàn toàn Mobile/Tablet/Desktop.


3. Tư duy Trực quan hóa (Visualization Rules)

Thay vì liệt kê văn bản thuần túy, hãy chuyển hóa chúng:
- Ranh giới địa lý (Đông/Tây/Nam/Bắc) -> Dùng CSS vẽ mô hình "Radar" hoặc "La bàn" để định vị.
- Chỉ tiêu so sánh (Quy chuẩn vs Đề xuất) -> Dùng Progress Bar hoặc Chart giả lập bằng CSS.
- Số liệu lớn (Diện tích, Dân số) -> Dùng thẻ KPI Cards với icon nổi bật.


4. Cấu trúc Dashboard (Layout Architecture)

Thiết kế bố cục màn hình gồm:
1. Sidebar: Menu điều hướng (Tổng quan, Chỉ tiêu Kỹ thuật, Pháp lý).
2. Header: Tiêu đề dự án, Số hiệu văn bản, Người ký, Trạng thái (Đã phê duyệt).
3. Main Content (Tabbed Interface):
   - Tab 1 (Executive View): Các chỉ số KPI tổng quan, Bản đồ định vị ranh giới.
   - Tab 2 (Technical details): Các bảng số liệu chi tiết (Đất đai, Hạ tầng, Giáo dục). Sử dụng Tabs con nếu dữ liệu quá nhiều.
   - Tab 3 (Legal): Danh sách căn cứ pháp lý và phân công trách nhiệm.


🚀 Hướng dẫn Sử dụng

Chuẩn bị dữ liệu: Mở file PDF quyết định (Ví dụ: 444/QĐ-UBND).

Thực thi:

Copy nội dung văn bản (hoặc upload file nếu Model hỗ trợ).

Dán Master Prompt ở trên vào.

Kiểm thử & Tinh chỉnh:

Copy code HTML sinh ra, lưu thành file index.html.

Mở bằng trình duyệt (Chrome/Edge).

So sánh ngược lại với file PDF xem các con số có khớp không.

💻 Dành cho Developer (Integration Notes)

Nếu bạn muốn tích hợp giao diện này vào hệ thống thực tế (Java Spring Boot / React):

React Integration:

Tách Sidebar, Header, KPICard thành các Components riêng biệt.

Dữ liệu trong HTML (ví dụ: 714.23 ha) nên được map từ API response.

Java Backend (Spring Boot 21):

Sử dụng Record (Java 14+) để tạo DTO hứng dữ liệu từ Database.

Ví dụ:

public record PlanningStatsDTO(
    String docNumber,
    LocalDate signedDate,
    BigDecimal totalArea,
    Integer population,
    List<BoundaryInfo> boundaries
) {}


🤝 Đóng góp

Mọi ý kiến đóng góp về cách tối ưu Prompt hoặc cải thiện UI/UX đều được hoan nghênh. Vui lòng tạo Issue hoặc Pull Request.

📜 License

MIT License.
