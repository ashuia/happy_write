## 正则基础与实例分析

* `\d` 匹配数字
* `\s` 匹配不可见字符，比如空白符、包括空格、制表符(Tab)、换行符或中文全角空格等
* `\w` 匹配可见字符，比如字母、数字、下划线或汉字
* `\b` 匹配**单词**的开始或结束
* `^` 匹配**字符串**的开始
* `$` 匹配**字符串**的结束
. 匹配除换行符以外的任意字符
* `*` 匹配任意次(不含0次)
* `+` 匹配任意次(含0次)
* `?` 匹配0次或一次

#### `[]` 的使用
> `[1aA]` 只能匹配1或a或A
>
> `[1-9]` 匹配1到9的数字
>
> `[^1aA]` 匹配除1、a和A的字符

### 示例

#### `\bhi\b.*\bLucy\b`

> .表示出换行符外的任意字符，*为前一个可以匹配任一次数，`.*`为任意数量的字符,\b为元字符，代表着单词的开始或结束。
```javascript
/\bhi\b.*\bLucy\b/.test('hi haha Luck'); //true
```

#### `0\d{2}-\d{8}`

> \d表示数字，{3}表示前一个匹配3次。
```javascript
/0\d{3}-\d{8}/.test('0571-88909090'); //true
```

#### `^\d{5,12}$`

> {5,12}表示匹配至少5次，至多12次。
```javascript
/^\d{5,12}$/.test('12345'); //true
/^\d{5,12}$/.test('1234'); //false
```

#### js 中正则的使用方法。
1. test方法
> `re.test(str);` //符合返回true，不符合返回false
2. exec方法
> `re.exec(str);` //符合返回符合的字符串，不符合返回null
3. match方法