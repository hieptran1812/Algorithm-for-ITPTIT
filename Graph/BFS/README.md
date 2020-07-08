# Thuật toán Breadth-First Search

## Tổng quan

Trong lý thuyết đồ thị, tìm kiếm theo chiều rộng (BFS) là một thuật toán tìm kiếm trong đồ thị trong đó việc tìm kiếm chỉ bao gồm 2 thao tác: (a) cho trước một đỉnh của đồ thị; (b) thêm các đỉnh kề với đỉnh vừa cho vào danh sách có thể hướng tới tiếp theo. Có thể sử dụng thuật toán tìm kiếm theo chiều rộng cho hai mục đích: tìm kiếm đường đi từ một đỉnh gốc cho trước tới một đỉnh đích, và tìm kiếm đường đi từ đỉnh gốc tới tất cả các đỉnh khác. Trong đồ thị không có trọng số, thuật toán tìm kiếm theo chiều rộng luôn tìm ra đường đi ngắn nhất có thể. Thuật toán BFS bắt đầu từ đỉnh gốc và lần lượt nhìn các đỉnh kề với đỉnh gốc. Sau đó, với mỗi đỉnh trong số đó, thuật toán lại lần lượt nhìn trước các đỉnh kề với nó mà chưa được quan sát trước đó và lặp lại. Xem thêm thuật toán tìm kiếm theo chiều sâu, trong đó cũng sử dụng 2 thao tác trên nhưng có trình tự quan sát các đỉnh khác với thuật toán tìm kiếm theo chiều rộng.

<p align = "center"><img src = "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_r%E1%BB%99ng_BFS.gif/465px-T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_r%E1%BB%99ng_BFS.gif"></p>

## Kĩ thuật

### Đặt vấn đề



### Mô tả thuật toán

<p align = "center"><img src = "https://he-s3.s3.amazonaws.com/media/uploads/0dbec9e.jpg" height = 1200></p>

The traversing will start from the source node and push s in queue. s will be marked as 'visited'.

First iteration

s will be popped from the queue
Neighbors of s i.e. 1 and 2 will be traversed
1 and 2, which have not been traversed earlier, are traversed. They will be:
Pushed in the queue
1 and 2 will be marked as visited
Second iteration

1 is popped from the queue
Neighbors of 1 i.e. s and 3 are traversed
s is ignored because it is marked as 'visited'
3, which has not been traversed earlier, is traversed. It is:
Pushed in the queue
Marked as visited
Third iteration

2 is popped from the queue
Neighbors of 2 i.e. s, 3, and 4 are traversed
3 and s are ignored because they are marked as 'visited'
4, which has not been traversed earlier, is traversed. It is:
Pushed in the queue
Marked as visited
Fourth iteration

3 is popped from the queue
Neighbors of 3 i.e. 1, 2, and 5 are traversed
1 and 2 are ignored because they are marked as 'visited'
5, which has not been traversed earlier, is traversed. It is:
Pushed in the queue
Marked as visited
Fifth iteration

4 will be popped from the queue
Neighbors of 4 i.e. 2 is traversed
2 is ignored because it is already marked as 'visited'
Sixth iteration

5 is popped from the queue
Neighbors of 5 i.e. 3 is traversed
3 is ignored because it is already marked as 'visited'
The queue is empty and it comes out of the loop. All the nodes have been traversed by using BFS.

If all the edges in a graph are of the same weight, then BFS can also be used to find the minimum distance between the nodes in a graph.

### Chứng minh thuật toán

Coming soon!

### Cài đặt

