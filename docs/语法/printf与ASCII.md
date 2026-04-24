---
title: printf与ASCII
parent: 语法
nav_order: 2
has_children: true
---

## printf与ASCII

[▶ 查看动画](/html/printf与ASCII.html)

### 一、核心语法：`printf`

#### 1）直接输出

```c
printf("hello");
```

#### 2）格式化输出

```c
printf("平均值为%.2lf", a);
```

#### 3）复杂格式化输出

```c
printf("平均值1为%.2lf，平均值2为%.3lf", a, b);
```

---

### 二、常用占位符速查

<table>
  <thead>
    <tr>
      <th>占位符</th>
      <th>参数类型</th>
      <th>描述</th>
      <th>示例输出</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>%d</code></td><td><code>int</code></td><td>有符号十进制整数</td><td><code>123</code> / <code>-123</code></td></tr>
    <tr><td><code>%2d</code></td><td><code>int</code></td><td>宽度 2，不足前补空格</td><td><code> 5</code></td></tr>
    <tr><td><code>%02d</code></td><td><code>int</code></td><td>宽度 2，不足前补 0</td><td><code>05</code></td></tr>
    <tr><td><code>%f</code></td><td><code>float</code></td><td>浮点数（默认 6 位小数）</td><td><code>3.141593</code></td></tr>
    <tr><td><code>%lf</code></td><td><code>double</code></td><td>双精度浮点数</td><td><code>3.141593</code></td></tr>
    <tr><td><code>%.2lf</code></td><td><code>double</code></td><td>保留 2 位小数</td><td><code>3.14</code></td></tr>
    <tr><td><code>%%</code></td><td>无</td><td>输出 <code>%</code> 本身</td><td><code>%</code></td></tr>
    <tr><td><code>%c</code></td><td><code>char</code></td><td>单个字符</td><td><code>A</code></td></tr>
    <tr><td><code>%s</code></td><td><code>char*</code></td><td>字符串（到 <code>\0</code>）</td><td><code>Hello</code></td></tr>
    <tr><td><code>%x</code> / <code>%X</code></td><td><code>int</code></td><td>十六进制（小写/大写）</td><td><code>ff</code> / <code>FF</code></td></tr>
    <tr><td><code>%o</code></td><td><code>int</code></td><td>八进制整数</td><td><code>177</code></td></tr>
  </tbody>
</table>

---

### 三、ASCII 可显示字符（32~126）速记

#### 常用起点

1. 数字：`'0'` 从 **48** 开始。  
2. 大写字母：`'A'` 从 **65** 开始。  
3. 小写字母：`'a'` 从 **97** 开始。

#### 高频区间表

<table>
  <thead>
    <tr>
      <th>区间</th>
      <th>十进制范围</th>
      <th>十六进制范围</th>
      <th>说明</th>
    </tr>
  </thead>
  <tbody>
    <tr><td>空格与标点（前段）</td><td>32~47</td><td>20~2F</td><td>空格、常见符号</td></tr>
    <tr><td>数字</td><td>48~57</td><td>30~39</td><td><code>0~9</code></td></tr>
    <tr><td>标点（中段）</td><td>58~64</td><td>3A~40</td><td><code>:;&lt;=&gt;?@</code></td></tr>
    <tr><td>大写字母</td><td>65~90</td><td>41~5A</td><td><code>A~Z</code></td></tr>
    <tr><td>标点（后段）</td><td>91~96</td><td>5B~60</td><td><code>[\]^_`</code></td></tr>
    <tr><td>小写字母</td><td>97~122</td><td>61~7A</td><td><code>a~z</code></td></tr>
    <tr><td>标点（尾段）</td><td>123~126</td><td>7B~7E</td><td><code>{|}~</code></td></tr>
  </tbody>
</table>

> 记忆技巧：`a - A = 32`，所以大小写转换常用 `±32`（仅限英文字母且注意边界）。

---

### 四、思路讲解（课堂建议）

1. 先讲“占位符像模板孔位”：`%d`、`%.2lf`、`%c`。  
2. 再讲“宽度与精度”：`%2d`、`%02d`、`%.3lf`。  
3. 最后讲 ASCII：字符和数字可互转（如 `'A'` ↔ `65`）。

---

### 五、示例代码（含详细注释）

```c
#include <stdio.h>

int main() {
    int n = 5;
    double a = 3.1415926, b = 2.7182818;
    char ch = 'A';

    // 1) 直接输出
    printf("hello\n");

    // 2) 常见整数格式
    printf("%%d: %d\n", n);      // %d
    printf("%%2d: %2d\n", n);    // 宽度2，前补空格
    printf("%%02d: %02d\n", n);  // 宽度2，前补0

    // 3) 浮点格式
    printf("%%f: %f\n", a);          // 默认6位小数
    printf("%%.2lf: %.2lf\n", a);    // 保留2位小数
    printf("平均值1为%.2lf，平均值2为%.3lf\n", a, b);

    // 4) 字符和 ASCII
    printf("字符 %c 的 ASCII 是 %d\n", ch, ch);

    // 5) 输出百分号本身
    printf("通过率：95%%\n");

    return 0;
}
```

---

### 六、易错点

1. `%d` 和 `%f/%lf` 混用（类型不匹配）。
2. 忘记写 `%%` 导致 `%` 打不出来。
3. 误以为 `%lf` 在 `printf` 里必须和 `%f` 严格区分（现代 C 中两者都可用于 `double` 输出，但教学中推荐统一 `%lf` 便于记忆）。
4. ASCII 大小写转换没做边界判断。
