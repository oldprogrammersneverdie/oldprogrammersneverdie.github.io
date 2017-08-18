---
title: Javascript | Method filter trong javascript hữu ích như thế nào?
description: Javascript | Method filter trong javascript hữu ích như thế nào?
header: Javascript | Method filter trong javascript hữu ích như thế nào?
---
Trong ví dụ này tôi sẽ giới thiệu cho bạn cách dùng method filter trong Javascript hiệu quả như thế nào.

Đầu tiên tôi xét tình huống như sau:

Tôi có một Array Cha: 

``` javascript
var arr = [
    {"name":"apple", "count": 2},
    {"name":"orange", "count": 5},
    {"name":"pear", "count": 3},
    {"name":"orange", "count": 16},
];

```
Giờ tôi muốn set lại một Array mới loại một object trong arr Cha đi, cụ thể là `apple`:
vậy nếu không sử dụng `filter` method thì sao :

### ex1: Trường hợp không xài filter.

{% highlight javascript linenos %}

var arr = [
    {"name":"apple", "count": 2},
    {"name":"orange", "count": 5},
    {"name":"pear", "count": 3},
    {"name":"orange", "count": 16},
];
    
var newArr = [];

for(var i= 0, l = arr.length; i< l; i++){
    if(arr[i].name === "orange" ){
		newArr.push(arr[i]);
	}
}

console.log("Filter results:",newArr);

{% endhighlight %}

### ex2: Trường hợp xài filter.

{% highlight javascript linenos %}

var arr = [
    {"name":"apple", "count": 2},
    {"name":"orange", "count": 5},
    {"name":"pear", "count": 3},
    {"name":"orange", "count": 16},
];
    
var newArr = arr.filter(function(item){
    return item.name === "orange";
});

console.log("Filter results:",newArr);

{% endhighlight %}


Vậy cái nào ngon hơn... Chưa biết ví dụ nào ngon nhưng tôi thấy ex2 gọn code rồi đó :d 