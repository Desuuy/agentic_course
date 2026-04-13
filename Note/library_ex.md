
# Nội dung tệp Markdown giải thích chi tiết các thư viện
markdown_content = """# 📑 Tài liệu Giải thích Thư viện: Agentic RAG & LangGraph

Tệp này tóm tắt các nhóm thư viện chính được sử dụng để xây dựng hệ thống AI Agent có khả năng suy luận, tra cứu và điều phối luồng công việc (workflow).

---

## 1. Nhóm Hệ thống & Cấu hình (System & Config)
Nhóm này xử lý các thao tác nền tảng như quản lý biến môi trường và ghi lại nhật ký hoạt động.

* **`os`**: Dùng để tương tác với hệ điều hành, phổ biến nhất là lấy API Keys từ biến môi trường (`os.getenv`) để đảm bảo bảo mật.
* **`logging`**: Cực kỳ quan trọng để theo dõi luồng chạy của Agent. Nó giúp bạn biết Node nào đang chạy, LLM đang "suy nghĩ" gì hoặc lỗi phát sinh tại đâu trong Graph.
* **`python-dotenv` (`load_dotenv`)**: Tự động nạp các biến từ tệp `.env` vào môi trường hệ thống, giúp bạn không phải hard-code thông tin nhạy cảm.

---

## 2. Nhóm Định nghĩa Kiểu dữ liệu (Typing)
Đảm bảo tính chặt chẽ của dữ liệu (Type Safety) khi luân chuyển giữa các Node trong đồ thị.

* **`TypedDict`**: Dùng để định nghĩa cấu trúc của **State** (Trạng thái). Ví dụ: State của bạn gồm danh sách tin nhắn, biến đếm, hoặc kết quả truy vấn.
* **`Literal`**: Giới hạn giá trị của biến trong một tập hợp cụ thể (ví dụ: `Literal["yes", "no"]`). Thường dùng để chỉ định các nhánh rẽ trong đồ thị.

---

## 3. Nhóm LangGraph - Xây dựng Luồng (Graph Logic)
Đây là khung xương điều khiển logic của Agent, cho phép tạo ra các vòng lặp (loops) và quản lý trạng thái phức tạp.



* **`StateGraph`**: Lớp chính để xây dựng đồ thị. Bạn dùng nó để thêm các Node (hành động) và Edge (đường nối giữa các hành động).
* **`MessagesState`**: Một kiểu State có sẵn chuyên dùng để quản lý lịch sử hội thoại (danh sách các tin nhắn).
* **`START` / `END`**: Các node đặc biệt đại diện cho điểm bắt đầu và kết thúc của một luồng xử lý.
* **`Command`**: Công cụ mạnh mẽ cho phép một Node điều hướng động (ví dụ: yêu cầu Graph nhảy tới một Node bất kỳ hoặc cập nhật State ngay lập tức).

---

## 4. Nhóm Prebuilt & Tools (Tiện ích có sẵn)
Các thành phần giúp giảm bớt việc viết code thủ công cho các tác vụ phổ biến.

* **`ToolNode`**: Một Node đặc biệt tự động thực thi các hàm (tools) khi LLM yêu cầu gọi (`tool_calls`).
* **`tools_condition`**: Hàm logic tích hợp sẵn để kiểm tra xem LLM có muốn gọi tool hay không. Nếu có, nó dẫn hướng sang `ToolNode`, nếu không, nó dẫn tới `END`.
* **`TavilyClient`**: API tìm kiếm tối ưu cho AI, giúp Agent lấy dữ liệu thời gian thực từ Internet một cách chính xác hơn các bộ máy tìm kiếm thông thường.

---

## 5. Nhóm Core LangChain (Adapters & Messages)
Các thành phần cơ bản để giao tiếp với các mô hình AI khác nhau.

* **`ChatGoogleGenerativeAI`**: Adapter để gọi các model Gemini (Pro, Flash).
* **`ChatOpenAI`**: Adapter để gọi các model GPT của OpenAI.
* **`@tool`**: Decorator biến một hàm Python bình thường thành một công cụ mà LLM có thể hiểu và sử dụng (thông qua docstring).
* **`HumanMessage`**: Đối tượng đại diện cho tin nhắn đầu vào từ người dùng.

---

## 💡 Lưu ý cho lập trình viên
Trong dự án sử dụng LangGraph, bạn nên tập trung vào việc quản lý **State** (Trạng thái). Thay vì dùng `create_agent` truyền thống, việc tự xây dựng Node với `ChatGoogleGenerativeAI` kết hợp với `ToolNode` trong LangGraph sẽ giúp bạn kiểm soát hoàn toàn logic của một hệ thống **Agentic RAG**.
"""
