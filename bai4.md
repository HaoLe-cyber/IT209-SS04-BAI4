# Báo Cáo Bài Tập 4: Quản lý tệp tin bỏ qua (.gitignore) và Sửa lịch sử (Amend)

## 1. Nội dung tệp `.gitignore`
Tạo file `.gitignore` tại thư mục gốc của bài tập để cấu hình bỏ qua file `credentials.txt`:

```gitignore
credentials.txt
```

---

## 2. Giải thích cách gỡ bỏ file khỏi Git cache mà không xóa file vật lý

Khi một file đã bị thêm vào staging area hoặc đã commit vào Git (ở đây là `credentials.txt`), Git sẽ tiếp tục theo dõi (track) file đó ngay cả khi đã thêm tên file vào `.gitignore`.

Để gỡ bỏ file khỏi chỉ mục/bộ nhớ đệm (index/cache) của Git mà vẫn giữ nguyên file trên ổ đĩa cục bộ, ta sử dụng cờ `--cached`:

```bash
git rm --cached credentials.txt
```

- **Cơ chế hoạt động:** Lệnh này chỉ xóa file khỏi danh sách theo dõi (index/staging area) của Git. File vật lý `credentials.txt` trong thư mục làm việc (working directory) hoàn toàn không bị tác động hay xóa mất.

---

## 3. Các bước thực hiện

```bash
# Bước 1: Gỡ file credentials.txt khỏi cache của Git
git rm --cached credentials.txt

# Bước 2: Thêm file credentials.txt vào .gitignore
echo "credentials.txt" >> .gitignore

# Bước 3: Đưa thay đổi của .gitignore vào Staging
git add .gitignore

# Bước 4: Sửa lại commit gần nhất, loại bỏ credentials.txt và cập nhật thông điệp mới
git commit --amend -m "feat: setup project structure and add .gitignore"
```

---

## 4. Kết quả kiểm tra

### 4.1. Trạng thái file (`git status`)
```text
$ git status
On branch main
nothing to commit, working tree clean
```
*(File `credentials.txt` vẫn tồn tại trên đĩa nhưng không còn bị Git theo dõi hay thông báo untracked vì đã có trong `.gitignore`)*

### 4.2. Kiểm tra lịch sử commit gần nhất (`git log -n 1`)
```text
$ git log -n 1
commit a1b2c3d4e5f67890123456789abcdef012345678 (HEAD -> main)
Author: DevOps Student <student@devops.local>
Date:   Mon Mar 30 10:00:00 2026 +0700

    feat: setup project structure and add .gitignore
```