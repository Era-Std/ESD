# ESD 001 - Bmap
<a href="./README.md">English</a>
## 什么是Bmap
Bmap是一个在部分场景下高性能,支持类型声明的Key Value结构信息交换格式

## Bmap如何工作
Bmap声明了一组特殊的占位符来分割数据,一般以二进制的状态出现,Bmap可以储存在任何支持二进制的位置例如文件,Bmap文件可以使用任意文件后缀名我们建议将其后缀名为 .bmap

### Bmap占位符
ESD-001 的官方介绍中, Bmap默认占位符为
Bmap所有的占位符均为16进制,而Bmap为二进制
```
‌\x00 --- Key And Value的分隔符
‌\x01 --- Body中每组Kv的分隔符
‌\x03 --- Key Body And Type的分隔符
‌\x09 --- Header And Body的分隔符
```
### Bmap Header
ESD-001 的官方介绍中,Bmap Header与Body类似,但只允许存放有关于Body的信息
例如:我想声明这个Bmap开启类型检查那么我需要在Header添加TypeCheck
TypeCheck\x00true
或者我需要传输一段视频流,但视频流文件体积过大无法一次性传输,那么我可以在Header添加Flag
Flag\x001

## Bmap类型检查
当你在Header中添加TypeCheck并设置其值为true后解析器返回的map中就会设置其的类型为声明的类型
例如:
```
TypeCheck\x00true\x09key\x032\x00value\x01mykey\x031\x00114514
```
这段Bmap(可视状态)声明了类型检查,且为每个Key指定了类型,如不出意外那么这段Bmap会返回
```
key      <string>   value
mykey    <int>      114514
```
解析出来了两个Key And Value 并且声明了指定的类型
转为JSON
```json
{
	"Header": {
		"TypeCheck": true
	},
	"Body": {
		"key": "value",
		"mykey": 114514
	}
}
```
在Bmap中每个类型都会有属于自己的数字代码
## Bmap的类型代码
```
‌1 - Integer
‌2 - String
‌3 - Boolean
‌4 - Float
‌5 - Byte
```
## 为什么使用Bmap
Bmap相比于其他信息交换格式例如 XML, JSON有着得天独厚的优势,没有XML的复杂性,也没有JSON符号的冗余性,Bmap属于Kv类型这点与大部分信息交换格式相同
