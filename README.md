# C Programming Language Course

## Variables

## Array

## Decision

## Looping

## Function

## Macro

## Bit Operation

### Giới thiệu

  | Bit A | Bit B | A AND B |  A OR B |  A XOR B  |   NOT A  |
  |:-----:|:-----:|:-------:|:-------:|:---------:|:--------:|
  | 0     | 0     | 0       | 0       | 0         | 1        |
  | 0     | 1     | 0       | 1       | 1         | 1        |
  | 1     | 0     | 0       | 1       | 1         | 0        |
  | 1     | 1     | 1       | 1       | 0         | 0        |

Trong ngôn ngữ C, có 6 toán tử được gọi là toán tử bitwise (hay còn được gọi là toán tử bit vì chúng hoạt động ở mức độ bit).

- **Toán tử & (bitwise AND)**: nhận hai số làm toán hạng và thực hiện phép AND trên từng bit của hai số đó.
    Kết quả của phép AND là 1 chỉ khi cả hai bit là 1.
- **Toán tử | (bitwise OR)**: nhận hai số làm toán hạng và thực hiện phép OR trên từng bit của hai số đó.
    Kết quả của phép OR là 1 nếu bất kỳ hai bit nào là 1.
- **Toán tử ^ (bitwise XOR)**: nhận hai số làm toán hạng và thực hiện phép XOR trên từng bit của hai số đó.
    Kết quả của phép XOR là 1 nếu hai bit khác nhau.
- **Toán tử << (left shift)**: nhận hai số, dịch chuyển các bit của toán hạng đầu tiên sang trái và toán hạng thứ hai quyết định số vị trí cần dịch chuyển.
- **Toán tử >> (right shift)**: nhận hai số, dịch chuyển các bit của toán hạng đầu tiên sang phải và toán hạng thứ hai quyết định số vị trí cần dịch chuyển.
- **Toán tử ~ (bitwise NOT)**: nhận một số và đảo ngược tất cả các bit của nó.

### Một số lưu ý khi sử dụng Bitwise Operations

#### **1. Toán tử dịch trái và dịch phải không nên được sử dụng cho các số âm.** 

- Nếu toán hạng thứ hai (quyết định số lần dịch) là một số âm, kết quả sẽ là không xác định trong C.
  Ví dụ, kết quả của cả $1 << -1$ và $1 >> -1$ là không xác định.
- Nếu số được dịch chuyển nhiều hơn kích thước của số nguyên, kết quả cũng là không xác định.
  Ví dụ, $1 << 33$ là không xác định nếu số nguyên được lưu trữ bằng 32 bit.

#### **2. Phép OR bit của hai số chỉ là tổng của hai số đó nếu không có nhớ, khi có nhớ kết quả sẽ cộng thêm phép AND bit của chúng.**

- Ví dụ, giả sử chúng ta có $a = 5 (101)$ và $b = 2 (010)$, vì không có nhớ, tổng của chúng chỉ là $a | b$.
- Bây giờ, nếu chúng ta thay đổi 'a' thành $6$, tức là $110$ nhị phân, tổng của chúng sẽ thay đổi thành $a | b + a \And b$ vì có nhớ.

#### **3. Toán tử XOR bit là toán tử phổ biến nhất**

- Một ví dụ đơn giản có thể là "Cho một tập hợp các số trong đó tất cả các phần tử xuất hiện một số lần chẵn, ngoại trừ một số duy nhất xuất hiện một số lần lẻ, hãy tìm số xuất hiện lẻ".
- Vấn đề này có thể được giải quyết hiệu quả bằng cách thực hiện XOR trên tất cả các số.
- Kết quả trả về sẽ là số duy nhất xuất hiện số lần lẻ vì phép XOR sẽ so sánh tất cả các số với nhau:
  - Kết quả là 0 với các số có số lần xuất hiện chẵn (do XOR các cặp số giống nhau).
  - Lúc này chỉ còn lại số có số lần xuất hiện lẻ.

