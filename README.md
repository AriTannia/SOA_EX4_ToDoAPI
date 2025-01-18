# README - TodoApi  

## Giới thiệu  
**TodoApi** là một ứng dụng API đơn giản được xây dựng bằng ASP.NET Core để quản lý danh sách việc cần làm (Todo List). API cung cấp các phương thức HTTP để tạo, đọc, cập nhật và xóa (CRUD) các mục Todo.  

---  

## Cấu trúc dự án  

### Các tệp chính  

#### **Todo.cs**  
- **Mô tả**: Lớp Todo đại diện cho một mục việc cần làm.  
- **Thuộc tính**:  
  - `Id` (int): Mã định danh duy nhất cho mỗi mục.  
  - `Name` (string?): Tên của công việc cần làm.  
  - `IsComplete` (bool): Trạng thái hoàn thành của công việc.  

#### **TodoDb.cs**  
- **Mô tả**: Lớp TodoDb quản lý kết nối cơ sở dữ liệu sử dụng Entity Framework Core với cơ chế lưu trữ dữ liệu trong bộ nhớ (In-Memory Database).  
- **Thuộc tính**:  
  - `Todos` (DbSet\<Todo>): Bảng chứa danh sách các mục việc cần làm.  

#### **Program.cs**  
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
## Kết quả đạt được
### Chạy API với Endpoint Explorer
- Sau khi cấu hình xong các phương thức GET, POST, PUT, DELETE trong tệp TodoApi.http, bạn có thể thực hiện các truy vấn API bằng cách:
- Mở Endpoint Explorer:
   - Vào View > Other Windows > Endpoint Explorer trong Visual Studio.
   - Chọn phương thức tương ứng trong tệp TodoApi.http.
   - Nhấn Send Request để gửi truy vấn.
- Lưu ý khi chạy các phương thức:
   - PUT và DELETE: Cần chỉnh sửa tham số id để phù hợp với các mục hiện có trong cơ sở dữ liệu. Ví dụ:
      - PUT /todoitems/1 để cập nhật mục có id = 1.
      - DELETE /todoitems/1 để xóa mục có id = 1.
   - POST: Đảm bảo cung cấp đúng định dạng dữ liệu đầu vào, ví dụ:

```csharp
{
  "name": "walk dog",
  "isComplete": true
}
```
### Kết quả giao diện
- Giao diện và kết quả: Sau khi nhấn Send Request, Visual Studio sẽ hiển thị kết quả truy vấn với thông tin chi tiết như:
- Status: Trạng thái HTTP (ví dụ: 201 Created cho POST thành công).
- Body: Nội dung phản hồi, ví dụ:
```csharp
{
  "id": 1,
  "name": "walk dog",
  "isComplete": true
}
```
