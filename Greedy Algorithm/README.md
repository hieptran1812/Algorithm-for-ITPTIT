# Thuật toán tham lam

## Tổng quan

Thuật toán tham lam là bất kỳ thuật toán nào sử dụng phương pháp giải quyết vấn đề để đưa ra lựa chọn tối ưu cục bộ (mình tạm gọi là đáp số tối ưu cho bài toán con tại thời điểm đó), sau đó kết hợp các đáp án để tìm kiếm tối ưu toàn cầu (đáp số bài toán lớn). 
Trong nhiều vấn đề, một chiến lược tham lam thường không tạo ra một giải pháp tối ưu, nhưng dù sao, nó có thể mang lại một kết quả gần đúng trong khoảng thời gian chấp nhận được.

<p align = "center"><img src = "https://www.researchgate.net/profile/Simone_Martins2/publication/226303975/figure/fig1/AS:669965959041037@1536743740856/Greedy-algorithm-for-minimization.png"></p>

## Kĩ thuật

Nói chung, các thuật toán tham lam có năm thành phần: 
* Một bộ các phương án có thể áp dụng.
* Hàm chọn, chọn phương án tốt nhất được thêm vào giải pháp.
* Một hàm kiểm tra tính khả thi, được sử dụng để xác định xem một phương có nên được sử dụng để đóng góp cho một giải pháp không. 
* Hàm mục tiêu, cập nhật giá trị bài toán tạm thời khi sử dụng một phương án.
* Một hàm giải pháp, sẽ cho biết khi nào chúng ta đã tìm ra một giải pháp hoàn chỉnh cho bài toán.

Khi dùng thuật toán tham lam phải hết sức cẩn thận xem đó có phải đáp án tối ưu nhất chưa. Muốn biết thì ta phải kiểm soát được đáp số của từng bài toán con và kết hợp của các đáp số đó có cho ta một đáp số như ý không. 

## Ví dụ

Có rất nhiều bài toán sử dụng hướng đi tham lam nên mình xin phép chọn ra ba ví dụ đơn giản sau:

### Tìm tích lớn nhất của dãy con cho trước

**Nguồn bài và code:** https://www.geeksforgeeks.org/minimum-product-subset-array/

**Ý tưởng giải** khi sử dụng tư tưởng tham lam:

Ta có bộ ba phương án tương ứng với các bài toán con sau:

1. Nếu có số chẵn số âm và không có số 0, kết quả là tích của tất cả phần tử, ngoại trừ số âm có giá trị lớn nhất.
2. Nếu có một số lẻ các số âm và không có số 0, kết quả chỉ đơn giản là tích của tất cả phần tử.
3. Nếu có số 0 và số dương, không có số âm, kết quả là 0. Trường hợp ngoại lệ là khi không có số âm và tất cả các phần tử khác dương thì kết quả phải là số dương nhỏ nhất.

### Tổng lớn nhất của các trị tuyệt đối của các hiệu khi hoán vị dãy (Nghe hơi ngang xíu :> mọi người đọc trong link để rõ hơn nha)

**Nguồn bài và code:** https://www.geeksforgeeks.org/maximum-sum-absolute-difference-array/

**Ý tưởng giải** khi sử dụng tư tưởng tham lam: 

Để giải quyết vấn đề này, ta sử dụng tư tưởng tham lam rằng làm thế nào có thể tối đa hóa giá trị chênh lệch của các phần tử để thu được tổng lớn nhất.
Điều này chỉ có thể nếu ta tính hiệu giữa một số giá trị rất cao và một số giá trị rất thấp (cao nhất - nhỏ nhất). Để thực hiện hóa ý tưởng trên ta chỉ cần sort tăng dần và giảm dần rồi tính kết quả thôi :))

## Let's practice

1. https://codeforces.com/problemset/problem/1321/A

2. https://codeforces.com/problemset/problem/892/A

3. https://codeforces.com/problemset/problem/1107/A

4. https://codeforces.com/problemset/problem/1011/A

5. https://codeforces.com/problemset/problem/1163/A

6. https://codeforces.com/problemset/problem/1132/B

7. https://codeforces.com/problemset/problem/814/A

8. https://codeforces.com/problemset/problem/991/B

## Tham khảo

1. [Viblo](https://viblo.asia/followings)
2. [Wikipedia](https://vi.wikipedia.org/wiki/Wikipedia)
3. [Giaithuatlaptrinh.com](https://www.giaithuatlaptrinh.com/?p=48)
4. [Codeforces.com](https://codeforces.com/)



