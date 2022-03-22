# Tìm hiều về Linux[3]
## FHS:
**Filesystem Hierarchy Standard**, viết tắt là **FHS**, là một tiêu chuẩn thiết kế các thư mục trong hệ thống các Linux distributions . Filesystem Hierarchy Standard được tạo ra và duy trì/cập nhập bởi [Linux Foundation](https://www.linuxfoundation.org/). Đến nay, FHS cũng đã qua nhiều lần thay đổi. Hiện tại, bản define mới nhất về FHS là phiên bản 3.0, được release vào ngày 3/6/2015.
Nhìn chung thì các Linux Distribution phổ biến đều tuân thủ theo hầu hết các quy tắc của FHS, để giúp người dùng có được những trải nghiệm quen thuộc khi chuyển đổi giữa các họ Distribution. Ngoài ra, những quy tắc của FHS cũng có rất nhiều điểm giống với các hệ điều hành Unix-like khác, chẳng hạn như MacOS, do đó bạn cũng có thể thấy có nhiều điểm tương đồng ở đây.
Mục đích của việc tạo ra và tuân thủ FHS là để:
-   Giúp cho các phần mềm khi cài đặt có thể phán đoán được nơi sẽ lưu trữ các file hay thư mục của mình, hay của phần mềm khác đã được cài đặt từ trước.
-   Giúp cho người dùng có thể phán đoán được nơi sẽ lưu trữ các file, hay thư mục của một phần mềm nào đó

Để thực hiện điều đó thì FHS:
-   Đưa ra một vài nguyên tắc hướng dẫn chung cho cách phân bổ thư mục trong filesystem
-   Chỉ định các file và thư mục tối thiểu cần phải có của một hệ thống
-   Đưa ra các ngoại lệ cho từng nguyên tắc
## Filesystem:
Hầu hết các Linux distributions đều sử dụng và tuân thủ FHS như đã nói bên trên. Chính vì vậy nên ta cần phải để ý đến một vài khái niệm quan trọng trong FHS đó là: "shareble / unshareable" và "variable / static", nói tiếng Việt thì nó sẽ là "chia sẻ được/không chia sẻ được" và "bất định/cố định".
Các file có thuộc tính ***Shareable*** là các file được lưu trữ ở tại một địa chỉ và có khả năng truy cập và sử dụng ở nơi khác. Trong khi đó, ***Unshareable*** thì ngược lại. Ví dụ như các file trong  thư mục `home` của người dùng là "shareable" trong khi đó thì các [Lock-files](https://tldp.org/HOWTO/Serial-HOWTO-13.html#:~:text=A%20lock%2Dfile%20is%20simply,files%20are%20usually%20named%20LCK..) thì không.
Đối với thuộc tính ***Static*** và ***Variable*** thì khá dễ nhận biết. Các file với thuộc tính ***Static*** thường là các binary / lib / doc files của hệ thống mà bắt buộc cần có quyền `root` để có thể thực hiện thay đổi. Ngược lại với file có thuộc tính ***Variable*** thì sẽ là các file logs / spool / ... có thể thay đổi bởi người dùng bình thường.

|  | ***Shareable*** | ***Unshareable*** |
| -- | -- | -- |
| ***Static*** | `/urs`<br/> `/opt` | `/etc`<br/> `/boot` |
| ***Variable*** | `/var/mail`<br/> `var/spool/news` | `/var/run`<br/> `/var/lock` (chứa các lock-files) |