**Mã giả**:
```
BFS (G, s)                   //G là đồ thị và s là đỉnh nguồn
      Đặt Q là hàng đợi (Queue)
      Q.enqueue(s) // Thêm đỉnh s vào hàng đợi Q cho đến khi tất cả đỉnh kề của s được đánh dấu

      mark s as visited. // Đánh dấu đỉnh s đã được xét
      while ( Q is not empty)
           //Removing that vertex from queue,whose neighbour will be visited now
           v  =  Q.dequeue( )

          //Xét tất cả đỉnh kề của đỉnh v
          for all neighbours w of v in Graph G
               if w is not visited 
                        Q.enqueue( w )             //Stores w in Q to further visit its neighbour
                        mark w as visited.
```

**Code**:
```C++

```

### Độ phức tạp

**Không gian**

Nếu V là tập hợp đỉnh của đồ thị và |V| là số đỉnh thì không gian cần dùng của thuật toán là O(|V|).

**Thời gian**

Nếu V và E là tập hợp các đỉnh và cung của đồ thị, thì thời gian thực thi của thuật toán là O(|E|+|V|) vì trong trường hợp xấu nhất, mỗi đỉnh và cung của đồ thị được thăm đúng một lần. Ghi chú: O(|E|+|V|) nằm trong khoảng từ O(|V|) đến O(|V|<sup>2</sup>), tùy theo số cung của đồ thị.

## Ví dụ



## Ứng dụng

Thuật toán tìm kiếm theo chiều rộng được dùng để giải nhiều bài toán trong lý thuyết đồ thị, chẳng hạn như:

* Tìm tất cả các đỉnh trong một thành phần liên thông
* Thuật toán Cheney cho việc dọn rác
* Tìm đường đi ngắn nhất giữa hai đỉnh u và v (với chiều dài đường đi tính bằng số cung)
* Kiểm tra xem một đồ thị có là đồ thị hai phía
* Thuật toán Cuthill–McKee
* Thuật toán Ford–Fulkerson để tìm luồng cực đại trong mạng

**Tìm các thành phần liên thông**

Tập hợp các đỉnh đã được quan sát bởi thuật toán tìm kiếm theo chiều rộng chính là thành phần liên thông chứa đỉnh gốc.

**Kiểm tra đồ thị hai phía**

Có thể dùng thuật toán tìm kiếm theo chiều rộng để kiểm tra xem một đồ thị có phải đồ thị hai phía hay không, bằng cách tìm kiếm từ một đỉnh bất kì và gán nhãn chẵn lẻ cho các đỉnh được quan sát. Nghĩa là, gán nhãn 0 cho đỉnh gốc, 1 cho tất cả các đỉnh kề đỉnh gốc, 0 cho tất cả các đỉnh kề với một đỉnh kề đỉnh gốc, và tiếp tục như vậy. Nếu ở một bước nào đó, có hai đỉnh kề nhau có cùng nhãn, thì đồ thị không là hai phía. Nếu quá trình tìm kiếm kết thúc mà điều này không xảy ra thì đồ thị là hai phía.

## Let's practice

1. https://codeforces.com/group/FLVn1Sc504/contest/274425/problem/A
2. https://codeforces.com/group/FLVn1Sc504/contest/274829/problem/L
3. https://codeforces.com/group/FLVn1Sc504/contest/274833/problem/U
4. https://codeforces.com/group/FLVn1Sc504/contest/274833/problem/R
5. https://codeforces.com/group/FLVn1Sc504/contest/274824/problem/D
6. https://codeforces.com/group/FLVn1Sc504/contest/274509/problem/Y
7. https://codeforces.com/group/FLVn1Sc504/contest/274830/problem/V
8. https://codeforces.com/group/FLVn1Sc504/contest/274827/problem/O

## Tham khảo
1. [Wikipedia.org](https://vi.wikipedia.org/wiki/T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_r%E1%BB%99ng)
2. [vnspoj.blogspot.com](https://vnspoj.blogspot.com/p/blog-page_41.html)
3. [www.hackerearth.com](https://www.hackerearth.com/practice/algorithms/graphs/breadth-first-search/tutorial/)
4. [cp-algorithms.com](https://cp-algorithms.com/graph/breadth-first-search.html)
