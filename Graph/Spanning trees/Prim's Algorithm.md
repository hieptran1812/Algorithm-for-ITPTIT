# Thuật toán Prim

## Tổng quan

Trong khoa học máy tính, thuật toán Prim là một thuật toán tham lam để tìm cây bao trùm nhỏ nhất của một đồ thị vô hướng có trọng số liên thông. Nghĩa là nó tìm một tập hợp các cạnh của đồ thị tạo thành một cây chứa tất cả các đỉnh, sao cho tổng trọng số các cạnh của cây là nhỏ nhất. Thuật toán được tìm ra năm 1930 bởi nhà toán học người Séc Vojtěch Jarník và sau đó bởi nhà nghiên cứu khoa học máy tính Robert C. Prim năm 1957 và một lần nữa độc lập bởi Edsger Dijkstra năm 1959. 
Do đó nó còn được gọi là **thuật toán DJP**, **thuật toán Jarník**, hay **thuật toán Prim–Jarník**.

## Kĩ thuật

### Đặt vấn đề



### Ý tưởng thuật toán

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/prim1.PNG"></p>

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/prim2.PNG"></p>

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/prim3.PNG"></p>

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/prim4.PNG"></p>

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/prim5.PNG"></p>


### Cài đặt

**Mã giả**:

```

```

**Code**:

```C++
#include <bits/stdc++.h>
using namespace std;

#define INF 9999999
#define V 5

int G[V][V] = {
  {0, 9, 75, 0, 0},
  {9, 0, 95, 19, 42},
  {75, 95, 0, 51, 66},
  {0, 19, 51, 0, 31},
  {0, 42, 66, 31, 0}};

int main() {
  int no_edge;  // number of edge
  int selected[V];

  // set selected false initially
  memset(selected, false, sizeof(selected));

  // set number of edge to 0
  no_edge = 0;

  // the number of egde in minimum spanning tree will be
  // always less than (V -1), where V is number of vertices in
  //graph

  // choose 0th vertex and make it true
  selected[0] = true;

  int x;  //  row number
  int y;  //  col number

  // print for edge and weight
  cout << "Edge"
     << " : "
     << "Weight";
  cout << endl;
  while (no_edge < V - 1) {
    //For every vertex in the set S, find the all adjacent vertices
    // , calculate the distance from the vertex selected at step 1.
    // if the vertex is already in the set S, discard it otherwise
    //choose another vertex nearest to selected vertex  at step 1.

    int min = INF;
    x = 0;
    y = 0;

    for (int i = 0; i < V; i++) {
      if (selected[i]) {
        for (int j = 0; j < V; j++) {
          if (!selected[j] && G[i][j]) {  // not in selected and there is an edge
            if (min > G[i][j]) {
              min = G[i][j];
              x = i;
              y = j;
            }
          }
        }
      }
    }
    cout << x << " - " << y << " :  " << G[x][y];
    cout << endl;
    selected[y] = true;
    no_edge++;
  }

  return 0;
}
```

### Độ phức tạp

## Ví dụ

## Let's practice

## Tham khảo
1. [kc97ble](https://sites.google.com/site/kc97ble/algorithm-graph/prim---tim-cay-khung-nho-nhat/prim-cpp)
2. [cp-algorithms.com](https://cp-algorithms.com/graph/mst_prim.html#toc-tgt-5)
3. [wikipedia.org](https://vi.wikipedia.org/wiki/Thu%E1%BA%ADt_to%C3%A1n_Prim)
4. Competitve Programming's handbook
5. Giải thuật và lập trình - Thầy Lê Minh Hoàng
