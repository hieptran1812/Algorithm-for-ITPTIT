# Đồ thị Euler, Chu trình Euler, Đường đi Euler

## Tổng quan

Bài toán bảy cây cầu Euler, còn gọi là Bảy cầu ở Königsberg là bài toán nảy sinh từ nơi chốn cụ thể, thành phố Königsberg, Phổ (nay là Kaliningrad, Nga) nằm trên sông Pregel, bao gồm hai hòn đảo lớn nối với nhau và với đất liền bởi bảy cây cầu. Bài toán đặt ra là tìm một tuyến đường mà đi qua mỗi cây cầu một lần và chỉ đúng một lần (bất kể điểm xuất phát hay điểm tới).

Năm 1736, Leonhard Euler đã chứng minh rằng bài toán này là không có lời giải. Kết quả này là cơ sở phát triển của lý thuyết đồ thị và là tiền đề cho tô pô học.

<p align = "center"><img src = "https://brilliant-staff-media.s3-us-west-2.amazonaws.com/tiffany-wang/MJufJoRB0r.pngg">
  
## Các định nghĩa

<p align = "center"><img src = "https://user-images.githubusercontent.com/35303672/48727417-28c3d500-ec58-11e8-9715-33b168a50b7c.png">

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

## Ứng dụng

Đường đi Euler có rất 
* Các vệt Euler được sử dụng trong Bioinformatics để tái cấu trúc chuỗi DNA từ các đoạn của nó. 
* Chúng cũng được sử dụng trong thiết kế mạch CMOS để tìm thứ tự cổng logic tối ưu. 
* Dựa vào đường đi Euler giải quyết các bài toán về xử lý tree (trong đó mỗi cạnh được coi là một cặp cung). 
* Trình tự De Bruijn có thể được xây dựng dưới dạng các đường Euler của đồ thị de Bruijn.

## Tham khảo
1. [Wikipedia.org](https://en.wikipedia.org/wiki/Eulerian_path)
2. [brilliant.org](https://brilliant.org/wiki/eulerian-path/)
3. [geeksforgeeks.org](https://www.geeksforgeeks.org/eulerian-path-and-circuit/)
4. Giải thuật và lập trình - Thầy Lê Minh Hoàng
