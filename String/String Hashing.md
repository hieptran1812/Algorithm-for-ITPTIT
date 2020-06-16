# String Hashing

## Tổng quan

Các thuật toán băm (hashing) rất hữu ích trong việc giải quyết rất nhiều vấn đề.
Với bài toán so sánh hai chuỗi, nếu ta sử dụng cách "duyệt trâu" (brute force) để so sánh từng đôi phần tử tương ứng trong hai chuỗi, ta sẽ 
có thuật toán với độ phức tạp O(min(a,b)) với a,b lần lượt là độ dài của chuỗi một và chuỗi hai. Đó là một cách làm ngây thơ và mất rất nhiều thời gian.
Ta phải tìm ra một cách giải quyết khác ổn áp hơn. Ý tưởng mời là: Thay vì so sánh hai chuỗi kí tự, ta chuyển mỗi chuỗi kí tự sang một số nguyên và so sánh hai số nguyên đó.
Cuối cùng việc so sánh hai số nguyên chỉ với độ phức tạp O(1). Đó là hướng đi của String Hashing.

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/hash2.PNG"></p>
 
## Kĩ thuật

Việc hashing được thực hiện qua 2 bước:

* Một phần tử sẽ được chuyển đổi thành 1 số nguyên bằng việc sử dụng hàm băm. Phần tử này được sử dụng như một chỉ mục để lưu trữ phần tử gốc và nó sẽ được đưa vào bảng băm.
* Phần tử sẽ được lưu giữ trong bảng băm, nó có thể được truy xuất nhanh bằng khóa băm:

  hash = hashfunc(key)
  
  index = hash % array_size
  
Theo cách trên thì việc băm sẽ phụ thuộc vào kích thước mảng array_size. Chỉ số index sau đó được đưa về [0; array_size-1] bằng việc sử dụng toán tử chia lấy dư %.

Để thực hiện bước chuyển đổi như đã nêu ở phần Tổng quan, ta cần một hàm được gọi là Hash function. Mục tiêu là **chuyển chuỗi sang số nguyên**.
Ta có điều kiện sau: Nếu hai xâu s và t bằng nhau (s = t) thì giá trị **hash** của chúng cũng bằng nhau (hash(s) = hash(t)). Ngược lại, ta không thể so sánh hai string (cùng giá trị hash thì chưa chắc hai xâu bằng nhau).

Hàm băm là bất kỳ hàm nào có thể được sử dụng để ánh xạ tập dữ liệu có kích thước tùy ý thành tập dữ liệu có kích thước cố định và đưa vào bảng băm. Các giá trị được trả về bởi hàm băm được gọi là giá trị băm.

Một hàm băm được đánh giá tốt nếu nó đạt được các yêu cầu cơ bản sau:

* **Dễ tính toán**: Nó phải dễ tính toán và bản thân nó không phải là một thuật toán
* **Phân bố đồng đều**: Nó cần phải phân phối đồng đều trên bảng băm, không xảy ra việc tập trung thành các cụm
* **Ít va chạm**: Va chạm xảy ra khi các cặp phần tử được ánh xạ tới cùng một giá trị băm
**Chú ý**: Bất kể hàm băm có tốt đên đâu, va chạm vẫn có thể xảy ra. Vì vậy, để duy trì hiệu suất của bảng băm, điều quan trọng là phải quản lý va chạm thông qua các kỹ thuật giải quyết va chạm.

Tính toán hàm băm của một string:

Cách tốt và được sử dụng rộng rãi để xác định hàm băm của chuỗi s có độ dài n là:

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/hash.PNG"></p>

trong đó p và m là số dương tùy chọn. 

Sẽ là hợp lý nếu ta chọn p là một số nguyên tố gần bằng số ký tự trong bảng chữ cái. Ví dụ: Nếu đầu vào chỉ bao gồm các chữ cái viết thường của bảng chữ cái tiếng Anh, p = 31 là một lựa chọn tốt. 
Nếu đầu vào có thể chứa cả chữ hoa và chữ thường, thì p = 53 là một lựa chọn không tồi. Code mình sẽ sử dụng với p = 31.

Rõ ràng, m nên là một số lớn bởi vì xác suất hai string va chạm (cùng giá trị hashing) xấp xỉ 1/m. Sự lựa chọn là m sẽ là một số nguyên tố lớn, chẳng hạn m = 10^9 + 9. 

