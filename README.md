# lining（李靖）

Golang command execute framework，命令执行包装，更方便的执行外部程序，提供更易于使用的功能扩展

- 一切可配置
- 默认最佳行为
- 方便接收输出

## 为什么要叫李靖

按照本人的一惯作风，所有项目都在`中国古代神话人物或者历史名人`寻找和项目`意义相近`的`神话人物或者历史人`来做作为项目的名称，原因

- 去TMD`崇洋媚外`
- 致敬`中华民族的先贤`

古人有云`军人以服务命令为天职`，契合命令执行器。而在军人中，李靖无人能出其右者。`李靖`作为古代杰出的军事家和`命令执行`不谋而和，故而使用`李靖`来命名项目是合适的

> 李靖（571年－649年7月2日），男，字药师（一称本名药师），雍州三原（今陕西三原县）人，祖籍陇西狄道（今甘肃临洮县）。
> 隋末至初唐时期杰出的军事家。
>
> 李靖出身陇西李氏丹杨房。初仕隋朝，拜马邑郡丞。后转仕唐朝，随秦王李世民进击王世充。 武德三年（620年）辅佐赵郡王李孝恭南平萧铣和辅公祏，
> 并招抚岭南诸部。 武德八年（625年）起在北疆抵御东突厥入侵，贞观三年（629年）以定襄道行军总管总统诸将北征，以精骑三千夜袭定襄，
> 使颉利可汗部惊溃，又奔袭阴山，一举灭亡东突厥，使唐朝疆域自阴山北直至大漠。因功拜尚书右仆射，成为宰相，获封代国公。
> 贞观九年（635年）以足疾为由告退，同年再获起用，统军西破吐谷浑。后改封卫国公，世称“李卫公”。晚年多病，阖门自守，不预政事。
> 贞观十七年（643年），列名“凌烟阁二十四功臣”。贞观二十三年（649年），李靖病逝，终年七十九岁。册赠司徒、并州都督，谥号“景武”，
> 陪葬昭陵。唐肃宗时配享武成王庙，位列十哲。晚唐以后逐渐被神化。后晋时追封“灵显王”，到南宋时累封为“辅世灵佑忠烈王”
>
> 李靖一生征战数十年，为唐王朝的建立及发展立下赫赫战功。他的治军作战经验，进一步丰富了中国古代的军事思想和兵法理论。
> 著有《六军镜》《卫公兵法》等多部兵书，多已失传

## 使用方法

### 安装

安装非常简单，推荐使用`go.mod`来使用`孟婆`

```go
package main

import `github.com/storezhang/mengpo`

func main() {
	// xxx
}
```

或者

```shell
go get github.com/storezhang/mengpo
```

### 简单使用

使用非常简单，只需要调用`mengpo.Set`就可以了

```go
package main

import `github.com/storezhang/mengpo`

type testByNormal struct {
	Addr string `default:"127.0.0.1"`
	Port int    `default:"80"`
}

func main() {
	normal := new(testByNormal)
	if err := mengpo.Set(normal); nil != err {
		panic(err)
	}
}
```

### 配置标签

可以很方便的使用其它`标签`，方法

```go
package main

import `github.com/storezhang/mengpo`

type testByTag struct {
	Addr string `test:"127.0.0.1"`
	Port int    `test:"80"`
}

func main() {
	tag := new(testByTag)
	if err := mengpo.Set(tag, mengpo.Tag(`test`)); nil != err {
		panic(err)
	}
}
```

### 配置复杂类型

可以使用`json`来配置复杂的类型，比如

- `map`
- `slice`
- `struct`

`json`写法支持使用单引号`'`来替换转义字符`\"`，这样在书写默认值`json`更容易

```go
package main

import `github.com/storezhang/mengpo`

type testByJson struct {
	Orders []string `default:"['mqtts', 'mqtt', 'wss', 'ws']"`
	// 同样支持这样写
	// Orders []string `default:"[\"mqtts\", \"mqtt\", \"wss\", \"ws\"]"`
}

func main() {
	json := new(testByJson)
	if err := mengpo.Set(json); nil != err {
		panic(err)
	}
}
```

### 使用环境变量

`孟婆`支持使用环境变量来配置默认值

```go
package main

import `github.com/storezhang/mengpo`

type testByEnv struct {
	Order string `default:"${ORDER}"`
	// 同样支持这种写法
	// Order string `default:"$ORDER"`
}

func main() {
	env := new(testByEnv)
	if err := mengpo.Set(env); nil != err {
		panic(err)
	}
}
```
