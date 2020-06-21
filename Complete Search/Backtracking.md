# Thuật toán quay lui

## Tổng quan

Thuật toán quay lui dùng để giải bài toán liệt kê các cấu hình. Mỗi cấu hình được xây dựng bằng cách xây dựng từng phần tử, mỗi phần tử được chọn bằng cách thử tất cả các khả năng. Cấu hình ở đây ta có thể hiểu là **các cách sắp xếp một tập các phần tử** (liệt kê hoán vị) hoặc **các cách xây dựng một tập phần tử từ tập phần tử cho trước** (xây dựng tập con). Trong những tình huống khác, bài toán có thể yêu cầu liệt kê các cây khung (spanning trees) của đồ thị. Liệt kê các đường đi có thể giữa hai đỉnh. Các cách tô màu các đỉnh của đồ thị sao cho hai đỉnh kề khác màu nhau,... (đây là các bài toán mình sẽ giới thiệu ở phần đồ thị nha).

<p align = "center"><img src = "https://ds055uzetaobb.cloudfront.net/brioche/uploads/jcGB2lJnfX-cubic_sudoku_portal1.png?width=1200"></p>

## Kĩ thuật

Điểm chung của các bài toán có thể áp dụng quay lui để giải là ta phải tạo ra một cấu hình **chính xác một lần**, tránh liệt kê cấu hình bị lặp và bị thiếu. Điều đó đồng nghĩa với việc ta phải tạo ra một cách **liệt kê trật tự và có hệ thống**. 

Giả thiết cấu hình cần liệt kê có dạng (x<sub>1</sub>, x<sub>2</sub>,... ,x<sub>n</sub>). Khi đó thuật toán quay lui thực hiện qua các bước sau: 
* Xét tất cả các giá trị x<sub>1</sub> có thể nhận, thử cho x<sub>1</sub> nhận lần lượt các giá trị đó. Với mỗi giá trị thử gán cho x<sub>1</sub> ta sẽ:
  * Xét tất cả các giá trị x<sub>2</sub> có thể nhận, lại thử cho x<sub>2</sub> nhận lần lượt các giá trị đó. Với mỗi giá trị thử gán cho x<sub>2</sub> lại tiếp tục xét tất cả các khả năng chọn x<sub>3</sub> ... cứ tiếp tục như vậy cho đến bước n.
  ...
    * Xét tất cả giá trị x<sub>n</sub> có thể nhận, thử cho x<sub>n</sub> nhận lần lượt các giá trị đó, thông báo cấu hình tìm được (x<sub>1</sub>, x<sub>2</sub>,... ,x<sub>n</sub>).
    
Mã giả:

```C++

void Try(int i){
  for(mọi giá trị có thể gán cho x[i]){
    x[i] = j;
    <Đánh dấu đã chọn x[i] nếu cần>;
    if(x[i] là phần tử cuối của cấu hình){
      <Thông báo cấu hình tìm được>;
    }
    else Try(i+1) // gọi đệ quy để chọn tiếp x[i+1]
    <Xóa đánh dấu đã chọn x[i] nếu cần>;
  }
}

```
Thuật toán quay lui bắt đầu bằng lời gọi Try(giá trị ban đầu)

## Ví dụ

### Liệt kê dãy nhị phân có độ dài n

**Đề bài**: Bạn có thể xem lại ở [đây](https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/Complete%20Search/Generation%20method.md)

**Ý tưởng**:

Sử dụng các bước cơ bản của quay lui hoy :))


**Code**:

```C++

#include<bits/stdc++.h>
using namespace std;

int a[100];
void Try(int i, int n){
	for(int j = 0; j <= 1; j++){
		a[i] = j;
		if (i == n-1){
			for (int k = 0; k < n; k++){
				cout << a[k];
			}
			cout << endl;
		}
		else Try(i+1, n);
	}
}

main(){
	int n;
	cin >> n;
	Try(0, n);
}

```

## Ứng dụng



## Let's practice
1. https://codeforces.com/group/FLVn1Sc504/contest/274856/problem/O
2. https://codeforces.com/group/FLVn1Sc504/contest/274809/problem/A
3. https://codeforces.com/group/FLVn1Sc504/contest/274516/problem/O
4. https://codeforces.com/group/FLVn1Sc504/contest/274804/problem/F
5. https://codeforces.com/group/FLVn1Sc504/contest/274811/problem/R
6. https://codeforces.com/group/FLVn1Sc504/contest/274823/problem/K
7. https://codeforces.com/group/FLVn1Sc504/contest/274862/problem/X
8. https://codeforces.com/group/FLVn1Sc504/contest/274823/problem/B
9. https://codeforces.com/group/FLVn1Sc504/contest/274711/problem/A
10. https://codeforces.com/group/FLVn1Sc504/contest/274804/problem/D

## Tham khảo
1. [brilliant.com](https://brilliant.org/wiki/recursive-backtracking/)
2. Handbook Competitve Programming
3. Giải thuật và lập trình - thầy Lê Minh Hoàng
