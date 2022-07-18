# ***Content***
- [***Git rules***](#git-rules)
- [***Git workflow***](#git-workflow)
- [***Git good commit***](#git-good-commit)

## Git Rules
- Triển khai code trên 1 nhánh riêng: có thể thoải mái tạo pull request mà không sợ làm ảnh hướng đến nhánh `master`
- Tạo các nhánh con từ nhánh `develop`: đảm bảo nhánh `master` có thể sử dụng trực tiếp để release ra
- Không được push trực tiếp vào 2 nhánh `develop` và `master` mà hãy tạo 1 *pull request*: Thông báo cho cả team về việc vừa hoàn thành 1 tính năng, cũng như dễ dàng review code trước khi *push*
- Trước khi *push* hay tạo 1 *pull request* cần update branch `develop` và tạo `rebase` để lịch sử commit đẹp hơn
- Xử lý các conflits trong khi `rebase` và trước khi tạo pull request
- Sau khi `merge` 1 nhánh thì nên xóa nhánh đó đi
- Trước khi tạo `pull request`, cần kiểm tra xem nó đã xây dựng đúng chưa, có qua dc các test không (bao gồm cả coding style)
- Sử dụng file `.gitignore` để khai báo các file không được up lên remote repo
- Các branch `develop` và `master` cần được bảo vệ

## Git Workflow
### Main steps
1. Khởi tạo git repo ở local
2. Tạo một branch cho 1 tính năng hoặc branch fix bugs
3. Thực hiện các thay đổi local (chỉ add các file có thay đổi )
    ```
    git add <file1> <file2> ...
    git commit
    ```
4. Đồng bộ các thay đổi trên remote repository để xử lý các conflits ngay trên local trước khi tạo `pull request`
    ```
    git checkout develop
    git pull
    ```
5. Update các thay đổi gần nhất từ `develop` về feature branch bằng *interative rebase*
    ```
    git checkout <branchname>
    git rebase -i --autosquash develop
    ```
    `--autosquash` để nén tất cả các commit vào thành 1 
6. Nếu có conflits, sửa conflits rồi không commit mà chạy `rebase --continue`
    ```
    git add <file1> <file2> ...
    git rebase --continue
    ```
7. Push branch đó. Vì `rebase` tạo ra các thay đổi trong history nên cần thêm tham số -f
8. Tạo `pull request`
9. Sau khi dc merged, có thể xóa *branch* này đi
    ``` 
    git branch -d <branchname>
    ```
## Git Good Commit
- Chia phần tiêu đề commit và nội dung thành 2 phần
- Giới hạn cho tiêu đề là 50 kí tự và nội dung là 70 kí tự
- Viết hoa chữ cái đầu của tiêu đề
- Không dùng dấu câu để kết thúc tiêu đề
- Tiêu đề nên có dạng câu mệnh lệnh
- Phần nội dung nên trả lời các câu hỏi cái gì, như thế nào, tại sao