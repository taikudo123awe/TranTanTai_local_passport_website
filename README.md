# Ứng dụng Xác thực với Passport.js và EJS

Đây là một dự án ứng dụng web hoàn chỉnh, được render phía server (Server-Side Rendering) để minh họa cách xây dựng một hệ thống xác thực người dùng đầy đủ chức năng. Dự án sử dụng **Passport.js** với chiến lược xác thực cục bộ (`local strategy`) và **EJS** làm view engine để tạo giao diện người dùng.

## Luồng hoạt động của Ứng dụng

1.  Người dùng truy cập trang đăng ký, điền thông tin và tạo tài khoản.
2.  Sau khi đăng ký thành công, người dùng được chuyển hướng đến trang đăng nhập.
3.  Người dùng đăng nhập bằng tài khoản vừa tạo. Nếu thành công, Passport.js sẽ tạo một session và chuyển hướng người dùng đến trang hồ sơ cá nhân (profile).
4.  Trang profile là một route được bảo vệ, chỉ những người dùng đã đăng nhập mới có thể truy cập.
5.  Người dùng có thể đăng xuất, hành động này sẽ hủy session và chuyển hướng họ về trang đăng nhập.

## Các công nghệ và tính năng chính

-   **Framework:** Express.js
-   **View Engine:** EJS (Embedded JavaScript templating)
-   **Cơ sở dữ liệu:** MongoDB với Mongoose ODM.
-   **Xác thực:** Sử dụng **Passport.js** và **passport-local**.
-   **Quản lý Session:** Tích hợp `express-session` để quản lý trạng thái đăng nhập.
-   **Bảo mật:** Mật khẩu được băm (hash) an toàn bằng `bcryptjs`.
-   **Giao diện:** Cung cấp các trang HTML cho Đăng ký, Đăng nhập và Hồ sơ người dùng.
## Yêu cầu

-   [Node.js](https://nodejs.org/) (phiên bản 16.x trở lên)
-   npm (đi kèm với Node.js)
-   [MongoDB](https://www.mongodb.com/try/download/community) phải được cài đặt và đang chạy.

## Cài đặt & Khởi chạy

1.  **Thiết lập dự án:**
    Sao chép tất cả các file mã nguồn vào đúng cấu trúc thư mục như trên. Bạn sẽ cần tự tạo các file trong thư mục `views` (xem mô tả bên dưới).

2.  **Mở Terminal:**
    Di chuyển vào thư mục gốc của dự án.

3.  **Cài đặt các dependency:**
    Chạy lệnh sau để cài đặt tất cả các thư viện cần thiết:
    ```bash
    npm install express mongoose express-session passport passport-local bcryptjs ejs
    ```

4.  **Khởi động MongoDB:**
    Hãy đảm bảo dịch vụ MongoDB của bạn đã được khởi động.

5.  **Khởi động máy chủ:**
    ```bash
    node app.js
    ```
    Bạn sẽ thấy thông báo: `Server running on http://localhost:3000`.

## Mô tả các file View (EJS)

Bạn cần tạo các file `.ejs` sau trong thư mục `/views`:

-   **`register.ejs`**: Chứa một form HTML với các trường `username` và `password`. Form này sẽ có `method="POST"` và `action="/register"`.
-   **`login.ejs`**: Chứa một form HTML tương tự với các trường `username` và `password`. Form này sẽ có `method="POST"` và `action="/login"`.
-   **`profile.ejs`**: Hiển thị thông tin chào mừng người dùng (ví dụ: `<h1>Welcome, <%= user.username %></h1>`) và một link hoặc button để đăng xuất (`<a href="/logout">Logout</a>`).

## Hướng dẫn sử dụng trên Trình duyệt

Vì đây là một ứng dụng web, bạn sẽ tương tác với nó hoàn toàn qua trình duyệt.

1.  **Đăng ký:** Mở trình duyệt và truy cập `http://localhost:3000/register`. Điền vào form và nhấn submit.
2.  **Chuyển hướng:** Sau khi đăng ký thành công, bạn sẽ tự động được chuyển đến trang `http://localhost:3000/login`.
3.  **Đăng nhập:** Nhập thông tin tài khoản bạn vừa tạo và nhấn submit.
4.  **Xem Profile:** Nếu đăng nhập thành công, bạn sẽ được đưa đến trang `http://localhost:3000/profile` và thấy thông tin của mình.
5.  **Thử truy cập trái phép:** Thử truy cập trực tiếp vào `http://localhost:3000/profile` khi chưa đăng nhập. Middleware `isAuthenticated` sẽ chặn bạn và chuyển hướng bạn về trang login.
6.  **Đăng xuất:** Trên trang profile, nhấp vào liên kết đăng xuất. Bạn sẽ được chuyển hướng về trang login và session của bạn sẽ bị hủy.
