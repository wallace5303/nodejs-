# TINYINT(M)中M表示的含义是什么

### 整数类型所占的字节数和能表示的数据范围  
```
type        bytes   range(unsigned)         range(signed)
TINYINT     1       0-255                   -128-127
SMALLINT    2       0-65535                 -32768-32767
MEDIUMINT   3       0-16777215              -8388608-8388607
INT         4       0-4294967295            -2147483648-2147483647 
BIGINT      8       0-18446744073709551615  -9223372036854775808-9223372036854775807 
```


### TINYINT(M)中M表示的含义是什么, 比如TINYINT(1)  

```
M的含义并不是允许存入的字符长度, 无符号TINYINT(1)可以存入其最大值255, 
而且存入的数值无论是0还是255, 占用的字节大小是固定的, 都是1.

那么这个M值到底代表什么, 有什么作用?

整型的字节数已经限制了存入数值的取值范围, M值在这里不会有任何影响, 比如TINYINT(1)和TINYINT(2)没有区别
如果设置zerofill(左前位置零填充), 对于TINYINT(1)和TINYINT(2), 
如果存入1, TINYINT(1)存入的是1, 而TINYINT(2)存入的是01

也就是说,没有zerofill,M值是没用的

所以在设计字段的时候, mysql会自动分配长度: int(11)、tinyint(4)、smallint(6)、mediumint(9)、bigint(20)
就用这些默认长度就可以了, 不用自己搞int(10), tinyint(1)之类的, 基本没什么用而且导致表的字段类型多样化

TINYINT(M)、SMALLINT(M)、MEDIUMINT(M)、INT(M)、BIGINT(M)是同理的, 没有zerofill, M值是没用的
```