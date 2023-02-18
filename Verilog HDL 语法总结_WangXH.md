<h1 style="text-align:center">Verilog 语法总结</h1>

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
  - [1.5. 值集合](#-15-值集合-)
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
- [2. 仿真与建模语法](#-2-仿真与建模语法-)
  - [2.1. 延时](#-21-延时-)
  - [2.2. 强行赋值](#-22-强行赋值-)
  - [2.3. 改写参数](#-23-改写参数-)
- [3. 编译指令](#-3-编译指令-)
- [4. 系统任务与函数](#-4-系统任务与函数-)
  - [4.1. 仿真控制任务](#-41-仿真控制任务-)
  - [4.2. 显示任务](#-42-显示任务-)
  - [4.3. 返回当前时间任务](#-43-返回当前时间任务-)
  - [4.4. 随机函数](#-44-随机函数-)
  - [4.5. 变换函数](#-45-变换函数-)
  - [4.6. 文件输入/输出](#-46-文件输入输出-)
    - [4.6.1. 读取CSV](#-461-读取csv-)
  - [4.7. 值变转储 (VCD) 文件](#-47-值变转储-vcd-文件-)
  - [4.8. 时间标度](#-48-时间标度-)
  - [4.9. 时序检验](#-49-时序检验-)

<!-- /code_chunk_output -->


--------------------------------------------------------------------------------
* 相关标准: IEEE Std 1364-2001; IEEE Std 1364-2005
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
always, and, assign, automatic,
begin, buf, bufif0, bufif1,
case, casex, casez, cell, cmos, config,
deassign, default, defparam, design, disable,
edge, else, end, endcase, endconfig, endfunction, endgenerate, endmodule, endprimitive, endspecify, endtable, endtask, event,
for, force, forever, fork, function,
generate, genvar,
highz0, highz1,
if, ifnone, incdir, include, initial, inout, input, instance, integer,
join,
large, liblist, library, localparam,
macromodule, medium, module,
nand, negedge, nmos, nor, noshowcancelled, not, notif0, notif1,
or, output,
parameter, pmos, posedge, primitive, pull0, pull1, pulldown, pullup, pulsestyle_onevent, pulsestyle_ondetect,
rcmos, real, realtime, reg, release, repeat, rnmos, rpmos, rtran, rtranif0, rtranif1,
scalared, showcancelled, signed, small, specify, specparam, strong0, strong1, supply0, supply1,
table, task, time, tran, tranif0, tranif1, tri, tri0, tri1, triand, trior, trireg,
unsigned, use,
vectored,
wait, wand, weak0, weak1, while, wire, wor,
xnor, xor
```

### 1.3.2. 分类
|    类别    | 关键词                                                                                                                  |
| :--------: | ----------------------------------------------------------------------------------------------------------------------- |
|    模块    | ==**module ... endmodule**==, macromodule                                                                               |
|    参数    | ==**parameter**==, ==**localparam**==, ~~defparam~~                                                                     |
|    端口    | ==**input**==, ==**output**==, ==**inout**==                                                                            |
|  数据类型  | 线网: ==**wire**==, wand, wor, tri, triand, trior, tri0, tri1, trireg, supply0, supply1                                 |
|     ^      | 寄存器:  ==**reg**==, **integer**, real, **time**, realtime                                                             |
|     ^      | 修饰:  ==**signed**==, ==**unsigned**==, scalared, vectored                                                             |
|     ^      | 信号强度: supply1, strong1, pull1, weak1, highz1, <br/>supply0, strong0, pull0, weak0, highz0 <br/>large, medium, small |
|  信号赋值  | ==**assign**== ... **deassign**, **force** ... **release**                                                              |
|  过程控制  | ==**initial**==, ==**always**==, ==**begin ... end**==, **fork ... join**, **disable**                                  |
|    事件    | ==**or**==, ==**posedge, negedge, edge**==, **event**, **wait**                                                         |
|    条件    | ==**if ... else**==, ==**case/casex/casez ... default ... endcase**==                                                   |
|    循环    | ==**for**==, **while**, **repeat**, **forever**                                                                         |
| 任务与函数 | ==**task ... endtask**==, ==**function ... endfunction**==, automatic                                                   |
|    生成    | ==**genvar ... generate ... endgenerate**==                                                                             |
|   门模型   | 多输入: and, nand, or, nor, xor, xnor                                                                                   |
|     ^      | 多输出: buf, not                                                                                                        |
|     ^      | 三态门: bufif0, bufif1, notif0, notif1                                                                                  |
|     ^      | 双向开关: tran, tranif0, tranif1, rtran, rtranif0, rtranif1                                                             |
|     ^      | MOS: cmos, nmos, pmos, rcmos, rnmos, rpmos                                                                              |
|     ^      | 上下拉: pulldown, pullup                                                                                                |
|    原语    | primitive ... endprimitive, table ... endtable                                                                          |
|  设计管理  | ==**include**==, library, config ... endconfig, design, instance, liblist, cell, use, incdir                            |
|  时序建模  | specify ... endspecify, specparam, ifnone                                                                               |
|    其他    | pulsestyle_onevent, pulsestyle_ondetect, showcancelled, noshowcancelled                                                 |

## 1.4. 数据类型

### 1.4.1. 线网类型
* 线网类型: `wire`, `wand`, `wor`, `tri`, `triand`, `trior`, `tri0`, `tri1`, `trireg`, `supply0`, `supply1`
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
* 变量类型: `reg`, `integer`, `real`, `realtime`, `time`
* 格式
    ```verilog
    reg [signed] [范围] 变量列表;
    integer 变量列表;
    real 变量列表;
    realtime 变量列表;
    time 变量列表;
    ```
* `real` 和 `realtime` 完全相同
* 可声明为数组, 格式`[bit范围] <数组名> [序号范围]`
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

### 1.4.3. 信号范围选取
* `[某位]`
* `[高位 : 低位] ` 或 `[低位 : 高位]`
* `[起始位 +: 宽度]` 或 ` [起始位 -: 宽度]`

## 1.5. 值集合
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

## 1.6. 操作符
* 操作符
    |                                   操作符                                    | 说明                     |
    | :-------------------------------------------------------------------------: | :----------------------- |
    |                                `{}`, `{{}}`                                 | 连接及复制运算符         |
    |                                  `+`, `-`                                   | 正负                     |
    |                                  `!`, `~`                                   | 一元逻辑非, 一元按位取反 |
    | `&`, `~&`, `^`, `^~`或`~^`, <code>&#124;&#124;</code>, <code>~&#124;</code> | 归约逻辑                 |
    |                        `**`,`*`, `/`, `%`, `+`, `-`                         | 数学运算                 |
    |                          `<<`, `<<<`, `>>`, `>>>`                           | 移位                     |
    |               `<`, `<=`, `>`, `>=`, `==`, `!=`, `===`, `!==`                | 比较                     |
    |               `&`, `^`, `^~`或`~^`, <code>&#124;&#124;</code>               | 按位逻辑运算             |
    |                       `&&`, <code>&#124;&#124;</code>                       | 逻辑运算                 |
    |                                    `?:`                                     | 条件操作符               |
    * 注 优先级由上到下降低, 从左到右降低
* 拼接及复制操作符:
    * `{变量1, 变量2, 变量3 ...}`
    * `{重复次数 { 变量 } }`


## 1.7. 参数
``` verilog
(parameter|localparam) [signed] [范围] 参数列表
(parameter|localparam) (integer|real|realtime|time) 参数列表
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
    * 声明: `event 事件名`
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
    1. ``` `define, `undef ```
    1. ``` `ifdef, `ifndef, `else, `elsif, `endif```
    1. ``` `timescale ```

* **其他**
    1. ``` `accelerate, `noaccelerate```
    1. ``` `autoexpand_vectornets, `expand_vectornets, `noexpand_vectornets```
    1. ``` `celldefine, `endcelldefine```
    1. ``` `default_nettype, `default_decay_time, `default_trireg_strength ```
    1. ``` `line```
    1. ``` `delay_mode_distributed, `delay_mode_path, `delay_mode_unit, `delay_mode_zero```
    1. ``` `protect, `endprotect```
    1. ``` `protected, `endprotected```
    1. ``` `remove_gatenames, `noremove_gatenames```
    1. ``` `remove_netnames, `noremove_netnames```
    1. ``` `resetall ```
    1. ``` `unconnected_drive, `nounconnected_drive ```

--------------------------------------------------------------------------------
# 4. 系统任务与函数

## 4.1. 仿真控制任务
* 暂停: `$stop`
* 结束: `$finish`

## 4.2. 显示任务
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

## 4.3. 返回当前时间任务
* `$time`: 返回时间, 64位整型
* `$stime`: 返回时间, 32位整型
* `$realtime`: 返回时间, 实数

## 4.4. 随机函数
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

## 4.5. 变换函数
| 函数                       | 说明                                |
| :------------------------- | :---------------------------------- |
| `$signed (<argument>)`     | 转为有符号                          |
| `$unsigned (<argument>)`   | 转为无符号                          |
| `$rtoi (real_value)`       | 实数转整数                          |
| `$itor (integer_value)`    | 整数转实数                          |
| `$realtobits (real_value)` | 实数转64位实数向量表示法 (IEEE 754) |
| `$bitstoreal (bit_value)`  | 实数向量表示法 (IEEE 754) 转实数    |

## 4.6. 文件输入/输出
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
* 写入文件: `写文件任务 (文件指针, 格式说明1, 参数列表1, 格式说明2, 参数列表2, ... );`
    * `$fdisplay`, `$fdisplayb`, `$fdisplayh`, `$fdisplayo`
    * `$fwrite`, `$fwriteb`, `$fwriteh`, `$fwriteo`
    * `$fstrobe`, `$fstrobeb`, `$fstrobeh`, `$fstrobeo`
    * `$fmonitor`, `$fmonitorb`, `$fmonitorh`, `$fmonitoro`
* 读取文件:
    | 函数                                                            | 说明                                                                         |
    | :-------------------------------------------------------------- | :--------------------------------------------------------------------------- |
    | `c = $fgetc (fd)`                                               | 读一个字节到 c 中, 文件尾返回 -1                                             |
    | `integer code = $ungetc (c, fd )`                               | 插入一个字符 c 到 buffer 中, 下次调用 fgetc 时返回 c, 文件本身不受影响       |
    | `integer code = $fgets (str, fd)`                               | 读入一行字符到变量 str 中                                                    |
    | `integer code = $fscanf (fd, format, args)`                     | 从文件 fd 中读取一行, 并格式化扫描, 变量存到 args 中, 返回值: 匹配成功的数量 |
    | `integer code = $sscanf (str, format, args)`                    | 并格式化扫描 str, 变量存到 args 中                                           |
    | `integer code = $fread (myreg, fd)`                             | 读取二进制数据                                                               |
    | `integer code = $fread (mem, fd)`                               | ^                                                                            |
    | `integer code = $fread (mem, fd, start)`                        | ^                                                                            |
    | `integer code = $fread (mem, fd, start, count)`                 | ^                                                                            |
    | `integer code = $fread (mem, fd, , count)`                      | ^                                                                            |
    | `$readmemb (文件名, memory_name [, start_addr [,finish_addr]])` | 从文件加载数据到内存数组                                                     |
    | `$readmemh (文件名, memory_name [, start_addr [,finish_addr]])` | ^                                                                            |

* 文件定位:
    | 函数                                    | 说明                                    |
    | :-------------------------------------- | :-------------------------------------- |
    | `integer pos = $ftell (fd)`             | 获取当前位置                            |
    | `code = $fseek (fd, offset, operation)` | 改变文件位置                            |
    | `code = $rewind ( fd );`                | 改变文件位置, 等效于 `$fseek (fd,0,0)`; |
* 其他
    | 函数              | 说明             |
    | :---------------- | :--------------- |
    | `$fflush(fd)`     | 刷新文件         |
    | `$ferror()`       | 最近一次文件错误 |
    | `$sdf_annotate()` |

### 4.6.1. 读取CSV
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

## 4.7. 值变转储 (VCD) 文件
| 函数或函数                                            | 说明          |
| :---------------------------------------------------- | :------------ |
| `$dumpfile (文件名)`                                  | 指定 VCD 文件 |
| `$dumpvars (levels [, list_of_modules_or_variables])` | 指定 VCD 变量 |
| `$dumpon`                                             | 启动 VCD      |
| `$dumpoff`                                            | 停止 VCD      |
| `$dumpall`                                            | 生成检查点    |
| `$dumpflush`                                          | 刷新 VCD      |
| `$dumplimit`                                          |

## 4.8. 时间标度
* 打印时间标度: `$printtimescale`
* 设置打印时间标度的格式: `$timeformat(units_number,precision, suffix, numeric_field_width);`
    * 其中: `units_numbers` 是 $10^n$ 秒, 如 -6 表示 1 us

## 4.9. 时序检验
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
