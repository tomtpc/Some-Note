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
|:--:|:--:|:--:|
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

### Quản lý các tiến trình hoạt động:
Chương trình trong Linux sau khi được khởi động và chạy thì sẽ được ghi danh ở trong hệ thống Linux là một tiến trình đi kèm với nó là một **PID** (Process ID). Chương trình có thể là chương trình can thiệp tới giao diện người dùng như `cat`, `less` hoặc là các chương trình chạy ở BackGround, hay còn gọi là **Daemon Program**.
Khi một chương trình chạy, nó có thể gọi đến nhiều chương trình con khác, hay nói cách khác là tiến trình cha sinh tiến trình con.
Chính vì vậy, việc quản lý các chương trình/tiến trình trong Linux là điều thiết yếu để kiểm soát hệ thống, phòng tránh lỗi và phát hiện những tiến trình lạ.
#### Các trạng thái của tiến trình:
Trong Linux, một tiến trình 5 trạng thái khác nhau, mỗi một trạng thái đều có một ý nghĩa riêng, hiểu và nhận biết được các trạng thái sẽ giúp ta khắp phục lỗi hệ thống dễ dàng hơn.
Năm trạng thái đó là: **Running& Runnable**, **Interrptable_sleep**,  **Uninterruptable_sleep**,  **Sleep**,  **Zombie**. Các trạng thái này sẽ được hiển thị nếu như ta sử dụng các câu lệnh `ps`, `top`, `htop` hoặc `atop`, các lệnh này sẽ cho ta biết các thông tin cơ bản về tiến trình đang chạy.
Khi hiển thị, các trạng thái sẽ được viết tắt chứ không có viết đầy đủ.
| Trạng Thái | Viết Tắt |
|:---:|:---:|
| UNINTERRUPTABLE_SLEEP | `D` |
| RUNNING & RUNNABLE | `R`|
| INTERRRUPTABLE_SLEEP | `S` |
| STOPPED | `T` |
| ZOMBIE | `Z` |

 - **RUNNING & RUNNABLE**: để ý trong bảng bên trên thì, khi hiển thị thông tin tiến trình, trạng thái **RUNNING** và **RUNNABLE** đều được ký hiệu chung là `R`. Điểm khác nhau giữa 2 trạng thái này, như tên gọi, **RUNNABLE** là trạng thái tiến trình đã sẵn sàng để chạy, nhưng vì một lý do nào đó mà CPU chưa lên lịch chạy để chuyển sang **RUNNING**. []()
 - **INTERRRUPTABLE_SLEEP**:
 - **UNINTERRUPTABLE_SLEEP**:
 - **STOPPED**:
 - **ZOMBIE**:

#### Câu lệnh `ps`:
Câu lệnh `ps` là 1 câu lệnh phổ biến để hiển thị các tiến trình đang hoạt động, đi kèm theo đó là một số thông tin cơ bản của nó.
`ps [Tùy Chọn]...`
Mặc định nếu như ta không sử dụng `[Tùy Chọn]` thì `ps` sẽ in lên màn hình các tiến trình đang hoạt động và được sử dụng bởi người dùng hiện tại trong phiên đăng nhập hiện tại.
```
tomtpc@training:~$ ps
    PID TTY          TIME CMD
   1486 pts/2    00:00:00 bash
  67635 pts/2    00:00:00 ps
tomtpc@training:~$
```
Trong đó:

 - `PID`: Process ID, ID định danh của tiến trình (là 1 số độc nhất trong phiên hoạt động của hệ thống).
 - `TTY`: Tele Type Terminal, ám chỉ Terminal đang chạy tiến trình đó.
 - `TIME`: thời gian chiếm, dụng của tiến trình tương ứng với nó.
 - `CMD`: tên của câu lệnh khởi động tiến trình tương ứng.

Đặt vào một trường hợp khác, nếu như ta muốn hiển thị toàn bộ các tiến trình đang hoạt động thì sao. `ps` cung cấp tùy chọn `-a -u x`, hoặc ta có thể viết tắt là `-aux`, đối với `-a` thì nó sẽ liệt kê toàn bộ thông tin của các tiến trình bao gồm: 
|  | Ý nghĩa |
|:--:|:--:|
| USER |  |
| PID |  |
| %CPU |  |
| %MEM |  |
| VSZ |  |
| RSS |  |
| TTY |  |
| STAT |  |
| TIME |  |
| COMMAND |  |

