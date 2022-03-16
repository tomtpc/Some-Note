# Tìm hiểu về Linux [1]
Trong phần này, ta sẽ học những kiến thức cơ bản nhất về Shell trong Linux.
>Tất cả kiến thức được viết bên dưới  được dựa vào cuốn sách: **[LPIC]Linux Professional Institute Certification Study Guide**
# Shell
Một số phần mềm Shell bạn cần biết:
 - **Bash**: viết tắt của The GNU Bourne Again shell, được phát hành lần đầu vào năm 1989, và thường được sử dụng làm shell mặc định cho các tài khoản người dùng Linux. The Bash shell được phát triển qua dự án GNU như là một sự thay thế cho shell mặc định của hệ thống hệ điều hành Unix, hay còn gọi là Bourne Shell (được đặt tên theo tác giả). Nó cũng tương thích với các hệ điều hành khác như Windows 10, macOS và các hệ điều hành Solaris.
 - **Dash**: được phát hánh lần đầu vào năm 2002, phần mềm shell nhỏ gọn này không cho phép chỉnh sửa dòng lệnh hay là hỗ trợ lịch sử lệnh, nhưng nó cho phép khả năng thực hiện các *script* nhanh hơn.
 - **KornShell**: chính thức ra mắt vào năm 1983, nhưng bị giữ làm phần mềm độc quyền cho đến tận năm 2000. Phền mềm shell này tương thích với Bourne Shell nhưng mà hỗ trợ nhiều chứng năng lập trình cao cấp, ví dụ như những tính năng được hỗ trợ trong ngôn ngữ lập trình C.
 - **tcsh**: ra mắt vào năm 1981, tcsh là viết tắt của *the TENEX C shell* là một phiên bản nâng cấp của C shell.
 - **Z shell**: ra đời vào năm 1990, đây là một shell cao cấp khi có trong mình những tính năng của các shell như Bash, tcsh và KornShell.
 ## Khám phá các tiện ích trong Shell
 ### Hiển thị bin/sh trong nhánh CentOS:
 ```
 tomtpc@training:~$ readlink /bin/sh
 bash
 ```
 ### Hiển thị bin/sh trong  nhánh Ubuntu:
 ```
 tomtpc@training:~$ readlink /bin/sh
 dash
 ```
 ### Hiển thị Shell hiện tại đang sử dụng trong nhánh CentOS:
 ```
 tomtpc@training:~$ echo $SHELL
 /bin/bash
 tomtpc@training:~$ echo $BASH_VERSION
 4.2.46(2)-release
 ```
Để ý thấy trong câu lệnh `echo $SHELL`, ta có biến môi trường là `SHELL` đi kèm trước nó là dấu `$`, dấu này được thêm vào trước tên biến để ta có thể truy cập vào dữ liệu được lưu bên trong.
### Hiển thị Shell hiện tại đang sử dụng trong nháng Ubuntu:
```
tomtpc@training:~$ uname
Linux
tomtpc@training:~$ uname -r
5.4.0-100-generic
tomtpc@training:~$ uname -a
Linux training 5.4.0-100-generic #113-Ubuntu SMP Thu Feb 3 18:43:29 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
```
Khi sử dụng một mình mà không có các tham số tùy chọn khác, câu lệnh `uname` sẽ chỉ trả về cho ta kết quả là tên của nhân ( cụ thể ở đây là *Linux*). Nếu như muốn biết thêm thông tin ví dụ như là phiên bản hiện tại của nhân, ta thêm tùy chọn `-r` (viết tắt của *revision* ) vào sau câu lệnh. Để xem tất cả các thông tin như loại kiến trúc vi xử lý, tên của hệ điều hành thì thêm tùy chọn `-a` đằng sau câu lệnh.

