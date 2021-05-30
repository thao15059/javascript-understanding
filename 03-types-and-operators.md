# Types và Javascript

Dynamic Typing: chúng ta không cần nói Javascript Engine là biêns này kiểu dữ liệu là gì thay vào đó Engine sẽ biết kiểu dữ liệu của biến khi chạy. Vì vậy biến của chúng ta có thể giữ nhiều kiểu dữ liệu khác nhau. Và sự thật là Javascript là ngôn ngữ lập lập dynamic typing.

# Primitive Types

Là những kiểu dữ liệu chỉ đại diện cho một giá trị duy nhất. Không đại diện cho object.

Hiện tại Javascript có 7 Primitive Types:

- undefined: đại diện cho cái gì đó không tồn tại (một biến nào đó chưa gán giá trị cho nó)
- null: đại diện cho cái gì đó không tồn tại (bản thân nó không có giá trị)
- boolean: true hoặc false
- number: đại diện cho số cả số thực và số nguyên.
- string: đại diện cho mỗi chuỗi ký tự (có thể sử dụng ' hoặc ")
- symbol:
- BigInt: đại diện cho số sử dụng trong tính toán chính xác.

# Operators

Là một hàm đặc biệt có cú pháp (cách viết) không giống bình thường. Thông thường toán tử sẽ nhận 2 tham số và trả về một kết quả.

```javascript
var sum = 3 + 4;
console.log(sum); //7
```

Chúng ta phải hỏi bản thân là tại sao Javascript biết cái toán tử + và làm phép toán +.

Thông thường nếu hàm của chúng ta là +(3, 4) hoặc +3 4 thì chúng ta gọi là prefix notation.

Thông thường nếu hàm của chúng ta là (3, 4)+ hoặc 3 4+ thì chúng ta gọi là postfix notation.

Thay vào đó nếu chúng ta viết 3 + 4 thì chúng ta gọi là infix notation (ký hiệu infix). Infix có nghĩa là 2 tham số nằm 2 bên và toán tử nằm giữa. Và cách viết này dễ đọc hơn.

Tương tự với các toán tử còn lại.

# Operator Precedence và Associativity

Operator Precedence: Là thứ tự toán tử nào được chạy trước. Các hàm toán tử này đều được chạy dựa vào thứ tự ưu tiên. Cái nào cao hơn sẽ được chạy trước. (Tham khảo ở đây: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

Associativity: Thứ tự mà hàm toán tử được gọi khi thứ tự ưu tiên bằng nhau. Ví dụ như từ trái sang phải hay phải sang trái.

```javascript
var a = 3 + 4 * 5;
console.log(a); // 23 (* có thứ tự ưu tiên cao hơn nên 4 * 5 = 20 và sau đó cộng 3 = 23, sau đó gán 23 vào biến a. Thứ tự trong ví dụ này là * + =)
```

```javascript
var a = 2,
  b = 3,
  c = 4;

a = b = c;

console.log(a);
console.log(b);
console.log(c);
```

Cả 3 toán tử giống nhau nên chỉ xét thứ tự thực hiện. Đối với toán tử = thì thứ tự thực hiện là từ phải sang trái cho nên b = c sẽ thực hiện trước. Là khi toán tử gán sẽ thực thi từ phải qua trái. Giá trị bên phải c = 4, và vì thế b = 4, tương tự a = 4.

# Coercion

Là chuyển đổi một giá trị từ từ kiểu này sang kiểu khác. Nó xảy ra khá thường xuyên trong JS thì JS là dynamic type.

```javascript
var a = 1 + "2";
console.log(a); // 12
```

Kết quả là 12 (string). JS Enginge đã tự hiểu là chúng ta muốn cộng vào và tự động chuyển 1 qua string.

# Comparison Operator (Toán tử so sánh)

Hãy xem qua đoạn code sau:

```javascript
console.log(1 < 2 < 3); // true
```

Kết quả trả ra là true, cùng xem đoạn code khác.

```javascript
console.log(3 < 2 < 1); // true
```

Kết quả vẫn là true. Vì sao???

Lý do là vì nếu ta xét về toán tử < khi có nhiều toán hàng nó sẽ làm từ trái qua phải (vì cùng độ ưu tiên). Vì thế ở ví dụ 1 nó sẽ thực hiện `1 < 2` trước và kết quả trả về `true`. Sau đó nó lại thực hiện tiếp `true < 3`. Do cả `true` và `3` đều không cùng kiểu cho nên nó phải Coercion (ép buộc), trong trường hợp này phải ép buộc `true` về số. Khi ép `true` về số kết quả là `1`. Vì thế so sánh thành `1 < 3` kết quả là true. Tương tự khi áp dụng ví dụ dưới.

Một toán tử khác là `==`. Khi so sánh cũng có Coercion nếu 2 toán hạng không cùng kiểu. Để loại trừ trường hợp này ta sử dụng toán tử `===` thì sẽ không diễn ra Coercion.

# Existence và Booleans

Chúng ta có các giá trị `undefined`, `null`, `""`, `0` khi chuyển những dữ liệu này qua kiểu Boolean, kết quả sẽ là `false`. Chúng ta có thể tận dụng nó để làm những việc về so sánh hay viết code gắn ngon hơn.

```javascript
var a;

if (a) {
  console.log("Something in there");
} else {
  console.log("Nothing in there");
}
```

Khi chúng ta viết toán tử `if` thì ngậm định nó sẽ Coercion hay ép buộc qua Boolean và kiểm tra. Ở đây khi nhớ những bài học trước chúng ta nhớ rằng ở Creation Phase JS Engine sẽ xét tạo bộ nhớ cho biến a và giá trị khi tạo bộ nhớ là `undefined`. Vì vậy khi chạy đoạn code trên kết quả sẽ là `Nothing in there`.

# Default Values (Giá trị mặc định)

Xem ví dụ sau:

```javascript
function greet(name) {
  console.log("Hello " + name);
}

greet("Thao"); // Hello Thao
```

Hoạt động hoàn hảo phải không. Nhưng nếu.

```javascript
function greet(name) {
  console.log("Hello " + name);
}

greet(); // Hello undefined
```

Kết quả sẽ trả về undefined. Đúng như những gì chúng ta đã học. Nó hoạt động không đúng vì vậy có một cách để chúng ta thiết lập giá trị mặc định là:

```javascript
function greet(name) {
  name = name || "<Your name here>";
  console.log("Hello " + name);
}

greet(); // Hello <Your name here>
```

Khi xét về toán tử `||` thì nó sẽ trả về kết quả nào là `true`. Ví dụ `null || 'hello'` thì nó sẽ trả về `hello`. Một ví dụ khác `'hi' || 'hello'` thì sẽ trả về `hi`. Nhờ vậy mà chúng ta có thể thiết lập giá trị mặc định trong hàm.

# Framework Aside Default Values

`index.html`

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <title>FW Aside</title>
  </head>
  <body>
    <script src="lib1.js"></script>
    <script src="lib2.js"></script>
    <script src="app.js"></script>
  </body>
</html>
```

`lib1.js`

```javascript
var libName = "Lib 1";
```

`lib2.js`

```javascript
var libName = "Lib 2";
```

`app.js`

```javascript
console.log(libName);
```

Nếu những đoạn code kia thì chúng ta load index.html ở browser những phải này sẽ chồng lên nhau chứ không phải tạo ra những Execution Context của riêng chúng. Và khi đó chúng ta thấy biến `libName` thuộc về Global Context vì vậy khi `console.log(libName)` kết quả sẽ là `Lib 2`.

`lib2.js`

```javascript
window.libName = window.libName || "Lib 2";
```

Nếu sửa file `lib2.js` lại như trên kết quả sẽ là `Lib 1` đúng như chúng ta mong đợi.

Cách này giống như những framework hay thư viện JS hay làm. giống như jQuery, ...