#### **4. Các toán tử Bitwise không nên được sử dụng thay thế cho các toán tử logic.**

- Kết quả của các toán tử logic (&&, || và !) là 0 hoặc 1, nhưng các toán tử bitwise trả về một giá trị số nguyên.
- Ngoài ra, các toán tử logic coi bất kỳ toán hạng khác không là 1.

#### **5. Toán tử dịch trái (left-shift) và dịch phải (right-shift) tương đương với phép nhân và chia cho 2 tương ứng.**

- Toán tử dịch trái (<<) dịch các bit của toán hạng trái sang trái theo số vị trí được xác định bởi toán hạng phải.
  Việc dịch trái tương đương với việc nhân toán hạng trái với $2^k$, trong đó k là số vị trí dịch.
- Toán tử dịch phải (>>) dịch các bit của toán hạng trái sang phải theo số vị trí được xác định bởi toán hạng phải.
  Việc dịch phải tương đương với việc chia toán hạng trái cho $2^k$ và lấy phần nguyên.

#### **6. Toán tử & (AND) có thể được sử dụng để kiểm tra nhanh xem một số có phải là số lẻ hay số chẵn.** 

- Giá trị của biểu thức (x & 1) sẽ khác 0 chỉ khi x là số lẻ, ngược lại giá trị sẽ bằng 0. 
- Điều này xuất phát từ tính chất của số nhị phân, trong đó bit cuối cùng của số lẻ là 1, trong khi bit cuối cùng của số chẵn là 0.
- Vì vậy, khi thực hiện phép AND với 1, chúng ta chỉ quan tâm đến bit cuối cùng để xác định tính chẵn lẻ của số.

#### **7. Toán tử ~ (NOT) cần được sử dụng cẩn thận.**

- Kết quả của toán tử ~ trên một số nhỏ có thể là một số lớn nếu kết quả được lưu trữ trong một biến không dấu (unsigned).
- Và kết quả có thể là một số âm nếu kết quả được lưu trữ trong một biến có dấu (signed) (giả sử rằng các số âm được lưu trữ dưới dạng bù hai với bit trái nhất là bit dấu). Điều này liên quan đến cách biểu diễn số âm và số không dấu trong bộ nhớ máy tính.

### Set, Clear, Toggle, Read bit

- **Cleat bit:** xoá giá trị của 1 bit trong biến.
  - Để xóa 1 bit sử dụng phép AND bit muốn xóa với 0.

  ```
  1 AND 0 = 0
  0 AND 0 = 0
  ```

- **Set bit:** đặt giá trị của 1 bit trong biến.
  - Để đặt 1 bit ta sử dụng toán tử OR bit muốn xóa với 1.

  ```
  1 OR 1 = 1
  1 OR 0 = 0
  ```

- **Toggle bit:** đảo giá trị của một bit trong biến.
  - Để đảo một bit, ta có thể sử dụng toán tử XOR (^) bit muốn đảo với 1.

  ```
  1 XOR 1 = 0
  0 XOR 1 = 1
  ```

- **Read bit:** đọc giá trị của một bit trong biến.
  - Để đọc một bit, ta có thể sử dụng toán tử AND bit muốn đảo với 0.

  ```
  0 AND 1 = 0
  1 AND 1 = 1
  ```
  
