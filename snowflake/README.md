
## 全局Id唯一生成器，输出为long型，递增。
* [代码详情](https://gitee.com/kongzhidea/codes/s1kxnl7j0w45dcho2rypa56)
* 线上应用时候，机器码可以通过redis自增取模实现。

```
其他方案1. 使用UUID生成
此种方式使用较简单，直接使用本地方法:UUID.randomUUID()
优点： 
1. 性能高，不依赖远程调用。
2. 扩展性高，本地ID随意生成。

缺点：
1. UUID并不能保证完全绝对不重覆。当生成的量绝对大的时候，可能会导致重覆。但基本上概率非常小。
2. UUID为字符串模式，查询效率会降低。
3. UUID为无序模式，无法使用到一些比较查询。
4. 空间相对说要占用较大，但基本可以忽略不计。
5. UUID 生成性能较高，因为uuid是杂乱无章的，每次插入的主键位置是不确定的，可能在开头，也可能在中间，在进行主键物理排序的时候，势必会造成大量的 IO操作影响效率，在数据量不停增长的时候，特别是数据量上了千万记录的时候，读写性能下降的非常厉害。

另： UUID可以变种转换为Int64 可以解决查询问题。


其他方案2. 使用当前时间
可以使用当前时间的毫秒、微秒、纳秒作为主键ID
优点： 
1. 性能高，不依赖远程调用。
2. 扩展性高，本地ID随意生成。
3. 查询性能高，数字ID，可索引。

缺点：
1. 不能保证唯一，当时间段并发量足够大的时候或非单机部署的时候，出现重覆的概率非常大。

基本上成熟的业务系统中，不会采用这种方式，重覆概率太大。
```
