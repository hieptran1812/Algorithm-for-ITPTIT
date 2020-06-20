# Cây khung (Spanning trees)

## Giới thiệu

Cho đồ thị vô hướng, liên thông G(V,E) trong đó mỗi cạnh e ∈ E được gán một trọng số (weight) w(e) ∈ R. 
Một cây khung (spanning tree) là một đồ thị con của G, không có chu trình, và chứa mọi đỉnh của G.

<p align = "center"><img src = "https://vietjack.com/cau-truc-du-lieu-va-giai-thuat/images/spanning_trees.jpg"></p>

## Tính chất

Cây khung có một vài tính chất chung như sau:
* Một đồ thị liên thông có ít nhất một và có nhiều nhất |v|<sup>|v|-2</sup> cây khung, trong đó |v| là số cạnh của đồ thị.
* Tất cả cây khung của đồ thị G đều có cùng số cạnh và số đỉnh.
* Cây khung của đồ thị không có bất cứ chu trình nào.
* Cây khung có |n| - 1 cạnh, trong đó |n| là số đỉnh của đồ thị.
* Thêm bất cứ một cạnh nào vào cây khung sẽ đều tạo ra một và chỉ một chu trình.
* Xóa bất cứ cạnh nào của cây khung sẽ làm mất tính liên thông của cây khung đó.
* Có duy nhất một đường nối hai đỉnh u và v trên cây khung.

## Cây khung nhỏ nhất

Cây khung nhỏ nhất là một biến thể của cây khung trong đồ thị. 

Cây khung nhỏ nhất của một đồ thị có hướng là cây khung mà tổng trọng số các cạnh của cây khung đó là nhỏ nhất.

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/spanning%20tree.PNG"></p>

## Một số thuật toán tìm cây khung nhỏ nhất

1. Thuật toán Kruskal
2. Thuật toán Prim
3. Thuật toán Borůvka
4. Thuật toán Karger-Klein-Tarjan

## Tham khảo
1. [giaithuatlaptrinh.com](https://www.giaithuatlaptrinh.com/?p=1266)
2. [brilliant.com](https://brilliant.org/wiki/spanning-trees/)
3. Guide to Competitve Programming [book](https://www.amazon.com/Guide-Competitive-Programming-Algorithms-Undergraduate/dp/3319725467)
