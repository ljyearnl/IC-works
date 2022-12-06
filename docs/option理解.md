- [1. `.OPTION XXXX<=xxxx>`理解](#1-option-xxxxxxxx理解)
  - [1.1. Introdution](#11-introdution)
  - [1.2. 通用（未确认）](#12-通用未确认)
    - [1.2.1. **`.OPTION ACCT<=0|1|2>`**](#121-option-acct012)
    - [1.2.2. **`OPTION BRIEF=0|1`和`.OPTION NXX`**](#122-option-brief01和option-nxx)
    - [1.2.3. **`.OPTION INGOLD=0|1|2`**](#123-option-ingold012)
    - [1.2.4. **`.OPTION NOMOD`**](#124-option-nomod)
    - [1.2.5. **`.OPTION PARHIER (or) .OPTION PARHIE=GLOBAL|LOCAL`**](#125-option-parhier-or-option-parhiegloballocal)
  - [1.3. **HSPICE**](#13-hspice)
    - [1.3.1. **`.OPTION ARTIST=0|1|2`**](#131-option-artist012)
    - [1.3.2. **`.OPTION ACCURATE=0|1`**](#132-option-accurate01)
    - [1.3.3. **`.OPTION PSF=0|1|2`**](#133-option-psf012)
  - [1.4. **Finesim**](#14-finesim)





# 1. `.OPTION XXXX<=xxxx>`理解

## 1.1. Introdution

**HSPICE®**和**FineSim®**还是有一些区别的，不是完全兼容。即使使用对方的OPTION，也不会有什么问题其实，他只是会不知道这是什么而忽略。

发现手册太巨大了，只写一些常用的。

`<>`表示可有可无，`0|1|2`表示选一个。

> 参考：
>
>[1] Synopsys, Inc. HSPICE® Reference Manual: Commands and Control Options[DB/OL]. California, USA, 2008.
>
>[2] Synopsys, Inc. FineSim® User Guide: Pro and SPICE Reference[DB/OL]. California, USA, September 2019.



<div STYLE="page-break-after: always;"></div>



## 1.2. 通用（未确认）

### 1.2.1. **`.OPTION ACCT<=0|1|2>`**

在输出列表最后生成一个详细的统计报告。

- 0 禁用报告。

- 1 或者没有=xxx （默认）效果一样，启用报告。

- 2 启用报告以及矩阵统计报告（不明）。



### 1.2.2. **`OPTION BRIEF=0|1`和`.OPTION NXX`**

**BRIEF**将以下选项重置为默认：**NODE** **LIST** **OPTS**并且

- 0 默认。

- 1 


### 1.2.3. **`.OPTION INGOLD=0|1|2`**

指定输出的数据格式

- 0 工程格式，指数用一个字母表示。

T=1e12  G=1e9   MEG=X=1e6   K=1e3   M=1e-3  U=1e-6  N=1e-9  P=1e-12 F=1e-15 A=1e-18 

MIL=25.4E-6

- 1 组合使用固定和指数格式（G格式）。固定格式用于0.1-999之间的数字。指数格式用于大于999或小于0.1的数字。

- 2 只使用指数格式（E格式）。指数格式生成固定的数字大小，适用于后分析工具。

建议使用`.OPTION INGOLD=2`


### 1.2.4. **`.OPTION NOMOD`**

抑制模型参数输出，`.OPTION NOMOD`应该和`.OPTION NOMOD=1`一样吧。


### 1.2.5. **`.OPTION PARHIER (or) .OPTION PARHIE=GLOBAL|LOCAL`**

指定同名参数生效顺序。

|.OPTION PARHIER=GLOBAL     |.OPTION PARHIER=LOCAL      |
|---------------------------|---------------------------|
|.PARAM statement (library) |.SUBCKT call (instance)    |
|.SUBCKT call (instance)    |.SUBCKT definition (symbol)|
|.SUBCKT definition (symbol)|.PARAM statement (library) |


<div STYLE="page-break-after: always;"></div>




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
LVLTIM=3
DVDT=2
RELVAR=0.2
ABSVAR=0.2
FT=0.2
RELMOS=0.01
```






### 1.3.3. **`.OPTION PSF=0|1|2`**

规定**HSPICE**运行来自**Cadence® Virtuoso® Analog Design Environment**的仿真时的输出。我完全没明白。

- 0 默认。

如果只使用`.OPTION PSF`，(没有`.OPTION ARTIST`)：

- `.OPTION PSF=1` **HSPICE**产生二进制输出。

- `.OPTION PSF=2` **HSPICE**产生ASCII输出。





<div STYLE="page-break-after: always;"></div>

## 1.4. **Finesim**
