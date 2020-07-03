# Thuật toán Floyd-Warshall

## Tổng quan

Khi nhắc đến thuật toán để tìm đường đi ngắn nhất trong đồ thị, người ta sẽ thường nghĩ tới những thuật toán dễ tiếp cận và có thể chạy trong giới hạn cho phép như Breadth First Search, Dijkstra hay Bellman-Ford. Tuy nhiên, ba thuật toán trên đều chỉ có thể tìm được đường đi ngắn nhất từ một đỉnh nguồn nhất định đến các đỉnh khác và do đó, trong một số trường hợp cụ thể cần chỉ ra đường đi ngắn nhất của mọi cặp đỉnh trong đồ thị, các thuật toán này sẽ hoạt động chưa hiệu quả khi phải chạy lặp đi lặp lại khá nhiều thao tác.
Thuật toán Floyd-Warshall sẽ giúp chúng ta giải quyết vấn đề này chỉ trong một lần chạy duy nhất. Hơn thế nữa, cách tiếp cận và cài đặt của nó cũng khá đơn giản và quen thuộc.

Thuật toán Floyd-Warshall còn được gọi là thuật toán Floyd được Robert Floyd tìm ra năm 1962 là thuật toán để tìm đường đi ngắn nhất giữa mọi cặp đỉnh. 
Floyd hoạt động được trên đồ thị có hướng, có thể có trọng số âm, tuy nhiên không có chu trình âm. Ngoài ra, Floyd còn có thể được dùng để phát hiện chu trình âm.

## Kĩ thuật

### Đặt vấn đề

Cho đồ thị vô hướng sau:

<p align = "center"><img src = "https://thuytrangcoding.files.wordpress.com/2018/03/cses-fi-floyd1.png"></p>

Tìm đường đi ngắn nhất giữa các cặp đỉnh trong đồ thị trên.

### Ý tưởng thuật toán

Khởi tạo ma trận khoảng cách ban đầu, ta được:

<p align = "center"><img src = "https://thuytrangcoding.files.wordpress.com/2018/03/cses-fi-floyd2.png"></p>

Quá trình thuật toán diễn ra như sau:

```
Chọn lần lượt từng đỉnh của đồ thị làm đỉnh trung gian (ta quy ước là K).
Chọn một cặp 2 đỉnh phân biệt và không trùng với đỉnh trung gian (ta quy ước lần lượt là I và J).

Thực hiện so sánh như ở trên: đường đi ngắn nhất giữa I và J sẽ bằng giá trị nhỏ nhất của một trong hai giá trị sau:
* Giá trị đường đi ngắn nhất hiện thời giữa I và J.
* Tổng của giá trị đường đi ngắn nhất hiện thời giữa I và K, và đường đi ngắn nhất hiện thời giữa K và J.
```

Đầu tiên, K = 1. Nhờ đỉnh 1 làm trung gian, ta thấy xuất hiện đường đi từ đỉnh 2 tới đỉnh 4 (độ dài 14), và từ đỉnh 2 tới đỉnh 5 (độ dài 6).
Đường đi trung gian qua đỉnh 1 để đi từ đỉnh 4 tới đỉnh 5 không tối ưu về chiều dài (9 + 1 > 2) nên ta không cập nhật lại đường đi ngắn nhất giữa 2 đỉnh 4 và 5.

Mảng lúc này trở thành:

<p align = "center"><img src = "https://thuytrangcoding.files.wordpress.com/2018/03/cses-fi-floyd3.png"></p>

Tiếp theo, ta duyệt tới K = 2.
Đường đi từ 3 tới 1 (độ dài 7), từ 3 tới 5 (độ dài 8) được hình thành.
Đường đi từ 3 tới 4 không cập nhật độ dài (7 < 2 + 5 + 9).

<p align = "center"><img src = "https://thuytrangcoding.files.wordpress.com/2018/03/cses-fi-floyd4.png"></p>

