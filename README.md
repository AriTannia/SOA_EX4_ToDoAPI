# README - TodoApi

## Giới thiệu

**TodoApi** là một ứng dụng API đơn giản được xây dựng bằng ASP.NET Core để quản lý danh sách việc cần làm (Todo List). API cung cấp các phương thức HTTP để tạo, đọc, cập nhật và xóa (CRUD) các mục Todo.

---

## Cấu trúc dự án

### Các tệp chính

#### `Todo.cs`
- **Mô tả**: Lớp `Todo` đại diện cho một mục việc cần làm.
- **Thuộc tính**:
  - `Id` (int): Mã định danh duy nhất cho mỗi mục.
  - `Name` (string?): Tên của công việc cần làm.
  - `IsComplete` (bool): Trạng thái hoàn thành của công việc.

#### `TodoDb.cs`
- **Mô tả**: Lớp `TodoDb` quản lý kết nối cơ sở dữ liệu sử dụng Entity Framework Core với cơ chế lưu trữ dữ liệu trong bộ nhớ (In-Memory Database).
- **Thuộc tính**:
  - `Todos` (DbSet<Todo>): Bảng chứa danh sách các mục việc cần làm.

#### `Program.cs`
- **Mô tả**: Tệp chính khởi chạy ứng dụng API và định nghĩa các điểm cuối (endpoints) để thao tác với các mục Todo.
- **Cấu hình**:
  - Sử dụng cơ sở dữ liệu trong bộ nhớ với `AddDbContext<TodoDb>()`.
  - Kích hoạt `DatabaseDeveloperPageExceptionFilter()` để hỗ trợ xử lý lỗi khi phát triển.
- **Các điểm cuối API**:
  - `GET /todoitems`: Trả về danh sách tất cả mục Todo.
  - `GET /todoitems/complete`: Trả về danh sách các mục Todo đã hoàn thành.
  - `GET /todoitems/{id}`: Trả về thông tin một mục Todo dựa trên ID.
  - `POST /todoitems`: Tạo một mục Todo mới.
  - `PUT /todoitems/{id}`: Cập nhật thông tin một mục Todo theo ID.
  - `DELETE /todoitems/{id}`: Xóa một mục Todo dựa trên ID.

---
### Tạo tệp `TodoApi.http` với cấu trúc như sau:

##### 1. **Biến Host Address**:  
   - `@TodoApi_HostAddress = https://localhost:7189`  
   - Định nghĩa địa chỉ máy chủ của API để sử dụng cho các truy vấn, giúp tránh việc lặp lại URL.

##### 2. **POST /todoitems**:  
   - Tạo một mục Todo mới.  
   - Dữ liệu mẫu:  
     - `name`: "walk dog"  
     - `isComplete`: `true`

##### 3. **GET /todoitems**:  
   - Lấy danh sách tất cả các mục Todo.

##### 4. **GET /todoitems/complete**:  
   - Lấy danh sách các mục Todo đã hoàn thành (`IsComplete = true`).

##### 5. **GET /todoitems/{id}**:  
   - Lấy thông tin chi tiết của một mục Todo dựa trên `id`.  
   - Ví dụ: `/todoitems/1` lấy mục Todo có `Id = 1`.

##### 6. **PUT /todoitems/{id}**:  
   - Cập nhật thông tin cho một mục Todo dựa trên `id`.  
   - Dữ liệu mẫu:  
     - `name`: "feed fish"  
     - `isComplete`: `false`

##### 7. **DELETE /todoitems/{id}**:  
   - Xóa một mục Todo dựa trên `id`.  
   - Ví dụ: `/todoitems/1` xóa mục Todo có `Id = 1`.
### Hướng dẫn chạy dự án
- Nhấn F5 hoặc nút Start trong Visual Studio để khởi động ứng dụng.
- Mở Endpoint Explorer:
- Vào View > Other Windows > Endpoint Explorer.
- Chọn các phương thức POST, GET, PUT, DELETE trong TodoApi.http và nhấn Send Request để thực hiện truy vấn.
### Yêu cầu hệ thống
- .NET SDK 7.0 hoặc mới hơn.
- Visual Studio 2022 hoặc bất kỳ trình biên dịch .NET hỗ trợ Endpoint Explorer.
