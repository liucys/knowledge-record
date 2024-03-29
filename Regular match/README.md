正则表达式的内容是一段存在于 / / 之间的特殊组合,它描述了一种字符串的匹配模式,可以用来检查一个字符串是否含有某个子串、可以将匹配的子串进行替换等.
正则表达式只能对字符串进行操作

语法：

```javascript
const reg = /正则表达式主体/修饰符(可选);

或者;

// 动态创建正则表达式
const reg = new RegExp("正则表达式主体", "修饰符(可选)");
```

目录

- [了解正则表达式](#11)
- [修饰符](#12)
- [RegExp 对象方法](#13)
- [RegExp 对象属性](#14)
- [字符串可以使用正则表达式的方法](#01)
- [正则表达式主体声明 方括号[ ] 用于表示逻辑 或](#02)
- [正则表达式主体声明 元字符](#03)
- [正则表达式主体声明 量词](#04)
- [正则表达式主体声明 分组`()`](#05)
- [正则表达式主体声明 其他](#09)
- [捕获组](#06)
- [非捕获组](#07)
- [命名捕获组](#08)
- [贪婪与懒惰](#10)

&nbsp;

#### <a name="01">字符串可以使用正则表达式的方法</a>

- search()：该方法用于检索匹配的指定子字符串,若是找到,则返回该子字符串的下标,若是找不到,则返回-1;该方法不执行全局匹配，它将忽略标志`g`。它同时忽略 RegExp 的 `lastIndex`属性，并且总是从字符串的开始进行检索，这意味着它总是返回第一个满足匹配条件的目标的下标位置.

```javascript
const reg = /l/g;
"hello,world".search(reg); // 2
```

- match()：该方法用于检索字符串中指定的子字符串,它将匹配的结果存在一个数组中返回.若是未找到则返回 null;该方法会受到修饰符`g`的影响,若是声明全局修饰符`g`,则返回匹配到的所有,若是没有声明全局修饰符`g`,则返回查找匹配到的第一个.

```javascript
const reg = /l/g;
"hello,world".match(reg); // ["l","l","l"]
```

- replace()：方法用于正则匹配替换,它可以将符合匹配规则的字符替换为新的规定的字符;该方法也受到修饰符`g`的影响,若是声明全局修饰符`g`,则将进行全局匹配替换,若是没有声明全局修饰符`g`,则替换匹配到的第一个.

```javascript
const reg = /l/g;
"love,love,love,you!".replace(reg, "L"); // "Love,Love,Love,you!"
```

&nbsp;

#### <a name="02">正则表达式主体声明 方括号[ ] 用于表示逻辑 或</a>

在`[]`中，特殊字符不需要转义，可以直接使用，比如`[.()]`,但是在外面，是需要转义的`\(` `\.`等

方括号用于声明查找指定范围内的字符

- /[abc]/ ：表示匹配 a b c 这三个字符中的任意

- /[^abc]/ ：表示不匹配 a b c 这三个字符中的任意

- /[a-z]/ ：表示匹配从 a 至 z 中的任意字符

- /[0-9]/ ：表示匹配从 0 至 9 中的任意数字

- /[A-Z]/ ：表示匹配从 大 A 至 大 Z 中的任意字符

- /[A-z]/ ：表示匹配从大 A 至 小 z 中的任意字符

- /(red|pink|blue)/ ：表示匹配圆括号中的 red,pink,blue 这三个单词中的任意一个
  `()也可以用于表示逻辑或`
- ......

&nbsp;

#### <a name="03">正则表达式主体声明 元字符</a>

- ^ ：表示匹配以指定字符内容开头`const reg = /^a/; const reg2 = /^(abc)`

- `$` ：表示匹配以指定字符内容结尾`const reg = /c$/; const reg2 = /(ve)$`

- a | b ：表示匹配字符 a 或者字符 b.`const reg = /red|blue/`

- `.` ：表示匹配除换行符之外的任意单个字符`const reg = /./`

- \w ：表示匹配数字、字母、下划线
  `const reg = /\w/g`

- \W ：表示匹配非单词字符,它是`[^a-zA-Z_0-9]`的简写.`const reg = /\W/`

- \d ：表示匹配数字.它是`[0-9]`的简写.`const reg = /\d/`

- \D ：表示匹配非数字字符.它是`[^0-9]`的简写.`const reg = /\D/`

- \s ：表示匹配空白字符(空格符、制表符、回车符、换行符、垂直换行符、换页符)，等价于[ \f\n\r\t\v]。`const reg = /\s/`

- \S ：表示匹配非空白字符。等价于[^ \f\n\r\t\v]。`const reg = /\S/`

- \b ：表示匹配单词边界(即单词的开头或结尾，也就是单词的分界处。虽然通常英文的单词是由空格、标点符号或者换行符来分隔的，但是`\b`并不匹配这些单词分隔字符中的任意一个,它只匹配一个位置。例如：`/\b/g`匹配单词`hello,wrold`,匹配位置为`|hello|,|world|`). `const reg = /\b/`

- \B ：表示匹配非单词边界`const reg = /\B/`

- \0 ：表示匹配 `NULL`字符. `const reg = /\0/`

- \n ：表示匹配换行符. `const reg = /\n/`

- \f ：表示匹配换页符. `const reg = /\f/`

- \r ：表示匹配回车符. `const reg = /\r/`

- \t ：表示匹配制表符.等价于\x09 和\cI。`const reg = /\t/`

- \v ：表示匹配垂直制表符. `const reg = /\v/`

- \A ：表示匹配字符串的开始`const reg = /\A/`

- \Z ：表示匹配字符串的结束`const reg = /\Z/`

- ......

&nbsp;

#### <a name="04">正则表达式主体声明 量词</a>

> 贪婪与非贪婪模式影响的是被量词修饰的子表达式的匹配行为，贪婪模式在整个表达式匹配成功的前提下，尽可能多的匹配，而非贪婪模式在整个表达式匹配成功的前提下，尽可能少的匹配

- {n} ：n 是一个正整数,表示匹配在{n}前面的一个字符刚好出现 n 次.`const reg = /c{2}/`

```javascript
const reg = /c{2}/;
reg.test("access"); // true
reg.test("click"); // false
```

- {n,} ：n 是一个正整数,表示匹配在{n,}前面的一个字符至少出现 n 次.`const reg = /l{2,}/`

```javascript
const reg = /l{n,}/;
reg.test("hello"); // true
reg.test("llly"); // true
reg.test("like"); //false
```

- {n,m} ：n 和 m 都是正整数,表示匹配在{n,m}前面的一个字符最少出现 n 次,最多出现 m 次,如果 n 或者 m 的值是 0,则这个值会被忽略.`const reg = /p{2,4}`

```javascript
const reg = /p{2,4}/;
reg.test("application"); // true
reg.test("fourpppp"); // true
reg.test("people"); // false
reg.test("fiveppppp"); // true
reg.test("pppppp"); // true
```

- ? ：表示匹配前面一个表达式 0 次或 1 次.即可有可无;如果紧跟在任何量词 `*`、 `+`、`?` 或 `{}` 的后面，将会使量词变为非贪婪（匹配尽量少的字符），和缺省使用的贪婪模式（匹配尽可能多的字符）正好相反，例如，对 "123abc" 使用 /\d+/ 将会匹配 "123"，而使用 /\d+?/ 则只会匹配到 "1"。等价于`{0,1}`.`const reg = /ap?/`

```javascript
const reg = /e?le?/g;
"angel,angle,oslo".match(reg); // ["el", "le", "l"]
```

- `+` ：表示匹配前面一个表达式 1 次或者多次.等价于`{1,}`.`const reg = /ap+/`

```javascript
const reg = /ap+/;
"application".match(reg); // ["app", index: 0, input: "application", groups: undefined]
```

- `*` ：表示匹配前面一个表达式 0 次或者多次.等价于`{0,}`.`const reg = /ap*/`

```javascript
const reg = /ap*/;
"application".match(reg); // ["app", index: 0, input: "application", groups: undefined]
```

&nbsp;

#### <a name="05">正则表达式主体声明 分组`()`</a>

正则表达式分组分为`捕获组`(Capturing Groups)与`非捕获组`.在正则中是通过使用成对的小括号`()`来表示分组的.如`(\d)`表示一个分组,`(\d)(\d)`表示两个分组,以此类推,有几对小括号元字符组成,就表示有几个分组.进行分组,主要是为了：

- 作为可选分支
- 简写重复模式
- 缓存捕获数据及反向引用(只有捕获组才可以被反向引用)

##### <a name="06">捕获组</a>

当我们将一个正则表达式主体使用一对小括号包起来，就形成了一个捕获组。捕获组会把括号里正则表达式主体匹配到的内容保存在该分组中，也就是说，它捕获的就是分组里面的正则表达式主体匹配到的内容。例如一个最简单的捕获组`()`，它所匹配的是一个空字符。

- 通过捕获组,我们可以将匹配到的数据进行拆分

```javascript
const reg1 = /\d{4}-\d{2}-\d{2}/; // 不使用分组
const reg2 = /(\d{4})-(\d{2})-(\d{2})/; // 使用分组
"2021-08-22".match(reg1); // ["2021-08-26", index: 0, input: "2021-08-26", groups: undefined]
"2021-08-22".match(reg2); // ["2021-08-26", "2021", "08", "26", index: 0, input: "2021-08-26", groups: undefined]
```

- 通过捕获组,我们可以进行反向引用

在正则表达式中,通过使用捕获组的编号( \1、\2、...、\n)来引用前面表达式所捕获的文本序列,称为反向引用。反向引用中引用的是捕获组匹配到的文本序列（即匹配项），而不是捕获组本身（捕获组的实质是一段正则）

```javascript
/* 例如匹配ABAB这种格式的内容,我们可以把AB先分组，然后在对其引用就可以了。如：1212,3434即(\d{2})\1，把\d{2}匹配到的内容先保存到捕获组1中，然后再对捕获组1进行引用，当(\d{2})匹配到的是12的时候，\1就表示12，当(\d{2})匹配到的是34的时候，\1就是34 */
const reg = /(\d{2})\1/;
"1212".match(reg); // ["1212", "12", index: 0, input: "1212", groups: undefined]
"1122".match(reg); // null
"1234".match(reg); // null
"2574".match(reg); // null
"2020".match(reg); // ["2020", "20", index: 0, input: "2020", groups: undefined]
```

&nbsp;

##### <a name="07">非捕获组</a>

非捕获组的语法是在捕获组的基础上，通过在左括号的右侧添加`?:`实现声明`(?:)`，例如`(\d)`表示捕获组,`(?:\d)`表示非捕获组。非捕获组不会占用内存,也不能被反向引用。非捕获组存在的意义是只匹配字符信息,不捕获文本。我们可以根据这一特性来实现某些预查匹配操作.即用于设置某些限定条件,使捕获组符合这些限定条件而达到预查这些捕获组的目的。

- 如捕获组`/(\d{4})-(\d{2})-(\d{2})/`改为非捕获组`/(?:\d{4})-(?:\d{2})-(?:\d{2})/`,那么它就和`/\d{4}-\d{2}-\d{2}/`匹配到的内容是一样的了。

```javascript
/* 例如，如果我们要查找 (go)+，但不希望括号内容（go）作为一个单独的数组项，则可以编写：(?:go)+ */
const str = "Gogogo John!";
const reg = /(go)+/;
const reg2 = /(?:go)+/;
str.match(reg); // ["gogo", "go", index: 2, input: "Gogogo John!", groups: undefined]
str.match(reg2); // ["gogo", index: 2, input: "Gogogo John!", groups: undefined]
```

&nbsp;

##### <a name="08">命名捕获组</a>

捕获组又分为`编号捕获组`和`命名捕获组`，默认是编号捕获组。命名捕获组也是捕获组,只是声明的语法不同。命名捕获组的声明语法`(?<name>group)`或者`(?'name'group)`,其中 name 表示捕获组的名称，group 表示捕获组的正则匹配规则。

> 命名捕获组的反向引用：我们可以用`\k<name>` 或 `\k'name'`的形式来对前面的命名捕获组捕获到的值进行引用。如之前的`(\d{2})\1`可以改写为`(?<key>\d{2})\k<key>`，其中，key 是我们对捕获组的命名，而`\k<key>`是对 key 这个分组捕获到的内容进行引用，所谓的引用，就是利用它前面匹配到的字符串的值

```javascript
const reg = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
"2021-08-22".match(reg); // ["2021-08-22", "2021", "08", "22", index: 0, input: "2021-08-22", groups: {year: "2021", month: "08", day: "22"}]
```

&nbsp;

#### <a name="09">正则表达式主体声明 其他</a>

- (x) ：表示匹配 'x' 并且记住匹配项。其中括号被称为捕获括号。`const reg = /(x)/`

- (?:x)：表示匹配 'x' 但是不记住匹配项。这种括号叫作非捕获括号，使得你能够定义与正则表达式运算符一起使用的子表达式.`const reg = /(?:x)/`

- x(?=y)：表示匹配'x'仅仅当'x'后面跟着'y'.这种叫做先行断言。`const reg = /x(?=y)/`

```javascript
const reg = /a(?=p)/;
"application".match(reg); // 因为a的后面跟着p,满足条件,所以会匹配到a
"ask".match(reg); // 因为a的后面没有跟着p,所以不匹配,返回null
```

- (?<=y)x：表示匹配'x'仅当'x'前面是'y'.这种叫做后行断言。`const reg = /(?<=y)x/`

```javascript
const reg = /(?<=v)e/;
"love".match(reg); // 因为e的前面是v,满足条件,所以可以将会匹配出e.
"blue".match(reg); // 因为e的前面不是v,不满足条件,因此不会匹配出e
```

- x(?!y)：表示仅仅当'x'后面不跟着'y'时匹配'x'，这被称为正向否定查找。`const reg = /x(?!y)/`

```javascript
const reg = /a(?!p)/;
"application".match(reg); // 因为a的后面紧跟着p.不满足条件.所以不会匹配出a.
"ask".match(reg); // 因为a的后面没有紧跟着p,因此满足条件,将会匹配出a.
```

- (?<!y)x：表示仅仅当'x'前面不是'y'时匹配'x'，这被称为反向否定查找。`const reg = /(?<!y)x/`

```javascript
const reg = /(?<!v)e/;
"love".match(reg); // 因为e的前面是v,因此不满足条件,不会匹配出e.
"blue".match(reg); // 因为e的前面不是v,因此满足条件,将会匹配出e
```

&nbsp;

#### <a name="10">贪婪与懒惰</a>

- 当正则表达式中包含能接受重复的限定符时,通常的行为是(在使整个表达式能够得到匹配的前提下)匹配尽可能多的字符。例如正则表达式`/a.*b/g`匹配字符串 `aabab`,他会匹配出整个字符串`aabab`(我们需要匹配`/a.*b/g`这种形式,它在发现这个字符串都满足匹配条件的情况下,就直接匹配该字符了)，这就是贪婪匹配。

- 有时候我们更需要的是懒惰匹配(即匹配出尽可能少的字符)。这时候我们只需要在这些数量声明符的后面添加一个`?`字符。类似于`/a.*?b/g`，这就意味着匹配任意数量的重复，但是在能使整个匹配成功的前提下使用最少的重复。

```js
const str = "aabab";
str.match(/a.*b/g); // 贪婪匹配,结果为 ["aabab"]
str.match(/a.*b?/g); // 懒惰匹配,结果为["aab","ab"]
```

部分懒惰语法描述
| 语法 | 描述 |
| ------ | :-------------------------------: |
| \*? | 重复任意次，但尽可能少重复 |
| +? | 重复 1 次或更多次，但尽可能少重复 |
| ?? | 重复 0 次或 1 次，但尽可能少重复 |
| {n,m}? | 重复 n 到 m 次，但尽可能少重复 |
| {n,}? | 重复 n 次以上，但尽可能少重复 |

&nbsp;

#### <a name="11">了解正则表达式</a>

正则表达式(RegExp)是一种使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式.
语法：

```javascript
const reg = /正则表达式主体/修饰符(可选)

或者

const reg = new RegExp("正则表达式主体","修饰符(可选)")
```

正则表达式的内容是一段存在于 / / 之间的特殊组合,它描述了一种字符串的匹配模式,可以用来检查一个字符串是否含有某个子串、可以将匹配的子串进行替换等.
' \ '是我们进行声明规则时的重要字符.它将下一个字符(即紧跟在其后面的字符)标记为特殊字符 或一个原义字符 或一个向后引用 或一个八进制转义符.

- 注意: 正则表达式只能对字符串进行操作.

例如:字符串 'no,This is My Love',当我们想要匹配字符'n'时,正则 /n/ 即可.当我们想要匹配一个换行符时,正则 /\n/ 即可,当我们想要匹配字符'\n'时,正则 /\\\n/ 即可

&nbsp;

#### <a name="12">修饰符</a>

修饰符用于执行区分大小写和全局匹配以及多行匹配

- i 修饰符用于执行对大小写不敏感的匹配。
- g 修饰符用于执行全局匹配(查询所有匹配而非在找到第一个匹配后就停止)
- m 修饰符用于执行多行匹配
- s 表示允许 元字符`.`匹配换行符
- u 表示使用 unicode 码的模式进行匹配
- y 表示执行'粘性(sticky)'搜索,匹配从目标字符串的当前位置开始.

修饰符可以一次声明多个

```javascript
const reg = /[a-z]/gm;

或者;

const reg = new RegExp("[a-z]", "gm");
```

&nbsp;

#### <a name="13">RegExp 对象方法</a>

- exec(string)：该方法主要用于检索字符串中的指定值.返回值为找到的值,并确定其位置.若是没有找到,则返回值为 null

```javascript
const reg = /d/g;
reg.exec("abcdefg"); // ["d", index: 3, input: "abcdefg", groups: undefined]
reg.exec("love"); // null
```

- test(string)：该方法主要用于检查字符串中是否存在指定的值,返回值为布尔值,若是存在返回 true,否则返回 false.

```javascript
const reg = /l/g;
reg.test("hello"); // true
reg.test("javascript"); // false
```

- toString()：改方法主要是用于将正则表达式以字符串的形式原样返回

```javascript
const reg = /[a-z]/gm;
reg.toString(); // "/[a-z]gm"
```

&nbsp;

#### <a name="14">RegExp 对象属性</a>

- constructor：该属性返回一个函数,该函数是一个创建 ExgExp 对象的原型

```javascript
const reg = /k/g;
reg.constructor; // ƒ RegExp() { [native code] }
```

- global：该属性用于判断是否设置了`g`修饰符,返回值为布尔值

```javascript
const reg = /d/gm;
reg.global; // true
```

- ignoreCase：该属性用于判断是否设置了`i`修饰符,返回值为布尔值

```javascript
const reg = /d/gm;
reg.ignoreCase; // false
```

- lastIndex：该属性用于规定下次匹配的起始位置.该属性只有设置修饰符`g`才能使用。该属性是可读可写的。只要目标字符串的下一次搜索开始，就可以对它进行设置。当方法 exec() 或 test() 再也找不到可以匹配的文本时，它们会自动把 lastIndex 属性重置为 0。

```javascript
const reg = /l/g;
const str = "hello,world";
while (reg.test(str)) {
  console.log(reg.lastIndex); // 3 4 10
}
```

- multiline：该属性用于判断是否设置了`m`修饰符,返回值为布尔值

```javascript
const reg = /d/gm;
reg.multiline; // true
```

- source：该属性用于返回正则表达式的匹配模式(即返回该正则表达式用于匹配那些内容)

```javascript
const reg = /he/gi;
reg.source; // he
```
