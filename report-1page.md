# FIT4012 Lab 7 - Báo cáo 1 trang: SHA-256

## 1. Mục tiêu / Objective

Mục tiêu của bài thực hành là:

- Hiểu cách hoạt động cơ bản của thuật toán SHA-256.
- Viết chương trình băm chuỗi và file bằng SHA-256.
- Kiểm tra toàn vẹn file với hash SHA-256.
- Băm mật khẩu bằng SHA-256 và mở rộng bằng salt để tăng bảo mật.

## 2. Cách làm / Approach

Quá trình thực hiện:

- Biên dịch các chương trình C++ bằng Makefile.
- Sử dụng `sha256` để kiểm tra known answer vectors và so sánh với kết quả chuẩn.
- Dùng `file_integrity` để tính hash file và xác thực trước/sau khi thay đổi nội dung.
- Dùng `password_hash` để ghi hash mật khẩu và kiểm tra đăng nhập đúng/sai.
- Dùng `salted_password_hash` để tạo hash kèm salt, chứng minh cùng mật khẩu nhưng kết quả hash khác nhau.

## 3. Kết quả / Result

- Hash của chuỗi `abc`:
  - `ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad`
- Hash của file mẫu trước khi sửa (`FIT4012 file integrity test\n`):
  - `35d437939467babb1161bedd39226936cac9730fb854447bf0bf33f0098cca92`
- Kết quả kiểm tra file sau khi sửa nội dung:
  - `[FAIL] File was changed or expected hash is incorrect` (thể hiện file đã bị thay đổi so với hash mong đợi).
- Kết quả đăng nhập với mật khẩu đúng:
  - `[PASS] Login success`
- Kết quả đăng nhập với mật khẩu sai:
  - `[FAIL] Login failed: wrong password`
- Hai bản ghi `salt:hash` của cùng một mật khẩu có giống nhau không?
  - Không giống nhau. Vì mỗi lần đăng ký salt được sinh ngẫu nhiên, nên cùng mật khẩu tạo ra hai bản ghi khác nhau.

## 4. Kết luận / Conclusion

- SHA-256 phát hiện thay đổi dữ liệu bằng cách tạo một giá trị băm 256-bit duy nhất cho từng nội dung. Nếu mọi thay đổi dù chỉ một bit xảy ra, hash sẽ thay đổi hoàn toàn.
- Salt cần thiết khi lưu hash mật khẩu để ngăn hai mật khẩu giống nhau tạo cùng một hash. Salt cũng làm cho các tấn công rainbow table và tra cứu băm trở nên khó hơn.
- SHA-256 demo trong lab chưa nên dùng trực tiếp cho hệ thống xác thực thật vì SHA-256 quá nhanh và không có cơ chế làm chậm/tránh brute-force. Với mật khẩu thực sự, nên dùng thuật toán chuyên dụng như Argon2id, bcrypt hoặc scrypt.
