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

# Function Statements và Function Expressions

Expression: là một đoạn code dẫn đến một giá trị. Nó không cần phải lưu biến.

```javascript
a = 3; // trả về giá trị 3
1 + 2; // trả về 3 nhưng không lưu nó vào
```

Giá trị có thể là Number, String, Object, ...Đây là ví dụ về Expression

Statement: không có trả về giá trị ví dụ như if

```javascript
var a;
if (a === 3) {
}
```

If là statement và bên trong lệnh If đó là Expression

Một ví dụ khác:

```javascript
function greet() {
  console.log("hi");
}
```

Hàm greet chỉ là một Statements vì khi chạy không có một giá trị gì trả về. Và khi JS Engine thấy nó sẽ bỏ nó vào bộ nhớ và được hoisted trong Createtion Phase ở Execution Context vì vậy có thể sử dụng trươc khi nó được định nghĩa.

```javascript
var anonymousGreet = function () {
  console.log("hi");
};
```

Nhìn chúng có vẻ giống nhau nhưng thực chất là khác nhau. Ví dụ dưới này là Function Expression. Vì sao? Lý do nó trả về giá trị, trong JS Function cũng là một object, và ở đây là anonymous function (không có tên) và sau khi khởi tạo nó trả về kết quả là object và gán vào biến anonymousGreet. Vì vậy ở đây đã trả về kết quả nên nó là Function Expression. Cách gọi nó cũng y như trên đó là `anonymousGreet()`.

![04](04.png)
Cách khởi tạo hàm trên

![05](05.png)
Cách khởi tạo hàm dưới

```javascript
anonymousGreet(); // sẽ không chạy vì biến này chỉ mới khởi tạo giá trị và không gán => Lỗi undefined is not a function

var anonymousGreet = function () {
  console.log("hi");
};

anonymousGreet(); // hi
```

Một ví dụ khác

```javascript
function log(a) {
  console.log(a);
}

log(3); // 3
log("Hi"); // Hi
log({ num: 3 }); // Object { num: 3 }
log(function () {
  console.log("a");
}); // Object function

function log(a) {
  a(); // Đây là cách chạy khi chúng ta truyền function vào tham số
}
```

# BY VALUE VÀ BY REFENRCE

Ví dụ về BY VALUE

Ta có một biến a là kiểu Primitive Value. Khi biến a khởi tạo và có giá trị nó sẽ có một địa chỉ trong bộ nhớ. Và chúng ta có thể `b = a` hoặc truyền a vào hàm b `b(a)`. Nếu nó là kiểu Primitive Value trong JS thì b sẽ copy giá trị của a và được tạo ra một địa chỉ mới. Đây được gọi là BY VALUE.

![06](06.png)

Ví dụ về BY REFENRCE

Tương tự như trên nhưng nó là Object thì sẽ khác
![07](07.png)

Cả 2 biến đều là Object đều trỏ cùng một địa chỉ.

```javascript
// BY VALUE
var a = 3;
var b;

b = a;
a = 2;

console.log(a); // 2
console.log(b); // 3, BY VALUE, đã copy giá trị và có địa chỉ khác với biến a
```

# Mutate

Nó có thể thay đổi một thứ gì đó, "immutate nó không thể thay đổi"

```javascript
// BY REFENRCE
var c = { greeting: "hi" };
var d;

d = c;
c.greeting = "hola"; // Mutate Object

console.log(c); // { greeting: "hola" }
console.log(d); // { greeting: "hola" }

// BY REFENRCE ngay cả khi là tham số
function changeGreeting(obj) {
  obj.greeting = "salu";
}

changeGreeting(d);

console.log(c); // { greeting: "salu" }
console.log(d); // { greeting: "salu" }

c = { greeting: "howdy" }; // toán tử  = đã tạo một địa chỉ mới cho c
console.log(c); // { greeting: "howdy" }
console.log(d); // { greeting: "salu" }
```

# OBJECTS, FUNCTION, THIS

Ở giai đoạn CREATION PHASE sẽ tạo ra:

- VARIABLE ENVIROMENT
- OUTER ENVIROMENT (scope chain => tìm kiếm biến ở các các môi trường khác)
- this

```javascript
console.log(this); // Window (Global Object ở môi trường Browser)

function a() {
  console.log(this);
  this.newVar = "hi";
}

a(); // Window

console.log(newVar); // hi

var b = function () {
  console.log(this);
};

b(); // Window

// => Khi tạo function ở môi trường ngoài thì this là Global Object (window)

var c = {
  name: "Object",
  log: function () {
    console.log(this);
  },
};

c.log(); // Object c => this ở đây là Object c

var d = {
  name: "Object",
  log: function () {
    (this.name = "Updated Object"), console.log(this);
  },
};

d.log(); // Giá trị name trong Object d cũng sẽ thay đổi

var e = {
  name: "Object",
  log: function () {
    (this.name = "Updated Object"), console.log(this);

    var setName = function (name) {
      this.name = name; // this ở đây là Global (Window) chứ không phải object e
    };

    setName("Updated Object Again!");
  },
};

e.log(); // name = "Updated Object"
console.log(name); // Updated Object Again!

// Có một pattern có thể khắc phục vấn đề này
var f = {
  name: "Object",
  log: function () {
    var self = this;
    (self.name = "Updated Object"), console.log(this);

    var setName = function (name) {
      self.name = name;
    };

    setName("Updated Object Again!");
  },
};

f.log(); // Updated Object Again! Kết quả như ý của chúng ta.
```

# ARRAY

Trong JS là một Collection của tất cả mọi thứ

```javascript
var arr = [1, 2, 3];
var arr2 = ["a", 1, { greeting: "hi" }];
var arr3 = [
  1,
  false,
  {
    name: "Thao",
  },
  function (name) {
    var greeting = "Hello ";
    console.log(greeting + name);
  },
];

arr3[3](arr3[2].name); // Hello Thao
```

# _arguments_ và spread

Trong giai đoạn CREATION PHASE sẽ tạo ra:

- Variable Enviroment
- Outer Enviroment
- this
- arguments (chứa toàn bộ tham số khi truyền vào function)

arguments: một tên khác khi chúng ta truyền parameter vào function.

```javascript
function greet(firstname, lastname, language) {
  console.log(firstname);
  console.log(lastname);
  console.log(lastname);
}

greet(); // undefined
greet("John", "Doe", "en"); // console.log(arguments) => ['John', 'Doe', 'en']. arguments giống array nhưng không phải array
```

# Và về Spread

```javascript
function greet(firstname, lastname, language, ...otherParams) {
  console.log(otherParams);
}

greet("a", "b", "c", "d", "e"); // ['d', 'e']
```

# Overloading

Ở những ngôn ngữ khác sẽ có Function Overload (cùng tên nhưng khác tham số) nhưng JS thì không có. Có 1 cách để chúng ta hiện thực nó.

![08](08.png)

# Syntax Parser More

- Đọc code của chúng ta kiểm tra xem có đúng ngữ pháp hay không? Nếu không đúng thì sẽ throw Error
- Khi đọc thì sẽ đọc từng ký tự và sẽ giả định nếu đúng theo như nó giả định thì chương trình sẽ chạy.
- Trong quá trình Syntax Parser, chương trình có thể thay đổi chứ không nhất thiết phải như chương trình cũ.

# Syntax Parser tự động thêm dấu ;

Khi chúng ta viết Code thì nó sẽ tự động thêm dấu ; vào cho chúng ta.

```javascript
function getPerson() {
  return
  {
    firstname: 'Thao',
  }
}

console.log(getPerson()); // undefined
```

Lý do return undefined vì nó tự thêm dấu ; vào return. Cách để hạn chế đó.

```javascript
function getPerson() {
  return {
    firstname: "Thao",
  };
}

console.log(getPerson()); // { firstname: 'Thao' }
```

Thì sẽ ra đúng kết quả chúng ta mong muốn.

# White Space

Chỉ là khoảng trắng khi chúng ta xuống hàng, nhấn Tab hoặc khoảng trắng.