## Sử dụng Shell để chạy chương trình:
Để chạy một chương trình trong Shell, trong giao diện dòng lênh, ta chỉ cần gõ câu lệnh của chương trình đó, sử dụng đúng cú pháp, và bấm **Enter** để thực thi. Câu lệnh `echo`, đã được sử dụng bên trên, là một chương trình đơn giản để ta bắt đầu chủ đề này. Chương trình đơn giản này có cú pháp như sau:
`echo [TÙY CHỌN]... [CHUỖI]...`
Trong  cấu trúc câu lệnh `echo`, `[TÙY CHỌN]` có nghĩa là có các tùy chọn khác nhau trong câu lệnh, các tùy chọn này thay đổi đầu ra của câu lệnh, cặp dấu [ ] biểu thị rằng đây là một lựa chọn không bắt buộc phải có khi thực thi câu lệnh. `CHUỖI` phần mục chứa giá trị mà ta muốn hiển thị lên trên màn hình và nó cũng là không bắt buộc vì được bao quanh bởi cặp dấu [ ].
Dưới đây là ví dụ sử dụng lệnh `echo` để dễ hình dung hơn:
```
tomtpc@training:~$ echo I love Linux
I love Linux
```
### Các siêu ký tự trích dẫn:
Ta sẽ sử dụng câu lệnh `echo` để minh họa một chức năng khá hữu dụng khác trong Shell: trích dẫn Shell. Trong Bash Shell, ta có một vài ký tự có ý nghĩa đặc biệt và chúng đều có chức năng riêng của mình. Những ký tự này được gọi là *metacharater* hay trong tiếng việt là *siêu ký tự*. Các ký tự này trong Bash Shell bao gồm:
\*		?		[		]		'		"		\		$		;		&		(		)		|  ^		<		> 
Ví dụ, dấu đô la `$` thường dùng để ám chỉ rằng các ký tự liền kề sau nó là một tên biến chứa giá trị. Khi sử dụng cùng `echo`, thì chương trình sẽ  lấy giá trị được lưu trong biến đó và in ra ngoài màn hình. Ví dụ:
```
tomtpc@training:~$ echo $SHELL
/bin/bash
tomtpc@training:~$ echo It cost $1.00
It cost .00
```
Như đã nói ở trên, vì `$` là một siêu ký tự, nên `echo` sẽ cố gắng lấy giá trị được lưu trữ trong `$SHELL` và `$1`, mà ta chưa gán hay lưu giá trị vào biến `$1` nên `echo` không in ra bất cứ giá trị nào khi đọc biến `$1`, điều đó lý giải kết quả ta thu được ở câu lệnh thứ 2. Vậy nếu ta muốn in ra câu lệnh thứ 2 đúng ngữ pháp tiếng Anh thì chúng ta cần sử dụng thêm một dấu gạch chéo trái `\` đằng trước `$`. Ví dụ:
```
tomtpc@training:~$ echo It cost \$1.00 
It cost $1.00
tomtpc@training:~$ echo Is Tom\'s cat alive or dead\? 
Is Tom's cat alive or dead? 
```
Sử dụng dấu gạch chéo trái `\` có thể giúp chúng ta hiển thị đúng như ngữ pháp, nhưng ở câu lệnh thứ 2 của ví dụ trên, ta thấy rằng nếu như trong 1 câu lệnh mà xuất hiện nhiều siêu ký tự và ta muốn hiển thị chúng thì sẽ cần rất nhiều dấu `\`. Vì vậy hãy chú ý 2 ví dụ bên dưới để thấy được cách giải quyết.
```
tomtpc@training:~$ echo "Is Tom's cat alive or dead?" 
Is Tom's cat alive or dead?
tomtpc@training:~$ echo 'Is Tom's cat alive or dead?'
 > ^C
```
Chú ý ở câu lệnh thứ 2, ta sẽ không thể in ra được, lý do vì khi sử dụng siêu ký tự `'` để in một câu hay một chuỗi, ta sẽ cần thêm một siêu ký tự nữa để phụ giúp hiển thị, ví dụ như cặp dấu `""` hay `\`.
### Thay đổi cấu trúc thư mục:
Các files trong hệ thống Linux được lưu trong một danh mục duy nhất được gọi là ***Danh mục ảo***  - *Virtual Directory*. Danh mục ảo này bao gồm tất cả các file từ thiết bị lưu trữ của máy tình và hợp nhất chúng thành một cấu trúc danh mục duy nhất. Cấu trúc này có một danh mục gốc gọi là ***danh mục root***, thường được gọi tắt là `root`.
Khi ta đăng nhập vào 1 hệ thống Linux, danh mục hiện tại mà các tiến trình của ta sẽ là danh mục `home`. Danh mục hiện tại đang sử dụng là danh mục mà tiến trình đang chạy trong cấu trúc danh mục ảo. Ví dụ dễ hiểu nhất là, phòng mà Tom đang làm việc trong ngôi nhà của cậu ta.
Để di chuyển trong cấu trúc danh mục ảo này, chúng ta sẻ sử dụng câu lệnh `cd`. Và đi kèm với câu lệnh `cd` chính là câu lệnh `pwd`, cho biết vị trí hiện tại của ta trong cấu trúc danh mục ảo. Hãy xem ví dụ bên dưới để hiểu hơn nhé.
```
tomtpc@training:~$ pwd
/home/tomtpc
tomtpc@training:~$ cd /etc
tomtpc@training:/etc~$ pwd 
/etc	
```
Khi sử dụng lệnh `cd`, ta có thể sử dụng đường dẫn tuyệt đối hoặc tương đối. ***Đường dẫn tuyệt đối*** thì sẽ  luôn luôn bắt đầu với dấu `/` để tham chiếu đến thư mục gốc, sau đó là đường dẫn đến vị trí thư mục.***Đường dẫn tương đối*** sẽ cho phép ta di chuyển với lệnh `cd` trong phạm vi thư mục mà ta đang hoạt động (đang sử dụng). Hãy xem ví dụ bên dưới để xem 2 ví dụ về sử dụng.
```
tomtpc@training:~$ cd /etc/fonts
tomtpc@training:/etc/fonts~$ pwd
etc/fonts
```

```
tomtpc@training:~$ cd /etc
tomtpc@training:/etc~$
```
Lệnh `cd ` còn có thể giúp taquay về, từ danh mục đang hoạt động về danh mục của tài khoản đang sử dụng. Bằng cách ghi các cách như sau:

 - `cd`
 - `cd ~`
 - `cd $HOME`

