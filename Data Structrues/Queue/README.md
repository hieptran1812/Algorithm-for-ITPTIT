# Queue - Hàng đợi

## Tổng quan

Hàng đợi(tiếng anh: Queue) là một cấu trúc dữ liệu dùng để lưu giữ các đối tượng theo cơ chế FIFO (viết tắt từ tiếng Anh: First In First Out), nghĩa là “vào trước ra trước”.

Hình ảnh về hàng đợi rất hay gặp trong đời sống hàng ngày, hình ảnh việc xếp hàng dưới đây là một mô phỏng dễ hiểu nhất cho cấu trúc dữ liệu hàng đợi(queue): Người vào đầu tiên sẽ được tiến đón đầu tiên; Người mới vào bắt buộc phải xếp hàng ở phía cuối.

<p align = "center"><img src = "https://nguyenvanhieu.vn/wp-content/uploads/2018/12/hang-doi-queue.jpg"></p>

Trong cấu trúc hàng đợi(queue), ta chỉ có thể thêm các phần tử vào một đầu của queue(giả sử là cuối), và cũng chỉ có thể xóa phần tử ở đầu còn lại của queue(tạm gọi là đầu). Như vậy, ở một đầu không thể xảy ra hai hành động thêm và xóa đồng thời.

## Operation của Queue

### Khai báo

```C++
#include<queue>
using namespace std; 
int main() 
{ 
    queue <int> q_data;
    q_data.push(1);
    q_data.push(2);
    q_data.push(3);
    q_data.push(4); 
    return 0;
}
```

### Các hàm thành viên

**size**: Lấy số lượng phần tử trong Queue. ĐPT O(1).
```C++
queue <int> q_data;
q_data.push(1);
q_data.push(2);
q_data.push(3);
q_data.push(4);
int length = q_data.size();
```

**push**: Thêm dữ liệu vào Queue. ĐPT O(1).
```C++
queue <int> q_data;
q_data.push(1);
q_data.push(2);
q_data.push(3);
q_data.push(4);
```

**pop**: Bỏ dữ liệu khỏi Queue. ĐPT O(1).
```C++
queue <int> q_data;
q_data.push(1);
q_data.push(2);
q_data.pop();
```

**front**: Lấy giá trị phần tử đầu của Queue. ĐPT O(1).
```C++
queue <int> q_data;
q_data.push(1);
q_data.push(2);
q_data.front();
```

**back**: Lấy phần tử cuối của Queue. ĐPT O(1).
```C++
queue <int> q_data;
q_data.push(1);
q_data.push(2);
q_data.back();
```

**empty**: Trả về true nếu queue rỗng, ngược lại false nếu queue có phần tử. ĐPT O(1).
```C++
queue <int> q_data;
q_data.push(1);
q_data.push(2);
q_data.empty();
```

## Ứng dụng

