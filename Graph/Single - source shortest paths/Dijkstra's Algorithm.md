# Thuật toán Dijkstra

## Tổng quan

Thuật toán Dijkstra, mang tên của nhà khoa học máy tính người Hà Lan Edsger Dijkstra vào năm 1956 và ấn bản năm 1959, 
là một thuật toán giải quyết bài toán đường đi ngắn nhất nguồn đơn trong một đồ thị có hướng không có cạnh mang trọng số âm. Thuật toán thường được sử dụng trong định tuyến với một chương trình con trong các thuật toán đồ thị hay trong công nghệ Hệ thống định vị toàn cầu (GPS).

Ví dụ: Chúng ta dùng các đỉnh của đồ thị để mô hình các thành phố và các cạnh để mô hình các đường nối giữa chúng. Khi đó trọng số các cạnh có thể xem như độ dài của các con đường (và do đó là không âm). Chúng ta cần di chuyển từ thành phố s đến thành phố t. Thuật toán Dijkstra sẽ giúp chỉ ra đường đi ngắn nhất chúng ta có thể đi.

Trọng số không âm của các cạnh của đồ thị **mang tính tổng quát hơn** khoảng cách hình học giữa hai đỉnh đầu mút của chúng. Ví dụ, với 3 đỉnh A, B, C đường đi A-B-C có thể ngắn hơn so với đường đi trực tiếp A-C.

## Kĩ thuật

### Đặt vấn đề

Cho đồ thị như hình dưới:
 
<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497257275137"</p>

Hãy tìm đường đi ngắn nhất giữa đỉnh C và các đỉnh còn lại trong đồ thị.

### Ý tưởng thuật toán

Tớ sẽ áp dụng thuật toán Dijsktra cho đồ thị trên, hãy nghiên cứu thật kĩ từng công đoạn một vì nếu chỉ bỏ qua một chi tiết nhỏ ta sẽ không thể hiểu thuật toán được:

1. Trong toàn bộ quá trình thực thi thuật toán, tớ sẽ đánh dấu tất cả các đỉnh bằng khoảng cách nhỏ nhất từ đỉnh C tới các đỉnh đó.
Với đỉnh C, khoảng cách sẽ là 0 (tất nhiên rồi :D). Với các đỉnh còn lại, ban đầu chưa biết khoảng cách nhỏ nhất nên tớ sẽ đánh dấu mỗi đỉnh bằng giá trị vô cùng (∞).

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497265537633"></p>

Chúng ta cũng đánh dấu đỉnh hiện tại đang xét (ban đầu là đỉnh nguồn C). Ở đồ thị trên, tớ đánh dấu bằng một chấm đỏ ở đỉnh C (đỉnh hiện tại đang xét).

2. Okay! Giờ chúng ta **kiểm tra các đỉnh kề với đỉnh hiên tại đang xét** (đỉnh C - current node) đó là đỉnh A, B, D (không cần theo thứ tự cụ thể). 
Hãy bắt đầu với đỉnh B. Tớ sẽ lấy giá trị dùng đánh dấu ở đỉnh C (giá trị 0) cộng với trọng số của cạnh nối đỉnh đang xét (đỉnh C) với đỉnh B (trong trường hợp này là 7), ta được 0 + 7 = 7.
Oke roài, sau đó ta sẽ so sánh giá trị vừa tính được với giá trị dùng đánh dấu ở đỉnh B (vô cùng). Ta sẽ đánh dấu đỉnh B nhận giá trị nhỏ hơn là 7 (7 nhỏ hơn vô cùng).

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497279927597"></p>

Đỉnh B đã xong, giờ ta kiểm tra đỉnh kề A. Ta cộng 0 (giá trị dùng đánh dấu ở đỉnh C) với 1 (trọng số của cạnh nối đỉnh C với đỉnh A) và được 0 + 1 = 1. Dễ thấy giá trị 1 nhỏ hơn vô cùng (giá trị dùng đánh dấu ở đỉnh A). Do đó ta sẽ đánh dấu đỉnh A nhận giá trị 1.

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497284902206"></p>

Tương tự với đỉnh D:

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497297264677"></p>

Yay! Ta đã xét xong các đỉnh kề với đỉnh đang xét (đỉnh C). Tớ sẽ đánh một dấu tick ở đỉnh C để thể hiện rằng các đỉnh kề nó đã được xét xong.

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497301316895"></p>

3. Giờ ta sẽ xét sang một đỉnh mới (gọi là đỉnh hiện tại đang xét - current node). Đỉnh này phải thỏa mãn điều kiện là **chưa được xét** và **được đánh dấu với giá trị nhỏ nhất**. Đó là đỉnh A (bạn đọc kiểm tra lại hai điều kiện trên với đỉnh A nhé :D).
Tương tự như đỉnh C, tớ sẽ đánh dấu đỉnh A bằng một dấu chấm đỏ.

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497311165233"></p>

Okay, bây giờ ta lặp lại thuật toán như đã làm với đỉnh C. Chúng ta kiểm tra các đỉnh kề với đỉnh A (Current node), nhớ rằng **không kiểm tra những đỉnh đã xét rồi (đỉnh C)**. Vậy là ta chỉ cần kiểm tra đỉnh B.