```
tomtpc@training:/etc/fonts~$ cd
tomtpc@training:~$
```
Ngoài ra, ta còn có câu lệnh `cd -` để quay lại danh mục hoạt động trước đó.
```
tomtpc@training:/etc~$ cd /var
tomtpc@training:/var~$ cd -
tomtpc@training:/etc~$
```
### Lệnh trong và ngoài luồng:
Trong một chương trình Shell, có một số câu lệnh bản thân chúng là một phần của chương trình. Đây là những lệnh trong luồng hay có tên tiếng Anh là *build-in commands*.
Các câu lệnh còn lại thì tất nhiên là ngoài luồng. Ta có thể kiểm tra xem một lệnh là trong hay ngoài luồng bằng cách sử dụng lệnh `type`. Xem ví dụ bên dưới để hiểu.
```
tomtpc@training:~$ type echo
echo is a shell buildin
tomtpc@training:~$ type pwd
pwd is a shell buildin
tomtpc@training:~$ type uname
uname is /urs/bin/name
```
Nếu là lệnh trong luồng thì sẽ là `is a shell buildin` còn ngoài luồng sẽ là `is [ĐƯỜNG DẪN TUYỆT ĐỐI]`. Như ví dụ bên trên thì `uname` là lệnh ngoài luồng.
### Sử dụng biến môi trường:
*Biến môi trường* là nơi lưu dữ những thông nhất định về hệ thống, như là tên người dùng đang sử dụng Shell, đường dẫn đến danh mục của tài khoản người dùng, .... Bên dưới là bảng một số biến môi trường thường dùng.
|Tên biến|Mô tả  |
|--|--|
|BASH_VERSION |Phiên bản hiện tại của Bash Shell.|
|EDITOR|Chương trình biên tập mặc định.|
|GROUPS|Tư cách thành viên nhóm của tài khoản. |
|HISTFILE|Đường dẫn tuyệt đối của file chứa lịch sử các câu lệnh của tài khoản hiện tại.|
|HISTSIZE|Số lượng tối đa các câu lệnh được lưu lại.|
|HOME|Đường dẫn tuyệt đối của danh mục người dùng hiện tại.|
|HOSTNAME|Tên máy chủ hiện tại|
|LANG|Danh mục ngôn ngữ của Shell|
|LC_*|Các danh mục cài đặt tùy chỉnh LANG|
|LC_ALL|Danh mục ngôn ngữ cho Shell để tùy chỉnh LANG|
|LD_LIBRARY_PATH|Danh sách các thư viện được phân cách bởi `:` giúp tìm kiếm trước các thư viện tiêu chuẩn|
|PATH|Danh sách thư mục được phân cách bởi `:` để dẫn đến phần thực câu lệnh|
|PS1|Giao diện Shell chính|
|PS2|Giao diện Shell phụ|
|PWD|Thư mục người dùng hiện tại|
|SHLVL|Cấp bậc của Shell hiện tại|
|TZ|Vùng thời gian của người dùng hiện tại (Time Zone)|
|UID|ID của người dùng hiện tại|
|VISUAL|Trình chỉnh sửa văn bản mặc định|
### Hiển thị các biến môi trường đang hoạt động:
```
tomtpc@training~$: set
[…] BASH=/bin/bash 
[…] 
HISTFILE=/home/tomtpc/.bash_history 
[…] 
HISTSIZE=1000 
HOME=/home/tomtpc
HOSTNAME=localhost.localdomain 
[…] PS1='$ ' 
PS2='> ' 
[…] 
SHELL=/bin/bash 
[…]
```
Ngoài lệnh `set` thì ta có thể sử dụng lệnh `env` và `printenv` để hiển thì các biến. Lệnh `env` và `printenv` cho phép ta thấy được các biến được định nghĩa cục bộ, ví dụ như các biến được khởi tạo trong một Shell script, cũng như là các biến môi trường.
### Hiểu tác dụng của biến `$PATH`
```
tomtpc@training:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr:/games:/usr/local/games:/snap/bin
tomtpc@training:~$ ls /home/tomtpc/Hello.sh
ls: cannt access '/home/tomtpc/Hello.sh': No such file or directory
tomtpc@training:~$ Hello.sh
Hello.sh: command not found
```
Để ý rằng, file Shell Script `Hello.sh` ở trong một thư mục, thư mục đó lại không có tồn tại trong thư mục biến môi trường. Do vậy, nên khi ta gọi đến file này, sẽ được trả lỗi như trên (và tất nhiên là file đó phải tồn tại rồi nha).
Để chạy một chương trình hay một file không có đường dẫn được ấn định trong biến `PATH`, thì ta cần cung cấp cho cửa sổ lệnh đường dẫn tuyệt đối đến chương trình hoặc file đó. Như ví dụ bên dưới.
```
tomtpc@training:~$ chmod +x /home/tomtpc/Hello.sh
tomtpc@training:~$ /home/tomtpc/Hello.sh
Hello World !
```
### Sử dụng câu lệnh `which`:
```
tomtpc@training:~$ which Hello.sh

tomtpc@training:~$ which echo
usr/bin/echo
```
Ta có thể thấy rằng, `which` không tìm thấy `Hello.sh` và trả về kết quả rỗng, nhưng khi tìm `echo` thì lại trả về vị trí của chương trình `echo`.
Từ đó ta có thể rút ra một điều là, nếu như một chương trình được ấn định đường dẫn vào trong biến `PATH` môi trường thì ta có thể gọi trực tiếp đến nó mà không cần truyền cho cửa sổ Shell đường dẫn tuyệt đối của chương trình.
### Sử dụng các kiểu tham chiếu khác nhau để hiển thị:
```
tomtpc@training:~$ echo Hello World !
Hello World !
tomtpc@training:~$ /usr/bin/echo Hello World !
Hello World !
```
### Thay đổi giá trị biến `PS1`:
Để hiểu vì sao khi thay đổi biến giá trị `PS1` thì ta cần biết các cửa sổ lệnh trong Bash.
|Tên biến|Ý nghĩa|
|--|--|
| PS1| Đây là cửa sổ lệnh chính. Nơi nhập các ký tự đặc biệt và các thông tin quan trọng. |
| PS2| Đây là cửa sổ phụ. Nó thường được sử dụng để ngăn cách với các cửa sổ hiển thị và phần nhập dữ liệu. Đồng thời đôi khi được sử dụng để hiển thị một lệnh dài được chia thành nhiều phần với dấu `\`.|
| PS3| Đây là cửa sổ chuyên cho câu lệnh `select`. |
| PS4| Đây là cửa sổ sử dụng để chạy Shell Script trong chế độ Debug. |

Thông thường, chúng ta sẽ chỉ sử dụng `PS1` và có thể  là `PS2`.
```
tomtpc@training:~$ PS1="My new prompt"
My new prompt:
```
Từ ví dụ trên, ta thấy để sửa đổi giá trị một biến, ta chỉ cần nhập tên biến và tiếp sau đó là một dấu `=`, sau đó là giá trị mới cần truyền. Như đã nói ở trên, `PS1` là biến hiển thị cửa sổ lệnh chính nên khi ta thay đổi giá trị của nó, thì ngay lập tức giao diện đã được thay đổi.
Tuy nhiên, ta sẽ gặp phải một số vấn đề nếu như sử dụng phương pháp thay thế giá trị biến này. Ví dụ, các cấu hình thay đổi của biến sẽ không được lưu giữ khi ta đi vào một *subshell*. Một *subshell* (hay còn gọi là một Shell con) được tạo ra khi ta thực hiện một số công việc nhất định, ví dụ như là chạy một Shell Script hoặc một số câu lệnh đặc thù.
Ta có thể biết được ta hiện tại đang ở trong một *subshell* hay không bằng cách nhìn vào giá trị của biến `$SHLVL`. Nếu giá trị là `1` thì ta không ở trong `subshell` nào cả, vì giá trị `subshell` thường có giá trị lớn hơn. Chính vì thế nếu như ta nhận được giá trị lớn hơn `1` thì tức là đang trong một `subshell`. Xem ví dụ bên dưới để hiểu thêm nhé.
```
My new prompt: 	echo $SHLVL
1
My new prompt: bash
tomtpc@training:~$
tomtpc@training:~$  echo $SHLVL
2
tomtpc@training:~$ exit
My new prompt:
```
Từ ví dụ bên trên, ta có thể thấy là giá trị mặc định của `$SHLVL` là `1` nếu như ta không ở trong một *subshell*, và hơn thế nữa, ta đã chứng minh là giá trị của `PS1` không hề tồn tại trong *subshell* `bash` mà ta truy cập.
Để có thể giữ được giá trị của một biến môi trường, ta cần sử dụng lệnh `export`.
Nếu như một biến không chứa bất kỳ giá trị nào (biến rỗng), điển hình thì ta có biến `$EDITOR`, ta có thể xóa bỏ toàn bộ những thay đổi đã làm với biến bằng câu lệnh `unset`. Xem ví dụ bên dưới để hiểu hơn.
```
tomtpc@training:~$ echo $EDITOR