```c
  #include <stdio.h>

  unsigned int setBit (unsigned int value, unsigned int k); 
  unsigned int clearBit (unsigned int value, unsigned int k);
  unsigned int readBit (unsigned int value, unsigned int k); 
  unsigned int toggleBit (unsigned int value, unsigned int k);
  void printBinary (unsigned int num);
  
  int main(){
      unsigned int value = 8; unsigned int k = 2;
      unsigned int SetBit, ClearBit, ReadBit, ToggleBit;
      SetBit = setBit(value, k - 1);
      ClearBit = clearBit(value, k - 1);
      ReadBit = readBit(value, k - 1);
      ToggleBit = toggleBit(value, k - 1); 
      printf("Value: %u, Order: %u\n", value, k);
      printf("Value in binary:"); printBinary(value);
      printf("SetBit: \t"); printBinary(SetBit);
      printf("ClearBit: \t"); printBinary(ClearBit);
      printf("ReadBit: \t"); printBinary (ReadBit); 
      printf("ToggleBit: \t"); printBinary(ToggleBit);
      return 0;
  }
  
  unsigned int setBit (unsigned int value, unsigned int k)
  {
      return value |= (1<<k);
  }
  
  unsigned int clearBit (unsigned int value, unsigned int k){
      return value &= ~(1<<k);
  }
  
  unsigned int readBit(unsigned int value, unsigned int k){ 
      return (value & (1<<k)) >> k;
  }
  
  unsigned int toggleBit (unsigned int value, unsigned int k){ 
      return value ^= (1<<k);
  };
  
  void printBinary(unsigned int num) {
      int i;
      int num_bits = (num == 0) ? 1 : log2(num) + 1;
      for (i = num_bits - 1; i >= 0; i--) {
          printf("%u", readBit(num, i));
      }
      printf("\n");
  }
```

### Bit mask

### Bit Field in C

- Trong ngôn ngữ C, chúng ta có thể chỉ định kích thước (theo bit) của các thành phần trong struct và union.

- Ý tưởng của bit field là sử dụng bộ nhớ một cách hiệu quả khi chúng ta biết rằng giá trị của một trường hoặc nhóm trường sẽ không vượt quá giới hạn hoặc nằm trong một khoảng nhỏ. 
- Bit field trong C được sử dụng khi không gian lưu trữ trong chương trình của chúng ta bị hạn chế.
- Lợi ích của Bit field trong C
  - Giảm tiêu thụ bộ nhớ.
  - Làm cho chương trình của chúng ta hiệu quả và linh hoạt hơn.
  - Dễ triển khai.

- Bit field _**là các biến được định nghĩa với một độ rộng hoặc kích thước được xác định trước**_. Cú pháp khai báo của bit field như sau:

```c
  struct
  {
  data_type member_name : width_of_bit-field;
  };
```

**data_type:** Đây là một kiểu số nguyên xác định giá trị của trường bit mà sẽ được hiểu. Kiểu có thể là int, signed int hoặc unsigned int.
**member_name:** Tên của bit field.
**width_of_bit-field:** Số bit trong trường bit. Độ rộng phải nhỏ hơn hoặc bằng với độ rộng bit của kiểu dữ liệu được chỉ định.

- **Một số ví dụ sử dụng Bit Field**
**VD1. Cho đoạn chương trình sau, dự đoán kết quả của chương trình.**

```c
  #include <stdio.h>
  union test {
      // Bit-field member x with 3 bits
      unsigned int x : 3;
     // Bit-field member y with 3 bits
     unsigned int y : 3;
     // Regular integer member z
     int z;
   };
   int main()
   {
     // Declare a variable t of type union test
     union test t;
     // Assign the value 5 to x (3 bits)
     t.x = 5;
     // Assign the value 4 to y (3 bits)
     t.y = 4;
     // Assign the value 1 to z (32 bits)
     t.z = 1;
     // Print the values of x, y, and z
     printf("t.x = %d, t.y = %d, t.z = %d", t.x, t.y, t.z);
     return 0;
   }
}
```

- **Kết quả:** t.x = 1, t.y = 1, t.z = 1
- **Giải thích:**
  - Khi khởi tạo union t, 1 vùng nhớ 4 bytes (32 bits) tương ứng với kích thước của trường có kích thước lớn nhất trong union (int).
  - Khi gán `t.z = 1;` giá trị 1 sẽ ghi vào vùng nhớ 32 bits này => giá trị của vùng nhớ (cả 32 bits) lúc này là 1.
  - Vậy giá trị `t.x`, `t.y` và `t.z` in ra sẽ là giá trị của vùng nhớ union t => Kết quả

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

