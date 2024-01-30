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
# Regular Expression trong Python
- **re.findall()**
- Phương thức re.findall() trả về một danh sách các chuỗi chứa tất cả các kết quả khớp với pattern đưa ra.
- findall(partern, string)
    - pattern là RegEx.
    - string là chuỗi cần so khớp
- Ví dụ: Trích xuất các số từ chuỗi cho trước sau: "hello 12 hi 89. Howdy 34"
```text
import re

string = 'hello 12 hi 89. Howdy 34'
pattern = '\d+'

result = re.findall(pattern, string) 
print(result)
```
- Kết quả trả về: ['12', '89', '34']
- **re.split()**
- Phương thức re.split() dùng biểu thức chính quy để ngắt chuỗi thành các chuỗi con và trả về danh sách các chuỗi con này.
- re.split(pattern, string, maxsplit)
    - pattern là RegEx.
    - string là chuỗi cần so khớp
    - maxsplit (số nguyên) là số chuỗi tối đa sẽ được ngắt. Nếu để trống thì Python sẽ so khớp và cắt tất cả các chuỗi đạt điều kiện.
- Ví dụ: Ngắt tại vị trí có ký tự khoảng trắng:
```text
import re

string = 'The rain in Vietnam.'
pattern = '\s'

result = re.split(pattern, string) 
print(result)
```
- Kết quả trả về: ['The', 'rain', 'in', 'Vietnam.']
- Ví dụ: Ngắt chuỗi ở ký tự khoảng trắng đầu tiên:
```text
import re

string = 'The rain in Vietnam.'
pattern = '\s'

result = re.split(pattern, string, 1) 
print(result)
```
- Kết quả: ['The', 'rain in Vietnam.']
- Nếu không tìm thấy pattern, re.split() trả về danh sách chứa chuỗi rỗng.
- **re.sub()**
- Re.sub() sẽ thay thế tất cả các kết quả khớp với pattern trong chuỗi bằng một nội dung khác được truyền vào và trả về chuỗi đã được sửa đổi.
- re.sub(pattern, replace, string, count)
    - pattern là RegEx.
    - replace là nội dung thay thế cho chuỗi kết quả khớp với pattern
    - string là chuỗi cần so khớp
    - count (số nguyên) là số lần thay thế. Nếu để trống thì Python sẽ coi giá trị này bằng 0, so khớp và thay thế tất cả các chuỗi đạt điều kiện
- Ví dụ: Code chương trình xóa tất cả các khoảng trắng
```text
import re

# chuỗi nhiều dòng
string = 'abc 12\
de 23 \n f45 6'

# so khớp các ký tự khoảng trắng
pattern = '\s+'

# chuỗi rỗng
replace = ''

new_string = re.sub(pattern, replace, string) 
print(new_string)
```
- Kết quả trả về: abc12de23f456
- 
- Ví dụ: Code chương trình xóa 2 khoảng trắng đầu tiên
```text
import re

# chuỗi nhiều dòng
string = 'abc 12\
de 23 \n f45 6 \n website'

# so khớp các ký tự khoảng trắng
pattern = '\s+'
replace = ''

new_string = re.sub(r'\s+', replace, string, 2) 
print(new_string)
```
- Kết quả trả về: abc12de23 f45 6 website
- **re.search()**
- Phương thức re.search() sử dụng để tìm kiếm chuỗi phù hợp với pattern RegEx. Nếu tìm kiếm thành công, re.search() trả về đối tượng khớp, nếu không, nó trả về None
- search(pattern, string)
    - pattern là RegEx.
    - string là chuỗi cần so khớp
```text
import re

string = "thonv12 hello"

# Kiem tra xem 'thonv12' co nam o dau chuoi khong
match = re.search('\Athonv12', string)

if match: # nếu tồn tại chuỗi khớp
  print("Tim thay 'thonv12' nam o dau chuoi") # in ra thong bao nay
else:
  print("'thonv12' khong nam o dau chuoi") # khong thi in ra thong bao nay
````
- Ở ví dụ này, match chứa đối tượng phù hợp khớp với pattern.
# **Một số phương thức và thuộc tính thường được sử dụng với đối tượng match**
- **match.group()**
- Phương thức group() trả về những phần của chuỗi khớp với pattern.
  ```text
  import re