tomtpc@training:~$ export EDITOR=nano
tomtpc@training:~$ echo $EDITOR
nano
tomtpc@training:~$ unset EDITOR

tomtpc@training:~$echo $EDITOR

```
***Lưu ý:*** Ta phải rất cẩn thận khi sử dụng lệnh `unset` vào các biến môi trường, hãy dùng lệnh này nếu như thật sự hiểu biết về biến môi trường mà ta đang thao tác. Ví dụ nếu như ta thay đổi nhầm biến `$PS1` mà ta dùng lệnh `unset` là không nên vì nó có thể gây ra một số lỗi, tốt nhất là nên thay đổi nó về mặc định bằng cách thông thường bên trên (để có thể làm như vậy, hãy kiểm tra giá trị biến trước khi thao tác và lưu nó).
## Một số công cụ giúp đỡ:
Khi sử dụng nhiều câu lệnh và chương trình trong Shell thì đôi khi ta có thể cần một số sự trợ giúp về cấu trúc câu lệnh cũng như các tùy chọn mà chương trình, câu lệnh đó có thể thực hiện. Nếu như có mạng Internet để kết nối đến nguồn tài liệu để tham khảo thì còn gì tuyệt vời hơn. Nhưng nếu là người sử dụng Linux thì chả phải đi đâu xa, `man` ở đây để giúp bạn những lúc như này. Được ví như là cuốn từ điển, `man` sẽ cho bạn biết được ý nghĩa, mục đích của câu lệnh, của chương trình được cài trên máy, thậm chí cả cấu trúc và các tùy chọn. Chúng sẽ được giải thích một cách dễ hiểu nhất.
Để có thể mở được cuốn từ điển này, bạn đơn giản chỉ cần sử dụng câu lệnh `man uname` trong Shell. Một màn hình toàn chữ, như một cuốn từ điển, sẽ được hiển thị và ta có thể sử dụng các phím mũi tên lên xuống để đọc.
Mặc định. `man` sử dụng cơ cấu hiển thị của `less` - sẽ được nói đến sau. Chính cơ cấu này giúp ta có thể sử dụng mũi tên lên xuống hoặc hai nút PageUP / PageDown để di chuyển và đọc nội dung.
### Sử dụng `man -k` để tìm theo từ khóa:
Ví dụ:
```
tomtpc@training:~$ man -k passwd
[...]
passwd (1)	- change users password
passwd (1ss1)	- compute password hashes
passwd (5)	- the password file
update-passwd (8)	- safely update /etc/passwd, etc/shadow and /etc/group
[...]
```
*Ta vẫn có thể sử dụng lênh `apropos passwd` thay cho `man -k` nhưng mà việc đánh `man -k` sẽ dễ nhớ hơn.*
Để ý thấy, trong ví dụ trên, ta thấy rằng sẽ có nhiều kết quả được trả lại và đằng sau mỗi một từ khóa sẽ được đánh một số giá trị trong dấu ngoặc đơn. Cuốn từ điển `man` sẽ bao gồm chín phần, các phần này bao gồn nhiều loại tài liệu. Hãy thử `man man` để xem thêm các thông tin hữu ích khi sử dụng `man` cũng như cách truy cập các phần khác.
Mặc dù là một công cụ rất hữu ích, nhưng đôi khi nó sẽ gây cho ta một số nhầm lẫn nếu không để ý, ví dụ khi các câu lệnh có cùng một tên, trong ví dụ này là `passwd`. Thông thường thì  `man` sẽ tìm kiếm theo kiểu mặc định, nếu như có tên trùng, `man` sẽ chỉ hiển thị số trang đằng sau tên câu lệnh chứ không hiển thị tài liệu về câu lệnh đó. Để truy cập vào các trang đó thì có một vài cách dưới đây.
```
tomtpc@training:~$ man -S 5 passwd
tomtpc@training:~$ man -s 5 passwd
tomtpc@training:~$ man 5 passwd
``` 
***Lưu ý:*** nếu như sử dụng `man` mà nhận được thông báo tương tự như là `nothing appropriate`, hãy kiểm tra lại xem đã đánh đúng từ cần tìm chưa. Trong trường hợp đúng rồi, có thể có khả năng là cơ sở dữ liệu của `man` chưa được cập nhật. Ta sẽ cần quyền Siêu người dùng và sử dụng lệnh `makewhatis`(nếu trên các hệ thông Linux cũ) hoặc lệnh `mandb` để kiểm tra.
### Xem lịch sử lệnh:
```
tomtpc@training:~$ history
1 echo $SHLVL
2 exit
[...]
20 man -k passwd
21 man man
[...]
```
Để ý rằng, trước mỗi lệnh đã được thực hiện đều được đánh số. Ta có thể sử dụng số đó để gọi lại lệnh đó lịch sử lệnh. Ví dụ xem bên dưới.
```
tomtpc@training:~$ !1
echo $SHLVL
1
```
Nhớ là để dấu `!` trước số thứ tự của câu lệnh trong lịch sử lệnh để có thể thực hiện lại câu lệnh đó.
Để thực hiện nhanh câu lệnh gần nhất hãy sử dụng `!!`. Cách nhanh hơn là sử dụng phím `Mũi tên lên`+`Enter`.  Sử dụng tổ hợp phím này cho phép ta thay đổi nội dung câu lệnh trước khi thực thi.
Danh sách lệnh đã được thực thi sẽ được lưu giữa các phiên đăng nhập và được chỉ định bởi biến môi trường `$HISFILE`. Nó thường là file `.bash_history` trong đường dẫn người dùng hiện tại.
### Xem file lịch sử lệnh:
```
tomtpc@training:~$ echo $HISFILE
/home/tomtpc/.bash_history
```
***Lưu ý:*** File lịch sử sẽ không có những lệnh đã/đang sử dụng trong phiên đăng nhập hiện tại. Những lệnh này chỉ được lưu trong danh sách lịch sử lệnh.
Nếu như ta muốn cập nhập file lịch sử lệnh hoặc danh sách lịch sử lệnh hiện tại, thì ta cần thực thi lênh `history` với một vài tùy chọn như sau:

 - `-a`: thêm danh sách lịch sử lệnh hiện tại vào cuối file lịch sử lệnh.
 - `-n`: thêm các lệnh trong file lịch sử lệnh của phiên hiện tại vào trong danh sách lịch sử lệnh.
 - `-r`: ghi đè danh sách lịch sử lệnh hiện tại với các lệnh được lưu trong file lịch sử lệnh.
 ### Phần mềm chỉnh sửa tệp văn bản:
 Ở trong Linux, ta có một số phần mềm chỉnh sửa văn bản phổ biến như:
 
 - emacs
 - nano
 - vim
 Sử dung chương trình chỉnh sửa văn bản *nano* trong Linux sẽ là bước khởi đầu khá hay nếu như ta chưa từng sử dụng một chương trình chỉnh nào bằng câu lệnh trước đó. Để sử dụng thì đơn giản chỉ cần gõ lệnh `nano` và cách sau đó là tên của file mà ta muốn tạo hoặc chỉnh sửa.
 Bên dưới là giao diện (GUI) của `nano`.
 ![Giao diện của phần mềm chỉnh sửa văn nano](https://uphinh.vn/images/2022/03/08/f2245e3967017b76e36f0b7ef04066dc.png)
 Một số phím tắt của `nano` sẽ được hiển thị bên dưới màn hình.  Để bấm được các phím tắt này thì ta phải chú ý bấm thêm nút `Ctrl` và sau đó là ký tự tương ứng với chức năng muốn thực hiện. Ví dụ như, ta muốn thoát, `^X `- Exit, thì ta bấm tổ hợp phím`Ctrl  X`. 
 ***Lưu ý:*** một số tiện ích như `crontab` thì sẽ sử dụng trình chỉnh sửa văn bản mặc định như `vim`. Nếu như ta mới sử dụng Linux thì sẽ thích sử dụng một trình chỉnh sửa văn bản nào dễ  tiếp cận hơn là trình nâng cao như `vim`. 
 Chính vì thế nên ta cần thay đổi giá trị của biến môi trường quy định trình chỉnh sửa văn bản mặc định đó là `EDITOR` và `VISUAL` trong đó. Biến `EDITOR` quy định trình biên tập dựa trên dòng, ví dụ như trình `ed` cũ trong Linux. Biến `VISUAL` sẽ quy định trình biên tập toàn bộ màn hình (hiển thị toàn bộ màn hình) như `nano`, `vim`, `emacs`.
 Như đã nói ở trên, để lưu lại giá trị của biến môi trường tại phiên đăng nhập hiện tại hoặc là tại *subshell* thì ta cần sử dụng lệnh `export`, trong trường hợp này ta cần lưu hai biến là `EDITOR` và `VISUAL` thì sẽ là `export EDITOR=nano` và `export VISUAL=nano`. Và nếu như ta cần giữ lại các giá trị này thì ta sẽ cần phải thao tác chỉnh sửa giá trị trong file lưu các biến môi trường (sẽ nhắc đến sau).
 ## Xử lý văn bản bằng bộ lọc
 Trong hệ thống Linux, ta thường xuyên cần xem các files, hoặc các thành phần nhỏ trong chúng. Chính vì vậy ta cần một vài các công cụ giúp đỡ để thu thập thông tin, hiển thị và xử lý.
 ### Các lệnh kết hợp tệp:
 Ghép nối các file nhỏ lại để hiển thị trên màn hình và so sánh chúng là điều mà đôi khi ta sẽ cần đến. Dưới đây là một câu lệnh để giúp ta có thể làm điều đó, thông thường thì mọi người hay sử dụng `cat` để xem các file nhỏ nhưng bản chất của nó có thể giúp ta xem nhiều file và so sánh chúng.
 `cat [Tùy Chọn]... [File]...`
 Ví dụ:
 ```
 tomtpc@training:~$ cat newfile.txt
 hello there
 my name is Tom
 Whats your?
 ```
 Ví dụ so sánh 2 file(s):
 ```
 tomtpc@training:~$ cat newfile.txt Hello.sh
 hello there
 my name is Tom
 Whats your?
 echo 'Hello World !'
 ```
 Mặc dù có thể hiển thị nhiều file để so sánh nhưng mà `cat` lại không có hight-light từ/ký tự giống nhau giúp ta. Dưới đây là một số `[Tùy chọn]` mà ta có thể sử dụng cùng với `cat`.
 
| Viết tắt|Đầy đủ|Ý nghĩa|
|---|---|---|
| -A | --show-all|Bằng với việc sử dụng `-vET` .|
|-E|--show-ends|Hiển thị thêm ký tự `$` khi gặp ký tự xuống dòng.|
|-n|--number|Đánh số thứ tự các dòng.|
|-s|--squeeze-blank|Không hiển thị các dòng trống.|
|-T|--show-tabs|Hiển thị `^I` khi gặp dấu `tab`.|
|-v|--show-nonprinting|Hiển thị các ký tự không in khi gặp bằng `^` và `/`|

Vì có thể hiển thị các ký tự không in được, nên nếu như ta đang có một file mà không thể nào sắp xếp được thì có thể sử dụng `cat -v [File]` để xem có ký tự không in nào không.
### So sánh file ngang hàng:
Nếu như `cat` hiển thị hàng dọc lần lượt các files được truyền vào thì `paste` sẽ để chúng ngang hàng cho ta xem để đối chiếu dễ dàng hơn.
```
tomtpc@training:~$ paste test1.txt test2.txt
tom		tpc
kma		tom
act		act
tpc		kma
tomtpc@training:~$ 
```
### Chuyển đổi file:
Đôi khi trong quá trình làm việc, ta sẽ cần nhìn nhận dữ liệu dưới một góc nhìn khác để có thể kiểm soát lỗi chẳng hạn.
Đó là khi lệnh `od` sẽ giúp ích ta. `od` có thể cho phép ta hiển thị dữ liệu của file dưới dạng cơ số 8, cơ số 16, cơ số 10 và cả dạng ASCII tiêu chuẩn.
`od [Tùy Chọn]... [File]...`
Mặc định của `od` sẽ hiển thị dữ liệu của file dưới dạng cơ số 10.
Ví dụ:
```
tomtpc@training:~$ cat test1.txt
tom
kma
act
tpc
tomtpc@training:~$ od test1.txt
0000000 067564 005155 066553 055141 061541 005164 070164 005143 
0000020
```
Cột đầu tiên sẽ là chỉ số của mỗi hàng được hiển thị lên. Nếu như  cảm thấy hơi khó đọc thì ta có thể thêm tùy chọn `-cb` để hiển thị ký tự đương ứng với giá trị cơ số 10.
```
tomtpc@training:~$ od -cb test1.txt
0000000		t	o	m	\n	k	m	a	\n	a	c	t	\n	t	p	c	\n
		164	157	155	012	153	155	141	012	141	143	164	012	164	160	143	012
