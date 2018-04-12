## 算法小结
--------------
> 性能优先时，使用循环算法，代码简洁优先时，使用递归算法

// 循环算法  计算N的阶乘
```javascript
function factorial(n) {
	var result = 1;
	for (var i = 1;i <= n; i ++) {
		result *= i;
	}	
	return result;
}
```

// 递归算法  计算N的阶乘
```javascript
function factorial(n) {
    if (n === 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}
```