```c
void insertion_sort(int *arr, int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        for (j = i - 1; j>=0; j--) {
            if (arr[j] > key) {
                arr[j+1] = arr[j];
            } else {
                break;
            }
        }
        arr[j+1] = key;
    }
}
```

#### Bubble Sort

```c
void bubble_sort(int*arr, int n) {
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n-i-1; j++) {
            if(arr[j] > arr[j+1]) {
                int temp = arr[j];
                arr[j] = arr[j+1];
                arr[j+1] = temp;
            }
        }
    }
}
```

#### Selection Sort

```c
void selection_sort(int *arr, int n) {
    for (int i = 0; i < n-1; i++) {
        int index_min = i;
        int min = arr[i];
        
        // tìm chỉ số và giá trị phần tử nhỏ hơn arr[i]
        for (int j = i+1; j < n; j++) {
            if (arr[j] < min) {
                index_min = j;
                min = arr[j];
            }
        }
        arr[index_min] = arr[i];
        arr[i] = min;
    }
}
```

#### Quick Sort

```c

void swap(int* a, int* b)
{
    int t = *a;
    *a = *b;
    *b = t;
}

// Partition the array using the last element as the pivot
int partition_sort(int arr[], int low, int high)
{
    // Choosing the pivot
    int pivot = arr[high];
 
    // Index of smaller element and indicates
    // the right position of pivot found so far
    int i = (low - 1);
 
    for (int j = low; j <= high - 1; j++) {
 
        // If current element is smaller than the pivot
        if (arr[j] < pivot) {
 
            // Increment index of smaller element
            i++;
            swap(&arr[i], &arr[j]);
        }
    }
    swap(&arr[i + 1], &arr[high]);
    return (i + 1);
}
 
// The main function that implements QuickSort
// arr[] --> Array to be sorted,
// low --> Starting index,
// high --> Ending index
void quickSort(int arr[], int low, int high)
{
    if (low < high) {
 
        // pi is partitioning index, arr[p]
        // is now at right place
        int pi = partition_sort(arr, low, high);
 
        // Separately sort elements before
        // partition and after partition
        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}
```

## Optimization

## Common Defects
### 1. Trộn số nguyên có dấu và không dấu trong phép tính số học
* Kiểu Signed Thông thường, việc trộn các unsigned số nguyên trong các phép tính số học thường không phải là một ý kiến hay. 
#### Ví dụ: đầu ra của ví dụ sau là gì?
```c
#include <stdio.h>
int main(void)
{ 
    unsigned int a = 1000;
    signed int b = -1;

    if (a > b) puts("a is more than b");
    else puts("a is less or equal than b"); 

    return 0;
}
```
* Vì 1000 lớn hơn -1 nên bạn mong đợi kết quả đầu ra là a is more than b, tuy nhiên điều đó sẽ không xảy ra.
* Các phép toán số học giữa các loại tích phân khác nhau được thực hiện trong một loại chung được xác định bởi cái gọi là chuyển đổi số học thông thường.
* Trong trường hợp này, loại "phổ biến" là unsigned int. Điều này có nghĩa là int toán hạng b sẽ được chuyển đổi unsigned int trước khi so sánh.
* Khi -1 được chuyển đổi thành unsigned int kết quả, giá trị tối đa có thể có unsigned int, lớn hơn 1000, nghĩa là giá trị đó a > bsai.

