# Thuật toán Fleury

## Tổng quan


### Đặt vấn đề

Giả sử đồ thị tồn tại chu trình Euler, tìm chu trình đó. 

### Mô tả thuật toán 

Xuất phát từ một đỉnh, ta chọn một cạnh liên thuộc với nó để đi tiếp theo hai nguyên tắc sau:
* Xóa bỏ cạnh đã đi qua.
* Chỉ đi qua cầu khi không còn cạnh nào khác để chọn.

Ta cứ chọn cạnh đi như vậy cho tới khi không đi tiếp được nữa, đường đi tìm được là chu trình Euler.

<p align = "center"><img src = "https://www.tutorialspoint.com/assets/questions/media/28707/fleurys_algorithm.jpg">

Cho đồ thị như trên:
1. Xuất phát từ đỉnh 2, ta có 3 cách đi tiếp là (2,0), (2,1), (2,3). Chọn cạnh (2,0) hoặc (2,1) vì (2,3) là cạnh cầu.
2. Giả sử đi theo cạnh (2,0), ta xóa cạnh (2,0) và hiện tại đang ở đỉnh 0.
3. Từ đỉnh 0 chỉ có một cạnh duy nhất để đi tiếp là (0,1), đi theo cạnh (0,1) và xóa cạnh (0,1).
4. Từ đỉnh 1 chỉ có một cạnh duy nhất để đi tiếp là (1,2), đi theo cạnh (1,2) và xóa cạnh (1,2).
5. Từ đỉnh 2 chỉ có một cạnh duy nhất để đi tiếp là (2,3), đi theo cạnh (2,3) và xóa cạnh (2,3).
6. Tất cả các cạnh đã được xóa, ta tìm được chu trình Euler 2 - 0 - 1 - 3.

Ở bước 1 nếu đi theo (2,1) ta vẫn tìm được chu trình.

### Tính đúng đắn của thuật toán

Coming soon!

### Code

**Thuật toán Fleury** tìm chu trình hoặc đường đi Euler

```Mã giả
findStartVert(graph)
Input: The given graph.
Output: Find the starting vertex to start algorithm.
Begin
   for all vertex i, in the graph, do
      deg := 0
      for all vertex j, which are adjacent with i, do
         deg := deg + 1
      done
      if deg is odd, then
         return i
      done
      when all degree is even return 0
End
isBridge(u, v)
Input: The start and end node.
Output: True when u and v are forming a bridge.
Begin
   deg := 0
   for all vertex i which are adjacent with v, do
      deg := deg + 1
   done
   if deg > 1, then
      return false
   return true
End
fleuryAlgorithm(start)
Input: The starting vertex.
Output: Display the Euler path or circuit.
Begin
   edge := get the number of edges in the graph //it will not initialize in next
   recursion call
   for all vertex v, which are adjacent with start, do
      if edge <= 1 OR isBridge(start, v) is false, then
         display path from start and v
         remove edge (start,v) from the graph
         decrease edge by 1
         fleuryAlgorithm(v)
   done
End
```

```C++
#include<iostream>
#include<vector>
#define NODE 5
using namespace std;
int graph[NODE][NODE] = {{0, 1, 1, 1, 1},
   {1, 0, 1, 1, 0},
   {1, 1, 0, 1, 0},
   {1, 1, 1, 0, 1},
   {1, 0, 0, 1, 0}
};
int tempGraph[NODE][NODE];

int findStartVert(){
   for(int i = 0; i<NODE; i++){
      int deg = 0;
      for(int j = 0; j<NODE; j++){
         if(tempGraph[i][j]) deg++; //increase degree, when connected edge found
      }
      if(deg % 2 != 0) //when degree of vertices are odd
      return i; //i is node with odd degree
   }
   return 0; //when all vertices have even degree, start from 0
}

bool isBridge(int u, int v){
   int deg = 0;
   for(int i = 0; i<NODE; i++)
      if(tempGraph[v][i]) deg++;
      if(deg>1) return false; //the edge is not forming bridge
   return true; //edge forming a bridge
}

int edgeCount(){
   int count = 0;
   for(int i = 0; i<NODE; i++)
      for(int j = i; j<NODE; j++)
         if(tempGraph[i][j])
            count++;
   return count; //count nunber of edges in the graph
}

void fleuryAlgorithm(int start){
   static int edge = edgeCount();
   for(int v = 0; v<NODE; v++){
      if(tempGraph[start][v]){ //when (u,v) edge is presnt and not forming bridge
         if(edge <= 1 || !isBridge(start, v)){
            cout << start << "--" << v << " ";
            tempGraph[start][v] = tempGraph[v][start] = 0; //remove edge from graph
            edge--; //reduce edge
            fleuryAlgorithm(v);
         }
      }
   }
}

int main(){
   for(int i = 0; i<NODE; i++) //copy main graph to tempGraph
    for(int j = 0; j<NODE; j++)
      tempGraph[i][j] = graph[i][j];
   cout << "Euler Path Or Circuit: ";
   fleuryAlgorithm(findStartVert());
}
```

### Độ phức tạp

Độ phức tạp thời gian trung bình: O(|E|<sup>2</sup>)

## Let's practice
1.
2.
3.
4.
5.
6.
7.
8.

## Tham khảo
1. [tutorialspoint.com](https://www.tutorialspoint.com/fleury-s-algorithm-for-printing-eulerian-path-or-circuit-in-cplusplus#:~:text=Fleury's%20Algorithm%20is%20used%20to,by%20removing%20the%20previous%20vertices.)
