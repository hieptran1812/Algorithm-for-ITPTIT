# Thuật toán Bellman-Ford 

## Tổng quan

Thuật toán Bellman-Ford là thuật toán dùng để tìm đường đi ngắn nhất từ một đỉnh tới các đỉnh còn lại trong đồ thị có trọng số. Cùng một vấn đề nhưng thuật toán Bellman-Ford **chậm hơn** so với thuật toán Dijsktra nhưng lại **đa năng hơn** ở chỗ thuật toán có thể xử lý **trên đồ thị có cạnh mang trọng số âm**. Thuật toán được đề xuất lần đầu tiên bởi Alfonso Shimbel (1955), nhưng được đặt tên theo Richard Bellman và Lester Ford Jr. Hai người đã công bố thuật toán lần lượt vào năm 1958 và 1956. 


## Kĩ thuật

### Đặt vấn đề

Cho đồ thị như sau:

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/bellman1.png"></p>
                                                                                                                   
Tìm đường đi ngắn nhất giữa đỉnh 1 với các đỉnh còn lại trong đồ thị.                                                                                                             

### Ý tưởng thuật toán

Ta xét ví dụ với đồ thị có hướng sau (giả định các đường đi là một chiều, chỉ đi từ đỉnh có số thứ tự thấp hơn tới đỉnh có số thứ tự cao hơn, số có màu đỏ cạnh mỗi đỉnh là độ dài đường đi ngắn nhất từ gốc tới đỉnh đó, và đỉnh gốc là đỉnh 1).

Khởi tạo:
<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/bellman1.png"></p>

Thực hiện lần duyệt đầu tiên, ta cập nhật được đường đi ngắn nhất thông qua các cạnh (1, 2); (1, 3); (1, 4):

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/bellman2.png"></p>

Tương tự với lần duyệt thứ 2, cạnh (2, 5) và (3, 4) là các cạnh tối ưu:
													    
<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/bellman3.png"></p>

Với lần duyệt thứ 3, chỉ có cạnh (4, 5) cải tiến đường đi tối ưu:
													    
<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/bellman4.png"></p>
													    
Tới lần duyệt thứ 4, ta thấy không còn cạnh nào có thể tối ưu hóa bất kỳ đường đi ngắn nhất nào nữa. Tới đây, ta hoàn toàn có thể dừng duyệt (vì chắc chắn việc không còn cạnh có thể tối ưu cũng đồng nghĩa với việc không có chu trình âm trong đồ thị).

### Chứng minh thuật toán

Coming soon!

### Cài đặt

**Mã giả**:
```C
 function BellmanFord(danh_sách_đỉnh, danh_sách_cung, nguồn)
   // hàm yêu cầu đồ thị đưa vào dưới dạng một danh sách đỉnh, một danh sách cung
   // hàm tính các giá trị khoảng_cách và đỉnh_liền_trước của các đỉnh, 
   // sao cho các giá trị đỉnh_liền_trước sẽ lưu lại các đường đi ngắn nhất.

   // bước 1: khởi tạo đồ thị
   for each v in danh_sách_đỉnh:
       if v is nguồn then khoảng_cách(v):= 0
       else khoảng_cách(v):= vô cùng
       đỉnh_liền_trước(v):= null
   
   // bước 2: kết nạp cạnh
   for i from 1 to size(danh_sách_đỉnh)-1:       
       for each (u,v) in danh_sách_cung:
           if khoảng_cách(v) > khoảng_cách(u) + trọng_số(u,v):
               khoảng_cách(v):= khoảng_cách(u) + trọng_số(u,v)
               đỉnh_liền_trước(v):= u

   // bước 3: kiểm tra chu trình âm
   for each (u,v) in danh_sách_cung:
       if khoảng_cách(v) > khoảng_cách(u) + trọng_số(u,v):
           error "Đồ thị chứa chu trình âm"
```

**Code**:

```C

// Thuat toan voi do thi khong co chu trinh am

#include <bits/stdc++.h>
using namespace std;

typedef pair<int, int> ii;
vector<ii> a[181220];
int n, m;

int d[181220];
bool inqueue[181220];
int pre[181220];
vector<int>path;

void bellman(int u) {
    queue<int> qu;
    //Buoc 1: Khoi tao
    for (int i = 1; i <= n; i++)
        d[i] = 99999999;
    d[u] = 0;
    qu.push(u); //push u vào queue
    inqueue[u] = true; //Đánh dấu đỉnh u đã trong queue
	// Buoc 2: Lap
    while (qu.size()) {
        u = qu.front(); //Lấy giá trị đầu của queue
        inqueue[u] = false; //Đánh dấu là đỉnh u đã pop ra khỏi queue (hay không còn trong queue)
        qu.pop(); // pop đỉnh u ra khỏi queue
        for (int i = 0; i < a[u].size(); i++) { // Duyệt các đỉnh kề u
            int v = a[u][i].second; 
            int uv = a[u][i].first;
            if (d[v] > d[u] + uv) {
                d[v] = d[u] + uv;
                pre[v] = u;
                if (!inqueue[v]) { // Nếu đỉnh v chưa trong queue
                    qu.push(v); // Cho v vào queue
                    inqueue[v] = true; // Đánh dấu là đỉnh v đã trong queue
                }
            }
        }
    }
}

int main() {
    int u, v; // dinh nguon va dinh dich
    scanf("%d%d%d%d", &n, &m, &u, &v);
    while (m--) {
        int p, q, w;
        scanf("%d%d%d", &p, &q, &w);
        // Do thi vo huong
        a[p].push_back(ii(w, q));
        a[q].push_back(ii(w, p));
    }
    bellman(u);
    printf("%d\n", d[v]);
    for(int i = v; i != u;  i = pre[i]) path.push_back(i); // them dinh vao duong di
    path.push_back(u);
    reverse(path.begin(), path.end());
    printf("Duong di: ");
    for(int i = 0; i < path.size(); i++){
    	if(i == path.size() - 1){
    		printf("%d", v);
    		break;
	} 
   	printf("%d -> ",path[i]);
    }
}

```

### Độ phức tạp

* Độ phức tạp thời gian trong trường hợp tốt nhất: O(|E|)
* Độ phức tạp thời gian trung bình: O(|E|.|V|)
* Độ phức tạp thời gian trong trường hợp xấu nhất: O(|E|.|V|)

## Ví dụ

Xem code trên :D

## Ứng dụng

Một biến thể phân tán của thuật toán Bellman-Ford được dùng trong các giao thức định tuyến vector khoảng cách, chẳng hạn giao thức RIP (Routing Information Protocol). Đây là biến thể phân tán vì nó liên quan đến các nút mạng (các thiết bị định tuyến) trong một hệ thống tự chủ (autonomous system), ví dụ một tập các mạng IP thuộc sở hữu của một nhà cung cấp dịch vụ Internet (ISP).

Thuật toán gồm các bước sau:

* Mỗi nút tính khoảng cách giữa nó và tất cả các nút khác trong hệ thống tự chủ và lưu trữ thông tin này trong một bảng.
* Mỗi nút gửi bảng thông tin của mình cho tất cả các nút lân cận.
* Khi một nút nhận được các bảng thông tin từ các nút lân cận, nó tính các tuyến đường ngắn nhất tới tất cả các nút khác và cập nhật bảng thông tin của chính mình.

Nhược điểm chính của thuật toán Bellman-Ford trong cấu hình này là:

* Không nhân rộng tốt.
* Các thay đổi của tô-pô mạng không được ghi nhận nhanh do các cập nhật được lan truyền theo từng nút một.
* Đếm dần đến vô cùng (nếu liên kết hỏng hoặc nút mạng hỏng làm cho một nút bị tách khỏi một tập các nút khác, các nút này vẫn sẽ tiếp tục ước tính khoảng cách tới nút đó và tăng dần giá trị tính được, trong khi đó còn có thể xảy ra việc định tuyến thành vòng tròn)

## Let's practice

1. https://codeforces.com/problemset/problem/601/A
2. https://codeforces.com/problemset/problem/986/A
3. https://codeforces.com/problemset/problem/689/B
4. https://codeforces.com/problemset/problem/954/D
5. https://codeforces.com/problemset/problem/916/C
6. https://codeforces.com/problemset/problem/793/B
7. https://codeforces.com/problemset/problem/253/C
8. https://codeforces.com/problemset/problem/1365/D

## Tham khảo

1. [Wikipedia.org](https://en.wikipedia.org/wiki/Bellman%E2%80%93Ford_algorithm)
2. [Brilliant.org](https://brilliant.org/wiki/bellman-ford-algorithm/#:~:text=The%20Bellman%2DFord%20algorithm%20is,other%20vertices%20in%20the%20graph.&text=Going%20around%20the%20negative%20cycle,the%20path%20length%20is%20increasing)
3. Giải thuật và lập trình - Thầy Lê Minh Hoàng
4. [cp-algorithms.com](https://cp-algorithms.com/graph/bellman_ford.html)
5. [kc97ble](https://sites.google.com/site/kc97ble/algorithm-graph/fordbellmanqueue-cpp)
6. Competitve Programming's Handbook 
7. [thuytrangcoding.wordpress.com](https://thuytrangcoding.wordpress.com/2018/03/19/graph-shortestpath-bellmanford/)