# Immediately Invoked Functions Expressions (IIFEs)

Là Function sẽ được chạy ngay lập tức sau khi nó được khởi tạo.

```javascript
var greeting = function(name) {
  console.log(`Hello ${name}`)
}('John'); // Hello John => đây là string chứ không còn là function nữa

3; // hợp lệ vẫn chạy được không báo lỗi

"I am a string"; // hợp lệ

function(name) {
  return `Hello ${name}`;
} // sẽ báo lỗi vì syntax parser sẽ ngầm hiểu nó là function statement nên sẽ cần một cái tên

(function(name) {
  return `Hello ${name}`;
})('John'); // Hello John => hợp lệ vì nó đã là function expresssion
```

# Framework Aside IIFEs và Safe Code

```javascript
(function (name) {
  var greeting = "Hello";
  console.log(greeting + " " + name);
})("John"); // Hello John
```

![09](09.png)

Nó tạo ra một Execution Context và tạo ra một biến greeting mà không ảnh hưởng gì đến global

```javascript
var greeting = "Hola";

(function (name) {
  var greeting = "Hello";
  console.log(greeting + " " + name);
})("John"); // Hello John

console.log(greeting); // Hola
```

![10](10.png)

Nó sẽ không chạm vào biến greeting vì môi trường thực thi của nó khác nhau. Một thằng ở Global 1 thằng ở trong chính nó.

![11](11.png)

Cách để sử dụng Global Object để truy cập nó.

# Closures

```javascript
function greet(whattosay) {
  return function (name) {
    console.log(whattosay + " " + name);
  };
}
```

Chúng ta định nghĩa hàm Greet và nó trả về một hàm (trong JS hàm cũng là Object nên có thể trả về được).

Nếu chúng ta gọi làm thế này `greet("Hi")("Thao")` thì kết quả sẽ là `Hi Thao`. Đúng như chúng ta dự kiến. Nhưng hãy xem đoạn code dưới.

```javascript
var sayHi = greet("Hi");
sayHi("Thao"); // Hi Thao
```

Kết quả vẫn như trên. Theo như chúng ta học khi một hàm thực thi sẽ tạo ra Execution Context. Sau khi thực thi xong nó sẽ bị pop ra khỏi stack. Nhưng sau khi hàm greet thực thi xong tại sao nó vẫn biết biến `whattosay` ở đâu mà nó lấy giá trị và kết quả của hàm vẫn đúng như ý của ta. Lý do là vì `Closure`.

![12](12.png)

Hàm `greet` đã bị pop ra khỏi stack nhưng các giá trị biến của nó vẫn còn trong memory. Vì vậy khi mà hàm thực thi nó muốn tìm kiếm biến `whattosay` thì nó phải `scope chain` và ra khỏi outer enviroment để tìm kiếm biến `whattosay` và nhờ `Closure` của JS mà code của chúng ta hoạt động như ý muốn của mình.

Một ví dụ khác

```javascript
function buildFunctions() {
  var arr = [];

  for (var i = 0; i < 3; i++) {
    arr.push(function () {
      console.log(i);
    });
  }

  return arr;
}

var fs = buildFunctions();

fs[0](); // 3
fs[1](); // 3
fs[3](); // 3
```

Cả 3 hàm trong Arr đều giá trị là 3 vì khi mà thực thi xong hàm buildFunctions thì giá trị của `i = 3`. Và khi thực thi hàm thì nó sẽ ra `outer enviroment` và tìm kiếm `i` và in ra nó. Vì vậy khi in giá trị sẽ là `3` ở cả 3 function.

# Function Factory

```javascript
function makeGreeting(language) {
  return function (firstname, lastname) {
    if (language === "en") {
      console.log("Hello " + firstname + " " + lastname);
    }

    if (language === "es") {
      console.log("Hola " + firstname + " " + lastname);
    }
  };
}

var greetingEnglish = makeGreeting("en");
var greetingSpanish = makeGreeting("es");

greetEnglish("John", "Doe"); // Hello John Doe
greetingSpanish("John", "Doe"); // Hola John Doe
```