Với B, Ta cộng 1 (giá trị được đánh dấu ở đỉnh A) với 3 (trọng số của cạnh nối đỉnh A với đỉnh B) và được 4. Vì 4 < 7 nên ta cập nhật giá trị dùng đánh dấu ở đỉnh B là 4.

Sau đó, tớ đánh dấu đỉnh A đã xét xong bằng dấu tick và chọn một đỉnh để xét mới (current node mới) thỏa mãn điều kiện chưa được xét và giá trị đang đánh dấu cho đỉnh đó nhỏ nhất, đó là đỉnh D.

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497330975308"></p>

4. Ta tiếp tục lặp lại thuật toán. Lần này, ta kiểm tra đỉnh kề với D là B và E. 
Với B, ta có 2 + 5 = 7. 7 > 4, vẫn giữ 4 là giá trị đánh dấu cho đỉnh B. Với E, ta có 2 + 7 = 9 (9 < vô cùng) nên ta cập nhật đỉnh E nhận giá trị đánh dấu mới là 9. 
Ta đánh dấu B đã xét xong và chuyển sang đỉnh B.

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497346742885"></p>

5. Tiếp tục, tương tự thôi :)) ta cập nhật được giá trị đánh dấu cho đỉnh E mới là 5. Đỉnh B xét xong, chuyển sang đỉnh cuối cùng là E.
<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497350226741"></p>

6. Đỉnh E lại **không có đỉnh kề mà chưa xét** nào, do đó ta không phải kiểm tra gì cả. Đánh dấu đỉnh E đã xét xong.

<p align = "center"><img src = "https://www.codingame.com/servlet/fileservlet?id=14497361633811"></p>

Done!!! Vậy là tất cả các đỉnh đều đã được xét. Giờ khoảng cách ngắn nhất từ đỉnh C tới các đỉnh còn lại chính là giá trị đang đánh dấu của đỉnh đó. Ví dụ, từ C đến B khoảng cách ngắn nhất là 4, từ C đến E khoảng cách ngắn nhất là 5,...

**Tóm lại** thuật toán thực hiện các bước như sau:

```
1. Đánh dấu đỉnh ban đầu (đỉnh nguồn) là 0 và các đỉnh còn lại là vô cùng.
2. Gọi đỉnh chưa xét với giá trị đánh dấu nhỏ nhất là C (current node).
3. Với mỗi đỉnh kề N (neighbour) với đỉnh C: Cộng giá trị đang đánh dấu của đỉnh C với trọng số của cạnh nối đỉnh C với đỉnh N. Nếu được kết quả nhỏ hơn giá trị đang đánh dấu ở đỉnh N ta cập nhật giá trị đánh dấu cho đỉnh N mới (Xem ví dụ trên để hiểu hơn).
4. Đánh dấu đỉnh C đã xét xong.
5. Nếu vẫn còn đỉnh chưa xét, lặp lại bước 2.
```

### Cài đặt

**Mã giả**:
```C++
void Dijkstra(Graph, source):
       dist[source]  := 0                     // Distance from source to source is set to 0
       for each vertex v in Graph:            // Initializations
           if v ≠ source
               dist[v]  := infinity           // Unknown distance function from source to each node set to infinity
           add v to Q                         // All nodes initially in Q

      while Q is not empty:                   // The main loop
          v = vertex in Q with min dist[v]    // In the first run-through, this vertex is the source node
          remove v from Q 

          for each neighbor u of v:           // where neighbor u has not yet been removed from Q.
              dist[u] = min(dist[u], dist[v] + length(v, u)
              
      return dist[]
  end function
```

**Code**:
```C
#include <stdio.h>
#include <vector>
#include <queue>
using namespace std;

const int oo = 9999999; // danh dau la vo cuc
typedef pair<int, int> ii;

vector<ii> a[2309];
int n, m;

int d[1812];

void dijkstra() {
    priority_queue<ii, vector<ii>, greater<ii>> pq; //Hang doi uu tien, gia tri first be hon len dau
    for (int i = 1; i <= n; i++)
        d[i] = oo; //gan gia tri d[i] bang vo cuc
    d[1] = 0;
    pq.push(ii(0, 1));
    while (pq.size()) {
        int u = pq.top().second;
        int du = pq.top().first;
        pq.pop();
        if (du != d[u]){ //Dieu kien de bo qua pair ma gia tri d[u] duoc cap nhat tu lan lap truoc
        	continue;
		}
        for (int i = 0; i < a[u].size(); i++) {
            int v = a[u][i].second;
            int uv = a[u][i].first;
            if (d[v] > du + uv) {
                d[v] = du + uv;
                pq.push(ii(d[v], v));
            }
        }
    }
}

int main() {
    int p, q, m, w;
    scanf("%d%d", &n, &m);
    while (m--) {
        scanf("%d%d%d", &p, &q, &w);
        a[p].push_back(ii(w, q));
        a[q].push_back(ii(w, p));
    }
    dijkstra();
    for (int i = 1; i <= n; i++)
        printf("d( 1 -> %d ) = %d\n", i, d[i]);
}
```
### Độ phức tạp

Độ phức tạp thời gian O(E.logV)

### Ưu, nhược điểm




## Ví dụ

## Ứng dụng



## Let's practice

1.

## Tham khảo

1. [Wikipedia](https://vi.wikipedia.org/wiki/Thu%E1%BA%ADt_to%C3%A1n_Dijkstra)
2. Handbook Competitive Programming


