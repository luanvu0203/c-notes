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
  + Kết quả là 0 với các số có số lần xuất hiện chẵn (do XOR các cặp số giống nhau).
  + Lúc này chỉ còn lại số có số lần xuất hiện lẻ.
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
  + Để xóa 1 bit sử dụng phép AND bit muốn xóa với 0. 
  ```
  1 AND 0 = 0
  0 AND 0 = 0
  ```
- **Set bit:** đặt giá trị của 1 bit trong biến.
  + Để đặt 1 bit ta sử dụng toán tử OR bit muốn xóa với 1.
  ```
  1 OR 1 = 1
  1 OR 0 = 0
  ```
- **Toggle bit:** đảo giá trị của một bit trong biến.
  + Để đảo một bit, ta có thể sử dụng toán tử XOR (^) bit muốn đảo với 1. 
  ```
  1 XOR 1 = 0
  0 XOR 1 = 1
  ```
- **Read bit:** đọc giá trị của một bit trong biến.
  + Để đọc một bit, ta có thể sử dụng toán tử AND bit muốn đảo với 0. 
  ```
  0 AND 1 = 0
  1 AND 1 = 1
  ```
### Bit mask

### Bit Field in C
- Trong ngôn ngữ C, chúng ta có thể chỉ định kích thước (theo bit) của các thành phần trong struct và union. 
- Ý tưởng của bit field là sử dụng bộ nhớ một cách hiệu quả khi chúng ta biết rằng giá trị của một trường hoặc nhóm trường sẽ không vượt quá giới hạn hoặc nằm trong một khoảng nhỏ. 
- Bit field trong C được sử dụng khi không gian lưu trữ trong chương trình của chúng ta bị hạn chế.
- Lợi ích của Bit field trong C
  + Giảm tiêu thụ bộ nhớ.
  + Làm cho chương trình của chúng ta hiệu quả và linh hoạt hơn.
  + Dễ triển khai.
- Bit field _**là các biến được định nghĩa với một độ rộng hoặc kích thước được xác định trước**_. Cú pháp khai báo của bit field như sau:
```
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
```
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
    + Khi khởi tạo union t, 1 vùng nhớ 4 bytes (32 bits) tương ứng với kích thước của trường có kích thước lớn nhất trong union (int).
    + Khi gán `t.z = 1;` giá trị 1 sẽ ghi vào vùng nhớ 32 bits này => giá trị của vùng nhớ (cả 32 bits) lúc này là 1.
    + Vậy giá trị `t.x`, `t.y` và `t.z` in ra sẽ là giá trị của vùng nhớ union t => Kết quả
## Memory Management

## Pointer Basic 

## Pointer Advance

## Data Structure

## Algorithms

## Optimization

## Common Defects

## Unit Testing

## Git Version Control
