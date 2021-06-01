# Objects và Functions

Object và Function có liên quan mật thiết với nhau

# Object và Dot

Object có thể chứa `Primitive "property"` và có thể có `Object "property"` và có thể chứa `Function gọi là "method"`. Tất cả các Object đều nằm trong bộ nhớ máy tính.

```javascript
var person = new Object();

person["lastname"] = "Thao"; // truy cập vào Object và gán giá trị. Nếu không có property lastname thì sẽ tạo ra. Hoặc
person.firstname = "Y"; // cách này tương tự như cách trên nhưng dễ đọc hơn.

var firstNameProperty = "firstname";

console.log(person[firstNameProperty]);

person.address = new Object(); // Trong object person ta tạo thêm object mới là address
person.address.street = "111 Main St."; // thứ tự toán tử . là từ trái qua phải. Vì vậy nó sẽ tìm address trong bộ nhớ và sau đó truy cập thêm.
```

# Objects và Object Literals ({})

Cách để tạo Object một cách đơn giản hơn và dễ đọc hơn là:

```javascript
var person = {};
person.firstname = "Thao";
person.lastname = "Y";
```

Hoặc

```javascript
var person = { firstname: "Thao", lastname: "Y" };
```

Từ đó chúng ta có thể mở rộng hơn. Chúng ta có thể thêm property cho object như dưới đây:

```javascript
person.address = {
  street: "111 Main St",
  city: "New York",
};
```

# Framework Aside Faking Namespaces

Namespace: là một container chứa biến và hàm. Thông thường người ta sẽ giữ những hàm và biến có cùng tên tách biệt nhau. Hãy xem ví dụ dưới:

```javascript
var english = {
  greetings: {
    basic: "Hello",
  },
};

var spanish = {
  greetings: {
    basic: "Hola",
  },
};
```

Cả english và spanish đều có các property giống nhau nhưng giá trị khác nhau. Đây là đặc điểm chủ yếu của namespace.

# JSON và Object Literals

Lý do người ta tạo ra JSON (JavaScipt Object Notation):

- Khi chưa có JSON người ta truyền dữ liệu từ server xuống client bằng XML nhưng XML lại tốn quá nhiều băng thông.
- Khi người ta thấy Object của JS rất tốt vì thế người ta đã sinh ra JSON để giải quyết vấn đề của XML.

Tất cả các JSON đều ra Object trong JS nhưng không phải tất cả các Object trong JS đều là JSON. Xem ví dụ dưới đây:

```javascript
var objectLiteral = {
  firstname: "Thao",
  isProgramer: true,
};

var jsonValue = {
  firstname: "Thao",
  isProgramer: true,
};
```

JSON trong phần key phải được bọc vào trong `"`. Và trong JS có JSON Object có 2 hàm đó là: `JSON.stringify(Object)` chuyển Object thành string và `JSON.parse(String)` chuyển String thành Object.

# Functions là Objects

First Class Function: trong JS Function là Object. First Class Function có nghĩa là tất cả những gì chúng ta làm được với các kiểu dữ liệu khác chúng ta có thể làm nó với Function. Ví dụ như gán một biến, truyền nó, tạo ra nó.

Function là một kiểu dữ liệu đặc biệt của Object

- Gán Primitive
- Gán Object
- Gán nó một hàm.
- Một trong 2 property bị giấu đó là Name (Tên) có thể Function không có Name gọi là anonymous
- Một Property khác là Code (những dòng code ta viết) và có Property này đặc biệt có thể chạy được (()).

```javascript
function greet() {
  console.log("Hi");
}

greet.language = "English";

console.log(greet.language); // English
```

Khi chúng ta tạo hàm greet, hàm greet này sẽ nằm trong bộ nhớ. Trong trường hợp này nó nằm ở Global Object. Có Property Name là greet, Property Code `console.log('Hi')`. Chúng ta nên suy nghĩ Function như một Container chứa code.