Cứ tiếp tục lựa chọn K như vậy cho tới hết, ta sẽ thu được mảng 2D hoàn chỉnh:

<p align = "center"><img src = "https://thuytrangcoding.files.wordpress.com/2018/03/cses-fi-floyd5.png"></p>

Giả sử, qua mảng này, ta thấy đường đi ngắn nhất từ đỉnh 2 tới đỉnh 4 có độ dài 8. Dựa theo đồ thị thì nó là đoạn đường sau:

<p align = "center"><img src = "https://thuytrangcoding.files.wordpress.com/2018/03/cses-fi-floyd6.png"></p>

### Chứng minh thuật toán

Coming soon!

### Cài đặt

**Code**:
```C++
// Author: Tran Quang Hiep - B18DCAT080

#include <bits/stdc++.h>
using namespace std;
const int oo = 99999;
int a[1812][1812];
int n, m;
int next1[100][100];
int graph[100][100];

int main() {
    cin >> n;
//    for (int i = 1; i <= m; i++) { // Nhap theo danh sach canh
//        int p, q, w;
//        cin >> p >> q >> w;
//        a[p][q] = a[q][p] = w;
//    }
	memset(next1, INT_MAX, sizeof next1);
	for(int i = 1; i <= n; i++){
		for(int j = 1; j <= n; j++){
			cin >> a[i][j];
			if(a[i][j] != oo && a[i][j] != 0){ // Co duong di giua i va j
				next1[i][j] = j;
			}
		}
	}
    // Bu?c 2: Lap
    for (int k = 1; k <= n; k++)
        for (int i = 1; i <= n; i++)
            for (int j = 1; j <= n; j++){
            	if((a[i][j] >  a[i][k] + a[k][j]) && (a[i][k] != oo) && (a[k][j] != oo)){
            		a[i][j] = a[i][k] + a[k][j];
                	next1[i][j] = next1[i][k];
            	}
            }
    cout << "Ma tran khoang cach: \n";
    for (int i = 1; i <= n; i++){
        for (int j = 1; j <= n; j++){
        	cout << a[i][j] << " ";
    	}
    	cout << endl;
    }
    for(int i = 1; i <= n; i++){
    	for(int j = 1; j <= n; j++){
    		if(a[i][j] == oo){
    			cout << "Khong co duong di tu " << i << " toi " << j << endl;
    			continue;
		}
    		if (i != j){
    			cout << "Duong " << i << " toi " << j <<": ";
    			for(int tmp = i; tmp != j; tmp = next1[tmp][j]){
    				cout << tmp << " ";
			}
			cout << j << endl;
		}
	}
    }
}
```

### Độ phức tạp

Độ phức tạp thời gian O(|V|<sup>3</sup>)

## Ví dụ

Xem code trên :D

## Ứng dụng

Thiết kế đường đi ngắn nhất giúp tiết kiệm nhiên liệu, thời gian, chi phí cho các hãng vận chuyển.

## Let's practice
1. https://codeforces.com/problemset/problem/295/B
2. https://codeforces.com/problemset/problem/339/C
3. https://codeforces.com/problemset/problem/598/D
4. https://codeforces.com/problemset/problem/1249/E
5. https://codeforces.com/problemset/problem/1204/C
6. https://codeforces.com/problemset/problem/1176/E
7. https://codeforces.com/problemset/problem/1320/B
8. https://codeforces.com/problemset/problem/1202/B

## Tham khảo

1. [Wikipedia](https://vi.wikipedia.org/wiki/Thu%E1%BA%ADt_to%C3%A1n_Floyd-Warshall)
2. [https://brilliant.org/](https://brilliant.org/wiki/floyd-warshall-algorithm/)
3. [thuytrangcoding.wordpress.com](https://thuytrangcoding.wordpress.com/2018/03/18/graph-shortestpath-floyd/)
4. [kc97ble](https://sites.google.com/site/kc97ble/algorithm-graph/floyd-cpp)