## Ví dụ

### Chuyển đổi cơ bản

Dưới đây là một ví dụ về tính toán hàm băm của một chuỗi s, chỉ chứa các chữ cái viết thường. Ta chuyển đổi từng ký tự của s thành một số nguyên. Ở đây ta sử dụng chuyển đổi a → 1, b → 2, ..., z → 26. 
Chuyển đổi a → 0 không phải là một ý tưởng hay, bởi vì sau đó các giá trị băm của các string a, aa, aaa, tất cả đều có giá trị là 0.

**Code**: https://ideone.com/4kC2kY

Việc tính toán trước các lũy thừa cơ số p giúp cho hàm chạy nhanh hơn.

### Tìm kiếm các string trùng lặp trong một mảng gồm các string

**Đề bài**: Cho một danh sách gồm n string s[i], mỗi string không quá m kí tự, tìm các chuỗi trùng lặp và chia chúng thành các nhóm.

**Ý tưởng**: Từ thuật toán rõ ràng liên quan đến việc sắp xếp các chuỗi, ta sẽ có được độ phức tạp O(nmlogn) trong đó việc sắp xếp có độ phức tạp O(nlogn) và mỗi so sánh có độ phức tạp trung bình O(m). Tuy nhiên, bằng cách sử dụng Hashing, chúng ta giảm thời gian so sánh xuống O(1) do đó ta có một thuật toán chạy trong thời gian O(nm + nlogn).

Ta tính toán hàm băm cho mỗi chuỗi, sắp xếp các giá trị băm cùng với các chỉ mục và sau đó nhóm các chỉ số theo các giá trị băm giống nhau.

**Code**: https://ideone.com/T3Of14

## Ứng dụng

### Trong lập trình thi đấu (Competitve Programming)

Trong các bài toán thông thường, các bạn thường chỉ cần sử dụng cấu trúc dữ liệu được cài đặt sẵn ở các ngôn ngữ lập trình: map, set trong C/C++, Java; Dictionary trong C#, Python. Đó chính là các bảng băm cực kỳ hữu dụng mà chúng ta vẫn hay sử dụng.

Nếu các bạn để ý thì multimap và multiset trong C++ cho phép lưu trữ key trùng nhau với giá trị khác nhau đó. Đó là 2 thằng đã được thiết lập cơ chế xử lý va chạm.

* Rabin-Karp algorithm để khớp mẫu trong một chuỗi, độ phức tạp O(n)
* Tính số lượng string con khác nhau trong string, độ phức tạp O(n^2 * logn)
* Tính số lượng string palindromic (xâu thuận nghịch) con trong một string

Hàm băm được sử dụng trong các thuật toán khác nhau để tăng tốc độ tính toán.

### Trong ứng dụng thực tế

* Associative arrays: Bảng băm thường được sử dụng để cài đặt nhiều loại in-memory tables. Chúng được sử dụng để thực hiện các mảng kết hợp (các mảng có chỉ số là các chuỗi tùy ý hoặc các đối tượng phức tạp khác).
* Lập chỉ mục CSDL: Các bảng băm cũng có thể được sử dụng làm cấu trúc dữ liệu để lập chỉ mục dữ liệu trong các CSDL.
* Caches: Bảng băm dùng để thiết lập cơ chế caches, thường được dùng để tăng tốc độ truy cập dữ liệu.
* Biểu diễn các đối tượng: Một số ngôn ngữ động, chẳng hạn như Perl, Python, JavaScript và Ruby sử dụng bảng băm để triển khai các đối tượng.

## Let's practice

1. https://codeforces.com/problemset/problem/525/A
2. https://codeforces.com/problemset/problem/4/C
3. https://codeforces.com/problemset/problem/486/B
4. https://codeforces.com/problemset/problem/182/D
5. https://codeforces.com/problemset/problem/1326/D1
6. https://codeforces.com/problemset/problem/1133/D
7. https://codeforces.com/problemset/problem/574/B
8. https://codeforces.com/problemset/problem/39/J

## Tham khảo

1. [Nguyenvanhieu.vn](https://nguyenvanhieu.vn/bang-bam-hash-tables/)
2. [cp-algorithms.com](https://cp-algorithms.com/string/string-hashing.html)
3. [Codeforces.com](https://codeforces.com/problemset#)
