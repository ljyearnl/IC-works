- [1. `.OPTION XXXX<=xxxx>`理解](#1-option-xxxxxxxx理解)
  - [1.1. Introdution](#11-introdution)
  - [1.2. 通用](#12-通用)
    - [1.2.1. **`.OPTION ACCT<=0|1|2>`**](#121-option-acct012)
    - [1.2.2. **`OPTION BRIEF=0|1`和`.OPTION NXX`**](#122-option-brief01和option-nxx)
    - [1.2.3. **`.OPTION`**](#123-option)
    - [1.2.4. **`.OPTION INGOLD=0|1|2`**](#124-option-ingold012)
    - [1.2.5. **`.OPTION NOMOD=<0|1>`**](#125-option-nomod01)
    - [1.2.6. **`.OPTION PARHIER (or) .OPTION PARHIE=GLOBAL|LOCAL`**](#126-option-parhier-or-option-parhiegloballocal)
    - [1.2.7. **`.OPTION SCALE`**](#127-option-scale)
  - [1.3. **HSPICE**](#13-hspice)
    - [1.3.1. **`.OPTION ARTIST=0|1|2`**](#131-option-artist012)
    - [1.3.2. **`.OPTION ACCURATE=0|1`**](#132-option-accurate01)
    - [1.3.3. **`.OPTION LIS_NEW=<0|1>`**](#133-option-lis_new01)
    - [1.3.4. **`.OPTION OPFILE=<0|1>`**](#134-option-opfile01)
    - [1.3.5. **`.OPTION PSF=0|1|2`**](#135-option-psf012)
    - [1.3.6. **`.OPTION RUNLVL=0|1|2|3|4|5|6`**](#136-option-runlvl0123456)
    - [1.3.7. **`.OPTION REDEFSUB=<0|1|2>`**](#137-option-redefsub012)
    - [1.3.8. **`.OPTION SPLIT_DP=<0|1|2>`**](#138-option-split_dp012)
  - [1.4. **Finesim**](#14-finesim)


<div STYLE="page-break-after: always;"></div>

-----------------------------
# 1. `.OPTION XXXX<=xxxx>`理解

## 1.1. Introdution

**HSPICE®**和**FineSim®**还是有一些区别的，不是完全兼容。即使使用对方的OPTION，也不会有什么问题其实，他只是会不知道这是什么而忽略。

发现手册太巨大了，只写一些用到的。

`<>`表示可有可无，`0|1|2`表示选一个。

> 参考：
>
>[1] Synopsys, Inc. HSPICE® Reference Manual: Commands and Control Options, Version I-2013.12[OL]. California, USA, 2012.
>
>[2] Synopsys, Inc. FineSim® User Guide: Pro and SPICE Reference, Version P-2019.06-SP1[OL]. California, USA, September 2019.



<div STYLE="page-break-after: always;"></div>


-----------------------------
## 1.2. 通用

### 1.2.1. **`.OPTION ACCT<=0|1|2>`**

在输出列表最后生成一个详细的统计报告。

- 0 禁用报告。
- 1 或者没有值 默认,启用报告。
- 2 启用报告以及矩阵统计报告（不明）。



### 1.2.2. **`OPTION BRIEF=0|1`和`.OPTION NXX`**

**BRIEF**将以下选项重置为默认：**NODE** **LIST** **OPTS**并且

- 0 默认。
- 1 


### 1.2.3. **`.OPTION`**

### 1.2.4. **`.OPTION INGOLD=0|1|2`**

指定输出的数据格式

- 0 工程格式，指数用一个字母表示。T=1e12  G=1e9   MEG=X=1e6   K=1e3   M=1e-3  U=1e-6  N=1e-9  P=1e-12 F=1e-15 A=1e-18 MIL=25.4E-6
- 1 组合使用固定和指数格式（G格式）。固定格式用于0.1-999之间的数字。指数格式用于大于999或小于0.1的数字。
- 2 只使用指数格式（E格式）。指数格式生成固定的数字大小，适用于后分析工具。

建议使用`.OPTION INGOLD=2`


### 1.2.5. **`.OPTION NOMOD=<0|1>`**

抑制模型参数输出

- 0 默认
- 1 或者没有值


### 1.2.6. **`.OPTION PARHIER (or) .OPTION PARHIE=GLOBAL|LOCAL`**

指定同名参数生效顺序。

|.OPTION PARHIER=GLOBAL     |.OPTION PARHIER=LOCAL      |
|---------------------------|---------------------------|
|.PARAM statement (library) |.SUBCKT call (instance)    |
|.SUBCKT call (instance)    |.SUBCKT definition (symbol)|
|.SUBCKT definition (symbol)|.PARAM statement (library) |



### 1.2.7. **`.OPTION SCALE`**


<div STYLE="page-break-after: always;"></div>



-----------------------------
## 1.3. **HSPICE**

### 1.3.1. **`.OPTION ARTIST=0|1|2`**

这个option通常和`.OPTION PSF`一起使用，建议直接`.OPTION ARTIST=2 PSF=2`。

- 0 默认。
- 2 启用**Cadence® Virtuoso® Analog Design Environment**接口，这需要特定的许可证。

原文感觉有歧义，管不了了。





### 1.3.2. **`.OPTION ACCURATE=0|1`**

使用该选项来保证**HSPICE**可以在电路具有高增益和动态范围时仍得到准确的解。

- 0 默认。
- 1 设置以下控制选项，各自有什么用我暂且蒙住：

```
LVLTIM=3        //
DVDT=2          //
RELVAR=0.2      //
ABSVAR=0.2      //
FT=0.2          //
RELMOS=0.01     //
```

### 1.3.3. **`.OPTION LIS_NEW=<0|1>`**

使用该选项以对`*.lis`文件进行精简改进。

- 0 默认，禁用
- 1 或者没有值，启用

改进项：

- 将`.PRINT`和`.NOISE`分析数据，分别放到不同的文件。。
- 抑制在`*.ic0#`文件中工作点节点电压表的输出。
- 为输入文件打印信息。
- 调用控制台打印仿真进度百分比。
- 添加收敛状态项更新到`*.lis`文件。
- 每10%分析进度就更新`*.lis`文件。
- 分析报告输出文件为专注于分析的格式。
- 打印电路状态统计信息的改进格式。
- 任何网表中的`.PRINT`语句会生成一个包含仿真结果的文本文件。对于瞬态分析，该文本文件有`.printtr#`的扩展名。
- 如果`.OP`语句在网表中被使用，工作点分析信息会被分离到单独的文件（`.OPTION LIS_NEW=1`自动设置`.OPTION OPFILE=1`）。
- 模型相关信息被抑制（`.OPTION LIS_NEW=1`自动设置[`.OPTION NOMOD=1`](#125-option-nomod01)





### 1.3.4. **`.OPTION OPFILE=<0|1>`**

向文件中输出工作点信息。

- 0 默认。
- 1 或者没有值。

各种情况：

- `.OPTION OPFILE=0`
  - 工作点信息写入标准输出。
- `.OPTION OPFILE=0` 且 `.OPTION SPLIT_DP=0`
  - `SPLIT_DP`选项被忽略。对于一个工作点，工作点信息被写入一个`*.op`文件。
- `.OPTION OPFILE=1` 且 `.OPTION SPLIT_DP=0`
  - 在`.OP`语句中指明的所有蒙特卡洛点的工作点信息被写入一个单个的`.dp0`文件。
    - 对于一维蒙特卡洛，工作点是`MC_sample`。
    - 对于二维蒙特卡洛，工作点是`MC_sample*parameter_sweep`。
- `.OPTION OPFILE=1` 且 `.OPTION SPLIT_DP=1`
  - 在`.OP`语句中指明的所有采样点的工作点信息被分别写入不同的文件。
    对于二维蒙特卡洛，文件名为`*.dp#@sample_number`，每一个OP文件包含着扫描参数工作点信息。

>注：`.OPTION OPFILE=1 SPLIT_DP=1`支持ASCII格式的波形文件。
>`.OPTION OPFILE=1 SPLIT_DP=2`支持PSF/WDF格式的波形文件。



### 1.3.5. **`.OPTION PSF=0|1|2`**

规定**HSPICE**运行来自**Cadence® Virtuoso® Analog Design Environment**的仿真时的输出。我完全没明白。

- 0 默认。

如果只使用`.OPTION PSF`，(没有`.OPTION ARTIST`)：

- 1 **HSPICE**产生二进制输出。
- 2 **HSPICE**产生ASCII输出。

见[`.OPTION ARTIST`](#131-option-artist012)

### 1.3.6. **`.OPTION RUNLVL=0|1|2|3|4|5|6`**

使用该选项来控制运行速度和仿真精度。该选项值越大，精度越高，仿真运行时间越长。

- 3 默认，和**HSPICE**的原始默认模式类似。
- 5或6 对应于大多数电路的**HSPICE**标准精确模式，5类似于**HSPICE**标准精确模式，6的精度最高。

后面还有许多解释。

### 1.3.7. **`.OPTION REDEFSUB=<0|1|2>`**

该选项允许在网表中重新定义子电路。

- 0 默认，为多重定义抛出一个错误消息。
- 1 或者没有值 使用最后一次声明的定义。
- 2 使用第一次的定义。
  


### 1.3.8. **`.OPTION SPLIT_DP=<0|1|2>`**


详见[`.OPTION OPFILE=<0|1>`](#134-option-opfile01)

- 0 默认。
- 1 或者没有值。
- 2 ~



<div STYLE="page-break-after: always;"></div>


-----------------------------
## 1.4. **Finesim**