### 2. Vượt qua ranh giới mảng
*Mảng luôn bắt đầu bằng chỉ số 0 và kết thúc với độ dài mảng chỉ số trừ 1.
** Sai:
```c
#include <stdio.h>
int main()
{
    int x = 0;
    int myArray[5] = { 1,2,3,4,5}; //Declaring 5 elements
    for(x=1; x<=5; x++) //Looping from 1 till 5.
       printf("%d\t”, myArray[x]);
    printf("\n");
    return 0;
}
//Output: 2 3 4 5 GarbageValue
```
** Chính xác:
```c
#include <stdio.h>
int main()
{
    int x = 0;
    int myArray[5] = { 1,2,3,4,5}; //Declaring 5 elements
    for(x=0; x<5; x++) //Looping from 0 till 4.
       printf("%d\t",myArray[x]);
    printf("\n");
    return 0;
}
//Output: 1 2 3 4 5
```
* Vì vậy, hãy biết độ dài mảng trước khi làm việc trên mảng, nếu không chúng ta có thể làm hỏng bộ đệm hoặc gây ra lỗi phân đoạn bằng cách truy cập vào vị trí bộ nhớ khác nhau.
### 3. Thiếu điều kiện cơ bản trong hàm đệ quy
Tính giai thừa của một số là một ví dụ cổ điển của hàm đệ quy.

Thiếu điều kiện cơ bản:
```c
#include <stdio.h>
int factorial(int n)
{
       return n * factorial(n - 1);
}
int main()
{
    printf("Factorial %d = %d\n", 3, factorial(3));
    return 0;
}
//Typical output: Segmentation fault
```
* Vấn đề với hàm này là nó sẽ lặp vô hạn, gây ra lỗi phân đoạn - nó cần một điều kiện cơ bản để dừng đệ quy.
* Điều kiện cơ bản được tuyên bố:
```c
#include <stdio.h>
int factorial(int n)
{
    if (n == 1) // Base Condition, very crucial in designing the recursive functions.
    {
       return 1;
    }
    else
    {
       return n * factorial(n - 1);
    }
}
int main()
{
    printf("Factorial %d = %d\n", 3, factorial(3));
    return 0;
}
//Output :  Factorial 3 = 6
```
* Hàm này sẽ chấm dứt ngay khi nó đạt điều kiện n bằng 1 (với điều kiện giá trị ban đầu của n đủ nhỏ - giới hạn trên là 12 khi int là số lượng 32 bit).
* Các quy tắc cần tuân thủ:
* Khởi tạo thuật toán. Các chương trình đệ quy thường cần một giá trị gốc để bắt đầu. Điều này được thực hiện bằng cách sử dụng tham số được truyền cho hàm hoặc bằng cách cung cấp hàm cổng không đệ * quy nhưng thiết lập các giá trị gốc cho phép tính đệ quy.
* Kiểm tra xem (các) giá trị hiện tại đang được xử lý có khớp với trường hợp cơ sở hay không. Nếu vậy, xử lý và trả về giá trị.
* Xác định lại câu trả lời theo một hoặc nhiều vấn đề phụ nhỏ hơn hoặc đơn giản hơn.
* Chạy thuật toán cho bài toán con.
* Kết hợp các kết quả để xây dựng câu trả lời.
* Trả về kết quả.
### 4. Sử dụng hằng ký tự thay vì chuỗi ký tự và ngược lại
Trong C, hằng ký tự và chuỗi ký tự là những thứ khác nhau.

* Một ký tự được bao quanh bởi dấu ngoặc đơn giống như 'a'một hằng số ký tự. Hằng ký tự là một số nguyên có giá trị là mã ký tự đại diện cho ký tự đó. Cách diễn giải các hằng ký tự có nhiều ký tự giống như 'abc'được xác định khi triển khai.
* Không hoặc nhiều ký tự được bao quanh bởi dấu ngoặc kép giống như "abc"một chuỗi ký tự. Chuỗi ký tự là một mảng không thể sửa đổi có các phần tử thuộc kiểu char. Chuỗi trong dấu ngoặc kép cộng với dấu chấm dứt null-characterlà nội dung, do đó "abc"có 4 phần tử ( {'a', 'b', 'c', '\0'})