0000020
```
### Chia nhỏ file:
Một công cụ hữu hiệu khác đó là `split`. Câu lệnh này sẽ giúp ta chia nhỏ file lớn thành các khối nhỏ hơn, dễ dàng để thao tác hơn.
`split [Tùy chọn]... [Đầu vào [Tiền tố đầu ra]]`
Ta có thể sử dụng `split` để chia theo kích thước file, bytes, theo dòng ,v.v. Tất nhiên là dữ liệu đầu vào sẽ không bị thay đổi sau khi sử dụng câu lệnh.
```
tomtpc@training:~$ cat test1.txt
tom
kma
act
tpc
tomtpc@training:~$ split -l 3 test1.txt split42
tomtpc@training:~$ ls split42*
split42aa	split42ab
tomtpc@training:~$ cat split42aa
tom
kma
act
tomtpc@training:~$ cat split42ab
tpc
```
Bên trên là ví dụ sử dụng `split -l` (chữ `L` thấp), để có thể chia file theo dòng. Bên trên ta chia mỗi file là 3 dòng, và tất nhiên file cuối sẽ có ít hơn 3 dòng nếu như số dòng không chia hết cho 3. Thêm vào đó tiền tố `split42` được viết trong câu lệnh là tiền tố tên của các file sẽ chứa dữ liệu sau khi chia nhỏ ra, tên hoàn chỉnh sẽ được tự động thêm vào sau tiền tố ta đã định.
### Sắp xếp dữ liệu:
Trong quá trình làm việc với dữ liệu, thật tuyệt với nếu như ta có một công cụ có thể giúp ta sắp xếp các dữ liệu trong file theo thứ tự tăng dần chẳng hạn. Trong Linux ta có `sort` sẽ giúp ta làm công việc này.
```
tomtpc@training:~$ cat Alphabet.txt
Thanh
An
Hoang
Quynh
Ngoc
Minh
tomtpc@training:~$ sort Alphabet.txt
An
Hoang
Minh
Ngoc
Quynh
Thanh
```
Nếu như trong file có ký tự số thì có thể dữ liệu sẽ không được sắp xếp theo ý muốn của ta. Để có thể sắp xếp dữ liệu số thì ta có thể thêm tùy chọn `-n`.
```
tomtpc@training:~$ cat numbers.txt
4
6
23
65
23
97
42
21
1
tomtpc@training:~$sort numbers.txt
1
21
23
23
4
43
6
65
97
tomtpc@training:~$ sort -n numbers.txt
1
4
6
21
23
23
43
65
97
```
Trong lần sắp xếp đầu tiên khi không có tùy chọn `-n` thì ta có thể thấy là thứ tự sắp xếp không được chính xác. Khi có thêm tùy chọn `-n` dành cho dữ liệu số thì mọi thứ đã đúng trật tự như ta mong muốn.
### Đánh số văn bản:
Một công cụ hữu ích khác khi ta thao tác với dữ liệu dưới dạng văn bản, đó là `nl` giúp ta đánh số các dòng.
Cấu trúc lệnh: `nl [Tùy Chọn]... [File]`
Nếu như ta không sử dụng bất kỳ `[Tùy Chọn]` của `nl` thì nó sẽ chỉ đếm những dòng không trống.
```
tomtpc@training:~$ nl ContainsBlankLines.txt 
1 Alpha 
2 Tango 

