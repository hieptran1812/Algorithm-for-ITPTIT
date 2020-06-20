# Thuật toán sinh

## Tổng quan

Trong nhiều bài toán ta có nhiệm vụ phải liệt kê các tổ hợp từ một tập giá trị cho trước hoặc đơn giản ta cần một tập hợp tập con các giá trị cho trước để sử dụng cho một mục đích khác trong bài toán. 
Đó là khi bạn cần dùng phương pháp sinh để thực hiện nhiệm vụ này.

## Kĩ thuật

Thuật toán sinh dùng để giải quyết lớp các bài toán thỏa mãn điều kiện:
* Có thể xác định được một thứ tự trên tập các cấu hình tổ hợp cần liệt kê. Từ đó có thể biết được cấu hình đầu tiên và cuối cùng của thứ tự đó.
* Xây dựng được thuật toán từ một cấu hình chưa phải cấu hình cuối, sinh ra được cấu hình kế tiếp nó.

Mã giả:

```C++

Bước 1: (Khởi tạo) Thiết lập cấu hình đầu tiên
Bước 2: (bước lặp)
        While (chưa phải cấu hình cuối cùng){
          Đưa ra cấu hình hiện tại;
          Sinh ra cấu hình kế tiếp;
        }
End

```

## Ví dụ

### Sinh các dãy nhị phân độ dài N

Một dãy nhị phân có độ dài n làm một dãy x = x<sub>1</sub>x<sub>2</sub>...x<sub>n</sub> trong đó x<sub>i</sub> nhận hai giá trị 0 và 1.

**Dễ thấy**: Một dãy nhị phân x độ dài n là biểu diễn nhị phân của một giá trị nguyên p(x) nào đó nằm trong đoạn [0, 2<sup>n</sup> - 1]. 
Số các dãy nhị phân độ dài n = số các số nguyên trong [0, 2<sup>n</sup> - 1] = 2<sup>n</sup>. Ta sẽ thiết kế chương trình liệt kê các dãy nhị phân theo thứ tự từ điển, có nghĩa là sẽ liệt kê lần lượt các dãy nhị phân biểu diễn các số nguyên theo thứ tự 0, 1,..., 2<sup>n</sup> - 1.

**Ví dụ**: Với n = 3, các dãy nhị phân độ dài 3 được liệt kê như sau:

| p(x) | x |
| --- | --- |
| 0 | 000 |
| 1 | 001 |
| 2 | 010 |
| 3 | 011 |
| 4 | 100 |
| 5 | 101 |
| 6 | 110 |
| 7 | 111 |

Như vậy dãy đầu tiên là 00...0 và dãy cuối cùng là 11...1. Okay! Với trường hợp không phải dãy cuối cùng ta dùng kĩ thuật sau: 
Xét từ cuối dãy về đầu (xét từ hàng đơn vị lên), gặp số 0 đầu tiên thì thay nó bằng số 1 và đặt tất cả các phần tử phía sau vị trí đó bằng 0.

Chương trình:

``` C++

#include<bits/stdc++.h>
using namespace std;

string s = "", s_end = "";
vector<string>gen; // vector lưu các giá trị
int n;

int main(){
	cin >> n; // Xâu độ dài n
	for(int i = 0; i < n; i++) s+='0'; // Xâu khởi tạo
	gen.push_back(s);
	for(int i = 0; i < n; i++) s_end+='1'; // Xâu cuối
	while(s != s_end){
		for(int i = n-1; i >= 0; i--){
			if(s[i] == '0'){
				s[i] = '1';
				for(int j = i+1; j < n; j++){
					s[j] = '0';
				}
				break;
			} 
		}
		gen.push_back(s);
	}
	for(int i = 0; i < gen.size(); i++) cout << gen[i] << endl; // In ra các giá trị
}

```

### Liệt kê các hoán vị

**Đề bài**: Liệt kê các hoán vị trong một tập số cho trước.

**Ý tưởng**: Dùng hàm [next_permutation](http://www.cplusplus.com/reference/algorithm/next_permutation/) để sinh hoán vị.

Chương trình:
```C++

#include<bits/stdc++.h>
using namespace std;

void search(int n){
	vector<int> permutation;
	int x;
	for (int i = 0; i < n; i++) {
		cin >> x;
		permutation.push_back(x);
	}
	sort(permutation.begin(),permutation.end());
	do {
		for(int i = 0; i < n; i++){
			cout << permutation[i] << " ";
		}
		cout << endl;
	}while (next_permutation(permutation.begin(),permutation.end()));
}

main(){
	int n;
	cin >> n;
	search(n);
}

```

## Tham khảo
1. Giải thuật và lập trình - thầy Lê Minh Hoàng
2. Handbook Competitve Programming

