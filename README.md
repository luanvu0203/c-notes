# C Programming Language Course

## Variables

## Array

## Decision

## Looping

## Function

## Macro

## Bit Operation

## Memory Management

## Pointer Basic 

## Pointer Advance

## Data Structure

## Algorithms

Thuật toán được chia ra nhiều loại khác nhau, tuy nhiên, note này chỉ nói đến thuật toán cơ bản là tìm kiếm và sắp xếp trên mảng hoặc trên danh sách liên kết.

### Searching algorithm

Mục đích của thuật toán tìm kiếm là tìm ra dữ liệu tương ứng với khóa $k$ trong danh sách. Dữ liệu tìm kiếm có thể là chỉ số của phần tử trong mảng hoặc dữ liệu được người dùng định nghĩa. Ví dụ:

```c
struct data {
    int key; // khóa tìm kiếm
    int data; // dữ liệu
};
```

Mỗi thuật toán lại có độ phức tạp tính toán khác nhau. Cần để ý đến:

- The average time.
- The worst-case time and.
- The best possible time.

#### Linear Search

Tìm kiếm tuần tự là phương pháp tìm kiếm phần tử trong một mảng hay một danh sách liên kết bằng cách so sánh lần lượt từng phần tử trong danh sách với khóa k.

Ví dụ tìm kiếm vị trí phần tử $k$ trong mảng:

```c
int find(int *arr, int len, int k) {
    for (int i = 0; i < len; i++) {
        if (arr[i] == k) {
            return i;
        }
    }
    return -1;
}
```

Ví dụ tìm kiếm phần tử $k$ trong danh sách liên kết:

```c
struct node {
    int key;
    int data;
    struct node* next;
};

struct node* find(struct node* node, int k) {
    struct node *inode;
    for (inode = node; inode->next != NULL; inode = inode->next) {
        if (inode->key == k) {
            return inode;
        }
    }
    return NULL;
}
```

Có thể thấy, với mỗi phần tử trong danh sách, có 2 thao tác so sánh được thực hiện: Kiểm tra điều kiện dừng khi hết mảng và kiểm tra phần tử hiện tại thỏa mãn hay chưa. Có thể tối ưu thao tác này bằng cách thay thế phần tử tìm kiếm cuối cùng bằng phần tử có khóa hợp lệ (**phần tử chặn**). Như vậy, chắc chắn sẽ tìm thấy phần tử trong mảng và không cần kiểm tra điều kiện hết mảng. Ví dụ minh họa:

```c
int find(int *arr, int len, int k) {
    int last = arr[len-1];
    arr[len-1] = k; // đặt phần tử cuối cùng = k

    int i;
    while (arr[i] != k) {
        i+=1;
    }
    
    arr[len-1] = last; // trả lại giá trị phần tử cuối

    if (i == len - 1) {
        if (last == k) {
            return len - 1;
        } else {
            return -1;
        }
    } else {
        return i;
    }
}
```

Độ phức tạp thời gian:

- Trường hợp xấu nhất: $O(n)$ khi phần tử tìm kiếm ở cuối cùng hoặc không có.
- Trường hợp tốt nhất: $O(1)$ khi phần tử tìm kiếm ở đầu danh sách.
- Trung bình: $O(\frac{n}{2}) = O(n)$ khi phần tử ở giữa danh sách.

#### Binary Search

Đối với danh sách kiểu mảng (**có thể truy cập phần tử bằng chỉ số**) đã được sắp xếp, việc tìm kiếm có thể được cải thiện đáng kể. Khi so sánh khóa $k$ với phần tử giữa danh sách, dựa vào kết quả so sánh mà **một nửa danh sách** có thể được loại bỏ do biết **chắc chắn** là các phần tử trong đó nhỏ hơn hoặc lớn hơn khóa tìm kiếm $k$.

Ví dụ tìm kiếm với $k = 8$ trong dãy $[1, 2, 3, 4, 5, 6, 7, 8, 9]$ có phần tử chính giữa bằng $5$. Với $k=8>5$, ta sẽ chỉ cần tìm kiếm $k$ trong dãy $[6, 7, 8, 9]$ với phương pháp tương tự.

```c
// tìm kiếm trong danh sách tăng dần
int binary_search(int *arr, int first, int last, int k) {
    if (last >= first) {
        int mid = (first+last)/2; // first + (last-first)/2
        if (arr[mid] == k) {
            return mid;
        } else if (arr[mid] > k) {
            // phần tử hiện tại lớn hơn khóa
            // -> tìm kiếm ở nửa trước
            binary_search(arr, first, mid-1, k);
        } else {
            // phần tử hiện tại nhỏ hơn khóa
            // -> tìm kiếm ở nửa sau
            binary_search(arr, mid+1, last, k);

        }
        
    } else {
        // last < first: danh sách rỗng - không tìm thấy
        return -1;
    }
}
```

Độ phức tạp thời gian:

- Trường hợp xấu nhất: $O(log(n))$
- Trường hợp tốt nhất: $O(1)$
- Trường hợp trung bình: $O(log(n))$

### Sorting algorithm

#### Insertion Sort

#### Bubble Sort

#### Selection Sort

#### Quick Sort

## Optimization

## Common Defects

## Unit Testing

## Git Version Control
