# Thuật toán Depth-first search

## Tổng quan

Tìm kiếm ưu tiên chiều sâu hay tìm kiếm theo chiều sâu (tiếng Anh: Depth-first search - DFS) là một thuật toán duyệt hoặc tìm kiếm trên một cây hoặc một đồ thị. Thuật toán khởi đầu tại gốc (hoặc chọn một đỉnh nào đó coi như gốc) và phát triển xa nhất có thể theo mỗi nhánh.

Thông thường, DFS là một dạng tìm kiếm thông tin không đầy đủ mà quá trình tìm kiếm được phát triển tới đỉnh con đầu tiên của nút đang tìm kiếm cho tới khi gặp được đỉnh cần tìm hoặc tới một nút không có con. Khi đó giải thuật quay lui về đỉnh vừa mới tìm kiếm ở bước trước. Trong dạng không đệ quy, tất cả các đỉnh chờ được phát triển được bổ sung vào một ngăn xếp LIFO.

<p align = "center"><img src = "https://miro.medium.com/max/1280/0*miG6xdyYzdvrB67S.gif"></p>

## Kĩ thuật

### Đặt vấn đề

Thực hiện thuật toán DFS.

### Mô tả thuật toán

<p align = "center"><img src = "https://he-s3.s3.amazonaws.com/media/uploads/9fa1119.jpg"></p>

Thuật toán bắt đầu bằng việc push đỉnh nguồn 1 vào stack và đánh dấu đỉnh 1 đã được duyệt.

**Lần lặp 1**:

* Đỉnh 1 được pop khỏi stack.
* Bắt đầu duyệt tới đỉnh kề với đỉnh 1 là đỉnh 2 và đỉnh 3.
* Đỉnh 2 và 3 đã được duyệt qua, push đỉnh 2 và 3 vào stack và được đánh dấu là đã duyệt.

**Lần lặp 2**:

* Đỉnh 3 được pop khỏi stack.

**Lần lặp 3**:

* Đỉnh 2 được pop khỏi stack.
* Đỉnh kề của 2 là đỉnh 4 và đỉnh 5. Duyệt qua 2 đỉnh này, push vào stack và đánh dấu là đã được duyệt.

**Lần lặp 4**:

* Đỉnh 5 được pop khỏi stack.
* Đỉnh kề của 5 là 2. Nhưng không cần duyệt đỉnh 2 vì đỉnh 2 đã được đánh dấu là duyệt rồi.

**Lần lặp 5**:

* Đỉnh 4 được pop khỏi stack.
* Đỉnh kề của 4 là 2. Nhưng không cần duyệt đỉnh 2 vì đỉnh 2 đã được đánh dấu là duyệt rồi.

Sau những lần lặp trên, stack rỗng, kết thúc vòng lặp và tất cả các đỉnh đã được duyệt.

### Chứng minh thuật toán

Coming soon!

### Cài đặt

**Mã giả**:
```
DFS-iterative (G, s):   //Đồ thị G và đỉnh nguồn s
      let S be stack
      S.push( s )       //Thêm s vào stack
      mark s as visited.
      while ( S is not empty):
         //Pop a vertex from stack to visit next
         v = S.top()
         S.pop()
         //Push all the neighbours of v in stack that are not visited   
         for all neighbours w of v in Graph G:
            if w is not visited :
               S.push(w)         
               mark w as visited
```

**Code**:
```C++
#include<bits/stdc++.h>
using namespace std;

bool visited[1812]; // Danh dau dinh da duyet
vector<int>adj[1812]; // Luu dinh ke
int n, m; // So dinh va so canh

//Do thi khong trong so, tim thanh phan lien thong

void DFS(int source){
	stack<int>s;
	memset(visited, false, sizeof visited);
	s.push(source);
	visited[source] = true;
	while(!s.empty()){
		int u = s.top(); s.pop();
		cout << u << " ";
		for(int i = 0; i < adj[u].size(); i++){
			if(!visited[adj[u][i]]){
				s.push(adj[u][i]);
				visited[adj[u][i]] = true;
			}
		}
	}	
}
main(){
	cin >> n >> m;
	for(int i = 1; i <= m; i++){
		int x, y;
		cin >> x >> y;
		adj[x].push_back(y); adj[x].push_back(y);
	}
	int solt = 0;
	for(int i = 1; i <= n; i++){
		if(!visited[i]){
			solt++;
			cout << "Thanh phan lien thong thu " << solt << ": ";
			DFS(i);
			cout << endl;
		}
	}
}
```

### Độ phức tạp

**Không gian**

Độ phức tạp không gian O(|V|) nếu duyệt toàn bộ đồ thị, mỗi đỉnh qua đúng một lần.

**Thời gian**

Độ phức tạp thời gian O(|E|+|V|) khi cài đặt sử dụng danh sách kề.

## Ví dụ

Các bạn xem ví dụ trên nha :D

## Ứng dụng

Nhiều giải thuật sử dụng tìm kiếm theo chiều sâu:

* Xác định các thành phần liên thông của đồ thị
* Sắp xếp tô-pô cho đồ thị
* Xác định các thành phần liên thông mạnh của đồ thị có hướng
* Kiểm tra một đồ thị có phải là đồ thị phẳng hay không

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
1. [Wikipedia.org](https://vi.wikipedia.org/wiki/T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_s%C3%A2u)
2. [www.hackerearth.com](https://www.hackerearth.com/practice/algorithms/graphs/depth-first-search/tutorial/)
3. [cp-algorithms.com](https://cp-algorithms.com/graph/depth-first-search.html)

