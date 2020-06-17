# Thuật toán Floyd-Warshall

## Tổng quan

Khi nhắc đến thuật toán để tìm đường đi ngắn nhất trong đồ thị, người ta sẽ thường nghĩ tới những thuật toán dễ tiếp cận và có thể chạy trong giới hạn cho phép như Breadth First Search, Dijkstra hay Bellman-Ford. Tuy nhiên, ba thuật toán trên đều chỉ có thể tìm được đường đi ngắn nhất từ một đỉnh nguồn nhất định đến các đỉnh khác và do đó, trong một số trường hợp cụ thể cần chỉ ra đường đi ngắn nhất của mọi cặp đỉnh trong đồ thị, các thuật toán này sẽ hoạt động chưa hiệu quả khi phải chạy lặp đi lặp lại khá nhiều thao tác.
Floyd-Warshall chính là người bạn có thể giải quyết vấn đề này của chúng ta chỉ trong một lần chạy duy nhất. Hơn thế nữa, cách tiếp cận và cài đặt của nó cũng khá đơn giản và quen thuộc.

Thuật toán Floyd-Warshall còn được gọi là thuật toán Floyd được Robert Floyd tìm ra năm 1962 là thuật toán để tìm đường đi ngắn nhất giữa mọi cặp đỉnh. 
Floyd hoạt động được trên đồ thị có hướng, có thể có trọng số âm, tuy nhiên không có chu trình âm. Ngoài ra, Floyd còn có thể được dùng để phát hiện chu trình âm.

Nếu cái ví dụ trên Brillie cho các bạn dễ tưởng tượng ha :D

<p align = "center"><img src = "https://ds055uzetaobb.cloudfront.net/brioche/uploads/mI5XN4iw6B-floyd-warshall.png?width=1200"></p>



## Kĩ thuật

## Ví dụ

## Ứng dụng

## Tham khảo

1. [Wikipedia](https://vi.wikipedia.org/wiki/Thu%E1%BA%ADt_to%C3%A1n_Floyd-Warshall)
2. [https://brilliant.org/](https://brilliant.org/wiki/floyd-warshall-algorithm/)
3. [thuytrangcoding.wordpress.com](https://thuytrangcoding.wordpress.com/2018/03/18/graph-shortestpath-floyd/)
