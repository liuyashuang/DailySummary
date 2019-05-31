## 工作学习总结
#### 1.BigDecimal类详解
<p>float和double类型的主要设计目标是为了科学计算和工程计算，它们没有提供完全精确的结果，
所有不应该被用于要求精确结果的场合，商业计算往往要求结果精确，这时候BigDecimal就可以排上
用场了</p>
<P>计算机是二进制的，浮点数没有办法用二进制进行精确表示。
cpu表示浮点数由两个部分组成：指数和尾数，这样的表示方法一般都会丢失一定的精度，有些浮点数运算也会产生一定的误差</P>
###### 1) BigDecimal构造方法</br>
  ```
  public BigDecimal(double val) //将double表示形式转换为BigDecimal(不建议使用)
  public BigDecimal(int val) //将int表示形式转换成 BigDecimal
  public BigDecimal(String val) //将String表示形式转换成 BigDecimal
  ```

![代码展示](https://github.com/liu yashuang/DailySummary/blob/master/img/day0101.png)

JDK的描述：参数类型为double的构造方法的结果有一定的不可预知性</br>
另一方面：String构造方法是完全可预知的，通常建议优先使用String 构造方法</br>
当double 必须用作BigDecimal的源时，可以先使用Double,toString(double) 转换成String</br>

###### 2)BigDecimal的加减乘除
  ```
  public BigDecimal add(BigDecimal value);                        //加法

  public BigDecimal subtract(BigDecimal value);                   //减法

  public BigDecimal multiply(BigDecimal value);                   //乘法

  public BigDecimal divide(BigDecimal value);                     //除法
  ```

**需要注意的是除法运算divide**</br>
BigDecimal除法可能出现不能整除的情况,比如4.5/1.3，这时就会报错
java.lang.ArithmeticException: Non-terminating decimal expansion; no exact representable decimal result

**divide方法可以传三个参数**</br>
`public BigDecimal divide(BigDecimal divisor,int scale,int roundingMode)`
<br>第一个参数表示除数，第二个参数表示小数点后保留几位，第三个参数表示舍入模式</br>

![第三个参数详情](https://github.com/liuyashuang/DailySummary/blob/master/img/day0102.png)

如果需要对BigDecimal进行截断和四舍五入可用setScale方法:</br>
`BigDecimal a = new BigDecimal("4.3286");`
`a = a.setScale(3,RoundingMode.HALT_UP); //保留三位小时，且四舍五入`

**减乘除其实最终都返回的是一个新的BigDecimal对象，因为BigInteger与BigDecimal都是不可
变的（immutable）的，在进行每一步运算时，都会产生一个新的对象**

###### 3）总结
    (1)商业计算使用BigDecimal。
    (2)尽量使用参数类型为String的构造函数。
    (3) BigDecimal都是不可变的（immutable）的，在进行每一步运算时，都会产生一个新的对
    象，所以在做加减乘除运算时千万要保存操作后的值。
    (4)我们往往容易忽略JDK底层的一些实现细节，导致出现错误，需要多加注意

参考链接:<https://www.cnblogs.com/LeoBoy/p/6056394.html>
