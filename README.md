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
a{2,3}
    abc dat	Không khớp vì không thỏa mãn điều kiện
    abc daat	Khớp vì có xuất hiện 2 ký tự a (daat)
    aabc daaat	Khớp vì có xuất hiện 2 và 3 ký tự a (aabc và daaat)
    aabc daaaat	Khớp vì có xuất hiện 2 và 3 ký tự a (aabc và daaaat)
```
- RegEx [0-9] {2, 4} này khớp với chuỗi có tối thiểu 2 chữ số và tối đa không quá 4 chữ số.
```text
[0-9]{2,4}
    ab123csde	Khớp vì thỏa mãn điều kiện: ab123csde
    12 and 345673	Khớp vì thỏa mãn điều kiện: 12 và 345673
    1 and 2	Không khớp vì chuỗi chỉ có 1 chữ số
```
# 9 Dấu | : Biểu tượng dấu sổ dọc | này có thể khớp với chuỗi tồn tại 1 trong 2 ký tự được định nghĩa trước và sau nó.
```text
a|b
    cde	Không khớp vì a, b đều không xuất hiện
    ade	Khớp vì thỏa mãn điều kiện, có a xuất hiện: ade
    acdbea	Khớp vì thỏa mãn điều kiện, a và b đều xuất hiện: acdbea
```
- Ở đây, a|b khớp với bất kỳ chuỗi nào chứa a hoặc b
- # 10 Dấu () : Dấu ngoặc đơn () được sử dụng để gom nhóm các pattern lại với nhau, chuỗi sẽ khớp với biểu thức chính quy bên trong dấu ngoặc này.
- Ví dụ: (a|b|c)xz khớp với bất kỳ chuỗi nào có a hoặc b hoặc c đứng trước xz
```text
(a|b|c)xz
    ab xz	Không khớp vì a hay b có đứng trước nhưng không liền với xz
    abxz	Khớp vì thỏa mãn điều kiện, có b xuất hiện sát trước xz: abxz
    axz cabxz	Khớp vì thỏa mãn điều kiện, cả a và b đều xuất hiện sát trước xz: axz cabxz
```
# 11 Dấu \ : Dấu gạch chéo ngược được sử dụng để thoát các ký tự đặc biệt, nghĩa là khi đứng trước một kí tự đặc biệt, \ sẽ biến kí tự này thành một kí tự thường, bạn có thể tìm kiếm kí tự đặc biệt này trong chuỗi như các kí tự thường khác.
- Một số pattern đi với \
- 1 \A - Khớp với các ký tự theo sau nó nằm ở đầu chuỗi.
```text
\Athe
    the sun	Khớp vì the nằm ở đầu chuỗi
    In the sun	Không khớp vì the không nằm ở đầu chuỗi
```
- 2 \b - Khớp với các ký tự được chỉ định nằm ở đầu hoặc cuối của từ.
```text
\bfoo
    football	Khớp vì thỏa mãn điều kiện, foo nằm ở đầu chuỗi
    a football	Khớp vì thỏa mãn điều kiện, foo nằm ở đầu từ thứ 2 trong chuỗi
    afootball	Không khớp vì foo nằm ở giữa từ trong chuỗi.
foo\b
    the afoo test	Khớp vì thỏa mãn điều kiện, foo nằm ở cuối từ thứ 2 trong chuỗi
    the afootest	Không khớp vì foo nằm ở giữa từ trong chuỗi.
```
- 3 \B - Trái ngược với \b, khớp với các ký tự được chỉ định không nằm ở đầu hoặc cuối của từ.
```text
\Bfoo
    football	Không khớp vì foo nằm ở đầu chuỗi
    a football	Không khớp vì foo nằm ở đầu từ thứ 2 trong chuỗi
    afootball	Khớp vì foo nằm ở giữa từ trong chuỗi.
foo\B
    the foo	Không khớp vì foo nằm ở cuối chuỗi
    the afoo test	Không khớp vì foo nằm ở cuối từ thứ 2 trong chuỗi
    the afootest	Khớp vì foo nằm ở giữa từ trong chuỗi.
```
- 4 \d - Khớp với các ký tự là chữ số, tương đương với [0-9]
```text
\d
    12abc3	Khớp vì thỏa mãn điều kiện: 12abc3
    Python	Không khớp vì không có số nguyên nào xuất hiện
```
- 5 \D - Khớp với các ký tự không phải số, tương đương với [^0-9]
```text
\D
    1ab34"50	Khớp vì thỏa mãn điều kiện: 1ab34"50
    1345	Không khớp vì chuỗi toàn số nguyên xuất hiện
```
- 6 \s - Khớp với bất kỳ ký tự khoảng trắng nào, tương đương với [ \t\n\r\f\v]
```text
\s
    Python RegEx	Khớp vì chuỗi có khoảng trắng
    PythonRegEx	Không khớp vì chuỗi không có khoảng trắng
```
- 7 \S - Khớp với bất kỳ ký tự nào không phải khoảng trắng, tương đương với [^ \t\n\r\f\v]
```text
\S
    a b	Khớp vì chuỗi có ký tự a b
        Không khớp vì chuỗi toàn bộ là khoảng trắng
```
- 8 \w - Khớp với bất kỳ ký tự chữ cái và chữ số nào, tương đương với [a-zA-Z0-9_]
- Lưu ý: Dấu gạch dưới _ cũng được coi là một ký tự chữ cái và chữ số.
```text
\w
    12&": ;c	Khớp vì chuỗi có ký tự chữ và số 12&": ;c
    %"> !	Không khớp vì chuỗi không có ký tự chữ và số
```
- 9 \W - Khớp với bất kỳ ký tự nào không phải là chữ cái và chữ số, tương đương với [^a-zA-Z0-9_]
```text
\w
    1a2%c	Khớp vì chuỗi có ký tự không phải chữ và số 1a2%c
    Python	Không khớp vì chuỗi chỉ có ký tự chữ cái
```