string = '39801 356, 2102 1111'

pattern = '(\d{3}) (\d{2})'

match = re.search(pattern, string)

if match: #nếu tồn tại chuỗi khớp
  print(match.group()) # in ra kết quả
else:
  print("Không khớp") # Không thì hiện thông báo

# Output: 801 35
  ```
- Ở đây, biến match chứa đối tượng match.
- Ta có pattern là (\d{3}) (\d{2}) chia làm hai nhóm nhỏ (\d{3}) và (\d{2}). Bạn có thể nhận được một phần của chuỗi tương ứng với các nhóm con trong ngoặc đơn này như sau:
```text
>>> match.group(1)
'801'

>>> match.group(2)
'35'

>>> match.group(1, 2)
('801', '35')

>>> match.groups()
('801', '35')
```
- **match.start()**
- Hàm start() trả về chỉ mục bắt đầu của chuỗi con phù hợp. Tương tự, end() trả về chỉ mục kết thúc của chuỗi con phù hợp.
```text
>>> match.start()
2
>>> match.end()
8
```
- Hàm span() trả về tuple chứa chỉ mục bắt đầu và kết thúc của phần chuỗi phù hợp.
```text
>>> match.span()
(2, 8)
```
- **match.re và match.string**
- Thuộc tính re của đối tượng match sẽ trả về một biểu thức chính quy. Tương tự, thuộc tính string trả về chuỗi đã được truyền trong đoạn code.
```text
>>> match.re
re.compile('(\\d{3}) (\\d{2})')
>>> match.string
'39801 356, 2102 1111'
```
- **Sử dụng tiền tố r trước RegEx**
- Khi tiền tố r hoặc R được sử dụng trước một biểu thức chính quy đại diện cho việc chuỗi tiếp sau nó chỉ là những ký tự bình thường.
- Ví dụ: '\n' là một dòng mới newline, còn r'\n' có nghĩa là chuỗi bao gồm hai ký tự: dấu gạch chéo ngược \ và n
- Dấu gạch chéo ngược \ được sử dụng để thoát các ký tự như đã nói ở trên. Tuy nhiên, sử dụng tiền tố r trước \ thì nó chỉ là một ký tự bình thường.
```text
import re

string = '\n and \r are escape sequences.'

result = re.findall(r'[\n\r]', string) 
print(result)

# Output: ['\n', '\r']
```
- **Chuỗi Raw bằng tiền tố r**
- RegEx dùng dấu gạch chéo ('\') để chỉ các biểu mẫu đặc biệt hoặc cho phép các ký tự đặc biệt được dùng mà không cần gọi ý nghĩa đặc biệt của chúng. Mặt khác, Python dùng ký tự giống ký tự thoát. Vì thế, Python dùng ký hiệu chuỗi thô.
- Một chuỗi trở thành chuỗi thô nếu nó có tiền tố r hoặc R trước các biểu tượng trích dẫn. Vì thế, ‘Hello’ là chuỗi bình thường, còn r’Hello’ là một chuỗi thô.
```text
>>> normal="Hello"
>>> print (normal)
Hello
>>> raw=r"Hello"
>>> print (raw)
Hello
```
- Ở những trường hợp bình thường, cả hai không có sự khác biệt. Tuy nhiên, khi ký hiệu thoát được nhúng vào chuỗi, chuỗi bình thường thực sự diễn giải chuỗi thoát, nơi mà chuỗi thô không xử lý ký tự thoát.
```text
>>> normal="Hello\nWorld"
>>> print (normal)
Hello
World
>>> raw=r"Hello\nWorld"
>>> print (raw)
Hello\nWorld
```
- Ở ví dụ trên khi một chuỗi bình thường được in, ký tự thoát '\n' được xử lý để giới thiệu một dòng mới. Tuy nhiên, do toán tử chuỗi thô 'r' nên hiệu ứng của ký tự thoát không được dịch theo nghĩa của nó.
