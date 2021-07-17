# Classical Inheritance

Inheritance: trong Javascript kế thừa của một object có nghĩa là có thể truy cập vào được đối tượng và phương thức của một object khác.

Classical Inheritance truyền thống chúng ta phải khó quản lý hơn cách mà Javascript quản lý. Với việc kế thừa của Javascript chúng ta có việc dễ mở rộng, linh hoạt và dễ hiểu.

Một số ví dụ về kế thừa:
![14](14.png)

```javascript
// Mỗi obj đều có thuộc tính là __proto__ nếu obj đó có kế thừa từ obj khác khi mà chúng ta truy cập thuộc tính hoặc phương thức của obj thì đầu tiên sẽ tìm trong obj đó, nếu obj đó không có thì sẽ đi tìm trong __pro__ của obj đó, nếu không có nữa sẽ tìm trong __proto__ của những obj mà nó kế thừa

var person = {
  firstname: "Default",
  lastname: "Default",
  getFullName: function () {
    return this.firstname + " " + this.lastname;
  },
};

var john = {
  firstname: "John",
  lastname: "Doe",
};

john.__proto__ = person;

console.log(john.getFullName()); // John Doe, this ở đây là john.
console.log(john.firstname); // John

var jane = {
  firstname: "Jane",
};

jane.__proto__ = person;
console.log(jane.getFullName()); // Jane Default
```

# Tất cả mọi thức trong Javascript đều là Object hoặc primitive

Hầu như tất cả trong Javascript đều là primitive như number, string, boolean, function, array, basic obj, ... Chúng đều có prototype nhưng ngoại trừ đó là base obj trong JS.

```javascript
var a = {};
var b = function () {};
var c = [];

a.__proto__; // là obj cơ bản nhất
b.__proto__; // cũng là obj cơ bản của hàm
c.__proto__; // cũng là prototype của array
```

Nhờ tất cả những thứ này (kế thừa mặc định) mà chúng ta có thể sử dụng những phương thức của các đối tượng này.