#### Ví dụ 1, một hằng số ký tự được sử dụng trong đó nên sử dụng một chuỗi ký tự. Hằng ký tự này sẽ được chuyển đổi thành một con trỏ theo cách được xác định khi triển khai và có rất ít cơ hội để con trỏ được chuyển đổi hợp lệ, vì vậy ví dụ này sẽ gọi hành vi không xác định.
```c
#include <stdio.h>
int main(void) {
    const char *hello = 'hello, world'; /* bad */
    puts(hello);
    return 0;
}
```
#### Ví dụ 2 , một chuỗi ký tự được sử dụng trong đó nên sử dụng hằng ký tự. Con trỏ được chuyển đổi từ chuỗi ký tự sẽ được chuyển đổi thành số nguyên theo cách do quá trình triển khai xác định và nó sẽ được chuyển đổi thành char theo cách do quá trình triển khai xác định. (Cách chuyển đổi một số nguyên thành loại có dấu không thể biểu thị giá trị cần chuyển đổi do việc triển khai xác định và liệu char có được ký hay không cũng do việc triển khai xác định.) Đầu ra sẽ là một thứ vô nghĩa.
```c
#include <stdio.h>
int main(void) {
    char c = "a"; /* bad */
    printf("%c\n", c);
    return 0;
}
```
* Trong hầu hết các trường hợp, trình biên dịch sẽ phàn nàn về những sự trộn lẫn này. Nếu không, bạn cần sử dụng nhiều tùy chọn cảnh báo trình biên dịch hơn hoặc bạn nên sử dụng trình biên dịch tốt hơn.

### 5. Theo mặc định, các ký tự dấu phẩy động có kiểu double
* Phải cẩn thận khi khởi tạo các biến thuộc loại floathoặc literal valuesso sánh chúng với các giá trị bằng chữ, bởi vì các ký tự dấu phẩy động thông thường như 0.1là loại double. Điều này có thể dẫn tới những bất ngờ:
```c
#include <stdio.h>
int main() {
    float  n = 0.1;
    if (n > 0.1) printf("Wierd\n");
    return 0;
}
```
// Prints "Wierd" when n is float
* Ở đây, n được khởi tạo và làm tròn đến độ chính xác đơn, dẫn đến giá trị 0,10000000149011612. Sau đó, n được chuyển đổi trở lại thành độ chính xác gấp đôi để so sánh với 0,1 chữ (bằng 0,100000000000000001), dẫn đến không khớp.

* Bên cạnh các lỗi làm tròn, việc trộn các biến float với các ký tự kép sẽ dẫn đến hiệu suất kém trên các nền tảng không hỗ trợ phần cứng cho độ chính xác kép.

### 6. Quên giải phóng bộ nhớ
* Người ta phải luôn nhớ giải phóng bộ nhớ đã được phân bổ, theo hàm của chính bạn hoặc theo hàm thư viện được gọi từ hàm của bạn.
```c
#include <stdlib.h>
#include <stdio.h>
int main(void)
{
    char *line = NULL;
    size_t size = 0;
    /* memory implicitly allocated in getline */
    getline(&line, &size, stdin);
    /* uncomment the line below to correct the code */
    /* free(line); */
    return 0;
}
```
* Đây là một lỗi khá vô hại trong ví dụ cụ thể này, vì khi một tiến trình thoát ra, hầu như tất cả các hệ điều hành đều giải phóng toàn bộ bộ nhớ được phân bổ cho bạn.
*  Cũng lưu ý rằng getline có thể bị lỗi theo nhiều cách khác nhau, nhưng dù lỗi theo cách nào đi nữa, bộ nhớ mà nó đã phân bổ phải luôn được giải phóng (khi bạn sử dụng xong) nếu dòng không phải là NULL.
*   Bộ nhớ có thể được phân bổ ngay cả khi lệnh gọi getline() đầu tiên phát hiện EOF (được báo cáo bằng giá trị trả về là -1, không phải EOF).

