<h1 style="text-align:center">System Verilog 语法总结</h1>

--------------------------------------------------------------------------------

<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->

<!-- code_chunk_output -->

- [1. 基本语法](#-1-基本语法-)
  - [1.1. 格式与注释](#-11-格式与注释-)
  - [1.2. 标识符](#-12-标识符-)
  - [1.3. 关键词](#-13-关键词-)
    - [1.3.1. 所有](#-131-所有-)
    - [1.3.2. 分类](#-132-分类-)
  - [1.4. 数据类型](#-14-数据类型-)
    - [1.4.1. 线网类型](#-141-线网类型-)
    - [1.4.2. 变量类型](#-142-变量类型-)
    - [1.4.3. 信号范围选取](#-143-信号范围选取-)
  - [1.5. 值](#-15-值-)
  - [1.6. 操作符](#-16-操作符-)
  - [1.7. 参数](#-17-参数-)
  - [1.8. 属性](#-18-属性-)
  - [1.9. 模块与端口](#-19-模块与端口-)
  - [1.10. 门级/结构建模](#-110-门级结构建模-)
  - [1.11. 数据流建模](#-111-数据流建模-)
  - [1.12. 行为描述](#-112-行为描述-)
    - [1.12.1. 过程语句类型](#-1121-过程语句类型-)
    - [1.12.2. 赋值](#-1122-赋值-)
    - [1.12.3. 事件控制](#-1123-事件控制-)
    - [1.12.4. 条件语句](#-1124-条件语句-)
    - [1.12.5. 分支语句](#-1125-分支语句-)
    - [1.12.6. 循环语句](#-1126-循环语句-)
    - [1.12.7. 语句块](#-1127-语句块-)
    - [1.12.8. 生成](#-1128-生成-)
  - [1.13. 任务和函数](#-113-任务和函数-)
  - [1.14. 属性](#-114-属性-)
- [2. 仿真与建模语法](#-2-仿真与建模语法-)
  - [2.1. 延时](#-21-延时-)
  - [2.2. 强行赋值](#-22-强行赋值-)
  - [2.3. 改写参数](#-23-改写参数-)
- [3. 编译指令](#-3-编译指令-)
- [4. 系统任务与函数](#-4-系统任务与函数-)
  - [4.1. 仿真控制任务](#-41-仿真控制任务-)
  - [4.2. 返回当前时间任务](#-42-返回当前时间任务-)
  - [4.3. 时间标度](#-43-时间标度-)
  - [4.4. 变换函数](#-44-变换函数-)
  - [4.5. 数据查询函数](#-45-数据查询函数-)
  - [4.6. 数组查询](#-46-数组查询-)
  - [4.7. 数学函数](#-47-数学函数-)
  - [4.8. bit 向量函数](#-48-bit-向量函数-)
  - [4.9. 错误与警告函数](#-49-错误与警告函数-)
  - [4.10. 断言控制函数](#-410-断言控制函数-)
  - [4.11. 采样函数](#-411-采样函数-)
  - [4.12. 覆盖率控制函数](#-412-覆盖率控制函数-)
  - [4.13. 随机分布函数](#-413-随机分布函数-)
  - [4.14. 随机分析函数](#-414-随机分析函数-)
  - [4.15. 其他函数](#-415-其他函数-)
  - [4.16. 显示任务](#-416-显示任务-)
  - [4.17. 文件输入/输出](#-417-文件输入输出-)
    - [4.17.1. 读取CSV](#-4171-读取csv-)
  - [4.18. 值变转储 (VCD) 文件](#-418-值变转储-vcd-文件-)
  - [4.19. 时序检验](#-419-时序检验-)

<!-- /code_chunk_output -->

--------------------------------------------------------------------------------
# 1. 基本语法

## 1.1. 格式与注释
* 语句通常以`;`结尾, 可跨行
* 注释: `//` 或 `/* ... */`

## 1.2. 标识符
* 以字母、下划线(`_`)开头
* 由字母、数字、下划线(`_`)、`$`组成
* 可转义标识符 `\`
* 区分大小写

## 1.3. 关键词

### 1.3.1. 所有
``` verilog
accept_on, alias, always, always_comb, always_ff, always_latch, and, assert, assign, assume, automatic
before, begin, bind, bins, binsof, bit, break, buf, bufif0, bufif1, byte
case, casex, casez, cell, chandle, checker, class, clocking, cmos, config, const, constraint, context, continue, cover, covergroup, coverpoint, cross
deassign, default, defparam, design, disable, dist, do
edge, else, end, enum, event, eventually, expect, export, extends, extern,
            endcase, endchecker, endclass, endclocking, endconfig, endfunction, endgenerate, endgroup, endinterface, endmodule, endpackage, endprimitive, endprogram, endproperty, endspecify, endsequence, endtable, endtask
final, first_match, for, force, foreach, forever, fork, forkjoin, function
generate, genvar, global
highz0, highz1
if, iff, ifnone, ignore_bins, illegal_bins, implements, implies, import, incdir, include, initial, inout, input, inside, instance, int, integer, interconnect, interface, intersect
join, join_any, join_none
large, let, liblist, library, local, localparam, logic, longint
macromodule, matches, medium, modport, module
nand, negedge, nettype, new, nexttime, nmos, nor, noshowcancelled, not, notif0, notif1, null
or, output
package, packed, parameter, pmos, posedge, primitive, priority, program, property, protected, pull0, pull1, pulldown, pullup, pulsestyle_ondetect, pulsestyle_onevent, pure
rand, randc, randcase, randsequence, rcmos, real, realtime, ref, reg, reject_on, release, repeat, restrict, return, rnmos, rpmos, rtran, rtranif0, rtranif1
s_always, s_eventually, s_nexttime, s_until, s_until_with, scalared, sequence, shortint, shortreal, showcancelled, signed, small, soft, solve, specify, specparam, static, string, strong, strong0, strong1, struct, super, supply0, supply1, sync_accept_on, sync_reject_on
table, tagged, task, this, throughout, time, timeprecision, timeunit, tran, tranif0, tranif1, tri, tri0, tri1, triand, trior, trireg, type, typedef
union, unique, unique0, unsigned, until, until_with, untyped, use, uwire
var, vectored, virtual, void
wait, wait_order, wand, weak, weak0, weak1, while, wildcard, wire, with, within, wor
xnor, xor
```

### 1.3.2. 分类
|    类别    | 关键词                                                                                                                                      |
| :--------: | ------------------------------------------------------------------------------------------------------------------------------------------- |
|    模块    | ==**module ... endmodule**==, macromodule                                                                                                   |
|    接口    | ==**interface ... endinterface**==, ==**modport**==, import, export, clocking ... endclocking, global, forkjoin                             |
|    参数    | ==**parameter**==, ==**localparam**==, **const**, ~~defparam~~                                                                              |
|    端口    | ==**input**==, ==**output**==, ==**inout**==, ref                                                                                           |
|  数据类型  | 线网: ==**wire/logic**==, **uwire**, wand, wor, tri, triand, trior, tri0, tri1, trireg, supply0, supply1, interconnect                      |
|     ^      | 变量 (基本): ==**reg/logic**==, **integer**, bit, byte, shortint, int, longint, **real**, shortreal, **time**, realtime                     |
|     ^      | 变量 (高级): var, **string**, ==**enum**==, ==**struct**==, union, ==**packed**==, tagged, chandle                                          |
|     ^      | 修饰:  ==**signed, unsigned**==, scalared, vectored                                                                                         |
|     ^      | 信号强度: supply0, strong0, pull0, weak0, highz0, supply1, strong1, pull1, weak1, highz1; large, medium, small                              |
|     ^      | 自定义: ==**typedef**==, nettype ... with, alias                                                                                            |
|     ^      | 动态: new                                                                                                                                   |
|     值     | void, null                                                                                                                                  |
|   操作符   | **type**, ==**inside**==, ==**dist**==, bind, let                                                                                           |
|  信号赋值  | ==**assign**== ... **deassign**, **force** ... **release**                                                                                  |
|  过程控制  | ==**initial**==, final, ==**always/always_ff/always_comb/always_latch**==, ==**begin ... end**==, **fork ... join/join_any/join_none**      |
|    事件    | **event**, ==**or**==, **iff**, ==**posedge, negedge**==, edge, **wait**, wait fork, wait_order                                             |
|    条件    | ==**if.. else**==, ==**case/casex/casez ... default ... endcase**==, ==**unique, unique0, priority**==, matches                             |
|    循环    | ==**for**==, ==**foreach**==, **while**, **do ... while**, **repeat**, **forever**, **continue**, **break**                                 |
| 任务与函数 | ==**task ... endtask**==, ==**function ... endfunction**==, return, automatic, static, context                                              |
|    生成    | ==**genvar ... generate ... endgenerate**==                                                                                                 |
|   门模型   | 多输入: and, nand, or, nor, xor, xnor                                                                                                       |
|     ^      | 多输出: buf, not                                                                                                                            |
|     ^      | 三态门: bufif0, bufif1, notif0, notif1                                                                                                      |
|     ^      | 双向开关: tran, tranif0, tranif1, rtran, rtranif0, rtranif1                                                                                 |
|     ^      | MOS: cmos, nmos, pmos, rcmos, rnmos, rpmos                                                                                                  |
|     ^      | 上下拉: pulldown, pullup                                                                                                                    |
|    原语    | primitive ... endprimitive, table ... endtable                                                                                              |
|  设计管理  | ==**include**==, **package ... endpackage**, library, config ... endconfig, design, instance, liblist, cell, use, incdir                    |
|  时序建模  | **timeunit**, **timeprecision**, specify ... endspecify, specparam, ifnone                                                                  |
|    验证    | program ... endprogram, checker ... endchecker,                                                                                             |
|    断言    | assert, assume, cover, restrict, sequence ... endsequence, intersect, first_match, throughout, within, untyped, expect                      |
|  property  | property ... endproperty, strong, weak, nexttime, s_nexttime, s_always, eventually, s_eventually, until, until_with, s_until, s_until_with, |
|     ^      | implies, accept_on, reject_on, sync_accept_on, sync_reject_on,                                                                              |
|   覆盖率   | covergroup ... endgroup, coverpoint, wildcard, bins, binsof, ignore_bins, illegal_bins, cross                                               |
|  面向对象  | class ... endclass, this, virtual, extends, implements, extern, pure, static, protected, local, super, constraint                           |
|    随机    | rand, randc, randcase, randsequence, before, solve, soft                                                                                    |
|    其他    | pulsestyle_onevent, pulsestyle_ondetect, showcancelled, noshowcancelled                                                                     |

## 1.4. 数据类型

### 1.4.1. 线网类型
* 线网类型: `wire`, `logic`, `uwire`, `wand`, `wor`, `tri`, `triand`, `trior`, `tri0`, `tri1`, `trireg`, `supply0`, `supply1`
* 格式
    ```verilog
    线网 [signed] [延迟] 变量列表;
    线网 [驱动强度] [signed] [延迟] 变量列表;
    线网 [vectored|scalared] [signed] 范围 [延迟] 变量列表;
    线网 [驱动强度] [vectored|scalared] [signed] 范围 [延迟] 变量列表;
    trireg [驱动强度|电荷强度] [signed] [延迟] 变量列表;
    trireg [驱动强度|电荷强度] [vectored|scalared] [signed] 范围 [延迟] 变量列表;
    ```
* 关键词 `scalared` 或 `vectored` 用于修饰线网类型
    * 向量类型可以截取范围访问
    * 标量类型只能整体访问
* 可用 `signed` 或 `unsigned` 修饰
* 自定义线网 `nettype`
    ```sv
    nettype 数据类型 线网名 [with [包或类::] 任务函数名]
    nettype 自定义线网 新的自定义线网名
    ```
    * 限制
        * 4 值整型, 包括 packed array, packed struct or union
        * 2 值整型, 包括 packed array, packed struct or union
        * `real`, `shortreal`
        * 固定长度的 unpacked array, unpacked struct or union
* `interconnect`
    * 线网的抽象
* 驱动强度 (仅用于仿真):
    ```verilog
    ( strength0 , strength1 )
    ( strength1 , strength0 )
    ( strength0 , highz1 )
    ( strength1 , highz0 )
    ( highz0 , strength1 )
    ( highz1 , strength0 )
    ```
    * 其中:
        ```verilog
        strength0 ::= supply0 | strong0 | pull0 | weak0
        strength1 ::= supply1 | strong1 | pull1 | weak1
        ```
* 电荷强度 (仅用于仿真):
    ```verilog
    电荷强度 ::= ( small ) | ( medium ) | ( large )
    ```

### 1.4.2. 变量类型
* 基本类型: `logic`, `reg`, `integer`, `bit`, `byte`, `shortint`, `int`, `longint`, `real`, `shortreal`, `time`, `realtime`
* 高级类型: `string`, `enum`, `struct`, `union`, `class`, `chandle`
* 格式
    ```verilog
    [const] [var] <bit|logic|reg> [signed|unsigned] [范围] 变量列表;
    [const] [var] <byte|shortint|int|longint|integer|time> [signed|unsigned] 变量列表;
    [const] [var] <shortreal|real|realtime> 变量列表;
    [const] [var] <struct|union> [packed [signed|unsigned]] {成员变量} [范围] 变量列表;
    [const] [var] enum 枚举数据类型 {枚举成员} [范围] 变量列表;
    [const] [var] string 变量列表;
    [const] [var] chandle 变量列表
    ```
* 基本类型
    |    类型     |   值集合   | 默认值 | 位宽  |  默认符号  |
    | :---------: | :--------: | :----: | :---: | :--------: |
    |    `bit`    |    0, 1    |   '0   | 任意  | `unsigned` |
    |   `logic`   | 0, 1, x, z |   'x   | 任意  | `unsigned` |
    |    `reg`    | 0, 1, x, z |   'x   | 任意  | `unsigned` |
    |  `integer`  | 0, 1, x, z |   'x   |  32   |  `signed`  |
    |   `byte`    |    0, 1    |   '0   |   8   |  `singed`  |
    | `shortint`  |    0, 1    |   '0   |  16   |  `singed`  |
    |    `int`    |    0, 1    |   '0   |  32   |  `singed`  |
    |  `longint`  |    0, 1    |   '0   |  64   |  `singed`  |
    | `shortreal` |     x      |  0.0   |  32   |     x      |
    |   `real`    |     x      |  0.0   |  64   |     x      |
    |   `time`    | 0, 1, x, z |   'x   |  64   | `unsigned` |
    | `realtime`  |     x      |  0.0   |  64   |     x      |

    * `real` 和 `realtime` 完全相同
    * 可声明为数组, 格式`[范围] <数组名> [序号范围]`
        * `reg`形数组也叫做**存储器**
        * `<数组名> [序号]` 是标量, 不能选取位宽
            * 可以用等宽的临时变量间接赋值
        ```verilog
        // 声明
        reg [0:3] myMem1 [0:63]  // 64 个 4 位寄存器的数组
        reg myMem2 [1:5]  // 5 个 1 位寄存器的数组
        // 灵活的设置位宽
        reg [3:0] tmpReg;
        tmpReg = myMem1[7]; // 可以使用 tmpReg 进行范围选取
        tmpReg[3:2] ~= tmpReg[1:0];
        myMem1[7] = tmpReg; // tmpReg 操作完成后, 赋值给数组中的某个元素
        ```
* `string`
    * 语法: `[const] [var] string 变量列表;`
    * `string变量.方法(...)`
        | 方法                          | 说明                     |
        | :---------------------------- | :----------------------- |
        | `int len()`                   | 长度                     |
        | `void putc(int i, byte c)`    | 用 *c* 替换第 *i* 个字符 |
        | `byte getc(int i)`            | 获取第 *i* 个字符        |
        | `string toupper()`            | 转为大写                 |
        | `string tolower()`            | 转为小写                 |
        | `int compare(string s)`       | 对比, 类似 `strcmp`      |
        | `int icompare(string s)`      | 对比, 大小写敏感         |
        | `string substr(int i, int j)` | 子字符串                 |
        | `integer atoi()`              | 解释为整数               |
        | `integer atohex()`            | 解释为十六进制数         |
        | `integer atooct()`            | 解释为八进制数           |
        | `integer atobin()`            | 解释为二进制数           |
        | `real atoreal()`              | 解释为实数               |
        | `void itoa(integer i)`        | 转为字符                 |
        | `void hextoa(integer i)`      | 转为字符                 |
        | `void octtoa(integer i)`      | 转为字符                 |
        | `void bintoa(integer i)`      | 转为字符                 |
        | `void realtoa(real r)`        | 转为字符                 |
* `enum`
    * 语法: `[const] [var] enum 枚举数据类型 {枚举成员} [范围] 变量列表;`
    * 如果未指定数据类型, 默认使用 `int`
    * 变量支持数组, 如
        ```verilog
        typedef enum { add=10, sub[5], jmp[6:8] } E1;
        // add = 10, sub0 = 11, ..., sub4 = 15, jmp6 = 16, ..., jmp8 = 18
        enum { register[2] = 1, register[2:4] = 10 } vr;
        // register0 = 1, register1 = 2, register 2 = 10, ..., register4 = 12
        ```
    * `enum变量.方法(...)`
        | 方法                              | 说明                |
        | :-------------------------------- | :------------------ |
        | `enum first()`                    | 返回第一个成员      |
        | `enum last()`                     | 返回最后一个成员    |
        | `enum next( int unsigned N = 1 )` | 返回之后第 N 个成员 |
        | `enum prev( int unsigned N = 1 )` | 返回之前第 N 个成员 |
        | `int num()`                       | 返回成员的数量      |
        | `string name()`                   | 返回成员的名称      |
* `struct`
    * 语法: `[const] [var] struct [packed [signed|unsigned]] {成员变量} [范围] 变量列表;`
    * 成员的访问: `.成员`
    * `packed`: 可被当作一个矢量数据,
    * 赋值: 使用 `'` 和 `{}` 操作符, 如
        ```verilog
        typedef struct {
            int addr = 1 + constant;
            int crc;
            byte data [4] = '{4{1}};
        } packet1;

        packet1 pi = '{1,2,'{2,3,4,5}}; //suppresses the typedef initialization
        ```
* `union`
    * 语法: `[const] [var] union [packed [signed|unsigned]] {成员变量} [范围] 变量列表;`
    * `tagged`: 需要类型检查
* 数组
    * packed 数组: `类型 "[" 范围 "]" 数组名`, 范围在数组名之前的数组
    * unpacked 数组: `类型 数组名 "[" 范围 "]"`, 范围在数组名之后的数组, 包括: 定长数组、动态数组、关联数组、队列等, 可由任意数据类型组成
        * 声明方式: `类型 数组名 {"[" 范围 "]"}` 或 `类型 数组名 {"[" 个数 "]"}`, 如
            ```verilog
            int Array[0:7][0:31]; // array declaration using ranges
            int Array[8][32]; // array declaration using sizes
            ```
    * 索引: `变量名 "[" 索引 "]"`
    * 动态数组: `类型 数组名 "[" "]"`, 声明式不指定范围或个数
        * 按需用 `new "[" 表达式 "]"` 动态赋值
* 自定义类型 `typedef`
    * 可结合 `interface` 使用, 提高 `module` 的灵活性
* 可用 `var` 声明变量, 如果没有指定类型, 默认为 `logic`

### 1.4.3. 信号范围选取
* `[某位]`
* `[高位 : 低位] ` 或 `[低位 : 高位]`
* `[起始位 +: 宽度]` 或 ` [起始位 -: 宽度]`

## 1.5. 值
* **四种基本值**: `0, 1, X/x, Z/z/?`
    * wire 的真值表
        | wire  |   0   |   1   |   x   |   z   |
        | :---: | :---: | :---: | :---: | :---: |
        |   0   |   0   |   x   |   x   |   0   |
        |   1   |   x   |   1   |   x   |   1   |
        |   x   |   x   |   x   |   x   |   x   |
        |   z   |   0   |   1   |   x   |   z   |
    * 其它类型请查阅 `EEE Std 1364-2001`
* **整数**
    * 普通十进制数
    * 基数格式:
        * 二进制: `[+/-] [宽度] 'B/b [01xXzZ?_]+`
        * 八进制: `[+/-] [宽度] 'O/o [0-7xXzZ?_]+`
        * 十进制: `[+/-] [宽度] 'D/d [0-9xXzZ?_]+`
        * 十六进制: `[+/-] [宽度] 'H/h [0-9a-fA-FxXzZ?_]+`
        <br/>
        * 如果**宽度** 比**值** 的宽度大, 左侧填充:
            * 如果常量最高位是`0/1`则填充`0`
            * 如果是`x/z`则填充`x/z`
        * 如果**宽度** 比**值** 的宽度小, 截断
        * 如果未定义宽度, 默认为数值的宽度, 例如: `'b1`是 1 bit, `'h1`是 4 bit
    * 下划线可随意用在数字中, 仅为了便于阅读

* **实数**
    * 普通十进制数 (0.xx 可以省略 0, 用 .xx 表示)
    * 支持`(e|E)`科学记数法
    * 下划线可随意用在数字中, 仅为了便于阅读

* **字符串**
    * 两个双引号(`"`)内的字符
    * 转义字符`\n, \t, \\, \", \ooo`

* **时间**
    * 单位: `s | ms | us | ns | ps | fs`
    * 字面量: 数字+单位, 中间无空格, 如: *1.2ns, 34ps*

* **结构体**
* **数组**
    * 类似 C 语言, 但使用 `{{}}`, 如:
        ``` Verilog
        int n[1:2][1:3] = '{'{0,1,2},'{3{4}}}
        ```

## 1.6. 操作符
* 操作符
    |                                                操作符                                                |    连接性     |
    | :--------------------------------------------------------------------------------------------------: | :-----------: |
    |                                          `()` `[]` `::` `.`                                          |      左       |
    |   `+` `-` `!` `~` `&` `~&` <code>&#124;</code> <code>~&#124;</code> `^` `~^`/`^~` `++` `--` (规约)   |       -       |
    |                                                 `**`                                                 |      左       |
    |                                             `*` `/` `%`                                              |       ^       |
    |                                            `+` `-` (二元)                                            |       ^       |
    |                                        `<<` `>>` `<<<` `>>>`                                         |       ^       |
    |                                  `<` `<=` `>` `>=` `inside` `dist`                                   |       ^       |
    |                                  `==` `!=` `===` `!==` `==?` `!=?`                                   |       ^       |
    |                                              `&` (二元)                                              |       ^       |
    |                                         `^` `~^`/`^~` (二元)                                         |       ^       |
    |                                      <code>&#124;</code> (二元)                                      |       ^       |
    |                                                 `&&`                                                 |       ^       |
    |                                      <code>&#124;&#124;</code>                                       |       ^       |
    |                                                 `?:`                                                 |      右       |
    |                                              `–>` `<–>`                                              |       ^       |
    | `=` `+=` `-=` `*=` `/=` `%=` `&=` `^=` <code>&#124;=</code> `<<=` `>>=` `<<<=` `>>>=` `:=` `:/` `<=` |     None      |
    |                                             `{}` `{{}}`                                              | Concatenation |
    * 注 优先级由上到下降低, 从左到右降低

* 拼接及复制操作符:
    * `{变量1, 变量2, 变量3 ...}`
    * `{重复次数 { 变量 } }`
* casting: `'` (单引号)
    * 语法: `类型 ' (变量或值)`
    * 语法: `位宽 ' (变量或值)` 适配到制定位宽
    * 语法: `' 变量或值` 位宽适配到变量
    * 语法: `<signed | unsigned> ' (变量或值)` 转为有/无符号数
    * 语法: `const ' (变量或值)` 转为常量
    * 语法: `$cast(singular dest_var, singular source_exp)` 动态转换
    * 系统函数: `$itor`, `$rtoi`, `$bitstoreal`, `$realtobits`, `$signed`, `$unsigned`
* 获取数据类型 `type`
    * 语法: `type (变量)`, 如
        ```verilog
        var type(a+b) c, d;
        c = type(i+3)'(v[15:0]);

        bit [12:0] A_bus, B_bus;
        parameter type bus_t = type(A_bus);
        generate
            case (type(bus_t))
                type(bit[12:0]): addfixed_int #(bus_t) (A_bus,B_bus);
                type(real):      add_float #(type(A_bus)) (A_bus,B_bus);
            endcase
        endgenerate
        ```

## 1.7. 参数
``` verilog
<parameter|localparam> [signed|unsigned] [范围] 变量列表
<parameter|localparam> 数据类型 参数列表
<parameter|localparam> type 类型列表
```
* 可用于 `module`, `interface`, `program`, `class`, `package`
* `$` 用于参数时, 表示未确定
* `type`
    ```verilog
    module ma
    #( parameter p1 = 1, parameter type p2 = shortint )
    (input logic [p1:0] i, output logic [p1:0] o);
        p2 j = 0; // type of j is set by a parameter, (shortint unless redefined)
        always @(i) begin
            o = i;
            j++;
        end
    endmodule

    module mb;
        logic [3:0] i,o;
        ma #(.p1(3), .p2(int)) u1(i,o); //redefines p2 to a type of int
    endmodule
    ```

## 1.8. 属性
* 格式: `(* 属性 [= 值] {, 属性2 [= 值2]} *) `
* 可用于限定信号或模块, 综合器, 布局布线器可以识别
* 如果没有指定值, 默认 = 1

## 1.9. 模块与端口
``` verilog
module <module_name> (
   input  [线网类型] [signed] [范围] <input_port_name>,
   // ...<other_inputs>...
   output [线网类型] [signed] [范围] <output_port_name>,
   output [reg] [signed] [范围] <output_port_name>,
   output [integer|time] <output_port_name>,
   // ...<other_outputs>...
   inout  [线网类型] [signed] [范围] <inout_port_name>,
   // ...<other_inouts>...
);
```
* 层次路径: `第一层模块名.第2层模块名.第n层模块名.元素`

## 1.10. 门级/结构建模
* **模块例化**
    ``` verilog
    模块名 例化名(
        端口映射
    );

    模块名 #(
        参数映射列表
    ) 例化名 (
        端口映射
    );
    ```
* **端口映射**
    * **顺序映射**: 映射的端口或声明的顺序一样
    * **命名映射**: `.模块信号名 (映射信号名),`
    * **输入端口**: 内部可以是 `wire` 或 `reg`, 外部可以是 `wire` 或 `reg`
    * **输出端口**: 内部可以是 `wire` 或 `reg`, 外部必须是 `wire`
    * **双向端口**: 内部可以是 `wire` 或 `reg`, 外部必须是 `wire`
    * **位宽匹配**: 从右向左匹配, 多余位截取, 不足的填充 0 (或x/z)
    * **未连接**: 一般默认为 0
* 内建的门和开关
    | n 输入门 | n 输出门 | 三态门 |  上拉门  | MOS 开关 | 双向开关 |
    | :------: | :------: | :----: | :------: | :------: | :------: |
    |   and    |   buf    | bufif0 | pulldown |   cmos   |  rtran   |
    |   nand   |   not    | bufif1 |  pullup  |   nmos   | rtranif0 |
    |   nor    |    -     | notif0 |    -     |   pmos   | rtranif1 |
    |    or    |    -     | notif1 |    -     |  rcmos   |   tran   |
    |   xnor   |    -     |   -    |    -     |  rnmos   | tranif0  |
    |   xor    |    -     |   -    |    -     |  rpmos   | tranif1  |
* 用户可以自定义原型
    * 实例
    ``` verilog
    primitive multiplexer (mux, control, dataA, dataB);
        output mux;
        input control, dataA, dataB;
        table
            // control dataA dataB mux
            0 1 ? : 1 ; // ? = 0 1 x
            0 0 ? : 0 ;
            1 ? 1 : 1 ;
            1 ? 0 : 0 ;
            x 0 0 : 0 ;
            x 1 1 : 1 ;
        endtable
    endprimitive
    ```
* 可以用 `config ... endconfig` 为某个例化模块指定使用的库

## 1.11. 数据流建模
* **连续赋值语句**
    ``` verilog {.line-numbers}
    assign 信号 = 值;
    assign 信号 = (条件) ? 值1 : 值2;
    assign 信号 = (条件1) ? 值1 : (条件2) ? 值2 : ...
    ```
* **线网说明赋值**
    ``` verilog {.line-numbers}
    wire 信号 = 值;
    ```
    * 如果位数不匹配, 从右往左赋值, 多余位被截断, 不足的左侧补0 (或x/z)

## 1.12. 行为描述

### 1.12.1. 过程语句类型
``` verilog
always ...
//
initial ...
```
### 1.12.2. 赋值
* **隐式赋值**: 声明的时候赋值
    ``` verilog
    reg 信号 = 值;
    integer 变量 = 值;
    real 变量 = 值;
    time 变量 = 值;
    ```
* **语句中赋值**
    * 阻塞赋值 `变量 <= 值`
    * 非阻塞赋值 `变量 = 值`
* 如果位数不匹配, 从右往左赋值, 多余位被截断, 不足的左侧补0 (或x/z)

### 1.12.3. 事件控制
* 常规事件控制
    * `@ (posedge 信号)`
    * `@ (negedge 信号)`
* OR事件控制
    * `@ (事件1 or 事件2 or ...)`
    * `@ (事件1 , 事件2, ...)`
* 电平敏感时序控制
    * `@事件`
    * `@(事件列表)`
    * `@*`
    * `@(*)`
    * 判断: `wait(事件判断条件)`
* 命令事件控制
    * 声明: `event 事件名 [= 值 | null]`
    * 触发: `-> 事件名`
    * 判断: `@ (事件名)`

### 1.12.4. 条件语句
``` verilog {.line-numbers}
if(条件) ...
else if(条件) ...
else if(条件) ...
else ...
```

### 1.12.5. 分支语句
``` verilog {.line-numbers}
case(表达式) ...
    分支1 :  ...
    分支2 :  ...
    分支3 :  ...
    default :  ...
endcase
```
* 变种 `casex`, `casez`
    * 区别:
        * `case`  treats `z` & `x`  as it is
        * `casez` treats `z`        as dont care
        * `casex` treats `z` & `x`  as dont care
    * 综合时, case列表里面的x和z被综合工具认为是不可达到的状态就被去掉了, casez和casex里面的x/z都被认为是don't care, 所以综合出的电路会是一致的

### 1.12.6. 循环语句
``` verilog {.line-numbers}
//--------------------------------
// 条件循环
while (条件) ...
//--------------------------------
// 增量或减量循环
for (初始化语句, 条件, 控制变量更改语句) ...
//--------------------------------
// 循环n次
repeat (次数) ...
//--------------------------------
// 无条件循环
forever ...
```
* 退出循环: 使用 `disable` 语句
    ``` verilog
    begin: break
        for(i=1;i<5;i=i+1) begin: continue
            if(a==0)
                disable break;      //从 break 这个 begin..end 中跳出, 终止了 for
            if(a==1)
                disable continue;   //从 continue 这个 begin..end 块中跳出, 从本次循环中跳出
        end
    end
    ```

### 1.12.7. 语句块
``` verilog {.line-numbers}
//--------------------------------
// 顺序块
begin [: 块名称]
    ...
end
//--------------------------------
// 并行块
fork [: 块名称]
    ...
join
//--------------------------------
// 禁用语句块
...
disable 块名称
...
```

### 1.12.8. 生成
``` verilog {.line-numbers}
//--------------------------------
// 循环生成
genvar 变量;
generate
    for (变量=0; 变量 < 上限; 变量=变量+1)
        ...
endgenerate
//--------------------------------
// 条件生成
generate
    if (条件) ...
    else if (条件) ...
    else ...
endgenerate
//--------------------------------
// 分支生成
generate
    case (表达式)
        值1: ...
        值2: ...
        default: ...
    endcase
endgenerate
```

## 1.13. 任务和函数
``` verilog {.line-numbers}
//--------------------------------
// 传统格式
task [automatic] 任务名;
    input  数据类型 端口名称,
    output 数据类型 端口名称
    begin
        ...
    end
endtask
//--------------------------------
// ANSI 格式
task [automatic] 任务名(
    input  数据类型 端口名称,
    output 数据类型 端口名称
);
    begin
        ...
    end
endtask
```
``` verilog {.line-numbers}
//--------------------------------
// 传统格式
function [automatic | signed] 数据类型 函数名;
    input 数据类型 端口名称,
    begin
        ...
    end
endfunction
//--------------------------------
// ANSI 格式
function [automatic | signed] 数据类型 函数名(
    input 数据类型 端口名称,
);
    begin
        ...
    end
endfunction
```
* `automatic` 表示自动重入任务, 每次调用任务使用独立的空间
* 函数支持递归调用

## 1.14. 属性
* 综合器, 布局布线器可以识别
* 语法:
    ```verilog
    (* 属性名 = 属性值 { , 属性名 = 属性值 } *)
    ```

--------------------------------------------------------------------------------
# 2. 仿真与建模语法

## 2.1. 延时
* **延时模型**:
    * `# 数字`
    * `#(上升延时, 下降延时)`
    * `#(上升延时, 下降延时, 关断延时)`
    * 每个延时都可以用 `(最小延时 : 典型延时 : 最大延时)` 表示
* **路径延时建模**
    ``` verilog
    specify
    ...
    endspecify
    ```

## 2.2. 强行赋值
``` verilog
assign ... deassign
force ... release
```

## 2.3. 改写参数
``` verilog
defparam 参数名 = 参数值;
```

--------------------------------------------------------------------------------
# 3. 编译指令
* **常用**
    1. ``` `include ```
    1. ``` `define, `undef,  `undefineall```
    1. ``` `ifdef, `ifndef, `else, `elsif, `endif```
    1. ``` `timescale ```

* **其他**
    1. ``` `__FILE__``` ``` `__LINE__ ```
    1. ``` `begin_keywords ... `end_keywords```
    1. ``` `celldefine, `endcelldefine```
    1. ``` `default_nettype```
    1. ``` `line```
    1. ``` `unconnected_drive, `nounconnected_drive ```
    1.  ``` `resetall ```
    1.  ``` `pragma```
    1. ``` `default_decay_time, `default_trireg_strength, `delay_mode_distributed, `delay_mode_path, `delay_mode_unit, `delay_mode_zero```

    <!-- 9. ``` `accelerate, `noaccelerate```
    10. ``` `autoexpand_vectornets, `expand_vectornets, `noexpand_vectornets```
    12. ``` `protect, `endprotect```
    13. ``` `protected, `endprotected```
    14. ``` `remove_gatenames, `noremove_gatenames```
    15. ``` `remove_netnames, `noremove_netnames``` -->

--------------------------------------------------------------------------------
# 4. 系统任务与函数

## 4.1. 仿真控制任务
* 暂停: `$stop`
* 结束: `$finish`
* 推出: `$exit`

## 4.2. 返回当前时间任务
* `$time`: 返回时间, 64位整型
* `$stime`: 返回时间, 32位整型
* `$realtime`: 返回时间, 实数

## 4.3. 时间标度
* 打印时间标度: `$printtimescale`
* 设置打印时间标度的格式: `$timeformat(units_number,precision, suffix, numeric_field_width);`
    * 其中: `units_numbers` 是 $10^n$ 秒, 如 -6 表示 1 us

## 4.4. 变换函数
| 函数                                            | 说明                                 |
| :---------------------------------------------- | :----------------------------------- |
| `$cast(singular dest_var, singular source_exp)` | 类型转换                             |
| `$signed (<argument>)`                          | 转为有符号                           |
| `$unsigned (<argument>)`                        | 转为无符号                           |
| `integer $rtoi (real_val)`                      | 实数转整数                           |
| `real $itor (int_val)`                          | 整数转实数                           |
| `[63:0] $realtobits (real_val)`                 | 实数转64位实数向量表示法 (IEEE 754)  |
| `[31:0] $shortrealtobits (shortreal_val)`       | 实数转32位实数向量表示法 (IEEE 754)  |
| `real $bitstoreal (bit_val)`                    | 实数向量表示法 (IEEE 754) 转64位实数 |
| `shortreal $bitstoshortreal (bit_val)`          | 实数向量表示法 (IEEE 754) 转32位实数 |

## 4.5. 数据查询函数
| 函数           | 说明 |
| :------------- | :--- |
| `$bits`        |
| `$isunbounded` |
| `$typename`    |

## 4.6. 数组查询
| 函数                   | 说明 |
| :--------------------- | :--- |
| `$unpacked_dimensions` |
| `$dimensions`          |
| `$left, right`         |
| `$low, high`           |
| `$increment`           |
| `$size`                |

## 4.7. 数学函数
| 函数                                                  | 说明     |
| :---------------------------------------------------- | :------- |
| `$clog2, $ln, $log10`                                 | 对数函数 |
| `$exp, $pow, $sqrt`                                   | 幂指函数 |
| `$floor, $ceil`                                       | 取整函数 |
| `$sin, $cos, $tan, $asin, $acos, $atan, $atan2`       | 三角函数 |
| `$hypot, $sinh, $cosh, $tanh, $asinh, $acosh, $atanh` | 双曲函数 |

## 4.8. bit 向量函数
| 函数                     | 说明 |
| :----------------------- | :--- |
| `$countbits, $countones` |
| `$onehot, $onehot0`      |
| `$isunknown`             |

## 4.9. 错误与警告函数
| 函数       | 说明 |
| :--------- | :--- |
| `$fatal`   |
| `$error`   |
| `$warning` |
| `$info`    |

## 4.10. 断言控制函数
| 函数                                     | 说明 |
| :--------------------------------------- | :--- |
| `$asserton, $assertoff`                  |
| `$assertkill, $assertcontrol`            |
| `$assertpasson, $assertpassoff`          |
| `$assertfailon, $assertfailoff`          |
| `$assertnonvacuouson, $assertvacuousoff` |

## 4.11. 采样函数
| 函数                           | 说明 |
| :----------------------------- | :--- |
| `$sampled, $rose`              |
| `$fell, $stable`               |
| `$changed, $past`              |
| `$past_gclk, $rose_gclk`       |
| `$fell_gclk, $stable_gclk`     |
| `$changed_gclk, $future_gclk`  |
| `$rising_gclk, $falling_gclk`  |
| `$steady_gclk, $changing_gclk` |

## 4.12. 覆盖率控制函数
| 函数                    | 说明 |
| :---------------------- | :--- |
| `$coverage_control`     |
| `$coverage_get_max`     |
| `$coverage_get`         |
| `$coverage_merge`       |
| `$coverage_save`        |
| `$get_coverage`         |
| `$set_coverage_db_name` |
| `$load_coverage_db`     |

## 4.13. 随机分布函数
| 函数                                            | 说明                           |
| :---------------------------------------------- | :----------------------------- |
| `signed int = $random [(seed)]`                 | 返回一个 32 位有符号整数随机数 |
| `$dist_uniform (seed, start, end)`              | 均匀分布                       |
| `$dist_normal (seed, mean, standard_deviation)` | 正态分布                       |
| `$dist_exponential (seed, mean)`                | 指数分布                       |
| `$dist_poisson (seed, mean)`                    | 泊松分布                       |
| `$dist_chi_square (seed, degree_of_freedom)`    | 卡方分布                       |
| `$dist_t (seed, degree_of_freedom)`             | t 分布                         |
| `$dist_erlang (seed, k_stage, mean)`            | 埃尔朗分布                     |

## 4.14. 随机分析函数
| 函数            | 说明 |
| :-------------- | :--- |
| `$q_initialize` |
| `$q_add`        |
| `$q_remove`     |
| `$q_full`       |
| `$q_exam`       |

## 4.15. 其他函数
| 函数      | 说明 |
| :-------- | :--- |
| `$system` |

## 4.16. 显示任务
* **格式**: `任务名 (格式说明1, 参数列表1, 格式说明2, 参数列表2, ...);`
* **显示和写入任务名**:
    * `$display`,`$displayb`, `$displayh`, `$displayo`
    * `$write`,`$writeb`, `$writeh`, `$writeo`
    * 其中: `b/h/o`表示没有格式说明时, 以 bin/hex/oct 格式显示
* **探测任务**: `$strobe`, `$strobeb`, `$strobeo`, `$strobeh`
    * 事件结束时显示
* **连续监控**: `$monitor`, `$monitorb`, `$monitoro`, `$monitorh`
    * 只要参数有变化, 整个参数表就在时间步结束时显示
    * 可以使用 `$monitoroff` 或 `$monitoron` 禁用或启用所有监控任务
* **转义字符**
    | 符号  | 说明                  |
    | :---: | --------------------- |
    |  \n   | 换行                  |
    |  \t   | 制表符                |
    | \\\\  | 字符 `\`              |
    |  \"   | 字符 `"`              |
    | \ooo  | 值为八进制值ooo的字符 |
    |  %%   | 字符 `%`              |
* **格式说明**
    |   符号   | 说明                |
    | :------: | :------------------ |
    | %b 或 %B | 二进制              |
    | %o 或 %O | 八进制              |
    | %d 或 %D | 十进制              |
    | %h 或 %H | 十六进制            |
    | %f 或 %F | 浮点数              |
    | %e 或 %E | 科学计数法          |
    | %g 或 %G | ^                   |
    | %t 或 %T | 当前时间格式        |
    | %c 或 %C | ASCII字符           |
    | %s 或 %S | 字符串              |
    | %m 或 %M | 层次名              |
    | %v 或 %V | 线网信号强度        |
    | %u 或 %U | 未格式化的 2 值数据 |
    | %z 或 %Z | 未格式化的 4 值数据 |
* **数据的宽度**
    * 正数或浮点数
    * 0开头

## 4.17. 文件输入/输出
* 打开文件: `integer fd = $fopen (文件名, 类型)`
    | 类型               | 说明                             |
    | :----------------- | :------------------------------- |
    | "r", "rb"          | 只读, 文件须存在                 |
    | "w", "wb"          | 写, 如果文件存在则清空, 否则新建 |
    | "a", "ab"          | 追加, 如果文件存在则清空, 则新建 |
    | "r+", "r+b", "rb+" | 读写                             |
    | "w+", "w+b", "wb+" | 追加, 如果文件不存在则新建       |
    | "a+", "a+b", "ab+" | 读或追加, 如果文件不存在则新建   |
* 关闭文件: `$fclose (fd)`
* 格式化数据到字符串:
    * `字符串任务名 (output_reg, list_of_arguments)`
        * 字符串任务名: `$swrite | $swriteb | $swriteh | $swriteo`
    * `$sformat (output_reg, format, list_of_arguments)`
    * `$sformatf (..)`
* 写入文件: `写文件任务 (文件指针, 格式说明1, 参数列表1, 格式说明2, 参数列表2, ... );`
    * `$fdisplay`, `$fdisplayb`, `$fdisplayh`, `$fdisplayo`
    * `$fwrite`, `$fwriteb`, `$fwriteh`, `$fwriteo`
    * `$fstrobe`, `$fstrobeb`, `$fstrobeh`, `$fstrobeo`
    * `$fmonitor`, `$fmonitorb`, `$fmonitorh`, `$fmonitoro`
    * `$writememb $writememh`
* 读取文件:
    | 函数                                                            | 说明                                                                   |
    | :-------------------------------------------------------------- | :--------------------------------------------------------------------- |
    | `c = $fgetc (fd)`                                               | 读一个字节到 c 中, 文件尾返回 -1                                       |
    | `integer code = $ungetc (c, fd )`                               | 插入一个字符 c 到 buffer 中, 下次调用 fgetc 时返回 c, 文件本身不受影响 |
    | `integer code = $fgets (str, fd)`                               | 读入一行字符到变量 str 中                                              |
    | `integer code = $fscanf (fd, format, args)`                     | 从文件 fd 中读取, 并格式化扫描, 变量存到 args 中                       |
    | `integer code = $sscanf (str, format, args)`                    | 并格式化扫描 str, 变量存到 args 中                                     |
    | `integer code = $fread (myreg, fd)`                             | 读取二进制数据                                                         |
    | `integer code = $fread (mem, fd)`                               | ^                                                                      |
    | `integer code = $fread (mem, fd, start)`                        | ^                                                                      |
    | `integer code = $fread (mem, fd, start, count)`                 | ^                                                                      |
    | `integer code = $fread (mem, fd, , count)`                      | ^                                                                      |
    | `$readmemb (文件名, memory_name [, start_addr [,finish_addr]])` | 从文件加载数据到内存数组                                               |
    | `$readmemh (文件名, memory_name [, start_addr [,finish_addr]])` | ^                                                                      |

* 文件定位:
    | 函数                                    | 说明                                    |
    | :-------------------------------------- | :-------------------------------------- |
    | `integer pos = $ftell (fd)`             | 获取当前位置                            |
    | `code = $fseek (fd, offset, operation)` | 改变文件位置                            |
    | `code = $rewind ( fd );`                | 改变文件位置, 等效于 `$fseek (fd,0,0)`; |
* 其他
    | 函数              | 说明     |
    | :---------------- | :------- |
    | `$fflush(fd)`     | 刷新文件 |
    | `$feof()`         |
    | `$ferror()`       |
    | `$sdf_annotate()` |

### 4.17.1. 读取CSV
``` verilog
reg [8*100:1] string;
integer sync_num;
reg [127:0] tdata;
reg is_sync;
reg is_talst;

initial begin
    fp = $fopen("./Stim_Dat.csv", "r");   // 打开文件

    $fgets(string, fp);   // 跳过文件头
    $display("%s",string);

    $fscanf(fp, "%d,%h,%d,%d", sync_num, tdata, is_sync, is_talst); // 读取数据
    $display("%d, %h, %d, %d",sync_num, tdata, is_sync,is_talst);

    $fclose(fp);    // 关闭文件
end
```

## 4.18. 值变转储 (VCD) 文件
| 函数或函数                                            | 说明          |
| :---------------------------------------------------- | :------------ |
| `$dumpfile (文件名)`                                  | 指定 VCD 文件 |
| `$dumpvars (levels [, list_of_modules_or_variables])` | 指定 VCD 变量 |
| `$dumpon, $dumpoff`                                   | 启动/停止 VCD |
| `$dumpall, $dumplimit`                                | 生成检查点    |
| `$dumpflush`                                          | 刷新 VCD      |
| `$dumpports`                                          |
| `$dumpportson, $dumpportsoff`                         |
| `$dumpportsall, $dumpportslimit`                      | 生成检查点    |
| `$dumpportsflush`                                     | 刷新 VCD      |

## 4.19. 时序检验
| 函数或函数                                                                    | 说明           |
| :---------------------------------------------------------------------------- | :------------- |
| `$setup (data_event, reference_event, limit)`                                 | 建立时间       |
| `$hold (reference_event, data_event, limit)`                                  | 保持时间       |
| `$setuphold (dreference_event, data_event, setup_limit, hold_limit)`          | 简历和保持时间 |
| `$recovery (reference_event, data_event, limit)`                              | 恢复时间       |
| `$removal (reference_event, data_event, limit)`                               | 恢复时间       |
| `$recrem (reference_event, data_event, limit)`                                | 恢复时间       |
| `$skew (reference_event, data_event, limit)`                                  | 偏斜           |
| `$timeskew (reference_event, data_event, limit)`                              | 偏斜           |
| `$fullskew (reference_event, data_event, limit)`                              | 偏斜           |
| `$period (reference_event, limit)`                                            | 周期           |
| `$width (reference_event, limit, threshold)`                                  | 脉宽           |
| `$nochange (reference_event, data_event, start_edge_offset, end_edge_offset)` | 数据变化       |
