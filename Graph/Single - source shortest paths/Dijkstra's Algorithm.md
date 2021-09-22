# Thuật toán Dijkstra và ứng dụng

# Tổng quan

Các bài toán về tìm đường đi ngắn nhất và biến tướng của nó luôn xuất hiện rất nhiều trong các cuộc thi lập trình thi đấu bởi sự đa dạng trong cách đưa ra đề bài và sử dụng. Một trong những thuật toán tìm đường đi ngắn nhất được sử dụng phổ biến đó là thuật toán Dijsktra.

Theo Wikipedia, thuật toán Dijkstra, mang tên của nhà khoa học máy tính người Hà Lan Edsger Dijkstra vào năm 1956 và ấn bản năm 1959, là một thuật toán giải quyết bài toán đường đi ngắn nhất nguồn đơn trong một đồ thị **có hướng không có cạnh mang trọng số âm**. Thuật toán thường được sử dụng trong định tuyến với một chương trình con trong các thuật toán đồ thị hay trong công nghệ Hệ thống định vị toàn cầu (GPS).

Ví dụ: Chúng ta dùng các đỉnh của đồ thị để biểu diễn các thành phố và các cạnh để biểu diễn các đường nối giữa chúng. Khi đó trọng số các cạnh có thể xem như độ dài của các con đường (do đó không âm). Chúng ta cần di chuyển từ thành phố s đến thành phố t. Thuật toán Dijkstra sẽ giúp chỉ ra đường đi ngắn nhất có thể đi.

Trọng số không âm của các cạnh của đồ thị **mang tính tổng quát hơn** khoảng cách hình học giữa hai đỉnh đầu mút của chúng. Ví dụ, với 3 đỉnh A, B, C đường đi A-B-C có thể ngắn hơn so với đường đi trực tiếp A-C.

# Kĩ thuật

## Mô tả thuật toán

Để dễ hình dung cách hoạt động của thuật toán, ta xét ví dụ sau.

Cho đồ thị như hình dưới:

![](https://www.codingame.com/servlet/fileservlet?id=14497257275137)

Nguồn ảnh: https://www.codingame.com

Hãy tìm đường đi ngắn nhất giữa đỉnh C và các đỉnh còn lại trong đồ thị.

Ta sẽ áp dụng thuật toán Dijsktra cho đồ thị trên, hãy nghiên cứu thật kĩ từng công đoạn một vì nếu chỉ bỏ qua một chi tiết nhỏ ta sẽ không thể hiểu thuật toán được:

1. Trong toàn bộ quá trình thực thi thuật toán, ta sẽ đánh dấu tất cả các đỉnh bằng khoảng cách nhỏ nhất từ đỉnh C tới các đỉnh đó.
   Với đỉnh C, khoảng cách sẽ là 0 (tất nhiên rồi :D). Với các đỉnh còn lại, ban đầu chưa biết khoảng cách nhỏ nhất nên ta sẽ đánh dấu mỗi đỉnh bằng giá trị vô cùng (∞).

![](https://www.codingame.com/servlet/fileservlet?id=14497265537633)

Chúng ta cũng đánh dấu đỉnh hiện tại đang xét (ban đầu là đỉnh nguồn C). Ở đồ thị trên, ta đánh dấu bằng một chấm đỏ ở đỉnh C (đỉnh hiện tại đang xét).

2. Okay! Giờ chúng ta **kiểm tra các đỉnh kề với đỉnh hiên tại đang xét** (đỉnh C - current node) đó là đỉnh A, B, D (không cần theo thứ tự cụ thể).
   Hãy bắt đầu với đỉnh B. Tớ sẽ lấy giá trị dùng đánh dấu ở đỉnh C (giá trị 0) cộng với trọng số của cạnh nối đỉnh đang xét (đỉnh C) với đỉnh B (trong trường hợp này là 7), ta được 0 + 7 = 7.
   Oke roài, sau đó ta sẽ so sánh giá trị vừa tính được với giá trị dùng đánh dấu ở đỉnh B (vô cùng). Ta sẽ đánh dấu đỉnh B nhận giá trị nhỏ hơn là 7 (7 nhỏ hơn vô cùng).

![](https://www.codingame.com/servlet/fileservlet?id=14497279927597)

Đỉnh B đã xong, giờ ta kiểm tra đỉnh kề A. Ta cộng 0 (giá trị dùng đánh dấu ở đỉnh C) với 1 (trọng số của cạnh nối đỉnh C với đỉnh A) và được 0 + 1 = 1. Dễ thấy giá trị 1 nhỏ hơn vô cùng (giá trị dùng đánh dấu ở đỉnh A). Do đó ta sẽ đánh dấu đỉnh A nhận giá trị 1.

![](https://www.codingame.com/servlet/fileservlet?id=14497284902206)

Tương tự với đỉnh D:

![](https://www.codingame.com/servlet/fileservlet?id=14497297264677)

Yay! Ta đã xét xong các đỉnh kề với đỉnh đang xét (đỉnh C). Tớ sẽ đánh một dấu tick ở đỉnh C để thể hiện rằng các đỉnh kề nó đã được xét xong.

![](https://www.codingame.com/servlet/fileservlet?id=14497301316895)

3. Giờ ta sẽ xét sang một đỉnh mới (gọi là đỉnh hiện tại đang xét - current node). Đỉnh này phải thỏa mãn điều kiện là **chưa được xét** và **được đánh dấu với giá trị nhỏ nhất**. Đó là đỉnh A (bạn đọc kiểm tra lại hai điều kiện trên với đỉnh A nhé :D).
   Tương tự như đỉnh C, ta sẽ đánh dấu đỉnh A bằng một dấu chấm đỏ.

![](https://www.codingame.com/servlet/fileservlet?id=14497311165233)

Okay, bây giờ ta lặp lại thuật toán như đã làm với đỉnh C. Chúng ta kiểm tra các đỉnh kề với đỉnh A (Current node), nhớ rằng **không kiểm tra những đỉnh đã xét rồi (đỉnh C)**. Vậy là ta chỉ cần kiểm tra đỉnh B.

Với B, Ta cộng 1 (giá trị được đánh dấu ở đỉnh A) với 3 (trọng số của cạnh nối đỉnh A với đỉnh B) và được 4. Vì 4 < 7 nên ta cập nhật giá trị dùng đánh dấu ở đỉnh B là 4.

Sau đó, ta đánh dấu đỉnh A đã xét xong bằng dấu tick và chọn một đỉnh để xét mới (current node mới) thỏa mãn điều kiện chưa được xét và giá trị đang đánh dấu cho đỉnh đó nhỏ nhất, đó là đỉnh D.

![](https://www.codingame.com/servlet/fileservlet?id=14497330975308)

4. Ta tiếp tục lặp lại thuật toán. Lần này, ta kiểm tra đỉnh kề với D là B và E.
   Với B, ta có 2 + 5 = 7. 7 > 4, vẫn giữ 4 là giá trị đánh dấu cho đỉnh B. Với E, ta có 2 + 7 = 9 (9 < vô cùng) nên ta cập nhật đỉnh E nhận giá trị đánh dấu mới là 9.
   Ta đánh dấu B đã xét xong và chuyển sang đỉnh B.

![](https://www.codingame.com/servlet/fileservlet?id=14497346742885)

5. Tiếp tục, tương tự thôi :)) ta cập nhật được giá trị đánh dấu cho đỉnh E mới là 5. Đỉnh B xét xong, chuyển sang đỉnh cuối cùng là E.
   ![](https://www.codingame.com/servlet/fileservlet?id=14497350226741)

6. Đỉnh E lại **không có đỉnh kề mà chưa xét** nào, do đó ta không phải kiểm tra gì cả. Đánh dấu đỉnh E đã xét xong.

![](https://www.codingame.com/servlet/fileservlet?id=14497361633811)

Done!!! Vậy là tất cả các đỉnh đều đã được xét. Giờ khoảng cách ngắn nhất từ đỉnh C tới các đỉnh còn lại chính là giá trị đang đánh dấu của đỉnh đó. Ví dụ, từ C đến B khoảng cách ngắn nhất là 4, từ C đến E khoảng cách ngắn nhất là 5,...

**Tóm lại** thuật toán thực hiện các bước như sau:

```
1. Đánh dấu đỉnh ban đầu (đỉnh nguồn) là 0 và các đỉnh còn lại là vô cùng.
2. Gọi đỉnh chưa xét với giá trị đánh dấu nhỏ nhất là C (current node).
3. Với mỗi đỉnh kề N (neighbour) với đỉnh C: Cộng giá trị đang đánh dấu của đỉnh C với trọng số của cạnh nối đỉnh C với đỉnh N. Nếu được kết quả nhỏ hơn giá trị đang đánh dấu ở đỉnh N ta cập nhật giá trị đánh dấu cho đỉnh N mới (Xem ví dụ trên để hiểu hơn).
4. Đánh dấu đỉnh C đã xét xong.
5. Nếu vẫn còn đỉnh chưa xét, lặp lại bước 2.
```

Khi đó ta có mã giả cho thuật toán như sau:

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

# Chứng minh thuật toán

Hiểu cơ bản ý tưởng của thuật toán rồi, nhưng hãy đặt câu hỏi, tại sao thuật toán này hoạt động? Ta sẽ chứng minh tính đúng đắn của thuật toán này. Hãy tham khảo cách chứng minh dưới đây:

**Định lý:** Khi thuật toán Dijsktra kết thúc, $dist[v]$ lưu độ dài chính xác đường đi ngắn nhất từ đỉnh $s$ tới đỉnh $v$.

**Chứng minh:**

Gọi Ký hiệu $SP(s, v)$ là độ dài của đường đi ngắn nhất từ $s$ đến $v$ trong đồ thị $G$. Ta sẽ thực hiện **chứng minh bằng phản chứng**:

Định nghĩa hàm $UPDATE()$ như sau: $UPDATE(u, v): dist[v] ← min\{dist[v],dist[u]+w(u, v)\}$.

Giả sử rằng tồn tại ít nhất một đỉnh $v$ sao cho $dist[v]> SP(s, v)$ khi $v$ được xóa khỏi hàng đợi ưu tiên $Q$. Cụ thể, gọi $f$ là đỉnh đầu tiên được xóa khỏi $Q$ có tính chất trên. Khi đó, $P_f = \langle s = u_1, u_2, ..., u_h = f \rangle$ là chuỗi các đỉnh trên đường đi ngắn nhất từ $​​s$ đến $f$, trong đó $h$ là số đỉnh trên đường đi ngắn nhất này.

Xét vòng lặp while mà ta dequeue $f$ từ $Q$. Coi một đỉnh $v$ được đánh dấu nếu tại thời điểm này $v$ đã bị xóa khỏi $Q$. Gọi $u_k$ là đỉnh đầu tiên trong $P_f$ không được đánh dấu, tức là mọi đỉnh trong đường dẫn con $\langle h_s, u_2, ..., u_{k − 1} \rangle$ được đánh dấu và do đó đã bị xóa khỏi $Q$.

Trong phần còn lại của chứng minh, ta sử dụng hai dữ kiện quan trọng sau:

**Dữ kiện 1:** _Vì $f$ là đỉnh đầu tiên bị xóa khỏi $Q$ nên tại thời điểm loại bỏ nó (ở cuối thuật toán), ta có $SP (s, f) <dist[f]$, theo đó $SP(s, u_i) = dist[u_i]$ với mọi $i <k$. Nói cách khác, vì tất cả các đỉnh trong đường dẫn con $\langle h_s, u_2, ..., u_{k − 1} \rangle$ đã bị xóa khỏi $Q$ trước $f$, mỗi đỉnh này phải được tính đúng các giá trị $dist[·]$._

**Dữ kiện 2:** _Với bất kỳ $1 ≤ i ≤ j ≤ h$, đường dẫn con $\langle h_s, u_2, ..., u_{k − 1} \rangle$ của $P_f$ phải là đường đi ngắn nhất từ ​​$u_i$ đến $u_j$ (nếu không, ta có thể thay thế đường dẫn con này trong $P_f$ bằng một đường dẫn ngắn hơn và kết quả thu được một đường đi ngắn hơn từ $s$ đến $f$)._

Sử dụng hai dữ kiện này, ta có hai trường hợp dựa trên giá trị của $k$:

- Trường hợp 1: $k = h$, và do đó $f$ là đỉnh không được đánh dấu đầu tiên trong đường đi. Do đó, $u_{h-1}$ được đánh dấu và bị xóa khỏi $Q$. Theo dữ kiện 1, ta biết rằng $dist[u_{h − 1}] = SP (s, u_{h−1})$, tức là đỉnh ngay trước $f$ trong $P_f$ chứa giá trị d [·] đúng. Do đó, sau khi ta gọi $UPDATE(u_{h-1}, f)$ trên lần lặp tại vị trí ta xóa $u_{k-1}$ khỏi $Q$, $dist[f]$ được đặt không lớn hơn $SP (s, u_{h − 1}) + w(u_{h−1}, f)$. Tuy nhiên, vì theo định nghĩa $P_f$ là đường đi ngắn nhất từ $s$ tới $f$, hay $SP(s, u_{h − 1}) + w (u_{h − 1}, f) = SP (s, f)$. Do đó, khi ta gọi hàm $UPDATE (u_{k-1}, f)$, trên thực tế, ta đã lưu trữ $SP (s, f)$ tại $dist[f]$. Đây là một mâu thuẫn vì ban đầu ta giả định rằng thuật toán sẽ kết thúc với $dist[f]$ lưu trữ một giá trị lớn hơn độ dài của đường đi ngắn nhất từ $s$ đến $f$.

- Trường hợp 2: $k<h$, do đó $u_k \neq f$ là một đỉnh không được đánh dấu trên $P_f$ chưa bị xóa khỏi hàng đợi ưu tiên $Q$ trước lần lặp này. Tuy nhiên, vì $u_k$ là đỉnh không bị đánh dấu đầu tiên dọc theo đường đi, ta biết rằng $u_{k-1}$ đã bị xóa khỏi $Q$, và vì vậy theo dữ kiện 1, ta được $dist[u_{k-1}] = SP (s, u_{k-1})$. Bây giờ, hãy quan sát rằng ở lần lặp mà ta đã xóa $u_{k-1}$ khỏi $Q$, gọi hàm $UPDATE (u_{k-1}, u_k)$, hay $dist[u_k] \le dist[u_{k-1}] + w(u_{k-1}, u_k)$, ta có:

$dist[u_k] ≤ dist[u_{k−1}] +w(u_{k−1},u_k)$ (vì ta gọi hàm $UPDATE(u_{k−1},u_k)$)

$d= SP(s,u_{k−1}) +w(u_{k−1},u_k)$ (sử dụng dữ kiện 1: $u_{k-1}$ được đánh dấu và $k−1 < k$)

$= SP(s,u_k)$ (dữ kiện 2: $\langle s,...,u_k\rangle$ là đường đi con của $P_f$)

$< SP(s, f)$ (vì cạnh có trọng số dương)

$< dist[f]$ (giả thiết ban đầu)

Ta đã chỉ ra rằng từ bất đẳng thức thứ hai đến bất đẳng thức cuối là sử dụng giả thuyết cạnh có trọng số dương — bởi vì phải có ít nhất một cạnh nữa trong đường đi sau $u_k$, đường đi ngắn nhất từ $s$ đến $u_k$ phải nhỏ hơn đường đi ngắn nhất từ $s$ đến $f$. Trên thực tế, thuật toán Dijkstra không chính xác khi các cạnh có trọng số âm tồn tại trong đồ thị.

Vậy $u_k$ là một đỉnh vẫn nằm trong $Q$, và ta đang dequeue đỉnh $f$ mặc dù bất đẳng thức trên chỉ ra rằng $dist[u_k]<dist[f]$. Đây là mâu thuẫn. Vậy điều giả sử sai. Ta có điều phải chứng minh.

# Cài đặt

**Code**:

```C
#include <stdio.h>
#include <vector>
#include <queue>
#include <algorithm>
using namespace std;

const int oo = 9999999; // Đánh dấu là vô cực
typedef pair<int, int> ii;
int pre[1812];
int graph[14][14];
vector<int>path[1812]; //Lưu đường đi tới đỉnh i
vector<ii> a[1812];
int n, m;

int d[1812];

void dijkstra(int source) {
    priority_queue<ii, vector<ii>, greater<ii>> pq; //Hàng đợi ưu tiên, giá trị second bé nhất cho lên đầu
    for (int i = 1; i <= n; i++)
        d[i] = oo; //gan gia tri d[i] bang vo cuc
    d[source] = 0;
    pq.push(ii(0, source));
    while (pq.size()) {
        int u = pq.top().second; //Lấy giá trị second của phần tử đỉnh của pq
        int du = pq.top().first;
        pq.pop();
        if (du != d[u]){ //Điều kiện để bỏ qua pair mà giá trị d[u] được cập nhật từ lần lặp trước.
        	continue;
	}
        for (int i = 0; i < a[u].size(); i++) { //Xét đỉnh kề đỉnh u
            int v = a[u][i].second;
            int uv = a[u][i].first;
            if (d[v] > du + uv) { //Nếu tổng của đỉnh đang xét + trọng số của cạnh nối 2 đỉnh u và v nhỏ hơn thì cập nhật d[v] mới
            	pre[v] = u; // Đỉnh trước v là đỉnh u
                d[v] = du + uv; // Lấy giá trị nhỏ hơn
                pq.push(ii(d[v], v)); // Thêm pair vào pq
            }
        }
    }
}

int main() {
     int p, q, w, source;
    //printf("Nhap dinh nguon: ");
    scanf("%d", &source);
    //printf("Nhap so dinh: ");
    scanf("%d", &n);
    for(int i = 1; i <= n; i++){
    	for(int j = 1; j <= n; j++){
    		scanf("%d", &graph[i][j]);
    		if(graph[i][j] != 0 && graph[i][j] != INT_MAX){
    			a[i].push_back(ii(graph[i][j], j));
    		}
    	}
    }
    dijkstra(source);
    for (int i = 1; i <= n; i++){
    	if(i == source) continue;
    	printf("=== Dinh %d\n", i);
    	if(d[i] == oo ){
    		printf("khong co duong di tu nguon toi dinh nay \n");
    		continue;
	}
        printf("d( %d -> %d ) = %d\n", source, i, d[i]);
	for(int tmp = i; tmp != source; tmp = pre[tmp]){
		path[i].push_back(tmp);
	}
	path[i].push_back(source);
	reverse(path[i].begin(),path[i].end());
	printf("Duong di: ");
	for(int j = 0; j < path[i].size(); j++){
		if(j == path[i].size()-1){
			printf("%d", path[i][j]);
			break;
		}
		else printf("%d -> ", path[i][j]);
	}
	printf("\n");
    }
    return 0;
}
```

Độ phức tạp thời gian $O(|E|.log|V|)$ với $|E|$ là số đỉnh và $|V|$ là số cạnh

# Ứng dụng thực tế của thuật toán Dijsktra

Một số ứng dụng của thuật toán Dijsktra trong thực tế:

- Tìm đường đi ngắn nhất trên bản đồ.
- Ứng dụng trong mạng xã hội.
- Ứng dụng trong hệ thống thông tin di động
- Ứng dụng trong hàng không

# Tổng kết

Vậy trong bài viết vừa rồi, ta đã tìm hiểu các nội dung trong thuật toán Dijsktra. Thuật toán Dijsktra được áp dụng rất nhiều trong các cuộc thi lập trình. Bên cạnh đó, có thêm một số các thuật toán tìm đường đi ngắn nhất khác, chúng ta sẽ bàn luận trong bài viết sau.

# Tài liệu tham khảo

1. Giải thuật và lập trình - Thầy Lê Minh Hoàng
2. [cp-algorithms.com](https://cp-algorithms.com/)
3. Handbook Competitive Programming - Antti Laaksonen
4. Competitve programming 3 - Steven Halim, Felix Halim
5. courses.cs.duke.edu