![13](13.png)
Đây là cách nó tạo ra Closure khi chạy 2 hàm greetEnglish và greetSpanish

# Closure và Callback

```javascript
function sayHiLater() {
  var greeting = "Hi";

  setTimeout(function () {
    console.log(greeting);
  }, 3000);
}

sayHiLater(); // Hi

function tellMeWhenDone(callback) {
  var a = 1000;
  var b = 2000;

  callback();
}

tellMeWhenDone(function () {
  console.log("I am done");
});
```

Sau 3 giây thì in ra `Hi`. Nhưng thực chất nó đã tạo ra Closure vì nếu không có Closure thì biến greeting chúng ta đã không có.

Và callback cũng là một hình thức khác của closure

# bind, call, apply

Khi một hàm được tạo ra mặc định nó sẽ có 3 methods (tất cả các hàm đều có 3 methods này) đó là: call, apply, bind

```javascript
var person = {
  firstname: "John",
  lastname: "Doe",
  getFullName: function () {
    return this.firstname + " " + this.lastname;
  },
};

var logName = function (lang1, lang2) {
  console.log("Logged: " + this.getFullName()); // this ở đây là global object chứ không phải person
};

var logPersonName = logName.bind(person); // bind ở đây là nó sẽ gắn this thành person, bind sẽ trả về một object mới

logPersonName(); // Loggedd: John Doe

/**
  Call và Apply chỉ khác cách truyền tham số vào
*/
logName.call(person, "en", "es"); // Loggedd: John Doe
logName.apply(person, ["en", "es"]); // Loggedd: John Doe

// Một cách sử dụng khác
(function (lang1, lang2) {
  console.log("Logged: " + this.getFullName()); // this ở đây là global object chứ không phải person
}.apply(person, ["en", "es"]));

// function borrowing
var person2 = {
  firstname: "Jane",
  lastname: "Doe",
};

console.log(person.getFullName.apply(person2)); // Jane Doe

// function currying: tạo ra một bản copy của một hàm nhưng đã có một vài tham số có giá trị sẵn
function multiply(a, b) {
  return a * b;
}

var multipleByTwo = multiply.bind(this, 2); // trở thành multiply(2, b)
console.log(multipleByTwo(4)); // 8
```

# Functional Programming

```javascript
var numbers = [1, 2, 3];

// Ví dụng chúng ta muốn tạo một mảng mới có giá trị x2 của mảng numbers
var numbersByTwo = [];

for (var i = 0; i < numbers.length; i++) {
  numbersByTwo = numbers[i] * 2;
}

console.log(numbersByTwo); // [2,4,6]

// Và nếu chúng ta muốn làm một việc khác với từng phần tử mảng thì chúng ta phải lặp lại code. Và nhờ Javascript là ngôn ngữ First Class Function nên chúng ta có thể tận dụng nó tạo một hàm sau
function mapForEach(arr, fn) {
  var newArr = [];

  for (var i = 0; i < arr.length; i++) {
    newArr.push(fn(arr[i]));
  }

  return newArr;
}

var numbersByTwo = mapForEach(numbers, function (number) {
  return number * 2;
});

console.log(numbersByTwo); // [2, 4, 6] -> cùng kết quả nhưng code clean hơn và hơn thế nữa chúng ta có thể có những logic khác.

var numbersLargerThanTwo = mapForEach(numbers, function (number) {
  return number > 2 && number;
});

console.log(numbersLargerThanTwo); // [3] -> đây là một ví dụ đơn giản về Functional Programing. Một cách khác để viết hàm trên.

var checkPastLimit = function (limiter, item) {
  return item > limiter && item;
};

var numbersLargerThanOne = mapForEach(numbers, checkPastLimit.bind(this, 1));

// Một phiên bản đơn giản hơn
var checkPastLimitSimplified = function (limiter) {
  return function (limiter, item) {
    return item > liminter && item;
  }.bind(this, limiter);
};

var numbersLargerThanOne = mapForEach(numbers, checkPastLimitSimplified(1));
```

Một trong những thư viện đó là lodash, underscorejs, ... đại diện cho Functional Programing
