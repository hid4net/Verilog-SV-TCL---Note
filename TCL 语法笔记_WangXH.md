<h1 style="text-align:center">Tcl语法总结</h1>

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=3 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 基本语法](#-1-基本语法-)
  - [1.1. 一切皆命令/字符串](#-11-一切皆命令字符串-)
  - [1.2. 常用命令](#-12-常用命令-)
  - [1.3. 三种替换](#-13-三种替换-)
    - [1.3.1. 变量替换](#-131-变量替换-)
    - [1.3.2. 命令替换](#-132-命令替换-)
    - [1.3.3. 反斜杠`\`替换](#-133-反斜杠替换-)
  - [1.4. 两种引用](#-14-两种引用-)
    - [1.4.1. 双引号`"`引用](#-141-双引号引用-)
    - [1.4.2. 大括号引用](#-142-大括号引用-)
  - [1.5. 参数展开](#-15-参数展开-)
  - [1.6. 注释](#-16-注释-)
- [2. 变量](#-2-变量-)
  - [2.1. 简单变量](#-21-简单变量-)
  - [2.2. 变量的管理](#-22-变量的管理-)
  - [2.3. 数组变量](#-23-数组变量-)
  - [2.4. 特殊变量](#-24-特殊变量-)
- [3. 表达式](#-3-表达式-)
  - [3.1. 数值操作数](#-31-数值操作数-)
  - [3.2. 操作符](#-32-操作符-)
  - [3.3. 数学函数](#-33-数学函数-)
  - [3.4. 表达式](#-34-表达式-)
- [4. 字符串,  列表,  字典](#-4-字符串--列表--字典-)
  - [4.1. 字符串](#-41-字符串-)
    - [4.1.1. 字符串命令](#-411-字符串命令-)
    - [4.1.2. 格式化字符串](#-412-格式化字符串-)
    - [4.1.3. 模式匹配](#-413-模式匹配-)
    - [4.1.4. 二进制字符串](#-414-二进制字符串-)
  - [4.2. 列表 list](#-42-列表-list-)
    - [4.2.1. list 命令](#-421-list-命令-)
    - [4.2.2. 与字符串互换](#-422-与字符串互换-)
  - [4.3. 字典](#-43-字典-)
    - [4.3.1. 字典命令](#-431-字典命令-)
- [5. 流程控制](#-5-流程控制-)
  - [5.1. 条件控制](#-51-条件控制-)
  - [5.2. 循环控制](#-52-循环控制-)
  - [5.3. 运行语句: eval](#-53-运行语句-eval-)
  - [5.4. 运行脚本: source](#-54-运行脚本-source-)
- [6. 过程](#-6-过程-)
  - [6.1. 声明与调用](#-61-声明与调用-)
  - [6.2. 局部变量和全局变量](#-62-局部变量和全局变量-)
  - [6.3. 缺省参数和可变个数参数](#-63-缺省参数和可变个数参数-)
  - [6.4. 引用: upvar](#-64-引用-upvar-)
  - [6.5. uplevel 命令](#-65-uplevel-命令-)
  - [6.6. 匿名过程](#-66-匿名过程-)
- [7. 命名空间](#-7-命名空间-)
  - [7.1. 基础](#-71-基础-)
  - [7.2. 其他命令](#-72-其他命令-)
  - [7.3. 命令集合](#-73-命令集合-)
- [8. 访问文件](#-8-访问文件-)
  - [8.1. 文件名](#-81-文件名-)
  - [8.2. 基本文件输入输出命令](#-82-基本文件输入输出命令-)
  - [8.3. 随机文件访问](#-83-随机文件访问-)
  - [8.4. 当前工作目录](#-84-当前工作目录-)
  - [8.5. 文件操作和获取文件信息](#-85-文件操作和获取文件信息-)
- [9. 进程间通信](#-9-进程间通信-)
- [10. 错误与异常](#-10-错误与异常-)
- [11. 创建和使用脚本](#-11-创建和使用脚本-)
- [12. Tcl内部管理](#-12-tcl内部管理-)
- [13. 历史](#-13-历史-)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 基本语法
## 1.1. 一切皆命令/字符串
* 命令格式: `命令 参数1 参数2 ...`
* Tcl 脚本包含一条或更多的命令, 命令通过换行符或分号隔开
    ``` tcl
    # ------------ 示例 ------------
    set a 1
    set b 2
    # 或
    set a 1; set b 2
    ```
* 命令要写在多行时, 行尾要使用 `\`

## 1.2. 常用命令
* 创建变量、赋值: `set 变量 值`
* 查看变量: `set 变量`
* 移除变量: `unset 变量`
    * 复杂类型有 `array unset`, `dict unset`, ...
* 打印变量: `puts $变量`
* 运行表达式: `expr 表达式/数学函数`
* 变量增加或减小: `incr 变量 自然数`
* 将值 (字符串, 变量替换) 添加到变量后: `append 变量 值`
    ```tcl
    # ------------ 示例 ------------
    set v1 1; set v2 2
    append v1 $v2   # 输出 12, v1 也变为 12
    ```
* 运行脚本: `source 脚本路径`
* 查看帮助: `help 命令`
* 获取信息: `info`

## 1.3. 三种替换
### 1.3.1. 变量替换
* 引用变量的值 `$变量`, 为了区分变量名和变量值
    ```tcl
    # ------------ 示例 ------------
    set kgrams 20
    expr $kgrams * 2.2046   # 结果: 44.092
    puts "kgrams = $kgrams" # 输出: kgrams = 20
    ```
### 1.3.2. 命令替换
* 用命令代替某个参数: `[命令]`
    ```tcl
    # ------------ 示例 ------------
    set kgrams 20
    set 1bs [expr $kgrams*2.2046]   # 1bs: 44.092
    ```
### 1.3.3. 反斜杠`\`替换
* 向单词中插入TCL中的特殊字符, 如 `\[`, `\$`, `\(空格)`
* TCL支持的`\`序列
    | 转义表达式 |           定义            |
    | :--------: | :-----------------------: |
    |     \a     |        警告 (0x7)         |
    |     \b     |        删除 (0x8)         |
    |     \f     |       换页符 (0xc)        |
    |     \n     |       换行符 (0xa)        |
    |     \r     |        回车 (0xd)         |
    |     \t     |       制表符 (0x9)        |
    |     \v     |     垂直制表符 (0xb)      |
    |   \空格    | 空格本身 (区别于命令间隔) |
    |    \\\\    |             \             |
    |    \ooo    |          八进制           |
    |    \xhh    |         十六进制          |
    |   \uhhhh   |          unicode          |

* 在行尾表示命名没有结束, 下一行继续

## 1.4. 两种引用
### 1.4.1. 双引号`"`引用
* 一个参数以`"`开始并以`"`结束, 才是双引号`"`引用
    * 如果参数不以双引号开始, 那么其中的双引号被当作普通字符
* 双引号`"`引用的参数中, 空格、制表符以及分号都被当做普通字符
    * `\"`被当作字符双引号
* 变量替换、命令替换以及反斜杠替换在双引号中正常进行
    ```tcl
    # ------------ 示例 ------------
    set a 2.1
    set msg "a is $a; the square of a is [expr $a * $a]"
    # 输出: a is 2.1; the square of a is 4.41
    ```
### 1.4.2. 大括号引用
* 以大括号 `{` 开始并以`}`结束的参数
* 取消所有字符的特殊意义

## 1.5. 参数展开
* `{*}`之后紧跟着非空白字符
    ``` tcl
    # ------------ 示例 ------------
    file delete {*} [glob *.o]
    # 等效于
    file delete a.o b.o c.o
    ```
## 1.6. 注释
* `#`, 必须出现在 Tcl 解释器期望命令的第一个字符出现的地方
* 不能使用行尾注释
    ```tcl
    # ------------ 示例 ------------
    # 整行注释
    set a 100   # 这里的文字会被当做参数, 会报错
    set b 101;  # 行尾注释, 需要加分号
    ```

--------------------------------------------------------------------------------
# 2. 变量

## 2.1. 简单变量
* 包含: 名字和值
    * 名字和值可以是任意字符串
    * 区分大小写
* ==无类型==
    * 内部保存为: 整数, 实数, 名称, 列表, Tcl 脚本等

## 2.2. 变量的管理
```tcl
set   变量  值  # 创建变量、赋值
set   变量      # 查看变量
puts  $变量     # 打印变量
unset 变量      # 删除变量
```

## 2.3. 数组变量
* 数组变量: `数组名(元素名)`, 数组名和元素名必须一起使用, 如:
    ```tcl
    earnings (January)
    ```
    * 注意: 元素名会被解释为字符串, 因此 1 和 1.0 不同, 内部用 hash 表存储数组元素
* 多维数组: `数组名(元素名,元素名,...)`
    * 注意: `matrix(1,1)` 和 `matrix(1, 1)` 是不同的, 最好不使用空格
* 如果数组声明时不存在, 会自动创建
* 访问元素: `$数组名(元素名字符串)` 或 `$数组名($元素名变量)`
    * 注意: 元素名如果是变量, 也需要变量替换
* 管理数组: `array option arrayName ?arg arg ...?`
    * 查找
        * `array startsearch arrayName`: 搜索, 返回搜索标识 (用于命令`array nextelement`、`array anymore`和`array donesearch`)
        * `array nextelement arrayName searchId`: 返回下一个元素, 如果搜索完则返回空字符串
            * 注意: 如果对`arrayName`的元素进行了添加或删除, 所有的搜索都会自动结束, 如同调用了命令`array donesearch`, 并导致`array nextelement`操作失败
        * `array anymore arrayName searchId`: 是否还有元素,
            * `searchId`必须是`array startserach`的返回值
        * `array donesearch arrayName searchId`: 中止搜索, 并销毁所有状态, 返回空字符串, 当一个搜索完成时一定要注意调用这个命令
    * 信息
        * `array exists arrayName`: 指定的数组是否是存在
        * `array size arrayName`: 返回数组元素的个数
        * `array names arrayName ?mode? ?pattern?`: 返回数组中和`pattern`匹配的元素的名字组成的一个list, 如果没有`pattern`参数, 返回所有元素; 如果数组中没有匹配的元素或者`arrayName`不是数组的名字, 返回空字符串
        * `array statistics arrayName`: 返回数组的统计信息
    * 维护
        * `array get arrayName ?pattern?`: 返回 (元素名,值) 的列表, 数据对的顺序没有规律,`pattern` 参数限定搜索范围 (用string match的匹配规则)
        * `array set arrayName list`: 设置数组中元素的值, list := (元素名,值), 如果`arrayName`不存在, 自动创建
        * `array unset arrayName ?pattern?`: 删除数组

## 2.4. 特殊变量
* `argvO`: 脚本文件名
* `argv`: 参数列表
* `argc`: 命令行参数的个数
* `env`: TCL预定义变量, 数组变量, 元素是所有过程的环境变量
    * 如 `env(home)`, `env(HOME)`, `env(LANG)`, `env(PROCESSOR_IDENTIFIER)`, `env(TEMP)`, `env(USERNAME)`, `env(COMPUTERNAME)`, `env(OS)`, `env(Path)` ...
    * 可用 `foreach {i} [array names env] {puts "$i = $env($i)"}` 命令打印全部元素名
* `tcl_platform`: TCL预定义变量, 数组变量
    * 元素名包括: `osVersion`, `pointerSize`, `byteOrder`, `threaded`, `machine`, `platform`, `os`, `user`, `wordSize`, ...
    * 可用 `foreach {i} [array names tcl_platform] {puts "$i = $tcl_platform($i)"}` 命令打印全部元素名
* `tcl_version`: TCL预定义变量, real, 版本信息

--------------------------------------------------------------------------------
# 3. 表达式

## 3.1. 数值操作数
* 整数: 十进制, 二进制 (`0b`开头), 八进制数 (`0o`开头), 十六进制数 (`0x`开头)
* 实数: 浮点数, 科学计数法

## 3.2. 操作符
|  类型  |   语法    |     意义      | 操作数类型         |
| :----: | :-------: | :-----------: | :----------------- |
| 正负号 |    - a    |      负a      | int, real          |
|   ^    |    + a    |      正a      | ^                  |
|  取反  |    ! a    | (a==0) ? 1 :0 | int, real          |
|   ^    |    ~ a    |   按位取反    | int                |
|  算术  |  a ** b   |     乘方      | int, real          |
|   ^    |   a * b   |      乘       | int, real          |
|   ^    |   a / b   |      除       | int, real          |
|   ^    |   a % b   |     取模      | int                |
|   ^    |   a + b   |      加       | int, real          |
|   ^    |   a - b   |      减       | int, real          |
|  移位  |  a << b   |    左移位     | int                |
|   ^    |  a >> b   |    右移位     | ^                  |
|  关系  |   a < b   |     小于      | int,float,string   |
|   ^    |   a > b   |     大于      | ^                  |
|   ^    |  a <= b   |   小于等于    | ^                  |
|   ^    |  a >= b   |   大于等于    | ^                  |
|   ^    |  a == b   |     等于      | ^                  |
|   ^    |  a != b   |    不等于     | ^                  |
|   ^    |  a eq b   |  字符串相同   | string             |
|   ^    |  a ne b   |  字符串不同   | ^                  |
|   ^    |  a in b   |    存在于     | a: string, b: list |
|   ^    |  a ni b   |   不存在于    | ^                  |
| 位运算 |   a & b   |    按位与     | int                |
|   ^    |   a ^ b   |   按位异或    | ^                  |
|   ^    |  a \| b   |    按位或     | ^                  |
|  逻辑  |  a && b   |    逻辑与     | int, real          |
|   ^    | a \|\| b  |    逻辑或     | ^                  |
|  选择  | a ? b : c |   选择运算    | a:int, real        |

## 3.3. 数学函数
|     分类     | 函数                                                                         |
| :----------: | :--------------------------------------------------------------------------- |
|   类型转换   | `int(x)`, `wide(x)`, `double(i)`, `bool(x)`                                  |
|     统计     | `max(arg, ...)`, `min(arg, ...)`                                             |
| 绝对值与近似 | `abs(x)`, `round(x)`, `ceil(x)`, `floor(x)`                                  |
|   乘方开方   | `pow(x, y)`, `sqrt(x)`, `exp(x)`, `log(x)`, `log10(x)`, `hypot(x, y)`        |
|     取余     | `fmod(x, y)`                                                                 |
| 三角与反三角 | `sin(x)`, `cos(x)`, `tan(x)`, `asin(x)`, `acos(x)`, `atan(x)`, `atan2(x, y)` |
|     双曲     | `sinh(x)`, `cosh(x)`, `tanh(x)`                                              |
|     随机     | `rand()`, `srand(x)`                                                         |

* 整数转实数: `double`
* 实数转整数:
    * `int`: 转为机器字长
    * `wide`: 转为 64 位
    * `entier`: 转为适当长度的整数, 可以占用任意长度的存储空间, 保证能存放完整的值

## 3.4. 表达式
``` tcl
expr {数学表达式}
expr {数学函数}
```
--------------------------------------------------------------------------------
# 4. 字符串,  列表,  字典

## 4.1. 字符串
* 两个双引号`"` 内的文本
* 索引: 0 based
    * 可以是: `整数`, `整数±整数`, `end`, `end±整数`
        * `+`/`-` 前后不要有空格

### 4.1.1. 字符串命令
> 注: 命令中 _string_ 需要变量替换, _varName_ 是变量名, 不要变量替换
* 取得字符串
    * `string index string charIndex`: 返回第 `charIndex` 个字符
    * `string range string first last`:  返回范围为 $[first, last]$ 的子字符串
        * 若 first < 0, first 被当作 0;
        * 若 last ≥ 总长度, last 被当作 `end`;
        * 若 first > last, 返回空
* 字符串长度
    * `string length string`: 返回字符串长度
* 修改字符串
    * `string repeat string count`: 重复字符串
    * `string reverse string`: 翻转字符串
    * `string toupper/tolower/totitle string ?first? ?last?`: 转为大写/小写/句首大写
    * `string trim/trimleft/trimright string ?chars?`: 从首尾/左侧/右侧剪裁 `chars`
        * 如果没有指定 `chars`, 将删除 spaces, tabs, newlines, carriage returns 等字符
* 简单搜索
    * `string first/last needleString haystackString ?startIndex?`: 从 `haystackString` 头/尾查找字符串 `needleString`
        * 返回第一个字母的索引, 如果没有找到则返回 -1
    * `string wordstart/wordend string charIndex`: 返回首/未个 word
* 字符串比较
    * `string compare ?-nocase? ?-length int? string1 string2`: 比较字符串
        * 若相同, 返回 0
        * 若 `string1` 在字典中先于 `string2`, 返回 -1; 否则返回 1
        * `-nocase`: 不区分大小写
        * `-length`: 只比较前 `int` 个字符, 如果 `int` 为负数则忽略
    * `string equal ?-nocase? ?-length int? string1 string2`: 两个字符串是否相同
        * 某些时候可以用 `expr string1 eq/ne string2`
* 字符串置换
    * `string replace string first last ?newstring?`: 替换字符串中 $[first, last]$ 的字符
        * 如果没有指定 `newstring`, 则删除字符
    * `string map ?-nocase? mapping string`: 字典替换, `mapping` 可以是 `{原字符串 替换字符串}`
* 字符串类型
    * `string is class ?-strict? ?-failindex varname? string`: 判断字符串类型
        * class
            |    类型     | 测试对象                                             |
            | :---------: | :--------------------------------------------------- |
            |    alnum    | Unicode字母或数字                                    |
            |    alpha    | Unicode字母                                          |
            |    ascii    | 7位ASCII字符                                         |
            |   boolean   | 可识别的bool值 (0, false, no, off, 1, true, yes, on) |
            |   control   | Unicode控制字符                                      |
            |    digit    | Unicode数字                                          |
            |   doouble   | 是否为 double 实数                                   |
            |    false    | 可识别的bool假 (0, false, no, off)                   |
            |    graph    | 非空白的Unicode打印字符                              |
            |   integer   | 32位整数                                             |
            |    list     | 是否为list                                           |
            |    lower    | Unicode小写字母                                      |
            |    print    | Unicode打印字符, 包括空白字符                        |
            |    punct    | Unicode标点符号                                      |
            |    space    | Unicode空白字符                                      |
            |    true     | 可识别的bool真 (1, true, yes, on)                    |
            |    upper    | Unicode大写字母                                      |
            | wideinteger | 长整型                                               |
            |  wordchar   | 字母或连字符                                         |
            |   xdigit    | 十六进制数                                           |
        * `-strict`: 空字符串将返回 0, 如果不指定该选项, 将总是返回 1
        * `-failindex`: If specified, then if the function returns 0, the index in the  string  where the class was no longer valid will be stored in the variable named varname.  The varname  will  not  be set if the function returns 1.

### 4.1.2. 格式化字符串
* 创建: `format formatString ?arg arg ...?`
    * 类似 C 语言的 `printf`
* 扫描: `scan string format ?varName varName ...?`
    * 类似 C 语言的 `scanf`

### 4.1.3. 模式匹配
* 通配符: `string match ?-nocase? pattern string`
    * `?`: 任意单个字符
    * `*`: 任意长的任意字符串, 包括空字符串
    * `[chars]`: 字符集合中的任意字符, 可以使用 A-Z 这种形式
    * `\x`: 单个字符, 转义 `*`,`-`,`[`,`]`

* 正则表达式: 支持基本正则表达式(BRE), 扩展正则表达式 (ERE) 和高级正则表达式 (ARE)
    * 匹配: `regexp ?switches? exp string ?matchVar? ?subMatchVar subMatchVar ...?`
    * 替换: `regsub ?switches? exp string subSpec ?varName?`
    > 参见文件 "TCL_TK Command Reference Guide.pdf"
    * 可用 `[[类型1][类型2]]` 表示多个系列的匹配项
    * 也可用 `[:class:]` 表示一系列类型
        | Class   | Description                                                                                                  |
        | ------- | ------------------------------------------------------------------------------------------------------------ |
        | alnum   | Unicode alphabet or digit characters, `[[:alpha:][:digit:]]`                                                 |
        | alpha   | Unicode alphabet characters `[[:lower:][:upper:]]`                                                           |
        | ascii   | Characters `[\u0000-\u007f]` (7-bit ASCII) (machine specific)                                                |
        | blank   | Space or tab characters (not used by string is)                                                              |
        | boolean | true or false, 0 or 1, yes or no, on or off (string is only)                                                 |
        | control | Unicode control characters true true, 1, yes, on (string is only)                                            |
        | digit   | Unicode digit charactes (not limited to [0-9])                                                               |
        | double  | Valid Tcl form of double (string is only) wideinteger Valid Tcl wide integer. (string is only)               |
        | false   | false, 0, no, off (string is only) wordchar Unicode word characters, `[[:alnum:][:punct:]]` (string is only) |
        | graph   | Unicode printing characters, except space xdigit hexadecimal digit characters `[[0-9][A-F][a-f]]`            |
        | integer | Valid Tcl form of integer (string is only)                                                                   |
        | lower   | Unicode lower-case alphabet characters                                                                       |
        | print   | Unicode printing characters, including space                                                                 |
        | punct   | Unicode punctuation characters (non-alnum or space) (string is only)                                         |
        | space   | Unicode white-space characters [\f\n\r\t\v ]                                                                 |
        | upper   | Unicode upper-case alphabet characters                                                                       |

### 4.1.4. 二进制字符串
* `binary format formatString ?arg arg ...?`
* `binary scan string formatString ?varName varName ...?`

## 4.2. 列表 list
* 表示集合, 由一堆元素组成的有序集合, 每个元素可以是任意字符串, 也可以是list
    ``` tcl
    # ------------ 示例 ------------
    {}          # 空 list
    {a b c d}   # 4 个值的 list
    {a {b c} d} # list 可以嵌套
    ```

### 4.2.1. list 命令
> 注: 命令中 _list_ 需要变量替换, _varName_ 是变量名, 不要变量替换
* 创建
    * 直接声明: `{元素 元素 ...}`
        * 不能用逗号隔离, 逗号会被认为是字符的一部分
    * 命令创建, 语法: `list ?arg arg ...?`
        ``` tcl
        # ------------ 示例 ------------
        set a [list 1 2 3 4]    # a 是一个 4 元素的 list
        set b [list 1 2 {3 4}]  # b 是一个 3 元素的 list
        puts "llength \$a = [llength $a], llength \$b = [llength $b]"
        # 输出: llength $a = 4, llength $b = 3
        llength [lindex $b 2]   # 输出: 2
        ```
* 取值
    * `lindex list ?index...?`: 返回第 index 个元素 (0-based)
    * `lrange list first last`: 返回截取的 list, 可使用 `end`
    * `lassign list varName ?varName ...?`: 将 list 中的元素依次赋给名为 varName 的变量
        * 如果 varName 比列表长, 多余的 varName 被设为空字符串
* 修改
    * `lset varName ?index...? newValue`: 将 varName 列表中第 index 个元素换成新值
    * `lappend varName ?value value value ...?`: 返回追加元素的 list, 如果 varName 不存在, 生成 list
    * `linsert list index element ?element element ...?`: 返回插入元素到第 index 个元素之前的 list
    * `concat ?arg arg ...?`: 返回合并的 list
    * `lreplace list first last ?element element ...?`: 返回替换的 list, 如果没有 value 参数, 删除元素
    * `lrepeat number element1 ?element2 element3 ...?`: 返回重复后的 list
* 信息
    * `llength list`: 返回 list 的元素个数
* 搜索
    * `lsearch ?options? list pattern`: 返回匹配的元素或 -1
        * `options`:
            * `-exact`: 精确匹配
            * `-glob`: 默认模式, 方式与 `string match` 相同
            * `-regexp`: 正规表达式匹配
            * `-sorted`: 针对排好序的 list
            </br>
            * `-all`: 将所有匹配的元素组成一个 list 返回
            * `-inline`: 返回元素而非索引
            * `-not`: 取反
            * `-start index`:
            </br>
            * `-ascii`: 元素被视为字符串, 默认模式
            * `-nocase`: 忽略大小写
            * `-dictionary`: 按字典排序, 与`-ascii`不同的地方是: 不考虑大小写, 数字被当作整数来排序
            * `-integer`: 元素被视为整数
            * `-real`: 元素被视为实数
            </br>
            * `-decreasing`:
            * `-increasing`:
            </br>
            * `-index indexList`: 针对嵌套 list
            * `-subindices`:
* 排序
    * `lsort ?options? list`: 返回排序后的列表
        * `options`:
            * `-ascii`: 按 ASCII 字符顺序排序, 默认模式
            * `-dictionary`: 按字典排序, 与`-ascii`不同的地方是: 不考虑大小写, 数字被当作整数来排序
            * `-integer`: 元素被视为实数整数
            * `-real`: 元素被视为实数
            * `-command command`:  按命令排序
            * `-increasing`: 升序 (按 ASCII 字符比较)
            * `-decreasing`: 降序 (按 ASCII 字符比较)
            * `-indices`:
            * `-index indexList`: 针对嵌套 list
            * `-nocase`: 忽略大小写
            * `-unique`: 删除重复项

### 4.2.2. 与字符串互换
* `split string ?splitChars?`: 拆分字符串, 返回列表, 缺省的 `joinString` 是空格
    * 如果 `splitChars` 是空字符`{}`, 按字符分开
* `join list ?joinString?`: 将列表合并为字符串, 缺省的 `joinString` 是空格, 可以是 `{}`

## 4.3. 字典
* 类似于偶数个元素的列表, 奇数个元素是键, 偶数个元素是值
* 字典可以嵌套
    ```tcl
    # ------------ 示例 ------------
    set employees {
        0001 {
            firstnarne  Joe
            surname     Schrnoe
            title       Mr
        }
        1234 {
            firstnarne  Ann
            initial     E
            surname     Huan
            title       Miss
        }
    puts [dict get [dict get $employees 1234] firstname] # 输出: Ann
    ```
### 4.3.1. 字典命令
> 其中 `dictionaryVariable` 是字典名, 不需要变量替换; `dictionaryValue` 是字典变量, 需要变量替换
* 创建
    * `dict create ?key value ...?`: 根据 key-value 对创建词典, 有多个重复的 key 时, 采用最后一个
    * `dict filter dictionaryValue filterType arg ?arg ...?`: 过滤 dict, 返回匹配的 key-value
* 取值
    * `dict get dictionaryValue ?key ...?`: 根据 key 取值
    * `dict for {keyVar valueVar} dictionaryValue body`: 列举 key-value
        * 与 `foreach` 相似, 也可以使用 `continue` 和 `break`
    * `dict keys dictionaryValue ?globPattern?`: 列举 key
    * `dict values dictionaryValue ?globPattern?`: 列举 value
    * `dict with dictionaryVariable ?key ...? body`: 使用脚本处理嵌套 dict
* 修改
    * `dict set dictionaryVariable key ?key ...? value`: 添加或修改
    * `dict unset dictionaryVariable key ?key ...?`: 删除
    * `dict append dictionaryVariable key ?string ...?`: 添加 key-value
    * `dict lappend dictionaryVariable key ?value ...?`: 为某个 key 附加一个或多个 value (列表)
    * `dict incr dictionaryVariable key ?increment?`: 增加某个 key 的 value
    * `dict update dictionaryVariable key varName ?key varName ...? body`: 使用脚本处理 key-value
    * `dict merge ?dictionaryValue ...?`: 合并词典, 有多个重复的 key 时, 采用最后一个
    * `dict replace dictionaryValue ?key value ...?`: 替换, 有多个重复的 key 时, 采用最后一个
    * `dict remove dictionaryValue ?key ...?`: 删除某个 key, 删除不存在的 key 时, 不会报错
* 信息
    * `dict size dictionaryValue`: 字典的尺寸
    * `dict exists dictionaryValue key ?key ...?`: 是否存在 key
    * `dict info dictionaryValue`: 打印 dict 的信息

--------------------------------------------------------------------------------
# 5. 流程控制

## 5.1. 条件控制
* **if** 分支, 语法: `if expr1 ?then? body1 elseif expr2 ?then? body2 elseif ... ?else? ?bodyN?`
    ``` tcl
    if {条件1} {
        代码
    } elseif {条件2} {
        代码
    } else {
        代码
    }
    #
    if {
        条件
    } then {
        代码
    }
    ```
    * `then` 可以省略
    * 建议总是把表达式和脚本放在大括号中, 这样直到命令执行前都不会有替换
    * `{` 一定要写在上一行, 否则 Tcl 解释器会认为 if 命令在换行符处结束, 下一行会被当成新的命令
* **switch** 分支
    * 语法: `switch ?options? string pattern body ?pattern body ...?`
    * 语法: `switch ?options? string {pattern body ?pattern body ...?}`
    * `optinons`
        * `-exact`: 精确匹配
        * `-glob`: glob匹配
        * `-regexp`: 正则表达式匹配
        * `-nocase`: 忽略大小写
        * `-matchvar varName`:
        * `-indexvar varName`:
        * `--`: options 的结束
    * 分支中 `-` 表示与下个分支一起执行脚本
    * 示例
        ``` tcl
        switch 选项 变量替换 {
            值1 -   # 运行和下一个值相同的代码
            值2 代码2
            值3 代码3
            default 默认代码
        }
        ```
## 5.2. 循环控制
* **while**循环, 语法: `while test body`
    ``` tcl
    while {条件} {
        代码
    }
    ```
* **for**循环, 语法: `for start test next body`
    ``` tcl
    for {初始条件} {结束条件} {每次循环后的操作} {
        代码
    }
    ```
* **foreach**循环
    * 语法: `foreach varname list body`
        ``` tcl
        foreach 变量 {列表} {
            代码
        }
        ```
    * 语法: `foreach varlist1 list1 ?varlist2 list2 ...? body`: 每次循环都会依次把元素值赋给对应的变量
        ``` tcl
        foreach {变量或变量列表1} {列表1} {变量或变量列表2} {列表2} ... {
            代码
        }
        ```
        ```tcl
        # ------------ 示例 ------------
        foreach i {a b} {j k} {v w x y z} {
            puts "i:<$i>, j:<$j>, k:<$k> "
        }
        # 输出:
        # i:<a>, j:<v>, k:<w>
        # i:<b>, j:<x>, k:<y>
        # i:<>, j:<z>, k:<>
        ```

* **break** 和 **continue**
    * 与C语言相同

## 5.3. 运行语句: eval
* 语法: `eval arg ?arg ...?`

## 5.4. 运行脚本: source
* 语法: `source  [-encoding <arg>] [-notrace] [-quiet] [-verbose] <file>`
    ``` tcl
    # ------------ 示例 ------------
    source ./hello.tcl
    ```
* 可用绝对路径, 也可用相对路径
* 返回值: 文件内容的返回值, 即文件中最后一条命令的返回值
* 支持 `return`

--------------------------------------------------------------------------------
# 6. 过程

## 6.1. 声明与调用
* 类似 C 语言中的函数, 语法: `proc name args body`
    ``` tcl
    # 声明
    proc 过程名 {参数列表} {
        代码
    }
    # 调用
    过程名 参数1 参数2 ...
    ```
    ``` tcl
    # ------------ 示例 ------------
    proc add {x y} {expr $x+$y}
    add 1 2 # 输出 3
    ```
* 参数之间用空格隔开
* 可以利用 `return` 在代码的任何地方中断过程, 并返回值
    ``` tcl
    # ------------ 示例 ------------
    proc abs {x} {
        if { $x >= 0 } {
            return $x
        }
        return [expr -$x]
    }
    ```
* 调用时, 参数个数需和声明的个数一致

## 6.2. 局部变量和全局变量
* 局部变量 vs 全局变量
    * 局部变量和全局变量可以同名
* 作用域:
    * 局部变量的作用域在过程内部
    * 全局变量的作用域不包括过程的内部
        * 在过程内部引用全局变量: `global` 命令
    > 和C语言有很大的不同
    ``` tcl
    # ------------ 示例 ------------
    set a 4
    proc sample { x } {
        global a
        incr a
        return [expr $a + $x]
    }
    sample 3 # 输出 8
    set a    # a = 5
    ```

## 6.3. 缺省参数和可变个数参数
* **无参**, 如
    ```tcl
    # ------------ 示例 ------------
    proc add {} { expr 2+3 }
    ```
* **缺省参数**: 有缺省值的参数只能位于参数列表的后部
    ``` tcl
    # ------------ 示例 ------------
    proc add {val1 {val2 2} {val3 3}}{
        expr $val1 + $val2 + $val3
    }
    # add 1     # 值为 6
    # add 2 20  # 值为 25
    # add 4 5 6 # 值为 15
    ```
* **可变个数参数**: 最后一个参数用 `args`
    * 局部变量 `args` 将会被设置为一个列表, 如果没有附加的变量, `args` 就设置成一个空串
    * 位于 `args` 以前的参数是普通参数
    ``` tcl
    # ------------ 示例 ------------
    proc add { val1 args } {
        set sum $val1
        foreach i $args {
            incr sum $i
        }
        return $sum
    }
    # add 2         # 值为 2
    # add 2 3 4 5 6 # 值为 20
    ```

## 6.4. 引用: upvar
* 对全局变量或其他过程中的局部变量进行访问
* 使用 `upvar` 绑定, 语法: `upvar ?level? otherVar myVar ?otherVar myVar ...?`
    * 参数 `level` 表: 调用 `upvar` 命令的过程相对于希望引用的变量 myVar 在调用栈中相对位置
        * `level` 的默认值为 1, 即可以访问当前过程的调用者中的变量
        * 如果要访问全局变量, `level` 为 `#0`
        ``` tcl
        # ------------ 示例 ------------
        upvar 2 other x     # 可以访问当前过程的调用者的调用者中的变量 other
        upvar #0 other x    # 可以访问全局变量 other
        ```
    * 参数 `otherVar` 是希望以引用方式访问的参数的名字
    * 参数 `myVar` 是当前过程中的局部变量的名字

    ``` tcl
    # ------------ 示例 ------------
    proc temp { arg } {
        upvar $arg b
        set b [expr $b+2]
    }
    proc myexp { var } {
        set a 4
        temp a
        return [expr $var+$a]
    }
    # myexp 7   # 输出 13
    ```
    > upvar 把 $arg (实际上是过程 myexp 中的变量 a) 和过程 temp 中的变量 b 绑定, 对b的读写就相当于对 a 的读写

## 6.5. uplevel 命令
* `uplevel` 命令像是 `eval` 和 `upvar` 的结合, 把参数作为脚本处理, 正如 `eval`, 但处理脚本的变量上下文环境却不在调用堆栈层级中, 正如 `upvar`
    ```tcl
    # ------------ 示例 ------------
    proc do {varName first last body} {
        upvar $varName v
        for {set v $first} {$v <= $last} {incr v} {
            uplevel $body
        }
    }
    set squares {}
    do i 1 5 { lappend squares [expr $i*$i] }
    set squares
    ```
## 6.6. 匿名过程
* `apply func ?arg1 arg2 ...?`
    ```tcl
    # ------------ 示例 ------------
    set states {California Delaware Hawaii Indiana Iowa}
    lsort -command { apply { { e1 e2} {
        expr { [string length $e1] - [string length $e2]}
        }
    } } $states
    # 输出: Iowa Hawaii Indiana Delaware California
    ```

--------------------------------------------------------------------------------
# 7. 命名空间

## 7.1. 基础
* 创建/使用命名空间: `namespace eval namespace arg ?arg ...?`
    * 如果使用指定的命名空间不存在, 则创建
    ```tcl
    # ------------ 示例 ------------
    proc whoAmI {} { return "global command" }
    namespace eval ns {
        proc whoAmI {} { return "namespace command"}
    }
    whoAmI                          # 输出: global command
    ns::whoAmI                      # 输出: namespace command
    narnespace eval ns { whoAmI }   # 输出: namespace command
    ```
* 删除命名空间: `namespace delete ?namespace namespace ...?`
* 命名空间内变量的声明和访问: `variable ?name value...? name ?value?`
    * 不能初始化数组, 可先声明变量, 然后单独进行一步初始化操作
* 限定符: `::`
    * 以 `::` 开头的表示全局命名空间
* 访问命名空间中的命令/变量:
    *  `空间名::命令/变量`
    *  `${空间名变量}::命令/变量`, 即: 空间名要加 `{}`

## 7.2. 其他命令
* 获取命名空间信息
    * `namespace qualifiers string`: 从命名空间路径中获取空间的名称
    * `namespace tail string`: 从命名空间路径中获取命令/变量的名称
* 导入/导出
    * `namespace export ?-clear? ?pattern pattern ...?`: 向外提供公共的命令/变量
    * `namespace origin command`: 查看一个可被导入的命令是由哪个命名空间原始导出的
    * `namespace import ?-force? ?pattern pattern ...?`: 从别的空间引用命令/变量
    * `namespace forget ?pattern pattern ...?`: 移除导入的命令/变量
* 命名空间 "路径" 管理
    * `namespace current`: 获取当前命名空间
    * `namespace parent ?namespace?`: 获取上级命名空间
    * `namespace children ?namespace? ?pattern?`: 获取下级命名空间
    * `namespace exists namespace`: 是否存在某个命名空间
    * `namespace which ?-command? ?-variable? name`: 获取命令/变量的完整 "路径"
* 访问其他命名空间的变量
    * `namespace upvar namespace otherVar myVar ?otherVar myVar ...`: 将一个命名空间中的一组变量导入当前命名空间
* 其他
    * `namespace code script`
    * `namespace inscope namespace script ?arg ...?`
    * `namespace path ?namespaceList?`

## 7.3. 命令集合
* 有关的命令组合成群组, 如 `string 子命令`, `dict 子命令`
* 相关命令
    * `namespace ensemble subcommand ?arg ...?`: 创建命令集合
    * `namespace unknown ?script?`

--------------------------------------------------------------------------------
# 8. 访问文件

## 8.1. 文件名
* 在表示文件的目录结构时它使用`/`, 而不是 `\`

## 8.2. 基本文件输入输出命令
* 基本示例
    ``` tcl
    proc tgrep { pattern filename} {
        set f [open $filename r]
        while { [gets $f line ] } {
            if {[regexp $pattern $line]} {
                puts stdout $line
            }
        }
        close $f
    }
    ```
* 基本命令
    * `open name ?access?`: 打开路径为`name`的文件, 返回文件标识。如果`name`的第一个字符是 `| `, 管道命令被触发, 而非打开文件
        * 文件的打开方式 `access`:
            * `r` 只读, 默认方式, 文件须已存在
            * `r+` 读写, 文件须已存在
            * `w` 只写, 如果文件存在则清空文件, 否则创建新的空文件
            * `w+` 读写, 如果文件存在则清空文件, 否则创建新的空文件
            * `a` 只写, 文件须存在, 并把指针指向文件尾
            * `a+` 只读, 并把指针指向文件尾; 如文件不存在, 创建新的空文件
    * `gets fileId ?varName?`: 获取下一行, 忽略换行符。如果有 varName 就把该行赋给它, 并返回该行的字符数 (文件尾返回-1) ; 如果没有 varName 参数, 返回文件的下一行 (文件尾返回空字符串)
    * `read ?-nonewline? fileId`: 读并返回文件中所有剩下的字节, 如果没有nonewline开关, 则在换行符处停止
    * `read fileId numBytes`: 从文件中读并返回 numbytes 字节
    * `puts ?-nonewline? ?fileId? string`: 写 string 到文件中, 如果没有 nonewline 开关, 添加换行符 </br> 默认是 stdout, 返回空字符串 </br> 使用 C 的标准 I/O 库的缓冲区方案
    * `flush fileId`: 把缓冲区内容写到文件中, 返回空字符串 </br> 直到数据被写完才返回, 当文件关闭时自动 flush
    * `close ?fileId?`: 关闭文件, 返回空字符串
* 文件标识: 一个字符串用于标识打开的文件, Tcl有三个特定的文件标识: `stdin`, `stdout` 和 `stderr`, 分别对应标准输入、标准输出和错误通道
* Tcl 中对串口、管道、`socket` 等的操作和对文件的操作类似

## 8.3. 随机文件访问
* 默认文件输入输出方式是连续的
    * 每个 `gets` 或 `read` 命令返回的是访问位置后面的字节
    * 每个 `puts` 命令写数据是接着上次写的位置接着写
    * `seek`, `tell` 和 `eof` 等命令使用户可以非连续访问文件
        * `seek fileId offset ?origin?`: 把文件的访问点设置为相对于 origin 偏移量为 offset 的位置. origin 可以是 start (默认), current, end, 分别对应文件头、当前位置、文件尾  返回空字符串
        * `tell fileId`: 返回当前访问位置
        * `eof fileId`: 是否到文件尾, 返回 1 or 0

## 8.4. 当前工作目录
* `pwd`
    * 没有参数, 返回当前目录的完整路径
* `cd`
    * 使用一个参数, 可以把工作目录改变为参数提供的目录
    * 不使用参数, 把工作目录变为启动 Tcl 脚本的用户的工作目录, Windows 下会把工作目录变为 window s操作系统的安装目录所在的盘的根目录 (如: C:/)

## 8.5. 文件操作和获取文件信息
* `glob ?switches? pattern ?pattern ...?`: 返回匹配这个 (些) 模式的所有文件的列表
    * switches:
        * `-nocomplain`: 允许返回一个空串, 没有`-nocomplain`时, 如果结果是空的, 就返回错误
        * `--`: 表示 switches 结束, 即后面以 `-` 开头的参数将不作为switches
    * 采用 `string match` 命令的匹配规则, 例如:
        ``` tcl
        # ------------ 示例 ------------
        glob *.c *.h    # 输出: main.c hash.c hash.h
        ```
    * 允许模式中包含括在`{}`中间以逗号分开的多种选择, 如:
        ``` tcl
        # ------------ 示例 ------------
        glob {{src,backup}/*.[ch]}  # 输出: src/main.c src/hash.c src/hash.h backup/hash.c
        # 等价于
        glob {src/*.[ch]} {backup/*.[ch]}
        ```
    * 模式以 `/` 结束, 那将只匹配目录名, 如:
        ``` tcl
        # ------------ 示例 ------------
        glob */ # 返回当前目录的所有子目录
        ```
    * 如果 glob 返回的文件名列表为空, 通常会产生一个错误
        * 但是 glob 的在样式参数之前的第一个参数是 `-nocomplain` 的话, 这时即使结果为空, 也不会产生错误
* `file`: 可以用来进行文件操作也可以检索文件信息
    * `file atime name ?time?`: 返回文件最后被修改的时间, 标准时间秒数
    * `file attributes name`
      `file attributes name ?option?`
      `file attributes name ?option value option value...?`: 返回文件属性, 支持的属性有
        * linux: `-group`, `-owner` `-permissions` `-readonly`
        * windows: `-archive`, `-hidden` `-longname` `-readonly` `-shortname` `-system`
    * `file channels ?pattern?`: 列举标准输入输出、文件等通道
    * ==`file copy ?-force? ?--? source target`==
      ==`file copy ?-force? ?--? source ?source ...? targetDir`: 复制文件或目录==
    * ==`file delete ?-force? ?--? pathname ?pathname ... ?`: 删除文件或目录==
    * ==`file dirname name`: 获取所在目录==
    * `file executable name`: 当前文件是否可运行
    * ==`file exists name`: 当前文件是否存在==
    * `file extension name`: 返回当前文件的扩展名
    * `file isdirectory name`: 当前路径是否为目录
    * `file isfile name`: 当前路径是否为文件
    * ==`file join name ?name ...?`: 拼接路径==
    * `file link ?-linktype? linkName ?target?`: 创建链接
    * `file lstat name varName`: 与`stat`类似, 用于链接路径
    * ==`file mkdir dir ?dir ...?`: 创建目录==
    * `file mtime name ?time?`: 返回文件最后被修改的时间, 十进制文本
    * `file nativename name`: 返回平台特定的文件名
    * `file normalize name`: 返回规则的路径名
    * `file owned name`: 是否允许访问
    * `file pathtype name`: 当前路径的类型: 绝对, 相对, 卷相对
    * `file readable name`: 是否可读
    * `file readlink name`: 返回当前路径的链接路径
    * ==`file rename ?-force? ?--? source target`==
      ==`file rename ?-force? ?--? source ?source ...? targetDir`: 重命名==
    * `file rootname name`: 返回路径主干 (即: 删除路径中最后的扩展名)
    * `file separator ?name?`: 返回路径分隔符
    * `file size name`: 返回文件尺寸
    * `file split name`: 分割路径, 返回列表
    * `file stat name varName`: 获取文件信息, `varName` 可以是: `atime`, `ctime`, `dev`, `gid`, `ino`, `mode`, `mtime`, `nlink`, `size`, `type`, `uid`
    * `file system name`: 系统属性, 返回一个 2 元素的列表, 第一个是文件系统的名称, 第二个是磁盘格式
    * `file tail name`: 路径的最后一个元素
    * `file type name`: 返回文件的类型: `file`, `directory`, `characterSpecial`, `blockSpecial`, `fifo`, `link`, or `socket`
    * `file volumes`: 各卷的路径
    * `file writable name`: 文件是否可写

--------------------------------------------------------------------------------
# 9. 进程间通信

--------------------------------------------------------------------------------
# 10. 错误与异常

--------------------------------------------------------------------------------
# 11. 创建和使用脚本

--------------------------------------------------------------------------------
# 12. Tcl内部管理

--------------------------------------------------------------------------------
# 13. 历史

