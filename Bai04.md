# Bài 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Mục tiêu

- Tạo và cấu hình file `.gitignore`.
- Bỏ qua file chứa thông tin nhạy cảm `credentials.txt`.
- Gỡ `credentials.txt` khỏi vùng theo dõi của Git nhưng vẫn giữ file vật lý trên máy.
- Sử dụng `git commit --amend` để sửa commit gần nhất.
- Kiểm tra trạng thái Repository và lịch sử commit.

---

## 2. Tạo file credentials.txt

Tạo file:

```text
credentials.txt
```

File này chứa thông tin nhạy cảm và không được đưa lên Git.

Ví dụ nội dung:

```text
username=demo
password=demo-password
api_key=demo-api-key
```

> Đây chỉ là dữ liệu minh họa. Không sử dụng mật khẩu hoặc API key thật trong repository.

---

## 3. Commit nhầm credentials.txt

Ban đầu file `credentials.txt` được đưa vào Staging Area:

```bash
git add credentials.txt
```

Sau đó commit:

```bash
git commit -m "Add credentials file"
```

File `credentials.txt` lúc này đã được Git theo dõi.

---

## 4. Tạo file .gitignore

Tạo file:

```text
.gitignore
```

Nội dung:

```gitignore
# Sensitive files
credentials.txt
*.env
.env

# IDE files
.idea/
*.iml

# OS generated files
.DS_Store
Thumbs.db

# Logs
*.log
```

Dòng:

```gitignore
credentials.txt
```

giúp Git bỏ qua file `credentials.txt` trong những lần thay đổi hoặc thêm file sau này.

---

## 5. Gỡ credentials.txt khỏi Git nhưng giữ file trên máy

Sử dụng:

```bash
git rm --cached credentials.txt
```

Tùy chọn `--cached` chỉ gỡ file khỏi Git Index/Staging Area.

File vật lý vẫn được giữ lại trong thư mục làm việc.

Kiểm tra:

```bash
git status
```

Git sẽ ghi nhận `credentials.txt` không còn được theo dõi.

---

## 6. Commit thay đổi .gitignore

Đưa `.gitignore` vào Staging Area:

```bash
git add .gitignore
```

Sau đó commit:

```bash
git commit -m "Add gitignore and remove credentials from tracking"
```

Sau commit này:

- `.gitignore` được Git theo dõi.
- `credentials.txt` vẫn tồn tại trên máy.
- `credentials.txt` không còn được Git theo dõi.

---

## 7. Kiểm tra credentials.txt

Kiểm tra file vẫn tồn tại:

```bash
ls credentials.txt
```

Trên Windows PowerShell có thể sử dụng:

```powershell
Test-Path credentials.txt
```

Kết quả:

```text
True
```

Điều này chứng minh file vật lý chưa bị xóa.

---

## 8. Kiểm tra trạng thái Git

Chạy:

```bash
git status
```

Kết quả mong đợi:

```text
nothing to commit, working tree clean
```

File `credentials.txt` không xuất hiện trong danh sách file cần commit.

---

## 9. Sửa commit gần nhất bằng Amend

Sử dụng:

```bash
git commit --amend -m "Configure gitignore and remove sensitive files"
```

Lệnh `--amend` thay thế commit gần nhất bằng một commit mới có nội dung/thông điệp đã chỉnh sửa.

Commit message mới:

```text
Configure gitignore and remove sensitive files
```

---

## 10. Kiểm tra commit gần nhất

Chạy:

```bash
git log -n 1
```

Kết quả mong đợi:

```text
commit xxxxxxx
Author: Đặng Thanh Bình <EMAIL>
Date:   ...

    Configure gitignore and remove sensitive files
```

Commit gần nhất đã có thông điệp mới.

---

## 11. Kiểm tra bằng git status

Chạy:

```bash
git status
```

Kết quả:

```text
nothing to commit, working tree clean
```

File `credentials.txt` vẫn tồn tại trên máy nhưng không còn xuất hiện như một file được Git theo dõi.

---

## 12. Các lệnh chính đã sử dụng

```bash
# Tạo credentials.txt
touch credentials.txt

# Commit nhầm credentials.txt
git add credentials.txt
git commit -m "Add credentials file"

# Tạo .gitignore
git add .gitignore

# Gỡ credentials.txt khỏi Git nhưng giữ file trên máy
git rm --cached credentials.txt

# Commit thay đổi
git commit -m "Add gitignore and remove credentials from tracking"

# Sửa commit gần nhất
git commit --amend -m "Configure gitignore and remove sensitive files"

# Kiểm tra trạng thái
git status

# Kiểm tra commit gần nhất
git log -n 1
```

---

## 13. Kết quả

### File `.gitignore`

Đã cấu hình Git bỏ qua:

```text
credentials.txt
*.env
.env
.idea/
*.iml
.DS_Store
Thumbs.db
*.log
```

### credentials.txt

File đã được gỡ khỏi Git bằng:

```bash
git rm --cached credentials.txt
```

File vật lý vẫn được giữ lại trên máy.

### Commit

Commit gần nhất đã được sửa bằng:

```bash
git commit --amend -m "Configure gitignore and remove sensitive files"
```

### Kiểm tra

```bash
git status
```

Kết quả:

```text
nothing to commit, working tree clean
```

```bash
git log -n 1
```

Hiển thị:

```text
Configure gitignore and remove sensitive files
```

---

## 14. Kết luận

Đã hoàn thành việc quản lý file bị bỏ qua bằng `.gitignore`, gỡ `credentials.txt` khỏi Git bằng `git rm --cached` mà không xóa file vật lý, đồng thời sử dụng `git commit --amend` để sửa thông điệp của commit gần nhất.
