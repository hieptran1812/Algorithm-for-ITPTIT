# Đồ thị

## Giới thiệu

Trên thực tế có nhiều bài toán liên quan tới một tập các đối tượng và những mối liên hệ giữa chúng, đòi hỏi toán học phải đặt ra một mô hình được biểu diễn một cách chặt chẽ và tổng quát bằng ngôn ngữ kí hiệu, đó là **đồ thị**. Những ý tưởng cơ bản về đồ thị được đưa ra từ thế kỉ thứ 18 bởi nhà toán học Thụy Sĩ Leonhard Euler, ông đã dùng mô hình đồ thị để giải [bài toán về những cây cầu Konigsberg](https://en.wikipedia.org/wiki/Seven_Bridges_of_K%C3%B6nigsberg#:~:text=The%20Seven%20Bridges%20of%20K%C3%B6nigsberg,prefigured%20the%20idea%20of%20topology.&text=The%20problem%20was%20to%20devise,bridges%20once%20and%20only%20once.) nổi tiếng.

<p align = "center"><img src = "https://upload.wikimedia.org/wikipedia/commons/5/5d/Konigsberg_bridges.png"></p>

Mặc dù Lý thuyết đồ thị đã được khoa học phát triển từ rất lâu nhưng lại có nhiều ứng dụng hiện đại. Đặc biệt trong những năm trở lại đây, cùng với sự ra đời của máy tính điện tử và sự phát triển nhanh chóng của Tin học, Lý thuyết đồ thị ngày càng được quan tâm đến nhiều hơn. Đặc biệt là các thuật toán trên đồ thị đã có nhiều ứng dụng trong nhiều lĩnh vực khác nhau như: Mạng máy tính, Lý thuyết mã, Tối ưu hóa, Kinh tế học,... Hiện nay, môn học này là một trong những kiến thức cơ sở của bộ môn khoa học máy tính.

## Các thuật ngữ cơ bản

### Định nghĩa đồ thị

Đồ thị là một cấu trúc rời rạc gồm các đỉnh và các cạnh nối các đỉnh đó. Được mô tả hình thức:

<p align = "center">G = (V,E)</p>

V gọi là tập các **đỉnh** (Vertices) và E gọi là tập các **cạnh** (Edges). Có thể coi E là tập các cặp (u,v) với u và v là hai đỉnh của V.

<p align = "center"><img src = "https://qph.fs.quoracdn.net/main-qimg-823c5ba84e4744d3145b91adbc78bc09.webp"></p>

Ví dụ, đồ thị dưới đây bao gồm 6 đỉnh, 7 cạnh.

<p align = "center"><img src = "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5b/6n-graf.svg/1200px-6n-graf.svg.png" height = 30% width = 60%></p>

Một **đồ thị vô hướng** là đồ thị gồm cạnh không định hướng, tức là cạnh nối hai đỉnh u, v cũng là cạnh nối hai đỉnh v, u.

Một **đồ thị có hướng** là đồ thị gồm cạnh có định hướng, tức là có cạnh nối từ đỉnh u tới đỉnh v nhưng chưa chắc đã có cạnh nối từ đỉnh v tới đỉnh u.

<p align = "center"><img src = "https://computersciencewiki.org/images/c/c6/Directed_graph.png"></p>

Như đồ thị trên, có đường đi từ đỉnh C đến F nhưng không có đường đi từ đỉnh F đến C.

**Đồ thị có trọng số** là đồ thị mà mỗi cạnh **được gán một trọng số**. Trọng số ở đây thường là độ dài cạnh. Ví dụ cho đồ thị dưới đây:

<p align = "center"><img src = "https://ucarecdn.com/a67cb888-aa0c-424b-8c7f-847e38dd5691/" height = 350></p>

### Đường dẫn (path)

Ví dụ với đồ thị dưới, một trong những đường nối hai đỉnh 1 và 4 là 1 -> 5 -> 4. 

<p align = "center"><img src = "https://upload.wikimedia.org/wikipedia/commons/thumb/5/5b/6n-graf.svg/1200px-6n-graf.svg.png" height = 30% width = 60%></p>

### Cạnh liên thuộc (incident), đỉnh kề, bậc

#### Đồ thị vô hướng

Với đồ thị vô hướng G = (V,E). Xét một cạnh e ∈ E, nếu e = (u, v) thì ta nói hai đỉnh u và v là **kề nhau** và cạnh e này **liên thuộc** với đỉnh u và đỉnh v.

Với một đỉnh v trong đồ thị, ta định nghĩa **bậc** (degree) của v, ký hiệu deg(v) là số cạnh liên thuộc với v.

**Định lý**: Giả sử G = (V, E) là đồ thị vô hướng với m cạnh, khi đó tổng tất cả các bậc đỉnh trong V sẽ bằng 2m:

<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/graph1.PNG"></p>

**Chứng minh**: Khi lấy tổng tất cả các bậc đỉnh tức là mỗi cạnh e = (u, v) bất kì sẽ được tính một lần trong deg(u) và một lần trong deg(v). Từ đó suy ra kết quả.

**Hệ quả**: Trong đồ thị vô hướng, số đỉnh bậc lẻ là số chẵn

#### Đồ thị có hướng

Với đồ thị vô hướng G = (V,E). Xét một cạnh e ∈ E, nếu e = (u, v) thì ta nói **u nối tới v** và **v nối từ u**, cung e là đi ra khỏi đỉnh u và đi vào đỉnh v. Với mỗi đỉnh v trong đồ thị có hướng, ta định nghĩa: **Bác bậc ra** của v ký hiệu là deg<sup>+</sup>(v) là số cung đi ra khỏi nó; **Bán bậc vào** của v ký hiệu là deg<sup>-</sup>(v) là số cung đi vào đỉnh đó.

**Định lý**: Giả sử G = (V, E) là đồ thị có hướng với m cùng, khi đó tổng các bán bậc ra của các đỉnh bằng tổng các bán bậc vào và bằng m:
<p align = "center"><img src = "https://github.com/hieptran1812/Algorithm-for-ITPTIT/blob/master/image/graph2.PNG"></p>

**Chứng minh**: Khi lấy tổng tất cả các bán bậc ra hay bán bậc vào, mỗi cung (u, v) bất kì sẽ được tính đúng một lần trong deg<sup>+</sup>(v) và cũng được tính đúng một lần trong deg<sup>-</sup>(v). Từ đó suy ra kết quả.



