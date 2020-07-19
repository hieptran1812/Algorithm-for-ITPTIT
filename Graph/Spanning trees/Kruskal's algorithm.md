# Thuật toán Kruskal

## Tổng quan

Thuật toán Kruskal được mô tả bởi Joseph Bernard Kruskal, Jr. năm 1956 dùng để tìm cây khung nhỏ nhất. 

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/kruskal.PNG"></p>

## Kĩ thuật

### Đặt vấn đề



### Ý tưởng thuật toán


### Chứng minh thuật toán

### Cài đặt

**Mã giả**:

```
Bước 1: Sắp xếp các cạnh của đồ thị theo thứ tự trọng số tăng dần.
Bước 2: Khởi tạo T:= Ø
Bước 3: Lần lượt lấy từng cạnh thuộc danh sách đã sắp xếp. Nếu T+{e} không chứa chu trình thì gán T:=T+{e}.
Bước 4: Nếu T đủ n-1 phần tử thì dừng, ngược lại làm tiếp bước 3.
```

**Code**:

```C
#include<bits/stdc++.h>
using namespace std;

int par[181220];
int anc(int p) { //Tim goc cua dinh
    if (par[p] == p)
        return p;
    else
        return par[p] = anc(par[p]); // Đệ quy
}
void join(int p, int q) { par[anc(p)] = anc(q); } // Hop hai goc dinh p và dinh q

typedef pair<int, int> ii;
typedef pair<int, ii> iii;
#define X first
#define Y second
vector<iii> edge;
int n, m;

main() {
    scanf("%d%d", &n, &m);
    for (int i = 1; i <= n; i++)
        par[i] = i;
    while (m--) {
        int p, q, w;
        scanf("%d%d%d", &p, &q, &w);
        edge.push_back(iii(w, ii(p, q)));
    }
    sort(edge.begin(), edge.end()); // Sap xep lai canh theo thu tu tang dan
    vector<iii>::iterator it;
    int r = 0; // Do dai cay khung nho nhat
    for (it = edge.begin(); it != edge.end(); it++) {
        if (anc(it->Y.X) != anc(it->Y.Y)) { // Neu goc cua hai dinh khac nhau
            join(it->Y.X, it->Y.Y); // Hop goc cua hai dinh lai
            r += it->X; // Cap nhat gia tri do dai cay khung nho nhat
        }
    }
    printf("%d\n", r);
}
```

## Độ phức tạp

Độ phức tạp trung bình O(|E|log|E|)

## Ứng dụng



## Let's practice

1. https://www.spoj.com/problems/MST/
2. https://vn.spoj.com/problems/NKCITY/
3. https://vn.spoj.com/problems/QBMST/
4. https://codeforces.com/group/FLVn1Sc504/contest/274710/problem/I
5. https://codeforces.com/group/FLVn1Sc504/contest/274813/problem/Z
6. https://codeforces.com/group/FLVn1Sc504/contest/274825/problem/J
7. https://codeforces.com/group/FLVn1Sc504/contest/274766/problem/K
8. https://codeforces.com/group/FLVn1Sc504/contest/274860/problem/E
9. https://codeforces.com/group/FLVn1Sc504/contest/274809/problem/M
10. https://codeforces.com/group/FLVn1Sc504/contest/274809/problem/S

## Tham khảo
1. Giải thuật và lập trình - Thầy Lê Minh Hoàng
2. Competitive Programming's Handbook
3. Guide to Competitve Programming [book](https://www.amazon.com/Guide-Competitive-Programming-Algorithms-Undergraduate/dp/3319725467)
4. [cp-algorithms.com](https://cp-algorithms.com/graph/mst_kruskal.html)
5. [kc97ble](https://sites.google.com/site/kc97ble/algorithm-graph/kruskal-cpp)
