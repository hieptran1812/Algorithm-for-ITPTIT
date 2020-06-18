# Dynamic Programming

## Tổng quan

Các thuật toán đệ quy có ưu điểm dễ cài đặt, tuy nhiên do bản chất của quá trình đệ quy, các chương trình này thường kéo theo những đòi hỏi lớn về không gian bộ nhớ và một khối lượng tính toán khổng lồ.
Với Quy hoạch động (Dynamic Programming) là một kĩ thuật nhằm đơn giản hóa việc tính toán các công thức truy hồi bằng cách lưu trữ toàn bộ hay một phần kết quả tính toán tại mỗi bước với mục đích sử dụng lại. 
Quy hoạch động tương tự như đệ quy ở chỗ, việc tính toán các trường hợp cơ sở (trường hợp con) cho phép chúng ta xác định một cách tự nhiên giá trị cuối cùng. Cách tiếp cận từ dưới lên (Bottom - up) này hoạt động tốt khi giá trị mới chỉ phụ thuộc vào các giá trị được tính toán trước đó.

Một tính chất quan trọng để giải quyết một vấn đề bằng Quy hoạch động là bạn phải nhìn ra được Công thức truy hồi trong bài toán đó.

<p><img src = "https://media.geeksforgeeks.org/wp-content/cdn-uploads/Dynamic-Programming-1-1024x512.png"></p>

Hiểu và áp dụng được Quy hoạch động không phải là chuyện đơn giản, mặc dù ý tưởng cơ bản là chỉ có vậy, thách thức là các bài toán mà áp dụng được Quy hoạch động lại rất đa dạng. 
Tớ sẽ trình bày những vấn đề và bài toán cơ bản, cốt lõi, còn những vấn đề khác sẽ update dần dần nha :D

## Kĩ thuật

### Các khái niệm

* Bài toán giải theo phương pháp Quy hoạch động gọi là **Bài toán quy hoạch động**.
* Công thức phối hợp nghiệm của các bài toán con để có nghiệm của bài toán lớn gọi là **Công thức truy hồi** của quy hoạch động.
* Tập các bài toán nhỏ nhất có ngay lời giải để từ đó giải quyết các bài toán lớn hơn gọi là **cơ sở quy hoạch động**.
* Không gian lưu trữ lời giải các bài toán con để tìm cách phối hợp chúng gọi là **bảng phương án quy hoạch động**.

### Điều kiện áp dụng

Điều kiện áp dụng Quy hoạch động:
* Bài toán lớn **phân rã** được thành nhiều bài toán con.
* **Sự phối hợp** lời giải của các bài toán con trên cho ta lời giải của bài toán lớn.
* Quy hoạch động là đi **giải tất cả** các bài toán con, nên nếu không đủ không gian lưu trữ lời giải (bộ nhớ, đĩa,...) để phối hợp chúng thì phương pháp quy hoạch động cũng không thể thực hiện được.
* Quá trình từ bài toán cơ sở tìm ra lời giải bài toán ban đầu phải qua hữu hạn bước.

### Các bước áp dụng

1. Giải tất cả các bài toán cơ sở (thông thường rất dễ), lữu trữ lời giải vào bảng phương án.
2. Dùng công thức truy hồi phối hợp những lời giải của những bài toán nhỏ đã lưu trong bảng phương án để tìm ra lời giải của những bài toán lớn hơn và lưu chúng vào bảng phương án. Cho tới khi bài toán ban đầu tìm được lời giải.
3. Dựa vào bảng phương án, truy vết tìm ra nghiệm tối ưu.

## Ví dụ

### Coin problem

**Đề bài**: Cho bạn các đồng xu có giá trị c<sub>1</sub>, c<sub>2</sub>,... , c<sub>k</sub>. Nhiệm vụ của bạn là lấy ít xu nhất có thể sao cho tổng giá trị của chung bằng tổng T cho trước.

