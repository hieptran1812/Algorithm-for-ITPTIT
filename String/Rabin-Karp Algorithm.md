# Thuật toán Rabin-Karp

## Tổng quan

Thuật toán Rabin-Karp là thuật toán được phát triển bởi Richard Karp và Michael Rabin vào năm 1987 được dùng để tìm kiếm các mẫu khớp trong một string.

Ví dụ, cho hai string: 
* s = "Algorithm for ITPTIT"
* t = "ITPTIT"
Yêu cầu là ta phải tìm vị trí của xâu t trong xâu s, trong trường hợp này là 13.

Ý tưởng trung tâm của thuật toán là coi mỗi xâu là một số nguyên và phép toán so sánh hai xâu được đưa về phép toán so sánh các số nguyên (Sử dụng hàm băm).

## Kĩ thuật

### Ý tưởng thuật toán

Tính toán giá trị hashing cho chuỗi t. Tính giá trị hashing tất cả tiền tố (prefix) của string s. Sau đó, ta có thể so sánh **string con có
độ dài |t|** trong string s với **string t** với độ phức tạp hằng số O(1) do đã tính bằng hàm băm. 

### Độ phức tạp thuật toán

Độ phức tạp thời gian trung bình: O(|s| + |t|)

O(|t|) là độ phức tạp thời gian khi tính giá trị hashing của xâu t.

O(|s|) là độ phức tạp thời gian khi so sánh các string con của string s với string t.

### Coding

Code ở [đây](https://ideone.com/zVDftg) nha :)))

## Ví dụ

## Ứng dụng

## Let's practice

1. https://codeforces.com/problemset/problem/245/B
2. https://codeforces.com/problemset/problem/196/A
3. https://codeforces.com/problemset/problem/312/A
4. https://codeforces.com/problemset/problem/90/B
5. https://codeforces.com/problemset/problem/1257/C
6. https://codeforces.com/problemset/problem/1185/B
7. https://codeforces.com/problemset/problem/1076/A
8. https://codeforces.com/problemset/problem/1305/B

## Tham khảo

1. [cp-algorithms.com](https://cp-algorithms.com/string/rabin-karp.html)
