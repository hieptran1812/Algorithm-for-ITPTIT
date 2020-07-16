# Đồ thị Euler, Chu trình Euler, Đường đi Euler

## Tổng quan



## Kĩ thuật

### Các định nghĩa

1. Chu trình đơn chứa tất cả các cạnh của đồ thị gọi là **chu trình Euler**
2. Đường đi đơn chứa tất cả các cạnh của đồ thị được gọi là **đường đi Euler**
3. Một đồ thị có chu trình Euler được gọi là **đồ thị Euler**
4. Một đồ thị có đường đi Euler được gọi là **đồ thị nửa Euler**

Rõ ràng một đồ thị Euler thì phải là nửa Euler nhưng điều ngược lại thì không phải luôn đúng

### Các định lý

1. Một đồ thị **vô hướng liên thông** G = (V,E) có **chu trình Euler** khi và chỉ khi mọi đỉnh của nó đều có bậc chẵn: deg(v) = 0 (mod 2) (∀v ∈ V).
2. Một đồ thị vô hướng liên thông **có đường đi Euler nhưng không có chu trình Euler** khi và chỉ khi nó có đúng 2 đỉnh bậc lẻ.
3. Một đồ thị **có hướng liên thông yếu** G = (V,E) có **chu trình Euler** thì mọi đỉnh của nó có bán bậc ra bằng bán bậc vào: deg+(v) = deg-(v) (∀v ∈ V); Ngược lại, nếu G **liên thông yếu** và mọi đỉnh của nó có bán bậc ra bằng bán bậc vào thì G có **chu trình Euler**, hay G sẽ là **liên thông mạnh**.
4. Một đồ thị có hướng liên thông yếu G = (V,E) có **đường đi Euler nhưng không có chu trình Euler** nếu tồn tại đúng hai đỉnh u, v ∈ V sao cho deg+(u) - deg-(u) = deg-(v) - deg+(v) = 1, còn tất cả những đỉnh khác u và v đều có bán bậc ra bằng bán bậc vào.

### Đặt vấn đề

### Mô tả thuật toán 

**Thuật toán Fleury tìm chu trình Euler**


### Tính đúng đắn của thuật toán

Coming soon!

### Code

```C++

```

### Độ phức tạp

Độ phức tạp thời gian trung bình: O()

## Ví dụ

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
1. [Wikipedia.org](https://en.wikipedia.org/wiki/Eulerian_path)
2. [brilliant.org](https://brilliant.org/wiki/eulerian-path/)
3. [geeksforgeeks.org](https://www.geeksforgeeks.org/eulerian-path-and-circuit/)
4. Giải thuật và lập trình - Thầy Lê Minh Hoàng
