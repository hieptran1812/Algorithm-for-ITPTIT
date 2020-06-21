# Thuật toán quay lui

## Tổng quan

Thuật toán quay lui dùng để giải bài toán liệt kê các cấu hình. Mỗi cấu hình được xây dựng bằng cách xây dựng từng phần tử, mỗi phần tử được chọn bằng cách thử tất cả các khả năng. Cấu hình ở đây ta có thể hiểu là **các cách sắp xếp một tập các phần tử** (liệt kê hoán vị) hoặc **các cách xây dựng một tập phần tử từ tập phần tử cho trước** (xây dựng tập con). Trong những tình huống khác, bài toán có thể yêu cầu liệt kê các cây khung (spanning trees) của đồ thị. Liệt kê các đường đi có thể giữa hai đỉnh. Các cách tô màu các đỉnh của đồ thị sao cho hai đỉnh kề khác màu nhau,... (đây là các bài toán mình sẽ giới thiệu ở phần đồ thị nha).

<p align = "center"><img src = "https://ds055uzetaobb.cloudfront.net/brioche/uploads/jcGB2lJnfX-cubic_sudoku_portal1.png?width=1200"></p>

## Kĩ thuật

Điểm chung của các bài toán có thể áp dụng quay lui để giải là ta phải tạo ra một cấu hình **chính xác một lần**, tránh liệt kê cấu hình bị lặp và bị thiếu. Điều đó đồng nghĩa với việc ta phải tạo ra một cách liệt kê **trật tự và có hệ thống**. 

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

### Bài toán 8 quân hậu

**Đề bài**: Nhiệm vụ của bạn là liệt kê các cách xếp 8 quân hậu lên bàn cờ sao cho chúng không chiếu nhau. (Các bạn biết chơi cờ chứ :>)

<p align = "center"><img src = "https://upload.wikimedia.org/wikipedia/commons/1/1f/Eight-queens-animation.gif"></p>

**Ý tưởng**:

Các quân hậu sẽ chiếu nhau nếu chúng cùng nằm trên hàng ngang hoặc hàng dọc hoặc đường chéo. Có rất nhiều cách tiếp cận bài toán này nhưng tớ sẽ sử dụng hướng quay lui để giải nha :))

```
1) Bắt đầu ở cột ngoài cùng bên trái.

2) Nếu tất cả quân hậu được đặt -> return true.

3) Thử tất cả các hàng trong cột hiện tại. Làm các bước dưới đây cho mỗi hàng đã duyệt. 
a) Nếu quân hậu có thể được đặt an toàn trong hàng này thì đánh dấu [hàng, cột] này là một phần của giải pháp và đệ quy tới các quân hậu tiếp theo.
b) Nếu đặt quân hậu vào [hàng, cột] dẫn đến một giải pháp thì return true. 
c) Nếu việc đặt quân hậu không dẫn đến một giải pháp thì bỏ đánh dấu [hàng, cột] (Backtrack) này và đi đến bước (a) để thử các hàng khác. 

3) Nếu tất cả các hàng đã được thử và không tìm được vị trí đặt quân hậu, return false để kích hoạt quay lui.

```

**Code**:

```C

#include<bits/stdc++.h>
#define N 4 //Kích thước bàn cờ
  
/* Hàm in Solution */
void printSolution(int board[N][N]) 
{ 
    for (int i = 0; i < N; i++) { 
        for (int j = 0; j < N; j++) 
            printf(" %d ", board[i][j]); 
        printf("\n"); 
    } 
} 
  
/* Hàm kiểm tra vị trí quân hậu mới có bị chiếu không */
bool isSafe(int board[N][N], int row, int col) 
{ 
    int i, j; 
  
    /* check hàng hiện tại ở bên trái */
    for (i = 0; i < col; i++) 
        if (board[row][i]) 
            return false; 
  
    /* check đường chéo trên */
    for (i = row, j = col; i >= 0 && j >= 0; i--, j--) 
        if (board[i][j]) 
            return false; 
  
    /* check đường chéo dưới */
    for (i = row, j = col; j >= 0 && i < N; i++, j--) 
        if (board[i][j]) 
            return false; 
  
    return true; 
} 
  
/* Hàm đệ quy giải bài toán quân hậu */
bool solveNQUtil(int board[N][N], int col) 
{ 
    /* nếu tất cả các cột đều đã duyệt (hay tất cả quân hậu đều được đặt */
    if (col >= N) 
        return true; 
  
    /* Xét cột hiện tại bằng cách duyệt hết các hàng */
    for (int i = 0; i < N; i++) { 
        /* Nếu quân hậu đặt ở vị trí board[i][col] */
        if (isSafe(board, i, col)) { 
            /* Đặt quân hậu ở vị trí board[i][col] */
            board[i][col] = 1; 
  
            /* Đệ quy để đặt tiếp các quân hậu ở cột khác */
            if (solveNQUtil(board, col + 1)) 
                return true; 
  
            /* Nếu đặt quân hậu ở vị trí board[i][col] 
              	không giúp ta tìm ra được giải pháp (không thể đặt được vị trí quân hậu tiếp theo) */
            board[i][col] = 0; // BACKTRACK 
        } 
    } 
  
    /* Nếu không tìm được vị trí đặt hậu phù hợp thì return false */
    return false; 
} 
  
bool solveNQ() 
{ 
    int board[N][N] = { { 0, 0, 0, 0 }, 
                        { 0, 0, 0, 0 }, 
                        { 0, 0, 0, 0 }, 
                        { 0, 0, 0, 0 } }; 
  
    if (solveNQUtil(board, 0) == false) { 
        printf("Solution does not exist"); 
        return false; 
    } 
  
    printSolution(board); 
    return true; 
} 
  
int main() 
{ 
    solveNQ(); 
    return 0; 
} 

```
Một cách khác (cách này theo hướng và vấn đề khác cách trên nha):

```C

#include<bits/stdc++.h>
int a[20];
bool Ok(int x2,int y2){
    //kiểm tra cách đặt có thỏa mãn không
    for(int i = 1; i < x2 ;i++)
        if(a[i] == y2 || abs(i-x2) == abs(a[i] - y2) )
            return false;
    //Nếu kiểm tra hết các trường hợp vẫn không sai thì trả về true
    return true;
}
 
void Xuat(int n){
    //in ra một kết quả
    for(int i=1;i<=n;i++)
        printf(" %d",a[i]);
    printf("\n");
}
 
void Try(int i,int n){
    for(int j = 1;j<=n;j++){
        // thử đặt quân hậu vào các cột từ 1 đến n
        if(Ok(i,j)){
            //nếu cách đặt này thỏa mãn thì lưu lại vị trí
            a[i] = j;
            //nếu đặt xong quân hậu thứ n thì xuất ra một kết quả
            if(i==n) Xuat(n);
            Try(i+1,n);
        }
    }
}
 
int main(){
    int n = 8;// bài toán là 8 quân hậu trên bàn 8*8
    Try(1,n);
    return 0;
}

```

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
4. [www.geeksforgeeks.org](https://www.geeksforgeeks.org/n-queen-problem-backtracking-3/)
5. [nguyenvanhieu.vn](https://nguyenvanhieu.vn/bai-toan-xep-hau/)