### 7. Thêm dấu chấm phẩy vào #define
* Chủ yếu xảy ra với tôi!! Rất dễ bị nhầm lẫn trong bộ tiền xử lý C và coi nó như một phần của chính C. Nhưng đó là một sai lầm, vì bộ tiền xử lý chỉ là một cơ chế thay thế văn bản. Ví dụ, nếu bạn viết
```c
// WRONG
#define MAX 100;
int arr[MAX];
Mã sẽ được chuyển đổi thành
int arr[100;];
```
* Đó là một lỗi cú pháp. Cách khắc phục là bỏ dấu chấm phẩy khỏi dòng #define.

### 8. Cẩn thận với dấu chấm phẩy
* Hãy cẩn thận với dấu chấm phẩy. Ví dụ sau
```c
if (x > a);
   a = x;
thực sự có nghĩa là:
if (x > a) {}
a = x;
```
* Có nghĩa là x sẽ được gán cho a trong mọi trường hợp, đây có thể không phải là điều bạn mong muốn ban đầu.
* Đôi khi, thiếu dấu chấm phẩy cũng sẽ gây ra vấn đề không thể nhận thấy:
```c
if (i < 0) 
    return
day = date[0];
hour = date[1];
minute = date[2];
```
* Dấu chấm phẩy phía sau trả về bị bỏ qua, do đó day = date[0] sẽ được trả về.

### 9. Viết nhầm = thay vì == khi so sánh
* Toán = tử được sử dụng để gán.
* Toán == tử được sử dụng để so sánh.
* Người ta phải cẩn thận không trộn lẫn cả hai. Đôi khi viết nhầm
/* assign y to x */
```c
if (x = y) {
     /* logic */
}
```
khi điều thực sự mong muốn là:
/* compare if x is equal to y */
```c
if (x == y) {
    /* logic */
}
```
 * Cái trước gán giá trị của y cho x và kiểm tra xem giá trị đó có khác 0 hay không, thay vì thực hiện so sánh, tương đương với:
```c
if ((x = y) != 0) {
    /* logic */
}
```
Truyện tranh này cho thấy điều tương tự. Trong đó, người lập trình sử dụng = thay vì == trong if câu lệnh.
### 10. Sao chép quá nhiều
```c
char buf[8]; /* tiny buffer, easy to overflow */
printf("What is your name?\n");
scanf("%s", buf); /* WRONG */
scanf("%7s", buf); /* RIGHT */
```
* Nếu người dùng nhập một chuỗi dài hơn 7 ký tự (-1 cho dấu kết thúc null), bộ nhớ phía sau bộ đệm đệm sẽ bị ghi đè. 
* Điều này dẫn đến hành vi không xác định. Các hacker độc hại thường khai thác điều này để ghi đè địa chỉ trả về và đổi thành địa chỉ mã độc của hacker.

### 11. Macro là sự thay thế chuỗi đơn giản
* Macro là sự thay thế chuỗi đơn giản. Vì vậy, chúng sẽ hoạt động với các mã thông báo tiền xử lý.
```c
#include <stdio.h>
#define SQUARE(x) x*x
int main(void) {
    printf("%d\n", SQUARE(1+2));
    return 0;
}
```
* Bạn có thể mong đợi mã này sẽ được in 9, (3*3) nhưng thực tế 5 nó sẽ được in vì macro sẽ được mở rộng thành 1+2*1+2.
* Bạn nên đặt các đối số đã lấy và toàn bộ biểu thức trong macro trong dấu ngoặc đơn để tránh vấn đề này.
```c
#include <stdio.h>
#define SQUARE(x) ((x)*(x))
int main(void) {
    printf("%d\n", SQUARE(1+2));
    return 0;
}
```
## Unit Testing

## Git Version Control
