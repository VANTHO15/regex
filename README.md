# Regular expressions

- Web demo:
```commandline
    https://regex101.com/
```
- **Khái niệm**:
- Một biểu thức chính quy Regular Expressions (RegEx) trong Python là một chuỗi ký tự đặc biệt dùng mẫu tìm kiếm để tìm một chuỗi hoặc một nhóm chuỗi. Python cung cấp mô đun re.
- **Ví dụ**
```commandline
    ^a...s$
```
- bất kỳ chuỗi nào có năm chữ cái, bắt đầu bằng a và kết thúc bằng s.
```text
import re

pattern = '^a...s$'
test_string = 'abyss'
result = re.match(pattern, test_string)

if result:
  print("Tim kiem thanh cong.")
else:
  print("Tim kiem khong thanh cong.")
```
## Các cú pháp pattern cơ bản [] . ^ $ * + ? {} () \ |
# 1 Dấu []: Dấu ngoặc vuông sử dụng để thể hiện tập các ký tự bạn muốn khớp
```text
[abc] :
    a	Khớp với ký tự a
    ac	Khớp với ký tự a hoặc c
    Tho	Không khớp
```
- Ở đây, [abc] sẽ khớp nếu chuỗi bạn truyền có chứa bất kỳ ký tự a, b hoặc c nào.
- [a-e] tương tự với [abcde]
- [1-4] tương tự với [1234]
- Nếu ký tự đầu tiên của tập hợp là ^ thì tất cả các ký tự không được định nghĩa trong tập hợp sẽ được so khớp.
- [^abc] nghĩa là khớp với các chuỗi không có ký tự a, b hay c
- [^0-9] nghĩa là khớp với các chuỗi không có ký tự chữ số nào
- Các ký tự đặc biệt trong [] sẽ được coi như ký tự thông thường.
- [(+)] khớp với bất kỳ chuỗi nào có ký tự (, + hoặc )
# 2 Dấu . : Dấu chấm khớp với bất kỳ ký tự đơn thông thường nào ngoại trừ ký tự tạo dòng mới '\n'
```text
..
    a	Không khớp vì chỉ có một ký tự
    ac	Khớp vì có hai ký tự
    acd	Khớp vì có hai ký tự trở lên
```
# 3 Dấu ^ : Biểu tượng dấu mũ ^ được sử dụng để khớp ký tự đứng đầu một chuỗi.
```text
^a
    a	Khớp vì bắt đầu bằng a
    abc	Khớp vì bắt đầu bằng a
    bac	Không khớp vì a không nằm ở đầu tiên
^ab
    abc	Khớp vì bắt đầu bằng ab
    acb	Không khớp, bắt đầu bằng a nhưng ký tự tiếp theo không phải b
```
# 4 Dấu $ : Biểu tượng Dollar $ được sử dụng để khớp ký tự kết thúc một chuỗi.
```text
a$
    a	Khớp vì kết thúc bằng a
    thona	Khớp vì kết thúc bằng a
    cab	Không khớp vì a không nằm ở vị trí cuối cùng
```
# 5 Dấu * : Biểu tượng dấu hoa thị * có thể khớp với chuỗi có hoặc không có ký tự được định nghĩa trước nó. Ký tự này có thể được lặp lại nhiều lần mà không bị giới hạn số lượng
```text
ma*n
    mn	Khớp vì ký tự trước * có thể không xuất hiện
    man	Khớp vì có xuất hiện đầy đủ các ký tự
    maaaan	Khớp vì ký tự trước * có thể xuất hiện nhiều lần
    main	Không khớp vì không giống pattern, n không nằm kế a
    woman	Khớp vì có xuất hiện đầy đủ các ký tự
```
# 6 Dấu + : Biểu tượng dấu cộng + có thể khớp với chuỗi có một hoặc nhiều ký tự được định nghĩa trước nó. Ký tự này có thể được lặp lại nhiều lần mà không bị giới hạn số lượng.
```text
ma+n
    mn	Không khớp vì ký tự a trước + không xuất hiện
    man	Khớp vì có xuất hiện đầy đủ các ký tự
    maaaan	Khớp vì ký tự trước + có thể xuất hiện nhiều lần
    main	Không khớp vì không giống pattern, n không nằm kế a
    woman	Khớp vì có xuất hiện đầy đủ các ký tự
```
# 7 Dấu ? : Biểu tượng dấu chấm hỏi có thể khớp với chuỗi có hoặc không có ký tự được định nghĩa trước nó. Ký tự này không thể được lặp lại nhiều lần, chỉ giới hạn số lượng với một lần xuất hiện
```text
ma?n
    mn	Khớp vì ký tự trước ? có thể không xuất hiện
    man	Khớp vì có xuất hiện đầy đủ các ký tự
    maaaan	Không khớp vì ký tự trước ? chỉ có thể xuất hiện 1 lần
    main	Không khớp vì không giống pattern, n không nằm kế a
    woman	Khớp vì có xuất hiện đầy đủ các ký tự
```
# 8 Dấu {} : Dấu ngoặc nhọn sử dụng theo công thức tổng quát: {n,m}, đại diện cho việc ký tự đằng trước nó có thể xuất hiện tối thiểu n lần vào tối đa m lần. n và m là số nguyên dương và n <= m.
- Nếu bỏ trống n, giá trị này mặc định bằng 0.
- Nếu bỏ trống m, giá trị này mặc định là vô hạn.
```text
ma?n
    mn	Khớp vì ký tự trước ? có thể không xuất hiện
    man	Khớp vì có xuất hiện đầy đủ các ký tự
    maaaan	Không khớp vì ký tự trước ? chỉ có thể xuất hiện 1 lần
    main	Không khớp vì không giống pattern, n không nằm kế a
    woman	Khớp vì có xuất hiện đầy đủ các ký tự
```