**Ý tưởng**: 
* Ta có thể dùng thuật toán tham lam bằng cách chọn những đồng xu có giá trị lớn nhất lần lượt. Tuy nhiên, trong đa số trường hợp, thuật toán tham lam lại không cho ta được một kết quả tối ưu.
* Ok! Ta thử áp dụng Quy hoạch động cho bài toán này xem sao :))

**Triển khai**:

Để ví dụ cụ thể hơn, tớ xin phép giả sử ta có 3 coin với giá trị lần lượt là 1,3,4 và tổng giá trị cần là 10. Bắt đầu thử suy nghĩ theo mạch dùng Quy hoạch động nha :D

Gọi hàm *solve(x)* là số xu ít nhất cần để có tổng giá trị là x. Ta có các giá trị sau:

*solve(0)* = 0 -> *solve(1)* = 1 -> *solve(2)* = 2 -> *solve(3)* = 1 -> *solve(4)* = 1 -> *solve(5)* = 2

-> *solve(6)* = 2 -> *solve(7)* = 2 -> *solve(8)* = 2 -> *solve(9)* = 3 -> *solve(10)* = 3

Ví dụ, *solve(10)* = 3 vì ta sẽ lấy 3 xu có giá trị lần lượt là 3, 3, 4 có 3 + 3 + 4 = 10. 

Vấn đề là tìm **công thức truy hồi** như nào đây???

Dễ thấy một quy luật rằng: Số xu ít nhất cho tổng T = số xu ít nhất cho tổng (T - c<sub>k</sub>) + 1 với c<sub>k</sub> là một giá trị của một đồng xu nào đó trong tập đồng xu đã cho. 
Có đoạn "+1" trong công thức chính là số lượng xu thêm :))

Trong bài toán này, ta có thể viết như sau:

```C++

solve(x) = min(solve(x-1)+1, solve(x-3)+1, solve(x-4)+1)

```

Do đó các bài toán con của solve(10) là solve(9), solve(8),... Bài toán cơ sở là solve(0) = 0. 

Ngon roài! Đã có công thức truy hồi, giờ triển code thoai :D

```C++

int solve(int x) {
  if (x < 0) return INF; // không có trường hợp tổng giá trị nhỏ hơn 0 nên gán bằng vô cực nha
  if (x == 0) return 0;
  int best = INF;
  for (auto c : coins) {
   best = min(best, solve(x-c)+1);
  }
  return best;
}

``` 

Nhưng mà chờ đã, đoạn code trên là đệ quy mà, vậy thì ta sẽ phải lưu giá trị của các bài toán con như nào? Đoạn code dưới sẽ giúp anh em:

```C++

int value[T+1] //T là tổng giá trị các đồng xu mà đề bài cho trước, value là số xu ít nhất để đạt tổng giá trị T 
int solve(int x) {
  value[0] = 0;
  for (int x = 1; x <= n; x++) {  
    value[x] = INF;
    for (auto c : coins) {
      if (x-c >= 0) {
        value[x] = min(value[x], value[x-c]+1);
      }
    }
  }
}

```

Yay! Một đoạn code sử dụng Quy hoạch động là như ở trên đó :)) Muốn thành thạo thì chỉ có làm nhiều bài tập thoai.

## Let's practice

1. https://codeforces.com/problemset/problem/732/B
2. https://codeforces.com/problemset/problem/1182/A
3. https://codeforces.com/problemset/problem/753/A
4. https://codeforces.com/problemset/problem/72/G
5. https://codeforces.com/problemset/problem/706/B
6. https://codeforces.com/problemset/problem/313/B
7. https://codeforces.com/problemset/problem/368/B
8. https://codeforces.com/problemset/problem/363/B


## Tham khảo
1. Giải thuật và lập trình - Thầy Lê Minh Hoàng
2. [cp-algorithms.com](https://cp-algorithms.com/)
3. Handbook Competitive Programming
