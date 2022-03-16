# Tìm hiều về Linux [2]
Trong phần này, ta sẽ đi tìm hiểu các kiến thức liên quan đến các tiến trình trong Linux.
>Tất cả kiến thức được viết bên dưới  được dựa vào cuốn sách: **[LPIC]Linux Professional Institute Certification Study Guide**
# Phần mềm & Tiến trình (Software & Processes)

## Sử dụng `dpkg`:
`dpkg` viết tắt của Debian Packeges, là một chương trình quản lý cài đặt phần mềm trên các hệ điều hành như Ubuntu.
Một file cài đặt DPKG thường có đuôi là `.deb` và có định dạng như sau:
`PACKAGE_NAME-VERSION-RELEASE.ARCHITECTURE.deb`

Trong đó:
***`PACKAGE_NAME`*** : đây sẽ là tên của phần mềm. Ví dụ như ta muốn cài đặt trình biên soạn `emacs`, thì file RPM của nó sẽ có tên là `emacs`. Nhưng lưu ý rằng, mỗi một phiên bản Linux khác nhau thì sẽ có tên gói khác nhau.

***`VERSION`*** : đây là số phiên bản của chương trình. Bình thường số phiên bản sẽ bao gồm 2 đến 3 số cách nhau bởi dấu `.`. Ví dụ: 1.13.1 hay 7.4p1.

***`RELEASE`*** : hay còn được gọi là số bản dựng (build number). Nó tượng trưng cho nhưng thay đổi nhỏ trong chương trình nhưng chưa đủ để nâng cấp chương trình lên một phiên bản mới.

***`ARCHITECTURE`*** : đây là phần mà nhà phát triển chỉ định rằng phần mềm này được tối ưu cho kiến trúc CPU nào. Ví dụ như `x86_64` dành cho các CPU 64 bit hoặc `noarch` là dành cho tất cả các kiến trúc.

### Hiển thị các gói `.deb`:
```
tomtpc@training:~$ ls -1 *.deb
docker_1.5-1build1_amd64.deb 
emacs_47.0_all.deb 
openssh-client_1%3a7.6p1-4ubuntu0.3_amd64.deb
vim_2%3a8.0.1453-1ubuntu1_amd64.deb 
zsh_5.4.2-3ubuntu3.1_amd64.deb
```
***Lưu ý:*** Nếu muốn cài đặt một gói phần mềm `.deb` như gói phần mềm *vim* thì ta có thể sử dụng câu lệnh `sudo apt-get download vim`, gói phần mềm sẽ được tải về và lưu tại thư mục hiện tại đang hoạt động của người dùng.

Cấu trúc lệnh `dpkg`:
`dpkg [Tùy Chọn]... [File]...`
Trong đó ta có các tùy chọn sau:
| Viết tắt | Đầy đủ | Ý nghĩa |
|--|--|--|
| -c | - - contents | Hiển thị nội dung file cài đặt |
| -C | - -audit | Tìm kiếm các gói cài đặt bị lỗi và đề suất cách sửa |
| N/A | - -configure | Thay đổi cài đặt của gói đã cài |
| N/A | - -get-selections | Hiển thị các gói đã cài |
| -i | - -install | Cài đặt gói / nếu đã cài thì nâng cấp |
| -I | - -info | Hiển thị thông tin về gói đã gỡ cài đặt |
| -l | - -list | Hiện thị các gói có chung định dạng |
| -L | - - listfiles | Hiện thị các files liên quan đến gói |
| -p | - -print-avail | Hiển thị thông tin về gói đã cài đặt |
| -P | - -purge | Xóa gói cài đặt và các file cấu hình |
| -r | - - remove | Xóa gói cài đặt nhưng giữ lại các file cấu hình |
| -s | - -status | Hiển thị trạng thái của gói |
| -S | - -search | Tìm kiếm các gói liên quan đến file |



