# 第一步

写一个要用的`666.sp`。

# 第二步

新建一个`xxx.sh~`。有无扩展名或者什么扩展名都不影响（除了.sh，原因参考[Shell 教程|菜鸟教程](https://www.runoob.com/linux/linux-shell.html)），内容为[better.sh~](./better.sh~)。

然后在terminal输入`chmod 755 xxx.sh~`。

# 第三步

修改`xxx.sh~`中的

```bash
main_sp_name="666.sp" 

multi_sp_dir="777"

queue="hspice" #hspice or dqueue
simulator="finesim" #hspcie or finesim
output_dir="888"
```

# 第四步

terminal输入`xxx.sh~`

terminal会出现

```
run_multicorner
sortmeas.sh~
```

这几个后缀名问题我还没完全明白。

terminal输入`run_multicorner`，仿真5工艺角×3温度。

会自动`watch bjobs`

结果在`./888/`下。

## 第五步（可选）

没有要mearsure的话可以不管这些。

terminal输入`sortmeas.sh~`，对mearsure文件进行处理，产生`./666.csv`。这个命名暂时没有更好的考虑。