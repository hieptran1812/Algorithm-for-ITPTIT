# Thuật toán Fleury

## Tổng quan


### Đặt vấn đề

Giả sử đồ thị tồn tại chu trình Euler, tìm chu trình đó. 

### Mô tả thuật toán 

Xuất phát từ một đỉnh, ta chọn một cạnh liên thuộc với nó để đi tiếp theo hai nguyên tắc sau:
* Xóa bỏ cạnh đã đi qua.
* Chỉ đi qua cầu khi không còn cạnh nào khác để chọn.

Ta cứ chọn cạnh đi như vậy cho tới khi không đi tiếp được nữa, đường đi tìm được là chu trình Euler.

<p align = "center"><img src = "https://www.tutorialspoint.com/assets/questions/media/28707/fleurys_algorithm.jpg">

Cho đồ thị như trên:
1. Xuất phát từ đỉnh 2, ta có 3 cách đi tiếp là (2,0), (2,1), (2,3). Chọn cạnh (2,0) hoặc (2,1) vì (2,3) là cạnh cầu.
2. Giả sử đi theo cạnh (2,0), ta xóa cạnh (2,0) và hiện tại đang ở đỉnh 0.
3. Từ đỉnh 0 chỉ có một cạnh duy nhất để đi tiếp là (0,1), đi theo cạnh (0,1) và xóa cạnh (0,1).
4. Từ đỉnh 1 chỉ có một cạnh duy nhất để đi tiếp là (1,2), đi theo cạnh (1,2) và xóa cạnh (1,2).
5. Từ đỉnh 2 chỉ có một cạnh duy nhất để đi tiếp là (2,3), đi theo cạnh (2,3) và xóa cạnh (2,3).
6. Tất cả các cạnh đã được xóa, ta tìm được chu trình Euler 2 - 0 - 1 - 3.

Ở bước 1 nếu đi theo (2,1) ta vẫn tìm được chu trình.

### Tính đúng đắn của thuật toán

Coming soon!

### Code

Thuật toán Fleury
```C++

```

### Độ phức tạp

Độ phức tạp thời gian trung bình: O(|E|)

## Let's practice
1.
2.
3.
4.
5.
6.
7.
8.

## Tham khảo