3 Bravo 
4 Echo 


5 Foxtrot
```
Nếu như muốn đếm thêm các dòng trống thì ta thêm tùy chọn `-ba`.
```
tomtpc@training:~$ nl -ba ContainsBlankLines.txt
1 Alpha 
2 Tango 
3 
4 Bravo 
5 Echo 
6 
7 
8 Foxtrot
```
## Một số lệnh xem file
Một trong những công việc thường được làm trong Linux đó là xem dữ liệu của 1 file. Nếu như file đó ngắn, dung lượng ít thì ta có thể sử dụng `cat` như đề cập bên trên để xem. Nhưng nếu như file đó có đến cả trăm dòng, nghìn dòng thì sao? Sau đây là một số câu lệnh vô cùng hữu ích để xem những file như vậy.
### Lệnh `more` và `less`:
Cách đơn giản khi ta muốn xem dữ liệu của một file lớn đến trăm, nghìn dòng là sử dụng `pager`. Như cái tên của nó, nó sẽ hiển thị  dữ liệu lên màn hình như trên một trang giấy. `pager` thường được sử dụng trong 2 câu lệnh `less` và ` more`.
`more [Tùy Chọn]... [File]...`
Nếu như ta sử dụng  `more` thì bên trên là cấu trúc câu lệnh của nó. `more` sẽ hiển thị dữ liệu trên màn hình, ta có thể di chuyển màn hình xuống để xem nội dung tiếp theo bằng cách bấm `Phím cách`(đi xuống 1 trang) hoặc nút `Enter`(đi xuống 1 dòng). Tuy vậy, `more` lại không cho ta đi lên để xem các nội dung đã qua. Để thoát khỏi chế độ xem dữ liệu của `more` thì ta bấm nút `Q`.
Khác với cái tên `less` lại vừa có thể thực thi chức năng của `more` mà lại cho ta xem các dữ liệu đã qua. Cấu trúc của `less` cũng giống như `more`.
`less [Tùy Chọn]... [File]...`
Còn hơn cả `more`, `less` đọc dữ liệu của file rất nhanh và ít tốn tài nguyên hệ thống. Bởi vì `less` không đọc liền một lúc tất cả dữ liệu của file rồi hiển thị chúng lên như `more`, nó sẽ đọc dữ liệu dần dần theo quá trình đọc của người dùng.
Sử dụng `less` để xem dữ liệu thì ta có thể sử dụng phím `mũi tên lên` và `mũi tên xuống` để di chuyển xuống/lên 1 dòng cũng như là phím `cách` (đi xuống 1 trang) hay tổ hợp `ESC V` để lùi 1 trang. Thậm chí khi bấm `? [Từ cần tìm] + Enter` hoặc `/ [Từ cần tìm] + Enter`thì ta có thể tìm từ mong muốn trong file đang xem, khác nhau ở chỗ là `?` sẽ tìm xuôi từ chỗ ta đang đọc xuống còn `/` thì ngược lại. Và cuối cùng, để thoát khỏi chế độ đọc thì ta bấm `Q`.
Còn rất nhiều các `[Tùy Chọn]` tuyệt vời mà `less` mang đến, ta nên lượn 1 vòng trong thư viện `man` để xem.
Xem thêm về `less`: `man less`
### Lệnh `head`:
Không muốn xem cả một file lớn và dài chỉ để lấy dữ liệu của vài dòng đầu file? `head` sẽ giúp ta khoản này.
`head [Tùy Chọn]... [File]...`
Mặc định nếu không có `[Tùy Chọn]` thì `head` sẽ hiển thị **10** dòng đầu tiên của file.
```
tomtpc@training:~$ head /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
```
Để hiển thị nhiều hơn hay ít hơn thì ta sử dụng tùy chọn `-n` hoặc `--lines=` sau đó là số dòng muốn hiển thị.
```
tomtpc@training:~$ head -n 2 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
```
Hoặc
```
tomtpc@training:~$ head -2 /etc/passwd
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
```
### Lệnh `tail`:
Nếu như ta muốn theo dõi các dữ liệu mới nhất được thêm vào file thì sao? Mở  `less` hoặc `more` hay `cat` rồi kéo xuống cuối ư? Không, `tail` sẽ cho ta xem những dòng cuối cùng của file.
`tail [Tùy Chọn]... [File]...`
Tương tự như `head` mặc định của `tail` là xem **10** dòng cuối cùng của file. Ta cũng có thể xem số lượng khác bằng tùy chọn `-n` hoặc `--lines=`.
```
tomtpc@training:~$ tail /etc/passwd
saslauth:x:992:76:Saslauthd
user:/run/saslauthd:/sbin/nologin
pulse:x:171:171:PulseAudio SystemDaemon:/var/run/pulse:/sbin/nologin
gdm:x:42:42::/var/lib/gdm:/sbin/nologin
setroubleshoot:x:991:985::/var/lib/setroubleshoot:/sbin/nologin 
rpcuser:x:29:29:RPC Ser viceUser:/var/lib/nfs:/sbin/nologin 
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
sssd:x:990:984:User for sssd:/:/sbin/nologin gnome-initialsetup:x:989:983::/run/gnome-initial-setup/:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
avahi:x:70:70:Avahi mDNS/DNS-SD Stack:/var/run/avahi-daemon:/sbin/nologin
```
```
tomtpc@training:~$ tail -n 2 /etc/passwd
tcpdump:x:72:72::/:/sbin/nologin
avahi:x:70:70:Avahi mDNS/DNS-SD Stack:/var/run/avahi-daemon:/sbin/nologin
```
