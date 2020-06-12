# Thuật toán chia để trị

## Tổng quan

<p align = "center"><img src = "https://miro.medium.com/max/855/1*SfBEvWNJpmLRf-Lj_M5f-g.png"></p>

Trong khoa học máy tính, chia để trị là một mô hình thiết kế thuật toán quan trọng dựa trên đệ quy với nhiều phân nhánh. Thuật toán chia để trị hoạt động bằng cách chia bài toán thành nhiều bài toán nhỏ hơn thuộc cùng thể loại, cứ như vậy lặp lại nhiều lần, cho đến khi bài toán thu được đủ đơn giản để có thể giải quyết trực tiếp. Sau đó lời giải của các bài toán nhỏ được tổng hợp lại thành lời giải cho bài toán ban đầu.

Tuy nhiên, khả năng hiểu và thiết kế thuật toán chia để trị là một kĩ năng đòi hỏi nhiều thời gian để làm chủ. Tương tự như chứng minh quy nạp, trong một số trường hợp, ta phải thay thế bài toán ban đầu bằng một bài toán tổng quát hơn để có thể tạo ra mối liên hệ đệ quy. Không có một phương pháp có hệ thống nào để tìm ra bài toán tổng quát thích hợp trong mọi trường hợp.Chứng minh tính đúng đắn của thuật toán chia để trị thường sử dụng quy nạp. Thời gian chạy của chúng thường được tính thông qua hệ thức truy hồi.

Chứng minh tính đúng đắn của thuật toán chia để trị thường sử dụng quy nạp. Thời gian chạy của chúng thường được tính thông qua hệ thức truy hồi.

## Kĩ thuật

* Bước 1 (divide): Chia bài toán lớn thành các bài toán con nhỏ hơn
* Bước 2 (conquer): Gọi đệ quy giải các bài toán con, sau đó dựa trên lời giải của bài toán con để giải bài toán lớn.

Cả hai bước đều yêu cầu những kĩ thuật nhất định và phương pháp tốt nhất để có thể áp dụng hai bước vào các bài toán khác nhau là thực hành nhiều. 

## Ví dụ

### Tìm kiếm nhị phân

Tìm kiếm nhị phân là một thuật toán dùng để tìm kiếm 1 phần tử trong một danh sách đã được sắp xếp. Thuật toán hoạt động như sau:
* Bước 1 (Chia): Danh sách ban đầu sẽ được chia thành 2 nửa
* Bước 2 (Trị): Trong mỗi bước, so sánh phần tử cần tìm với phần tử nằm ở chính giữa danh sách. Nếu hai phần tử bằng nhau thì phép tìm kiếm thành công và thuật toán kết thúc. Nếu chúng không bằng nhau thì tùy vào phần tử nào lớn hơn, thuật toán lặp lại bước so sánh trên với nửa đầu hoặc nửa sau của danh sách. Vì số lượng phần tử trong danh sách cần xem xét giảm đi một nửa sau mỗi bước, nên thời gian thực thi của thuật toán là hàm lôgarit.
* Bước 3: Bằng việc lặp lại cách giải quyết như bước 2 ta sẽ tìm được kết quả.

<p align = "center"><img src = "https://nguyenvanhieu.vn/wp-content/uploads/2018/07/thuat-toan-tim-kiem-nhi-phan-minh-hoa-code-su-dung-c-java.gif"></p>

Code: [ở đây](https://ideone.com/YTTgaB)

### Tính (a ^ b) % c

Thuật toán hoạt động như sau:
* Bước 1 (Chia): b được chia 2 và xét hai trường hợp: b chia hết cho 2 và b không chia hết cho 2.
* Bước 2 (Trị): Tính (a^b) % c tại mỗi trường hợp
* Bước 3: Sử dụng đệ quy để từ các b/2 "nhỏ" ta gộp thành giá trị b "lớn" ban đầu.

Code: [ở đây](https://ideone.com/a3kKNQ)

### Quicksort

Thuật toán quicksort dùng để sắp xếp dãy số, hãy cùng tìm hiểu thuật toán này áp dụng chia để trị như thế nào.
* Bước 1(chia): Thuật toán quicksort chia danh sách cần sắp xếp mảng array[1..n] thành hai danh sách con có kích thước tương đối bằng nhau nhờ chỉ số của phần tử gọi là chốt, ta có thể chọn chốt là phần tử ở giữa, ở cuối, ở đầu hoặc phần tử ngẫu nhiên nào trong mảng.
* Bước 2 (trị): Sau khi đã chia thành 2 mảng dựa vào phần tử chốt nhiệm vụ của bước này là phải sắp xếp sao cho: những phần tử nhỏ hơn hoặc bằng phần tử chốt được đưa về phía trước và nằm trong danh sách con thứ nhất, các phần tử lớn hơn chốt được đưa về phía sau và thuộc danh sách đứng sau. Cứ tiếp tục chia như vậy tới khi các danh sách con đều có độ dài bằng 1
* Bước 3: Bằng việc lặp các bước giải quyết các bài toán con trên ta sẽ thu được kết quả là mảng sẽ được sắp xếp.

<p align = "center"><img src = "https://miro.medium.com/max/5142/1*Wb7sjviC18Hj5yRS6CdqKw.jpeg" width = 60% height = 60%></p>

Code: [ở đây](https://ideone.com/SLuEOq)

## Let's practice
Thử sức với các bài sau:

https://codeforces.com/problemset/problem/1167/B

https://codeforces.com/problemset/problem/768/B

https://codeforces.com/problemset/problem/234/G

https://codeforces.com/problemset/problem/559/B

https://leetcode.com/problems/k-closest-points-to-origin/

https://leetcode.com/problems/beautiful-array/

https://leetcode.com/problems/different-ways-to-add-parentheses/

https://leetcode.com/problems/search-a-2d-matrix-ii/

https://leetcode.com/problems/kth-largest-element-in-an-array/


## Tham khảo
1. [Viblo](https://viblo.asia/followings)
2. [Wikipedia](https://vi.wikipedia.org/wiki/Wikipedia)
3. [Giaithuatlaptrinh.com](https://www.giaithuatlaptrinh.com/?p=48)
4. [Codeforces.com](https://codeforces.com/problemset?tags=divide%20and%20conquer)
5. [Leetcode.com](https://leetcode.com/problemset/all/?topicSlugs=divide-and-conquer&difficulty=Medium)
