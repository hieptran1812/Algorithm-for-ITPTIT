# Thuật toán Breadth-First Search

## Tổng quan

Trong lý thuyết đồ thị, tìm kiếm theo chiều rộng (BFS) là một thuật toán tìm kiếm trong đồ thị trong đó việc tìm kiếm chỉ bao gồm 2 thao tác: (a) cho trước một đỉnh của đồ thị; (b) thêm các đỉnh kề với đỉnh vừa cho vào danh sách có thể hướng tới tiếp theo. Có thể sử dụng thuật toán tìm kiếm theo chiều rộng cho hai mục đích: tìm kiếm đường đi từ một đỉnh gốc cho trước tới một đỉnh đích, và tìm kiếm đường đi từ đỉnh gốc tới tất cả các đỉnh khác. Trong đồ thị không có trọng số, thuật toán tìm kiếm theo chiều rộng luôn tìm ra đường đi ngắn nhất có thể. Thuật toán BFS bắt đầu từ đỉnh gốc và lần lượt nhìn các đỉnh kề với đỉnh gốc. Sau đó, với mỗi đỉnh trong số đó, thuật toán lại lần lượt nhìn trước các đỉnh kề với nó mà chưa được quan sát trước đó và lặp lại. Xem thêm thuật toán tìm kiếm theo chiều sâu, trong đó cũng sử dụng 2 thao tác trên nhưng có trình tự quan sát các đỉnh khác với thuật toán tìm kiếm theo chiều rộng.

<p align = "center"><img src = "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_r%E1%BB%99ng_BFS.gif/465px-T%C3%ACm_ki%E1%BA%BFm_theo_chi%E1%BB%81u_r%E1%BB%99ng_BFS.gif"></p>

## Kĩ thuật

### Đặt vấn đề

Tìm đường đi ngắn nhất từ đỉnh nguồn tới các đỉnh còn lại trên đồ thị không trọng số.

### Mô tả thuật toán

<p align = "center"><img src = "https://he-s3.s3.amazonaws.com/media/uploads/0dbec9e.jpg" height = 1200></p>

Thuật toán bắt đầu bằng việc push đỉnh nguồn s vào hàng đợi và đánh dấu đỉnh s đã được duyệt.

**Lần lặp 1**:

* Đỉnh s được pop khỏi hàng đợi.
* Bắt đầu duyệt tới hai đỉnh kề với đỉnh s là đỉnh 1 và 2.
* Đỉnh 1 và 2 đã được duyệt qua. Hai đỉnh này sẽ được push vào hàng đợi và đánh dấu là đã được duyệt.

**Lần lặp 2**:

* Đỉnh 1 được pop khỏi hàng đợi.
* Đỉnh kề của 1 là 3 bắt đầu được duyệt. Không cần duyệt qua đỉnh s bởi vì s đã được đánh dấu rồi :D.
* Đỉnh 3 đã được duyệt qua. Đỉnh này được push vào hàng đợi và đánh dấu là đã được duyệt.

**Lần lặp 3**:

* Đỉnh 2 được pop khỏi hàng đợi.
* Đỉnh kề của 2 là 3 và 4 bắt đầu được duyệt. Nhưng không cần duyệt đỉnh 3 vì đỉnh 3 đã được đánh dấu là duyệt rồi.
* Đỉnh 4 đã được duyệt qua. Đỉnh này sẽ được push vào hàng đợi và đánh dấu là đã được duyệt.

**Lần lặp 4**:

* Đỉnh 3 được pop khỏi hàng đợi.
* Đỉnh kề của 3 là 1, 2, 5 bắt đầu được duyệt. Đỉnh 1 và 2 được đánh dấu rồi thì bỏ qua.
* Đỉnh 5 đã được duyệt qua. Đỉnh này sẽ được push vào hàng đợi và đánh dấu là đã được duyệt.

**Lần lặp 5**:

* Đỉnh 4 được pop khỏi hàng đợi.
* Đỉnh kề đỉnh 4 là đỉnh 2 đã được duyệt nên bỏ qua.

**Lần lặp 6**:

* Đỉnh 5 được pop khỏi hàng đợi.
* Đỉnh kề đỉnh 5 là đỉnh 3 đã được duyệt nên bỏ qua.

Sau những lần lặp trên, hàng đợi rỗng, kết thúc vòng lặp và tất cả các đỉnh đã được duyệt.

### Chứng minh thuật toán

Coming soon!

### Cài đặt

**Mã giả**:
```
BFS (G, s)      //G là đồ thị và s là đỉnh nguồn
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
#include<bits/stdc++.h>
using namespace std;

bool visited[1812]; // Danh dau dinh da duyet
int pre[1812]; // Luu dinh truoc
vector<int>adj[1812]; // Luu dinh ke
int n, s; // So dinh va dinh nguon
int graph[1812][1812]; // Do thi
int oo = 18121812; // Danh dau la vo cuc
vector<int>path[1812];

//Do thi khong trong so

void BFS(int source){
	queue<int>q;
	memset(visited, false, sizeof visited);
	q.push(source);
	visited[source] = true;
	while(!q.empty()){
		int u = q.front(); q.pop();
		for(int i = 0; i < adj[u].size(); i++){
			if(!visited[adj[u][i]]){
				q.push(adj[u][i]);
				visited[adj[u][i]] = true;
				pre[adj[u][i]] = u;
			}
		}
	}	
}
main(){
	cin >> n >> s;
	memset(pre, oo, sizeof pre);
	for(int i = 1; i <= n; i++){
		for(int j = 1; j <= n; j++){
			cin >> graph[i][j];
			if(i != j && graph[i][j] != 0){ // tao danh sach ke, them vao neu hai dinh khong trung lap va co duong di giua i va j
				adj[i].push_back(j); adj[j].push_back(i);
			}
		}
	}
	BFS(s);
	for(int i = 1; i <= n; i++){
		if(i != s){
			for(int j = i; j != s; j = pre[j]) path[i].push_back(j);
			path[i].push_back(s);
			reverse(path[i].begin(), path[i].end());
			cout << "Duong di tu " << s << " den " << i <<":\n";
			for(int tmp = 0; tmp < path[i].size(); tmp++) cout << path[i][tmp] << " ";
			cout << endl;
		}
		else cout << "Khong co duong di hoac trung dinh tu " << s << " toi " << i << endl;
	}
}
```

### Độ phức tạp

**Không gian**

Nếu V là tập hợp đỉnh của đồ thị và |V| là số đỉnh thì không gian cần dùng của thuật toán là O(|V|).

**Thời gian**

Nếu V và E là tập hợp các đỉnh và cung của đồ thị, thì thời gian thực thi của thuật toán là O(|E|+|V|) vì trong trường hợp xấu nhất, mỗi đỉnh và cung của đồ thị được thăm đúng một lần. Ghi chú: O(|E|+|V|) nằm trong khoảng từ O(|V|) đến O(|V|<sup>2</sup>), tùy theo số cung của đồ thị.

## Ví dụ

Các bạn xem ví dụ trên nha :D

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
