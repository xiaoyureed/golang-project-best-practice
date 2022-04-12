<!-- TOC -->

- [简介](#简介)
- [环境配置](#环境配置)
    - [相关的环境变量](#相关的环境变量)
    - [install](#install)
    - [国内镜像](#国内镜像)
    - [IDE](#ide)
- [quickstart 读取命令行参数](#quickstart-读取命令行参数)
- [golang 的坑](#golang-的坑)
- [basic](#basic)
    - [== DeepEqual 判断相等](#-deepequal-判断相等)
    - [长赋值 短赋值](#长赋值-短赋值)
    - [make 和 new 和 var](#make-和-new-和-var)
    - [零值 nil](#零值-nil)
    - [基本数据类型](#基本数据类型)
    - [字符串 string](#字符串-string)
        - [string 基本使用](#string-基本使用)
        - [高效的拼接方式](#高效的拼接方式)
        - [格式化占位符](#格式化占位符)
    - [array 和 slice](#array-和-slice)
        - [数组](#数组)
        - [切片](#切片)
            - [切片基本使用](#切片基本使用)
            - [切片引用 Full Slice Expression](#切片引用-full-slice-expression)
            - [使用 copy 防止大量内存得不到释放](#使用-copy-防止大量内存得不到释放)
    - [map](#map)
        - [map 基本使用](#map-基本使用)
        - [并发安全的 map](#并发安全的-map)
    - [container 包](#container-包)
        - [heap](#heap)
        - [ring](#ring)
        - [list](#list)
    - [迭代 range](#迭代-range)
        - [迭代slice](#迭代slice)
        - [迭代 map](#迭代-map)
        - [迭代 channel](#迭代-channel)
        - [for 和 range 性能差异](#for-和-range-性能差异)
    - [指针](#指针)
    - [结构体struct](#结构体struct)
        - [struct 基本使用](#struct-基本使用)
        - [空 struct](#空-struct)
            - [利用 map实现集合set](#利用-map实现集合set)
            - [利用 channel 作为通知通道](#利用-channel-作为通知通道)
        - [匿名结构体 继承 重写](#匿名结构体-继承-重写)
    - [接口 interface](#接口-interface)
        - [接口作为函数形参 值接收者 指针接收者](#接口作为函数形参-值接收者-指针接收者)
        - [空接口](#空接口)
        - [类型断言](#类型断言)
        - [内置接口](#内置接口)
        - [接口嵌套](#接口嵌套)
        - [接口完整性检查](#接口完整性检查)
    - [函数](#函数)
        - [函数基本语法](#函数基本语法)
        - [值传递 引用传递](#值传递-引用传递)
        - [函数返回局部变量 逃逸分析](#函数返回局部变量-逃逸分析)
    - [闭包](#闭包)
    - [方法 和 接收器](#方法-和-接收器)
    - [流程控制](#流程控制)
        - [死循环 for 和 select 区别](#死循环-for-和-select-区别)
        - [if 和 for 循环](#if-和-for-循环)
        - [标签 goto break](#标签-goto-break)
        - [defer](#defer)
    - [sort 包](#sort-包)
    - [http](#http)
        - [原理](#原理)
        - [案例:客户端超时取消](#案例客户端超时取消)
    - [context](#context)
        - [context注意实现](#context注意实现)
        - [WithCancel](#withcancel)
        - [WithDeadline](#withdeadline)
        - [WithTimeout](#withtimeout)
        - [WithValue](#withvalue)
    - [io](#io)
        - [文件操作](#文件操作)
        - [scanner](#scanner)
    - [image](#image)
    - [channel csp并发控制](#channel-csp并发控制)
        - [channel 使用](#channel-使用)
        - [利用 nil channel 实现动态 的 select case](#利用-nil-channel-实现动态-的-select-case)
        - [迭代 channel 元素](#迭代-channel-元素)
            - [使用 for range](#使用-for-range)
            - [使用 for select](#使用-for-select)
        - [使用回调而不是返回 channel](#使用回调而不是返回-channel)
        - [仅需任意任务完成-利用 buffered channel 实现](#仅需任意任务完成-利用-buffered-channel-实现)
        - [需要所有任务完成-利用 buffered channel 实现](#需要所有任务完成-利用-buffered-channel-实现)
        - [利用 close channel 实现广播](#利用-close-channel-实现广播)
        - [对象池](#对象池)
            - [利用 no buffered channel 实现对象池](#利用-no-buffered-channel-实现对象池)
            - [sync.pool 对象缓存](#syncpool-对象缓存)
        - [优雅关闭 channel](#优雅关闭-channel)
    - [goroutine](#goroutine)
        - [goroutine原理](#goroutine原理)
            - [如何理解协程](#如何理解协程)
            - [和线程对比](#和线程对比)
        - [协程在内存层面的实现](#协程在内存层面的实现)
        - [goroutine基本使用](#goroutine基本使用)
        - [goroutine 捕获外部变量](#goroutine-捕获外部变量)
        - [使用select 处理超时](#使用select-处理超时)
        - [优雅退出 goroutine](#优雅退出-goroutine)
            - [通过全局变量 waitGroup](#通过全局变量-waitgroup)
            - [通过 channel 的方式](#通过-channel-的方式)
            - [通过 context 官方推荐](#通过-context-官方推荐)
        - [限制并发数量](#限制并发数量)
        - [案例-分段执行任务的退出](#案例-分段执行任务的退出)
    - [锁 共享内存下的并发控制](#锁-共享内存下的并发控制)
        - [Mutex 互斥锁](#mutex-互斥锁)
        - [锁的公平性](#锁的公平性)
        - [RWMutex读写锁](#rwmutex读写锁)
        - [sync.Once只允许执行一次](#synconce只允许执行一次)
        - [sync.Cond 多个观察者等待某个任务完成 广播](#synccond-多个观察者等待某个任务完成-广播)
        - [waitGroup 等待多个任务全部必须完成](#waitgroup-等待多个任务全部必须完成)
        - [锁相关案例](#锁相关案例)
            - [单例模式](#单例模式)
    - [atomic 原子操作](#atomic-原子操作)
    - [反射 reflect](#反射-reflect)
        - [反射基本使用](#反射基本使用)
            - [获取函数名称](#获取函数名称)
            - [实现类型断言](#实现类型断言)
            - [为任何 struct 设置值](#为任何-struct-设置值)
            - [从环境变量读取配置](#从环境变量读取配置)
        - [反射性能优化](#反射性能优化)
        - [反射实现 filter map reduce](#反射实现-filter-map-reduce)
    - [泛型](#泛型)
        - [泛型使用](#泛型使用)
        - [go generation](#go-generation)
    - [unsafe 不安全编程](#unsafe-不安全编程)
    - [http 服务](#http-服务)
        - [http 包](#http-包)
        - [自定义复用器](#自定义复用器)
        - [自定义中间件](#自定义中间件)
        - [获取 ip 地址](#获取-ip-地址)
        - [更好用的路由 router](#更好用的路由-router)
    - [json 包](#json-包)
        - [json基本使用](#json基本使用)
        - [临时忽略json 字段](#临时忽略json-字段)
        - [临时粘合两个struct](#临时粘合两个struct)
        - [一个json切分成两个struct](#一个json切分成两个struct)
        - [用字符串传递数字](#用字符串传递数字)
        - [使用 json的RawMessage](#使用-json的rawmessage)
    - [socket 编程](#socket-编程)
        - [tcp](#tcp)
            - [粘包问题](#粘包问题)
            - [解决粘包 scanner](#解决粘包-scanner)
            - [解决粘包 自定义编解码](#解决粘包-自定义编解码)
        - [udp](#udp)
    - [websocket](#websocket)
    - [Unicode 包](#unicode-包)
    - [time 包](#time-包)
        - [定时器](#定时器)
        - [统计运行时间](#统计运行时间)
        - [时间初始化](#时间初始化)
        - [时间格式化 时区 加减](#时间格式化-时区-加减)
    - [math 包](#math-包)
        - [随机值](#随机值)
        - [精密计算和 big 包](#精密计算和-big-包)
    - [数据库操作](#数据库操作)
    - [runtime包](#runtime包)
    - [flag包](#flag包)
    - [embed 包](#embed-包)
        - [内嵌 react 页面](#内嵌-react-页面)
    - [编译时生成 编译时约束 go-generate go-build](#编译时生成-编译时约束-go-generate-go-build)
- [工程实践 编程思维](#工程实践-编程思维)
    - [设计模式](#设计模式)
        - [创建型](#创建型)
            - [简单工厂](#简单工厂)
            - [单例](#单例)
        - [行为型](#行为型)
            - [观察者](#观察者)
                - [基本示例](#基本示例)
                - [实现 event bus](#实现-event-bus)
        - [结构型](#结构型)
            - [代理模式](#代理模式)
    - [调试 debug](#调试-debug)
    - [模块拆分](#模块拆分)
        - [按照 mvc 模式拆分](#按照-mvc-模式拆分)
        - [按照职责对进行拆分](#按照职责对进行拆分)
        - [按依赖拆分](#按依赖拆分)
    - [项目目录结构规范](#项目目录结构规范)
    - [package 导入自定义包](#package-导入自定义包)
    - [init 方法](#init-方法)
        - [init使用](#init使用)
        - [执行顺序](#执行顺序)
    - [go mod](#go-mod)
        - [go mod 简介](#go-mod-简介)
        - [使用方法 相关命令](#使用方法-相关命令)
        - [GO111MODULE](#go111module)
        - [依赖 间接依赖](#依赖-间接依赖)
    - [编码套路](#编码套路)
        - [面向接口编程](#面向接口编程)
        - [functional options 构造对象](#functional-options-构造对象)
        - [控制反转](#控制反转)
        - [修饰器](#修饰器)
        - [pipeline 模式](#pipeline-模式)
        - [visitor 模式](#visitor-模式)
        - [microKernel 架构](#microkernel-架构)
    - [单元测试](#单元测试)
        - [开源测试库](#开源测试库)
        - [通用 mock](#通用-mock)
        - [数据层 mock测试](#数据层-mock测试)
        - [web层测试](#web层测试)
        - [testing 包](#testing-包)
            - [命令行基本使用](#命令行基本使用)
            - [testing 通用方法](#testing-通用方法)
            - [表格测试 http测试](#表格测试-http测试)
    - [错误处理](#错误处理)
        - [以闭包的形式封装错误检测](#以闭包的形式封装错误检测)
        - [panic recover 机制](#panic-recover-机制)
        - [对错误进行比较](#对错误进行比较)
        - [对错误进行包装 erros包 Is As Unwrap 自定义错误](#对错误进行包装-erros包-is-as-unwrap-自定义错误)
        - [if err错误处理优化套路](#if-err错误处理优化套路)
        - [使用 pkg-errors库](#使用-pkg-errors库)
    - [日志](#日志)
        - [自带日志包](#自带日志包)
        - [日志切分](#日志切分)
        - [日志全局配置](#日志全局配置)
        - [zerolog](#zerolog)
        - [zap](#zap)
        - [logrus](#logrus)
        - [日志文件切分](#日志文件切分)
    - [依赖注入](#依赖注入)
- [性能优化调优](#性能优化调优)
    - [计算内存占用](#计算内存占用)
    - [内存对齐对性能影响](#内存对齐对性能影响)
    - [通过相关工具查看性能瓶颈](#通过相关工具查看性能瓶颈)
    - [编译优化](#编译优化)
        - [优化编译体积](#优化编译体积)
        - [逃逸分析友好的代码](#逃逸分析友好的代码)
    - [编程实践](#编程实践)
- [GC](#gc)
    - [gc 算法](#gc-算法)
    - [gc 分析](#gc-分析)
    - [写GC 友好代码的原则](#写gc-友好代码的原则)
- [golang runtime 运行时](#golang-runtime-运行时)
- [golang 命令工具使用](#golang-命令工具使用)
    - [有哪些命令](#有哪些命令)
    - [交叉编译](#交叉编译)
- [开源自己的类库](#开源自己的类库)
- [开发restful api](#开发restful-api)
    - [项目结构](#项目结构)
    - [gin 中的 json](#gin-中的-json)
    - [中间件](#中间件)
- [开发单体app](#开发单体app)
- [开发微服务 microservice](#开发微服务-microservice)
    - [服务之间通信](#服务之间通信)
    - [微服务框架选型](#微服务框架选型)
    - [go-micro](#go-micro)
    - [网关](#网关)
- [开源库](#开源库)
    - [监听文件改动](#监听文件改动)
    - [Python 解释器](#python-解释器)
    - [权限管理](#权限管理)
    - [网络](#网络)
    - [热加载 live-reloading hot reload](#热加载-live-reloading-hot-reload)
    - [容器](#容器)
    - [数据库](#数据库)
    - [缓存](#缓存)
    - [解析库](#解析库)
    - [颜色](#颜色)
    - [好的编程体验](#好的编程体验)
        - [数据库表转 struct](#数据库表转-struct)
        - [struct 解析](#struct-解析)
        - [格式化日期](#格式化日期)
        - [流式处理 流式编程](#流式处理-流式编程)
        - [池](#池)
        - [依赖注入](#依赖注入-1)
    - [定时任务](#定时任务)
    - [api 和文档](#api-和文档)
    - [系统信息 运维](#系统信息-运维)
    - [时间工具](#时间工具)
    - [持续追踪读取日志](#持续追踪读取日志)
    - [分布式](#分布式)
    - [实现插件机制](#实现插件机制)
    - [和其他语言交互](#和其他语言交互)
    - [音频视频图片处理](#音频视频图片处理)
    - [常用工具库](#常用工具库)
    - [代码生成](#代码生成)
    - [注解编程](#注解编程)
    - [生成假数据](#生成假数据)
    - [网络抓包](#网络抓包)
    - [gui框架](#gui框架)
- [参考链接](#参考链接)

<!-- /TOC -->


# 简介

- 完整的开发工具链 （tools， test，benchmark，builtin。。。）
- 部署简单（直接编译生成二进制文件， 丢到服务器就可以了）
- 标准库已经包含了很多工具, 依赖少
- 优秀的并发模型；


创始人:

- Rob pike : Unix 开发者之一, utf-8 作者
- Ken Thompson:  Unix 作者, c 语言作者
- Robert Griesemer: V8 engine 作者, hot spot 开发者  


和 java 对比:

- Java 包相当于单个 .go 源文件。 
- Go 语言包相当于整个 Maven 模块或 .NET 程序集。

场景:

- 云计算: docker, kubernetes
- 区块链: 以太坊(ethereum), hyperledger



# 环境配置

## 相关的环境变量

```
$GOROOT 表示 Go 在你的电脑上的安装位置，它的值一般都是 $HOME/go，当然，你也可以安装在别的地方。

	$GOBIN 表示编译器和链接器的安装位置，默认是 $GOROOT/bin，如果你使用的是 Go 1.0.3 及以后的版本，一般情况下你可以将它的值设置为空，Go 将会使用前面提到的默认值

$GOARCH 表示编译目标机器的处理器架构，它的值可以是 386、amd64 或 arm。

$GOOS 表示目标机器的操作系统，它的值可以是 darwin、freebsd、linux 或 windows。

$GOHOSTOS 和 $GOHOSTARCH 设置本地机器的操作系统名称和编译体系结构

	只有在进行交叉编译的时候才会用到，如果你不进行显示设置，他们的值会和本地机器（$GOOS 和 $GOARCH）一样。

$GOPATH 默认采用和 $GOROOT 一样的值，但从 Go 1.1 版本开始，你必须修改为其它路径。如果使用 go module, 则不用设置

$GOARM 专门针对基于 arm 架构的处理器，它的值可以是 5 或 6，默认为 6。

$GOMAXPROCS 用于设置应用程序可使用的处理器个数与核数
```

## install

https://studygolang.com/dl

对于 Unix:

```sh
# 环境变量
# 
#若不设置, Unix默认 ${home}/go, win 默认为 %userprofile%/go
GOPATH=xxx
# 开启 go module 
GO111MODULE=on
# 国内镜像代理
GOPROXY=https://goproxy.io,direct
# 设置不走 proxy 的私有仓库，多个用逗号相隔（可选）
#go env -w GOPRIVATE=*.corp.example.com
# 设置不走 proxy 的私有组织（可选）
#go env -w GOPRIVATE=example.com/org_name

# 下载压缩包
curl -L https://studygolang.com/dl/golang/go1.14.6.linux-amd64.tar.gz --output xxx.tar.gz
# 解压到 /usr/local
tar -C /usr/local -zxvf go1.14.6.tar.gz 


# vim /etc/profile
# centos 要加到这个文件里, 才能所有用户登录都执行 go verison  有效
vi /etc/bashrc

# 
# export GOPATH=/opt/gopath
# export GOROOT=/usr/lib/golang
# export GOBIN=$GOROOT/bin
#需要添加到 path, 
# export PATH=$PATH:$GOBIN ....

source /etc/profile

# 验证
go version


# 查看环境变量是否设置好了
go env


```

## 国内镜像

```sh

# 国内代理 参考 https://goproxy.io/zh/
# https://goproxy.cn
# or https://athens.azurefd.net/
```


## IDE

vscode + go 插件 (https://zhuanlan.zhihu.com/p/269215596), go struct tag (https://github.com/wangzeping722/go-struct-tag, https://github.com/guyanyijiu/go-struct-tag)

idea + go 插件



# quickstart 读取命令行参数


编写代码

```go
package main

import (
  "flag" // 专门处理命令行参数的工具包
  "fmt"
  "os"
)

func main() {
  cmd := os.Args[0]            //命令行第一个值, 即 “当前命令”
  fmt.Println("cmd: ", cmd)    //D:\gopath\src\cli-example\cli-example.exe
  argCount := len(os.Args[1:]) // 命令行参数个数
  fmt.Println("arg count: ", argCount)
  //遍历打印参数
  for i, v := range os.Args[1:] {
    fmt.Printf("参数%d: %s\n", i+1, v)
  }

  var port int
  flag.IntVar(&port, "port", 8080, "端口, 默认 8080") // 为名称为 port 的flag赋值, 设置默认值8080
  flag.Parse()                                    // 开始解析
  fmt.Println("端口号: ", port)
  /*
    $ ./cli-example.exe -port=9000 // 如果指定了 port , 则为指定值
    端口号:  9000
  */
}

```

运行: 三种方法

- 通过 IDE 的启动按钮

- `go run app.go`

- 先编译, 再运行  `go build xxx.go` + `./xxx.exe` (可执行文件名 为 go 文件名)

	go build 若不加任何参数, 则是编译 main 包, 可执行文件名 为 包名



# golang 的坑

```go
// 左大括号 { 不能单独放一行
// 编译器会在每行代码尾部特定分隔符后加;来分隔多条语句，比如会在 ) 后加分号：



// 不能用简短声明方式来单独为一个变量重复声明，:=左侧至少要有一个新变量才行，
// 错误示例
func main() {  
    one := 0
    one := 1 // error: no new variables on left side of :=
}
// 正确示例
func main() {
    one := 0
    one, two := 1, 2    // two 是新变量，允许 one 的重复声明。比如 error 处理经常用同名变量 err
    one, two = two, one    // 交换两个变量值的简写
}


// 短声明常常会用来重复声明某个变量, 如重复声明 err, 然后错误处理
// 这实际是变量覆盖




// 允许对值为 nil 的 slice 添加元素，不允许对值为 nil 的 map添加元素
// map 错误示例
func main() {
    var m map[string]int
    m["one"] = 1        // error: panic: assignment to entry in nil map
    // m := make(map[string]int)// map 的正确声明，分配了实际的内存
}    
// slice 正确示例
func main() {
    var s []int
    s = append(s, 1)
}



// 在创建 map 类型的变量时可以指定容量，但不能像 slice 一样使用 cap() 来检测分配空间的大小
// 错误示例
func main() {
    m := make(map[string]int, 99)
    println(cap(m))     // error: invalid argument m1 (type map[string]int) for cap  
}  



// string 类型的变量值不能为 nil
// 错误示例
func main() {
    var s string = nil    // cannot use nil as type string in assignment
    if s == nil {    // invalid operation: s == nil (mismatched types string and nil)
        s = "default"
    }
}
// 正确示例
func main() {
    var s string    // 字符串类型的零值是空串 ""
    if s == "" {
        s = "default"
    }
}



// Array 类型的值作为函数参数, 是值传递, 如果想修改外部的参数数组, 需要:
// - 直接传递指向这个数组的指针类型
// - 或者 直接使用 slice：即使函数内部得到的是 slice 的值拷贝，但依旧会更新 slice 的原始底层数组  (推荐)
// 数组使用值拷贝传参
func main() {
    x := [3]int{1,2,3}

    func(arr [3]int) {
        arr[0] = 7
        fmt.Println(arr)    // [7 2 3]
    }(x)
    fmt.Println(x)            // [1 2 3]    // 并不是你以为的 [7 2 3]
}

// 传址会修改原数据
func main() {
    x := [3]int{1,2,3}

    func(arr *[3]int) {
        (*arr)[0] = 7    
        fmt.Println(arr)    // &[7 2 3]
    }(&x)
    fmt.Println(x)    // [7 2 3]
}

// 会修改 slice 的底层 array，从而修改 slice
func main() {
    x := []int{1, 2, 3}
    func(arr []int) {
        arr[0] = 7
        fmt.Println(x)    // [7 2 3]
    }(x)
    fmt.Println(x)    // [7 2 3]
}


// log 标准库提供了不同的日志记录等级，与其他语言的日志库不同，Go 的 log 包在调用 Fatal*()、Panic*() 时能做更多日志外的事，如中断程序的执行

func main() {
	log.Fatal("Fatal level log: log entry")        // 输出信息后，程序终止执行
	log.Println("Nomal level log: log entry") // 这里不会执行到了
}





// 不导出(即大写)的 struct 字段无法被 encode
// 以小写字母开头的字段成员是无法被外部直接访问的，所以 struct 在进行 json、xml、gob 等格式的 encode 操作时，这些私有字段会被忽略，导出时得到零值：



// https://www.topgoer.cn/docs/golang/chapter21-1 TODO 35 条

```


# basic

## == DeepEqual 判断相等

```go
// == 比较的不是地址, 而是内容 (和 java 不同)
p1 := People{"msr", 17}
p2 := People{"msr", 17}
fmt.Printf("%p %p\n", &p1, &p2) //输出地址不同
fmt.Println(p1 == p2)           //输出:true

// reflect.DeepEqual() 可用于做一些==判断不了的事情, 例如 对 slice 和 map 进行比较
//
// 复杂结构的相等比较
//reflect包中的 DeepEqual()函数
//
type data struct {
	num    int               //ok
	checks [10]func() bool   //not comparable
	doit   func() bool       //not comparable
	m      map[string]string //not comparable
	bytes  []byte            //not comparable
}

func compareDemo() {
	v1 := data{}
	v2 := data{}
	fmt.Println("v1 == v2:", reflect.DeepEqual(v1, v2)) //prints: v1 == v2: true

	m1 := map[string]string{"one": "a", "two": "b"}
	m2 := map[string]string{"two": "b", "one": "a"}
	fmt.Println("m1 == m2:", reflect.DeepEqual(m1, m2)) //prints: m1 == m2: true

	s1 := []int{1, 2, 3}
	s2 := []int{1, 2, 3}
	fmt.Println("s1 == s2:", reflect.DeepEqual(s1, s2)) //prints: s1 == s2: true

	//DeepEqual()不会认为空的slice与“nil”的slice相等
	//bytes.Equal()认为“nil”和空的slice是相等的
	var b1 []byte = nil
	b2 := []byte{}
	fmt.Println("b1 == b2:", reflect.DeepEqual(b1, b2)) //prints: b1 == b2: false
	fmt.Println("b1 == b2:", bytes.Equal(b1, b2))       //prints: b1 == b2: true

}


```

## 长赋值 短赋值

https://blog.learngoprogramming.com/learn-go-lang-variables-visual-tutorial-and-ebook-9a061d29babe

```go


```

## make 和 new 和 var

```
都是用来申请内存的

new  用来给值类型和struct申请内存 (int, string, bool..., 也包括 struct 这种值类型),  返回指针

make 用来给内置引用类型开辟内存 (slice, map, channel), 返回类型对应的值 (返回的类型对象实际包含了指针 https://www.flysnow.org/2018/02/24/golang-function-parameters-passed-by-value.html)

// var 可以声明变量为零值


```

## 零值 nil

```go


// 假设变量没有初始化，每个变量声明都会自动初始化为与零内存的内容相匹配的值
// 数字类型 ,  0
// bool类型 , false
// 
// 数组/struct类型, [每个元素的对应的零值]
// 
// map、slice、pointer、channel、func、interface 类型, nil

// 
// nil 标识符是不能比较的
// nil 不是关键字或保留字
// 
// 不同类型 nil 的指针是一样的
// 
// 
// 
// 
// demo1
type MyInt struct {
	mu  sync.Mutex
	val int
}
func main() {
	var i MyInt

	// i.mu 无需初始化, 直接使用即可
	i.mu.Lock()
	i.val++
	i.mu.Unlock()
}

	// demo2
	var b bytes.Buffer
	b.WriteString("Hello, world!\n")
	io.Copy(os.Stdout, &b)


	// demo3
	// s := make([]string, 0)   
	// s := []string{}
	var s []string  // 只需要声明即可

	s = append(s, "Hello")
	s = append(s, "world")
	fmt.Println(strings.Join(s, " "))


	// demo4: 通过 nil 指针调用方法, 返回默认值
	var c1 *Config
	var c2 = &Config{
		path: "/export",
	}
	fmt.Println(c1.Path(), c2.Path())
	//
type Config struct {
path string
}

func (c *Config) Path() string {
	if c == nil {
		return "/usr/home"
	}
	return c.path
}

```

## 基本数据类型

```go


//Basic types
/* golang 的基本类型
bool

string

有符号 int (32 or 64 bit, os 决定)  int8  int16  int32  int64
无符号 uint (32 or 64 bit, os 决定) uint8 uint16 uint32 uint64 uintptr

byte // alias for uint8, 不支持中文 (支持英文字符)

rune // alias for int32
	 // represents a Unicode code point , 所以支持中文

uintptr //无符号整型，用于存放一个指针

float32 float64 (若需要精确计算, 涉及到金额金钱价格相关的业务, 使用 https://github.com/shopspring/decimal)

complex64 complex128 实数+虚数
*/
// 
/* 引用类型
slice
map
channel
interface
func()
*/
// 
func basicType() {
	// 定义变量, 赋值
	// var c, python, java bool
	// var x, y int = 1, 2

	// 字符串
	var s string = "hello"
	s1 := "world" // 省略的写法, 只能在函数内部使用, 这样声明的变量可以重复赋值, 常用来接收 err
	fmt.Println("s + s1 = ", s, s1)
	// 类型推断
	// i := 42           // int
	// f := 3.142        // float64
	// g := 0.867 + 0.5i // complex128

	// 声明常量
	const World = "世界" // 注意 Constants cannot be declared using the := syntax.

	//  多个变量声明也可以这样
	var (
		ToBe   bool       = false
		MaxInt uint64     = 1<<64 - 1
		z      complex128 = cmplx.Sqrt(-5 + 12i)
	)
	println(ToBe, MaxInt, z)

	var boo1 bool = false
	fmt.Println("boo1 = ", boo1)

	//
	// 数字类型
	//
	// int、uint 和 uintptr 位数有系统决定
	//
	var a int8 = 1
	var b, c int16 = 2, 3
	println("a = ", a)
	println("b = ", b, ", c = ", c)
	var d, e int32 // 先声明
	d, e = 5, 6    // 再使用
	println("d = ", d, ", e = ", e)

	//Zero values 零值
	var i int
	var f float64
	var x bool
	var y string
	// %q 存疑?
	fmt.Printf("%v %v %v %q\n", i, f, x, y) //0 0 false ""

//保留两位小数
func Decimal(value float64) float64 {
	value, _ = strconv.ParseFloat(fmt.Sprintf("%.2f", value), 64)
	return value
}



	// 
	//Type conversions 类型转换
	//
	// 
	//The expression T(v) converts the value v to the type T.
	var zz int = 42
	var w float64 = float64(i)
	var u uint = uint(f)
	// 在func 里可以更简单
	// i := 42
	// f := float64(i)
	// u := uint(f)

	fmt.Println(zz, w, u) //42 42 42

	// 将整型 (或任意数据类型) 转为字符串
	i := 123
	// 错误
	s := string(i) // "E"
	// 正确
	t := strconv.Itoa(i)
	// or
	t:= fmt.Sprintf("%d", i)


}




```


## 字符串 string


### string 基本使用

strings 包相关 api 实例: https://www.cnblogs.com/unqiang/p/6682281.html
TODO


```go
// string 是只读的 byte array, 可以热河任何数据
func stringDemo() {
	var s1 = "hello world \n"
	s2 := `hello world \n` // 多行字符串
	fmt.Println(s1) // 输出换行, "\n"被解释成换行
	fmt.Println(s2) // 不换行, "\n" 原样输出
	// 长度
	//  len() 返回的是字符串的 byte 即字节数，而不是像 Python 中那样是计算 Unicode 字符数
	fmt.Println(len(s1)) // 13
	// 如果要得到字符串的字符数
	char := "♥"
	fmt.Println(len(char))    // 3   字节数
    fmt.Println(utf8.RuneCountInString(char))    // 1 字符数
				// 或者  len([]rune(str))

	// 第一个字符, 用字节类型接收, 所以打印对应的 ascii 码
	fmt.Println(s1[0]) // 104
	// 原样打印字符
	// 其他占位符: %v 用于复杂类型占位如 struct (%#v 会把 struct 的字段名也打印), %s 用于字符串占位, %T 用于打印类型占位
	fmt.Printf("%c\n", s1[0]) //h

	// 字符串判空
	if len(str) == 0{ }
	if str == "" { }

	// 根据下标获取
	// string  x[0]取出来的索引是[]byte类型，必须要string(x[0])才是想要的索引值

	// 修改
	// string 类型的值是常量，不可更改
	// s1[0] = "X" // 报错, string 类型不可修改
	// 先转为字节数组再修改; 
	strArr := []byte(s1)
	// strArr[0] = "X" // 报错 : cannot use "X" (type string) as type byte in assignment
	strArr[0] = 'X'             // 字符, 是 rune 类型, 不是 字符串
	fmt.Println(string(strArr)) //Xello world
	// 上边的示例并不是更新字符串的正确姿势，
	// 因为一个 UTF8 编码的字符可能会占多个字节，比如汉字就需要 3~4个字节来存储，此时更新其中的一个字节是错误的
	// 正确姿势：将 string 转为 rune slice（此时 1 个 rune 可能占多个 byte），直接更新 rune 中的字符
	x := "text"
    xRunes := []rune(x)
    xRunes[0] = '我'
    x = string(xRunes)
    fmt.Println(x)    // 我ext

	// 遍历
	// bad
	str := "hello 世界" // 1个中文占3byte
	for i, l := 0, len(str); i < l; i++ {
		var c byte = str[i]
		// 对应index, ascii, char
		fmt.Printf("%d - %v - %c\n", i, c, c) // 有乱码
	}
	// good
	for i, c := range str {
		fmt.Printf("%d - %v - %c\n", i, c, c)
	}

	// 获取字符串的子串
	substr := str[n:m]


	// 标准库中有 "unicode/utf8" 包来做 UTF8 的相关解码编码
	str1 := "ABC"
    fmt.Println(utf8.ValidString(str1))    // true
	c := str1
    str2 := "A\xfeC"
    fmt.Println(utf8.ValidString(str2))    // false
    str3 := "A\\xfeC"
    fmt.Println(utf8.ValidString(str3))    // true    // 把转义字符转义成字面值
}



```

### 高效的拼接方式

```go
	// byte.Buffer 类似 Java 中的 Stringbuffer
	var buffer bytes.Buffer
	// or
	buf := new(bytes.Buffer)
	buffer.WriteString("hello")
	fmt.Println(buffer.String())

	// 更新的方式, strings.Builder
	// strings.Builder 和 bytes.Buffer 底层都是 []byte 数组，但 strings.Builder 性能比 bytes.Buffer 略快
	// 区别在于，bytes.Buffer 转化为字符串时重新申请了一块空间，存放生成的字符串变量，而 strings.Builder 直接将底层的 []byte 转换成了字符串类型返回了回来
	var builder strings.Builder
	// 预分配内存
	builder.Grow(n * len(str))
	for i := 0; i < n; i++ {
		builder.WriteString(str)
	}

	// 使用 []byte	// 
	str := "hello"
	buf := make([]byte, 0)
	// 如果长度是可预知的，那么创建 []byte 时，我们还可以预分配切片的容量(cap)
	buf := make([]byte, 0, n*len(str))
	for i := 0; i < n; i++ {
		buf = append(buf, str...)
	}
	
}

/*
原理:
strings.Builder 和 + 直接就是生成新的字符串, 新空间的大小是原来两个字符串的大小之和

strings.Builder，bytes.Buffer，包括切片 []byte 的内存是以倍数申请的, 超过一定大小，比如 2048 byte 后，申请策略上会有些许调整

*/

```

### 格式化占位符

%d	格式化整数
%0d	用于规定输出定长的整数 其中开头的数字 0 是必须的
%g	格式化浮点型
%n.mg	用于表示数字 n 并精确到小数点后 m 位，除了使用 g 之外，还可以使用 e 或者 f
%f	格式化浮点数	
%X, %x	格式化 16 进制表示的数字
%b	位的格式化标识符
%e	科学计数表示法
%t	格式化布尔型
%c	格式化字符
%s	格式化字符串
%U, %u	Unicode，格式为 U+hhhh 的字符串
%p	格式化指针
%v	使用类型的默认输出格式的标识符

%T	打印某个类型的完整说明
%#v	打印包括字段和限定类型名称在内的实例的完整信息
%+v	打印包括字段在内的实例的完整信息


## array 和 slice

### 数组

```go

func arrayAndSlice() {

	// Arrays
	//定长的相同类型元素的序列, An array's length is part of its type, so arrays cannot be resized 容量无法更改
	// 语法
	// var a [10]int 声明
	// a := [3]int{2, 1, 3} // 初始化/ array literal
	// 省略长度的写法, 创建的还是数组, 不是 slice (如果省掉 ...三个点, 就是 slice 了	)
	// var student = [...]string{"Tom","Ben","Peter"} // ...三个点会自动计算长度
	//
	
	var a [2]string
	a[0] = "Hello"
	a[1] = "World"
	fmt.Println(a[0], a[1]) //Hello World
	fmt.Println(a)          //[Hello World]
	
	// 增
	// 底层会创建新数组
	newArr = append(arr, xxx_ele)
	// 删除
	newArr = append(arr[:index], arr[index+1:]...) // ...三个点表示依次取出元素
	// 清空切片中的所有元素
	student = student[0:0]
	// 改
	// arr[index] = xxx
	// 查
	for index, value := range arr {}

```

### 切片

#### 切片基本使用

```go

	//
	//
	/*
	Slices
	
	array 的 切片/视图,底层是引用的一个数组 (切片本身并不存储任何元素，而只是对现有数组的引用);
	本质是一个 struct:
	struct {
			ptr *[]T // 地址：切片的地址一般指切片中第一个元素所指向的内存地址，用十六进制表示。即底层数组的指针
			len int // 长度：切片中实际存在元素的个数。长度：切片中实际存在元素的个数。
			cap int  // 容量：从切片的起始元素开始到其底层数组中的最后一个元素的个数。
	}
			
	
	先声明/初始化长度容量, 然后赋值使用
	语法
	var slice []T 声明, 切片声明后其内容为空，长度和容量均为0
	
	通过内建函数 make() 初始化
	a := make([]int, 5)  // len(a)=5, cap=5
	b := make([]int, 0, 5) // len(b)=0, cap(b)=5
	slice := make([]string, 2, 10) 初始化长度为 2, 容量为 10
	
	一步到位, 声明同时初始化
	slice := []string{"bb", "dd"} 
	q := []int{2, 3, 5, 7, 11, 13} //Slice literals 是初始化数组更好的方式(不必指定长度),底层是 先 正常创建一个数组, 然后创建一个数组的 slice
	
	 //直接从数组获取, 左闭右开
	如果切片是从其他数组或切片生成，新切片的元素添加需要考虑对原有数组或切片中数据的影响
	mySlice := myArray[beginIndex:endIndex] 
	
	常见操作: https://ueokande.github.io/go-slice-tricks/
	复制
	b = make([]T, len(a))
	copy(b, a)
	或者
	b = append([]T(nil), a...)
	或者
	b = append(a[:0:0], a...)
	
	添加元素, 通过内建函数 func append(s []T, vs ...T) []T
		slice 被修改, 则原始 array 也会相应改变 (slice就像数组的部分的引用)
		当 append 之后的长度小于等于 cap，将会直接利用原底层数组剩余的空间。
		当 append 后的长度大于 cap 时，则会分配一块更大的区域来容纳新的底层数组。
	a = append(a[:i], append([]T{x}, a[i:]...)...)
	
	删除
		删除意味着后面的元素需要逐个向前移位。每次删除的复杂度为 O(N)，因此切片不合适大量随机删除的场景，这种场景下适合使用链表
		删除后，将空余的位置置空，有助于垃圾回收
	a = append(a[:i], a[i+1:]...)

	过滤filter
	当原切片不会再被使用时，就地 filter 方式是比较推荐的，可以节省内存空间
	n := 0
	for _, x := range a {
		if keep(x) {
			a[n] = x
			n++
		}
	}
	a = a[:n]

	Nil slices  - zero value == nil
	
	*/
	var s []int = primes[1:4]
	fmt.Println(s) //[3 5 7]

	// 用切片的完整写法 slice[start:len:cap]
	var ls = []int{0, 1, 3, 4}
    ls = append(append(ls[:2:2], 2), ls[2:]...)
    fmt.Println(ls)
    // prints: [0 1 2 3 4]

	// 错误写法
	// var ls = []int{0, 1, 3, 4}
    // ls = append(append(ls[:2], 2), ls[2:]...)
    // fmt.Println(ls)
    // prints: [0 1 2 2 4] but we want [0 1 2 3 4]

	// slice defaults  - slice的默认index
	/* 对于数组 var a [10]int , 以下是等同的
	   a[0:10]
	   a[:10]
	   a[0:]
	   a[:]
	*/

	//
	//struct slice
	ss := []struct {
		i int
		b bool
	}{
		{2, true},
		{3, false},
		{5, true},
		{7, true},
		{11, false},
		{13, true},
	}
	fmt.Println(ss) //[{2 true} {3 false} {5 true} {7 true} {11 false} {13 true}]

	// 二维 slice 初始化
	board := [][]string{
		[]string{"_", "_", "_"},
		{"_", "_", "_"}, // []string 可省略
		[]string{"_", "_", "_"},
	}
	fmt.Println(board) //[[_ _ _] [_ _ _] [_ _ _]]

	sliceLengthAndCapacity()

	makeSliceDemo()

	sliceAppendingDemo()
}

//Slice length and capacity
// length - 切片包含的 element 个数, 切片改变的就是这个变量
// capacity - 切片的容量: 即基础数组中元素的数量，从切片中的第一个元素开始计算, 到 原始数组的末尾
// 通过 len(s) and cap(s) 获得
// 这两者关系: 只要 capacity 足够, 可以通过 re-slice 来延长切片的 length
func sliceLengthAndCapacity() {
	s := []int{2, 3, 5, 7, 11, 13}
	printSlice(s) //len=6 cap=6 [2 3 5 7 11 13]

	// Slice the slice to give it zero length.
	zeroSlice := s[:0]
	printSlice(zeroSlice) //len=0 cap=6 []

	// Extend its length.
	s = zeroSlice[:4] // s 被重新赋值
	printSlice(s)     //len=4 cap=6 [2 3 5 7]

	// Drop its first two values.
	// 注意 s 已经被重新赋值了
	s = s[2:]
	printSlice(s) //len=2 cap=4 [5 7]

	// nil slice
	var sli []int
	fmt.Println(sli, len(sli), cap(sli)) //[] 0 0
	fmt.Println(sli == nil)              // true
}
func printSlice(s []int) {
	fmt.Printf("len=%d cap=%d %v\n", len(s), cap(s), s)
}

// Creating a slice with make
// make([]int, xxLenCap)
// make([]int, xxLen, xxCap)
func makeSliceDemo() {
	a := make([]int, 5) // 创建的是 zeroed array 的一个slice;
	printSlice2("a", a) //a len=5 cap=5 [0 0 0 0 0]

	b := make([]int, 0, 5)
	printSlice2("b", b) //b len=0 cap=5 []

	c := b[:2]
	printSlice2("c", c) //c len=2 cap=5 [0 0]

	d := c[2:5]
	printSlice2("d", d) //d len=3 cap=3 [0 0 0]
}
func printSlice2(s string, x []int) {
	fmt.Printf("%s len=%d cap=%d %v\n",
		s, len(x), cap(x), x)
}

// Appending to a slice 向 slice 添加元素
func sliceAppendingDemo() {
	var s []int
	printSlice(s) //len=0 cap=0 []

	// append works on nil slices.新的容量更大的 array 被创建, 返回它的 slice
	s = append(s, 0)
	printSlice(s) //len=1 cap=1 [0]

	// The slice grows as needed.
	s = append(s, 1)
	printSlice(s) //len=2 cap=2 [0 1]

	// We can add more than one element at a time.
	s = append(s, 2, 3, 4)
	printSlice(s) //len=5 cap=6 [0 1 2 3 4]
}

/////////////////////////////////////////////

	//值为 nil 的切片与具有零长度的切片可以比较, 结果不等
	var s1 = []string{}
	var s2 []string
	fmt.Println(reflect.DeepEqual(s1, s2)) // false
```

#### 切片引用 Full Slice Expression



```go




func main() {
    path := []byte("AAAA/BBBBBBBBB") // 字符串转为字节数组, 就是字符数组
    sepIndex := bytes.IndexByte(path,'/')

	// dir1 和 dir2 共享一个底层数组
    dir1 := path[:sepIndex]
	// 应该这样使用
	// 使用了 Full Slice Expression，其最后一个参数叫“Limited Capacity”，于是，后续的 append() 操作将会导致重新分配内存
	dir1 := path[:sepIndex:sepIndex]
	
    dir2 := path[sepIndex+1:]

    fmt.Println("dir1 =>",string(dir1)) //prints: dir1 => AAAA
    fmt.Println("dir2 =>",string(dir2)) //prints: dir2 => BBBBBBBBB

	// 若不使用 Full Slice Expression, 这里 dir 新增加的数据会扩展到了 dir2 的空间, 覆盖 dir2 的内容
    dir1 = append(dir1,"suffix"...)

    fmt.Println("dir1 =>",string(dir1)) //prints: dir1 => AAAAsuffix
    fmt.Println("dir2 =>",string(dir2)) //prints: dir2 => uffixBBBB
}


// 在看一个例子
func TestSlice(t *testing.T) {
	slice := []int{0, 1, 3, 4}

	//slice1 := slice[:2]
	//正确写法
	slice1 := slice[:2:2]

	t.Log(slice1)//[0 1]
	slice2 := slice[2:]
	t.Log(slice2)//[3 4])

	slice1 = append(slice1, 2)
	t.Log(slice1) // [0 1 2]
	t.Log(slice2) // [2 4]

	newSlice := append(slice1, slice2...)
	t.Log(newSlice) //[0 1 2 2 4]
}
```

#### 使用 copy 防止大量内存得不到释放

```go
// 原切片由大量的元素构成，但是我们在原切片的基础上切片，虽然只使用了很小一段，但底层数组在内存中仍然占据了大量空间，得不到释放。
// 比较推荐的做法，使用 copy 替代 re-slice。

//取 origin 切片的最后 2 个元素
// bad
func lastNumsBySlice(origin []int) []int {
	// 直接在原切片基础上进行切片
	return origin[len(origin)-2:]
}

// good
func lastNumsByCopy(origin []int) []int {
	// 创建了一个新的切片，将 origin 的最后两个元素拷贝到新切片上，然后返回新切片
	result := make([]int, 2)
	copy(result, origin[len(origin)-2:])
	return result
}

```

## map

### map 基本使用

```go


// map - 键值对, 无序, key 是唯一的, value 可为 空/空 struct (使用空结构体可以达到同样的效率，同时不会占用额外的内存)
//Map literals
//Map literals continued
// 声明: var m map[keyType]valueType
// 初始化: make(map[string]Vertex)
// 		或者 make(map[string]Vertex, 10) // 同时设置 capacity, 不是 length (无法设置 length, 因为设置 length 会初始化零值, 而 key 无法初始化零值, key 必须唯一)
// 插入: m[key] = elem
// retrieve检索: elem = m[key]
// 是否存在: elem, ok = m[key] 如果key存在, ok==true, 否则false, 此时elem==zero value
// 删除: delete(m, key)
// zero value == nil
// 
// len()函数获取map的当前长度 (cap()函数只能用于获取切片的容量，无法获得map的容量)
// 
// 查询/迭代 for k,v:=range m {}
// 
func mapDemo() {
	type Vertex struct {
		Lat, Long float64
	}
	// 声明
	var m map[string]Vertex
	// make初始化
	// 可以不指定map容量，但是对于map的多次扩充会造成性能损耗
	m = make(map[string]Vertex)
	// 声明同时初始化
	var studentScoreMap = map[string]int{
		"Tom":80,
		"Felix":85,
		"Peter":90,
	}
	// 赋值
	m["key"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["key"]) //{40.68433 -74.39967}
}

// Map literals - map的初始化
func mapInitDemo() {
	type Vertex struct {
		Lat, Long float64
	}

	var m = map[string]Vertex{
		"Bell Labs": { // Vertex 可以省略
			40.68433, -74.39967,
		},
		"Google": Vertex{
			37.42202, -122.08408,
		},
	}

	fmt.Println(m) //map[Bell Labs:{40.68433 -74.39967} Google:{37.42202 -122.08408}]
	fmt.Println(m2)
}

//////////////////////////////////////////

// 排序
// 如果你想为 map 排序，需要将 key（或者 value）拷贝到一个切片，再对切片排序（使用 sort 包)

```


### 并发安全的 map

```go
// 切片和map都是线程不安全的，建议不要开携程，否则就需要加锁

// 最常见的解决方案就是使用sync包对map加锁 (效率没有 sync.Map 好)
// 或直接使用Go在1.9版本中提供的线程安全的 sync.map
// 		适合读多写少场景 (对于读多写多, 需要自己实现, 类似 java 中的 concurrent map, 通过将一个大 map 分区为多个小 map)
// 		采用空间换时间的方案

// 加锁
var lock sync.RWMutex

func readMap(Gomap map[int]int,key int) int {
	lock.Lock() //读map操作前先加锁
	m := Gomap[key]
	lock.Unlock() //读完map后解锁
	return m
}
func writeMap(Gomap map[int]int,key int,value int){
	lock.Lock() //写map操作前先加锁
	Gomap[key] = value
	lock.Unlock() //写完map后解锁
}
func main() {
	GoMap := make(map[int]int)
	for i := 0; i < 10000; i++ {
		go writeMap(GoMap,i,i)
		go readMap(GoMap,i)
	}
	fmt.Println("Done")
}


// ------------ ------------ ------------


func readMap(Gomap sync.Map,key int) int {
	res ,ok := Gomap.Load(key) //线程安全读取
	if ok == true {
		return res.(int)//Load()方法的第一个返回值是接口类型，需要将其转换为map值的类型
	} else {
		return 0
	}

}

func writeMap(Gomap sync.Map,key int,value int){
	Gomap.Store(key,value) //线程安全设置
}

func main() {
	var GoMap sync.Map //无须初始化，直接声明即可
	for i := 0; i < 10000; i++ {
		go writeMap(GoMap,i,i)
		go readMap(GoMap,i)
	}
	fmt.Println("Done")
}



```

## container 包

### heap

heap： 堆容器，提供 heap 的实现, 底层是数组

```go
堆（Heap）就是用数组实现的完全二叉树。根据堆的特性可以分为两种：最大堆和最小堆，两者的区别在于节点的排序方式上：

在最大堆中，父节点的值比每一个子节点的值都要大，堆最大元素在 root 节点
在最小堆中，父节点的值比每一个子节点的值都要小， 堆最小元素在 root 节点 (Go 的堆容器 heap 在实现上是一个最小堆)


```

### ring

```go
// ring：循环链表容器

type Ring
    func New(n int) *Ring  // 初始化环
    func (r *Ring) Do(f func(interface{}))  // 循环环进行操作
    func (r *Ring) Len() int // 环长度
    func (r *Ring) Link(s *Ring) *Ring // 连接两个环
    func (r *Ring) Move(n int) *Ring // 指针从当前元素开始向后移动或者向前（n 可以为负数）
    func (r *Ring) Next() *Ring // 当前元素的下个元素
    func (r *Ring) Prev() *Ring // 当前元素的上个元素
    func (r *Ring) Unlink(n int) *Ring // 从当前元素开始，删除 n 个元素
```

### list

```go
// 链表容器 (双向链表)

type Element
    func (e *Element) Next() *Element
    func (e *Element) Prev() *Element
type List
    func New() *List
    func (l *List) Back() *Element   // 最后一个元素
    func (l *List) Front() *Element  // 第一个元素
    func (l *List) Init() *List  // 链表初始化
    func (l *List) InsertAfter(v interface{}, mark *Element) *Element // 在某个元素后插入
    func (l *List) InsertBefore(v interface{}, mark *Element) *Element  // 在某个元素前插入
    func (l *List) Len() int // 在链表长度
    func (l *List) MoveAfter(e, mark *Element)  // 把 e 元素移动到 mark 之后
    func (l *List) MoveBefore(e, mark *Element)  // 把 e 元素移动到 mark 之前
    func (l *List) MoveToBack(e *Element) // 把 e 元素移动到队列最后
    func (l *List) MoveToFront(e *Element) // 把 e 元素移动到队列最头部
    func (l *List) PushBack(v interface{}) *Element  // 在队列最后插入元素
    func (l *List) PushBackList(other *List)  // 在队列最后插入接上新队列
    func (l *List) PushFront(v interface{}) *Element  // 在队列头部插入元素
    func (l *List) PushFrontList(other *List) // 在队列头部插入接上新队列
    func (l *List) Remove(e *Element) interface{} // 删除某个元素

a).列表初始化
方式一：通过container/list包的New方法初始化list
l := list.New()
 
方式二:通过声明初始化list
var l list.List
 
列表没有具体元素类型的限制。因此列表的元素可以是任意类型
 
b).在列表中插入元素
l := list.New()
l.PushBack("first")              //从链表尾部插入元素“first”
element := l.PushFront(67)       //从链表头部插入元素67
l.InsertAfter("high", element)   //在element后插入元素
l.InsertBefore("noon", element)  //在element前插入元素
 
c).从链表中删除元素
l.Remove(element)
 
d).遍历列表
 
for i := l.Front(); i != nil; i = i.Next() {
    fmt.Println(i.Value)
}

```

## 迭代 range

### 迭代slice

```go


/*
range
迭代 slice 或 map, 返回 index 和 value(value的复制, 不是引用), value 可选

所以如果希望在 for range 中修改原始集合中数据, 只能通过索引/下标 data[i] = xxx (因为在“range”语句中生成的数据的值是真实集合元素的拷贝。它们不是原有元素的引用)

/当然, 如果集合中是指针, 那么还是可以通过 迭代出的 item 修改原始数据的

如果在循环中修改切片的长度不会改变本次循环的次数

针对 nil 切片，迭代次数为 0


语法
for index, value := range sliceName {}
*/
func rangeDemo() {
	var pow = []int{1, 2, 4, 8, 16, 32, 64, 128}
	for i, v := range pow {
		fmt.Printf("index=%d, value=%d\n", i, v)
	}
	// Range continued
	// 只想使用 index
	for i := range pow {
		pow[i] = 1 << uint(i) // == 2**i
	}
	// 只想使用 value
	for _, value := range pow {
		fmt.Printf("%d\n", value)
	}
}


```

### 迭代 map

```go

// 对于 map:
// 迭代 map 过程中，删除还未迭代到的键值对，则该键值对不会被迭代。
// 在迭代过程中，如果创建新的键值对，那么新增键值对，可能被迭代，也可能不会被迭代
// 针对 nil 字典，迭代次数为 0
```

### 迭代 channel

```go
// 如果是 nil 信道，循环将永远阻塞
```

### for 和 range 性能差异

```go
/*
与 for 不同的是，range 对每个迭代值都创建了一个拷贝


遍历 []int 类型的切片，for 与 range 性能几乎没有区别, 因为 range 对 int 类型拷贝此时还看不出性能区别

遍历 []struct, 
	仅遍历下标的情况下，for 和 range 的性能几乎是一样的
	遍历下标和值, ，for 的性能大约是 range (同时遍历下标和值) 的 2000 倍
*/
```

## 指针

```go


// Pointers 指针
//A pointer holds the memory address of a value.保存着一个value的内存地址
// &变量 - 根据变量获得指针
// *指针   - 根据指针获取变量
// var t *int  - 声明一个指针类型变量 , "*Type" 表示某个类型的指针
// 
// 零值为 nil.
// 
// 永远不要使用一个指针指向一个接口类型，因为它已经是一个指针, 即不能存在 var xxx *Interface , 因为接口类型的变量已经是一个指针了
// 
func pointerDemo() {
	i, j := 42, 2701

	p := &i         // point to i
	fmt.Println(*p) // read i through the pointer
	*p = 21         // set i through the pointer
	fmt.Println(i)  // see the new value of i

	p = &j         // point to j
	*p = *p / 37   // divide j through the pointer
	fmt.Println(j) // see the new value of j

	type MyStruct struct {
		X int
		Y int
	}
	myStruct := MyStruct{1, 2}
	p := &myStruct
	fmt.Println(p.Y) // 2 ; "(*p).X" 中的 "*" 被省略

}
```

## 结构体struct

### struct 基本使用

```go



//// Struct
// A struct is a collection of fields.
func structDemo() {
	// 可在 func 中, 也可在func外定义
	type MyStruct struct {
		X int
		Y int
	}

	// struct init
	myStruct := MyStruct{1, 2}
	fmt.Println(myStruct) //{1 2}
	// access field by variable
	fmt.Println(myStruct.X) // 1
	// access field by pointer
	p := &myStruct
	fmt.Println(p.Y) // 2 ; "(*p).X" 中的 "*" 被省略

	//Struct Literals : 通过列出指定field来为 struct 中的某个相应 field 重新赋值
	//语法
	// var v = MyStruct{FieldName: fieldValue ...}
	type Vertex struct {
		X, Y int
	}
	var (
		v1 = Vertex{1, 2}  // has type Vertex
		v2 = Vertex{X: 1}  // Y:0 隐式的, y被赋值为零值
		v3 = Vertex{}      // X:0 and Y:0
		p1 = &Vertex{1, 2} // has type *Vertex, p 为指针类型
	)

	fmt.Println(v1, p1, v2, v3) //{1 2} &{1 2} {1 0} {0 0}


	// 匿名结构体
	var a = struct {
		name string
		age  int
	}{"aa", 11}

	fmt.Println(a)

	// 匿名字段
	s := struct {
		string
		int
	}{"hello", 11}
	println(s.string)
}
```

### 空 struct

#### 利用 map实现集合set

```go
type Set map[string]struct{}

func (s Set) Has(key string) bool {
	_, ok := s[key]
	return ok
}

func (s Set) Add(key string) {
	s[key] = struct{}{}
}

func (s Set) Delete(key string) {
	delete(s, key)
}

```

#### 利用 channel 作为通知通道

```go
func worker(ch chan struct{}) {
	<-ch
	fmt.Println("do something")
	close(ch)
}

func main() {
	ch := make(chan struct{})
	go worker(ch)
	ch <- struct{}{}
}
```

### 匿名结构体 继承 重写

或者叫 "内嵌结构体	"

```go
package main

import (
	"fmt"
)

// 【基类】
//定义一个最基础的struct类MsgModel，里面包含一个成员变量msgId
type MsgModel struct {
	msgId   int
	msgType int
}

// MsgModel的一个成员方法，用来设置msgId
func (msg *MsgModel) SetId(msgId int) {
	msg.msgId = msgId
}
func (msg *MsgModel) SetType(msgType int) {
	msg.msgType = msgType
}

//【子类】
type GroupMsgModel struct {
	// 具体实现就是一个 struct 里面包含一个匿名的 struct
	MsgModel

	// 当两个字段拥有相同的名字（可能是继承来的名字）时
	// - 外层名字会覆盖内层名字（但是两者的内存空间都保留），这提供了一种重载字段或方法的方式；
	// - 如果相同的名字在同一级别出现了两次，如果这个名字被程序使用了，将会引发一个错误（不使用没关系）, 比如 c 包含 a,b 两个匿名 struct, a,b 都有一个 field 具有相同类型相同名字, 那么调用的时候回报错 
	msgId int
}

func (group *GroupMsgModel) GetId() int {
	return group.msgId
}



// ==============


// struct 的继承
type Human struct {
	name  string
	age   int
	phone string
}

type Student struct {
	Human  //匿名字段
	school string
}

type Employee struct {
	Human   //匿名字段
	company string
}

//在human上面定义了一个method
// 那么 Student, employee 自动继承了这个方法
func (h *Human) SayHi() {
	fmt.Printf("Hi, I am %s you can call me on %s\n", h.name, h.phone)
}

//Employee的method重写Human的method
func (e *Employee) SayHi() {
	fmt.Printf("Hi, I am %s, I work at %s. Call me on %s\n", e.name,
		e.company, e.phone) //Yes you can split into 2 lines here.
}

func methodExtendsOverride() {
	mark := Student{Human{"Mark", 25, "222-222-YYYY"}, "MIT"}
	sam := Employee{Human{"Sam", 45, "111-888-XXXX"}, "Golang Inc"}

	mark.SayHi()
	sam.SayHi()
}


```


## 接口 interface

### 接口作为函数形参 值接收者 指针接收者

```go
// 接收器语法: 类似方法参数 func (receiver T) xxxMethod(xxx, xx) {} , 底层是对普通方法定义的语法糖, 类似 Python: def xxx(self, arg1, arg2...)), 因此 不要用 self 作为接收器参数名
// 
// 这个接收器所在的方法必须和 type 定义在同一个包下
// 
// //pointer receiver指针指向原始值(可以修改原始值); 而 value receiver 只是原始值的 "一份复制",不可能修改原始值(和function参数性质一样)


//  对于接收器区别:
// 如果使用指针接收器
// 		- 只能使用指针调用接收器方法
// 		- 若实现了某个接口 (仅仅指针类型会被视为是接口 的子类), 则接口作为形参变量, 只能接收指针实参
// 		- 可以修改接收器内部字段
// 如果使用变量接收器
// 		- 既可以通过指针调用接收器方法, 也可以通过变量调用接收器方法
// 		- 若实现了接口 (指针类型和变量类型都被视为是接口的子类), 则接口作为形参变量, 即可以接收指针实参, 也可以接收变量实参
// 		- 无法修改接收器内部字段
//
////////////////////////////////
// 我们可以通过指针直接调值接收器方法，也可以通过值直接调指针接收器方法，go会为我们自动做值和指针之间的转换
//
// 在实现某个 interface 时, 
// 使用了普通变量接收器, 那么 interface 形参变量 可以接收实例, 也可以接收实例的指针 
// 若 使用的是指针接收器实现的 interface, 那么 interface 形参变量只能接收实例指针
// 
// 
type Abser interface {
	Abs() float64
}
type MyFloatInterfaceDemo float64

//
//为MyFloatInterfaceDemo类型添加 Abs(), 表示 MyFloatInterfaceDemo 实现了 Abser 接口
// 类似 Python 中的 duck type
func (f MyFloatInterfaceDemo) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

//
type VertexInterfaceDemo struct {
	X, Y float64
}
//
// 为 VertexInterfaceDemo 指针类型 添加 Abs();
// 注意 接收器不是变量类型而是指针类型, 所以后面代码中单纯的VertexInterfaceDemo类型还是不能赋值给 interface类型的变量
func (v *VertexInterfaceDemo) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

func interfaceDemo() {
	var a Abser // 定义 interface 类型变量
	var b Abser
	v := VertexInterfaceDemo{3, 4}         // 定义 VertexInterfaceDemo 类型的 struct
	f := MyFloatInterfaceDemo(-math.Sqrt2) // 定义 MyFloatInterfaceDemo 类型变量

	// &v 是指针, 作为指针, 实现了 abser interface, 所以可以接收
	a = &v // a *Vertex implements Abser
	// f 作为普通变量, 实现了 abser interface
	b = f // a MyFloat implements Abser

	// In the following line, v is a Vertex (not *Vertex) and does NOT implement Abser.
	// 错误, 因为 v 是普通变量, 作为普通变量 v 并没有实现 Abser interface
	//a = v

	// 正确 (所以 在实现某个 interface 时, 使用了变量接收器, 那么 interface 变量可以接收实例变量, 也可以接收实例指针)
	//      (若 使用的是指针接收器, 那么 interface 变量只能接收实例指针)
	b = &f

	fmt.Println(a.Abs()) //5
	fmt.Println(b.Abs()) //1.4142135623730951





//
// pointer 作为func的 "参数" and "接收器"
// 区别: 定义时指针作为 "参数" - 则函数调用时, 必须给 pointer
//       定义时指针作为 "接收器" - 函数调用时, 给 pointer 或 普通变量 均可
//
// 相应的: 普通变量 作为func的 "参数" and "接收器" - 区别和上面类似 https://tour.golang.org/methods/7
type ParamAndReceiverPointerVertex struct {
	X, Y float64
}

func (v *ParamAndReceiverPointerVertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}
func ScaleFunc(v *ParamAndReceiverPointerVertex, f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}
func paramAndReceiverPointerDemo() {
	v := ParamAndReceiverPointerVertex{3, 4}
	v.Scale(2)        //虽然定义时接收器是指针, 但是这里接收器可以是普通变量
	ScaleFunc(&v, 10) // 定义时参数是指针, 这里必须是传指针
	//ScaleFunc(v, 10)  // Compile error! 如果是变量则报错

	p := &ParamAndReceiverPointerVertex{4, 3}
	p.Scale(3)      // 接收器可以是pointer
	ScaleFunc(p, 8) // 参数必须是指针

	fmt.Println(v, p) //{60 80} &{96 72}
}
```

### 空接口

```go

	//
	//
	//empty interface 空接口 - 空接口可以接受任意类型变量
	//例如 fmt.Print方法可以接受任意类型变量, 定义时就是使用的interface{}类型
	//  例如 空接口作为map的值
	//
	describe := func(i interface{}) {
		fmt.Printf("(%v, %T)\n", i, i) // 打印值, 类型
	}

	var i interface{}
	describe(i) //(<nil>, <nil>)

	i = 42
	describe(i) //(42, int)

	i = "hello"
	describe(i) //(hello, string)

	//
	//
	stringerInterface()

	//
	//
	errorInterface()
}



```

### 类型断言

```go

// Type assertions 类型断言 - 提供对 空接口变量 具体类型的访问
// 语法: t := i.(T)
func typeAssert() {
	var i interface{} = "hello"

	s := i.(string)
	fmt.Println(s) //hello

	s, ok := i.(string)
	fmt.Println(s, ok) ////hello true

	f, ok := i.(float64)
	fmt.Println(f, ok) //0 false

	// f = i.(float64) // 触发 panic
	// fmt.Println(f)
}

// Type switches  - 类型断言的升级版: 多个类型断言写在一起 (必须和 switch,case 合用)
func typeSwitch() {
	do := func(i interface{}) {
		switch v := i.(type) { //type 是关键字(固定写法), v 的值是转型后的值, 不是类型
		case int:
			fmt.Printf("Twice %v is %v\n", v, v*2)
		case string:
			fmt.Printf("%q is %v bytes long\n", v, len(v))
		default:
			fmt.Printf("I don't know about type %T!\n", v)
		}
	}

	do(21)      //Twice 21 is 42
	do("hello") //"hello" is 5 bytes long
	do(true)    //I don't know about type bool!

}

```

### 内置接口

```go

//
// Stringer interface - 类似 Java 中的 toString() - 定义在 fmt 包, 只有一个方法: String() string
type Person struct {
	Name string
	Age  int
}

// 实现 Stringer接口
func (p Person) String() string {
	return fmt.Sprintf("%v (%v years)", p.Name, p.Age)
}
func stringerInterface() {
	a := Person{"Arthur Dent", 42}
	z := Person{"Zaphod Beeblebrox", 9001}
	fmt.Println(a, z) //Arthur Dent (42 years) Zaphod Beeblebrox (9001 years)
}

//
// error interface - 类似 Stringer 接口, 只有一个方法: Error() string
type MyError struct {
	When time.Time
	What string
}

// 实现 error 接口
// 之后 就可以 被 error 接收
func (e *MyError) Error() string {
	return fmt.Sprintf("at %v, %s",
		e.When, e.What)
}
func errorInterface() {
	run := func() error {
		return &MyError{
			time.Now(),
			"it didn't work",
		}
	}

	if err := run(); err != nil {
		fmt.Println(err) //at 2018-10-16 12:56:02.8149885 +0800 CST m=+0.092996101, it didn't work
	}
}
```


### 接口嵌套

```go

// interface 的继承
type ReadWrite interface {
    Read(b Buffer) bool
    Write(b Buffer) bool
}

type Lock interface {
    Lock()
    Unlock()
}

type File interface {
    ReadWrite
    Lock
    Close()
}
```

### 接口完整性检查

```go
// 声明一个 _ 变量（没人用），把一个 nil 的空指针，从 Square 转成 Shape，这样，如果*Square没有实现完Shape相关的接口方法，编译器就会报错
var _ Shape = (*Square)(nil)

```

## 函数

### 函数基本语法

```go

//////////////////////////////////////
func funcDemo() {

	//Functions continued
	//// 多个参数类型相同, 可共享类型
	add1 := func(x, y int) int {
		return x + y
	}
	println(add1) // 0x4ce678

	//Multiple results
	//多个返回值
	swap := func(x, y string) (string, string) {
		return y, x
	}
	println(swap) //0x4ce680

	//Named return values
	// 被命名的 "返回值" - 直接 "return"
	// 只适合在短函数中使用, 因为 They can harm readability in longer functions.
	split := func(sum int) (x, y int) {
		x = sum * 4 / 9
		y = sum - x
		return
	}
	println(split)

	// 函数作为参数传递
	// 这个函数接受一个 函数, 用来处理 参数 "3" "4"
	compute := func(fn func(float64, float64) float64) float64 {
		return fn(3, 4)
	}
	hypot := func(x, y float64) float64 { // 求直角三角形第三边
		return math.Sqrt(x*x + y*y)
	}
	fmt.Println(hypot(5, 12))      //13
	fmt.Println(compute(hypot))    //5
	fmt.Println(compute(math.Pow)) //81
```

### 值传递 引用传递

```go
//
// 值传递 vs 引用传递
// 在方法传参时全部都是值传递，在闭包捕获外部变量时是引用传递 (一个函数总是得到一个被传递的东西的副本, 闭包拿到的外部变量都是引用), 
// 所有看上去像是引用传递的场景, 实际传递的是指针(指针的拷贝, 指向同一个地址)
//
// 对于基本类型, 都是值传递, 如 byte,int,bool,string, 数组
// 对于 struct 值传递
// 对于 slice 和 map , channel, 是值传递, 底层实际是封装的指针类型, 引用的是原来的数据, 所以修改会作用到原来的数据 (所以行为类似于传引用)
// 对于 interface{}  复制一个接口值会复制存储在接口值中的东西 (如果接口值持有一个结构，复制接口值就会复制该结构。如果接口值持有一个指针，复制接口值会复制该指针)
// 对于函数, 也是值传递(传递的是指向函数的指针)
//对于 "指针" , 传递的是指针的拷贝(两个指针拷贝指向同一个对象/内存地址), 效果相当于指向对象的 "引用传递"
//
array := [3]int{0, 1, 2}
// 数组是值传递
var array2 = array
array2[2] = 5
fmt.Println(array, array2) // [0 1 2] [0 1 5]




// 对于切片, 也是值传递, 但是对切片参数的修改会影响原来的切片。 (因为切片实际是对底层数组的部分引用)
func passSlice(_s []int){
    _s[0]=99
    fmt.Printf("_s 值：%v,地址：%p\n",_s,&_s)
}
func exp6(){
    s:=[]int{11,22,33,44}
    fmt.Printf("s 值：%v,地址：%p\n",s,&s)
    passSlice(s)
    fmt.Printf("执行函数后 s 值：%v,地址：%p\n",s,&s)
	/*
	s值[11 22 33 44], 地址 0x00001
	_s值[99 22 33 44] 地址 0x00099
	执行函数后s 值: [99 22 33 44], 地址 0x00001
	*/
}


// 对于数组, 也是值传递, 但是对于数组参数的修改不会影响原来切片/数组
func passArray(_a [3]int){
    _a[0]=99
    fmt.Printf("_a 值：%v,地址：%p\n",_a,&_a)
}
func exp7(){
    a:=[3]int{22,33,44}
    fmt.Printf("a 值：%v,地址：%p\n",a,&a)
    passArray(a)
    fmt.Printf("执行函数后 a 值：%v,地址：%p\n",a,&a)
	/*
	s值[11 22 33 44], 地址 0x00001
	_s值[99 22 33 44] 地址 0x00099
	执行函数后s 值: [11 22 33 44], 地址 0x00001
	*/
}
}

```

指针作为函数参数 也是拷贝: 看一个典型错误


```go
// 功能: 传入一个指针作为 GetOne 的参数，然后在函数内给这个指针变量设置值
func main() {
	var oi OrderInfo
	
	GetOne(&oi)

	fmt.Println(oi)
}
type OrderInfo struct {
	Id string
	Price float64
	Status int
}
// 因为给函数传参是值传递, 这里传递的是指针的拷贝
func GetOne(orderInfo *OrderInfo) {
	// 错误的写法 (这里orderInfo指针指向了一个全新地址, 和 main() 中的 io 无关了)
	orderInfo = &OrderInfo{
		Id: "aaaa",
		Price: 100.00,
		Status: 1,
	}

	// 正确的写法: 直接对指针指向的值进行赋值
	*orderInfo = OrderInfo{
		Id: "aaaa",
		Price: 100.00,
		Status: 1,
	}
}

```

### 函数返回局部变量 逃逸分析

```go
// 在C/C++语言中，局部变量分配在栈空间，因为函数返回后，系统会自动回收函数里定义的局部变量，
// 		所以在返回局部变量的值时，实际是返回局部变量的副本; 
// 		若返回了局部变量的指针, 一定会发生空指针异常 (要解决这种问题，只需将内存空间分配在堆中即可。)
// 在Go语言中返回局部变量的值也是一样的，
// 		返回的也是局部变量的副本; 
// 		若返回指针, 函数内部局部变量，无论是动态new出来的变量还是创建的局部变量，它被分配在堆还是栈，是由编译器做“逃逸分析”之后做出的决定
// 			- 局部变量分配空间时会尽可能地分配在栈空间中, 但是若编译器无法确定局部变量是否会被返回出函数外部(也就是可能存在局部变量逃逸) 则会将该局部变量分配在堆空间中, 
// 			- 如果局部变量占用内存很大，Go编译器会将其存储在堆空间中 

func foo() int {    //int类型函数
	tmp := 1
	fmt.Println(&tmp)  // 0xc00000a0e0
	return tmp      //返回局部变量
}
func main() {
	v := foo()
	fmt.Println(&v)  // 0xc00000a0c8(和tmp地址不同)
}

// ---------------------
 func foo() *int {    // 返回int类型指针
	tmp := 2020
	return &tmp      // 返回局部变量tmp的地址
}

func main() {
	var ptr *int
	// main函数中引用了foo函数内的局部变量tmp
	// 根据“逃逸分析”，编译器会将其分配在堆空间上
	ptr = foo()
	// foo函数执行结束后tmp不会被释放
	fmt.Println(*p) // 结果为2020，不会报错
}

```

## 闭包 

```go

func closureDemo() {

	// Function closures 闭包
	// 闭包是一个 function value，它引用来自其体外的变量。
	// 闭包构成了一个独立的context, 有了 "状态"
	adder := func() func(int) int {
		sum := 0 // 一直维持在内存中, 会造成累加效果
		// 返回一个闭包
		return func(x int) int {
			sum += x // 访问体外的变量sum
			return sum
		}
	}

	pos, neg := adder(), adder()
	for i := 0; i < 5; i++ {
		fmt.Println(
			pos(i),
			neg(-2*i),
		)
		/*
			0 0
			1 -2
			3 -6
			6 -12
			10 -20
		*/
	}

}

```

## 方法 和 接收器

```go


////////////////////////////////
//
// Methods & 接收器 receiver
//
//指定函数的接收器 - -  只是在 "func" 关键字 和 "func name"之间 添加了 "接收器"
// 接收器语法: 类似方法参数
// 这个接收器所在的方法必须和 type 定义在同一个包下
type vertex1 struct {
	X, Y float64
}

// 接收器可以是任意类型, 这里指定为 Vertex1, 相当于给Vertex1添加方法
func (v vertex1) abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
func structMethodReceiver() {
	v := vertex1{3, 4}
	fmt.Println("structMethod", v.abs()) //5

	methodContinue()

	pointerReceiverDemo()

	paramAndReceiverPointerDemo()

}

///////////////////////

//MyFloat : Methods continued
// 接收器可以是任意类型, 比如 float64, 下面的 func中 的接收器就是这个类型
type MyFloat float64

// Abs 到处必须大写
func (f MyFloat) Abs() float64 {
	if f < 0 {
		return float64(-f)
	}
	return float64(f)
}

func methodContinue() {
	var f MyFloat = -2.2
	println(f.Abs())     //+2.200000e+000
	fmt.Println(f.Abs()) //2.2
}

////////////////////////////////////////

// Pointer receivers 指针接收器
//相比于 value receiver 使用更加广泛
//对比 pointer receiver vs. value receiver:
//pointer receiver指针指向原始值(可以修改原始值); 而 value receiver 只是原始值的 "一份复制",不可能修改原始值(和function参数性质一样)
// 指针接收器 使用场景:
//1. 希望通过接收器修改指向的变量的值; 2. 希望避免在每次方法调用时复制值, 尤其当receiver是一个big struct 的时候
type PointerVertex struct {
	X, Y float64
}

// 使用普通接收器
func (v PointerVertex) Abs() float64 {
	return math.Sqrt(v.X*v.X + v.Y*v.Y)
}

// 使用指针接收器
// 可以直接修改 pointer 指向的原始值;
//这个function作用: 放大 f 倍
func (v *PointerVertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}
func pointerReceiverDemo() {
	v := PointerVertex{3, 4}
	v.Scale(10)
	fmt.Println(v.Abs()) //50
}

/////////////////////////////////////

//
// pointer 作为func的 "参数" and "接收器"
// 区别: 定义时指针作为 "参数" - 则函数调用时, 必须给 pointer
//       定义时指针作为 "接收器" - 函数调用时, 给 pointer 或 普通变量 均可
//
// 相应的: 普通变量 作为func的 "参数" and "接收器" - 区别和上面类似 https://tour.golang.org/methods/7


// 对于方法接收器: 定义时使用指针, 使用时可以用 变量 or 指针
// 对于方法参数: 定义时是啥类型, 使用时必须是啥类型
type ParamAndReceiverPointerVertex struct {
	X, Y float64
}

func (v *ParamAndReceiverPointerVertex) Scale(f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}
func ScaleFunc(v *ParamAndReceiverPointerVertex, f float64) {
	v.X = v.X * f
	v.Y = v.Y * f
}
func paramAndReceiverPointerDemo() {
	v := ParamAndReceiverPointerVertex{3, 4}
	v.Scale(2)        //虽然定义时接收器是指针, 但是这里接收器可以是普通变量
	ScaleFunc(&v, 10) // 定义时参数是指针, 这里必须是传指针
	//ScaleFunc(v, 10)  // Compile error! 如果是变量则报错

	p := &ParamAndReceiverPointerVertex{4, 3}
	p.Scale(3)      // 接收器可以是pointer
	ScaleFunc(p, 8) // 参数必须是指针

	fmt.Println(v, p) //{60 80} &{96 72}
}

//////////////////////////////////

```


## 流程控制

### 死循环 for 和 select 区别

```go
func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprintln(w, "Hello, GopherCon SG")
	})
	go func() {
		if err := http.ListenAndServe(":8080", nil); err != nil {
			log.Fatal(err)
		}
	}()
	// bad
	//将阻塞 main goroutine, 无限循环中浪费 CPU 资源
	for {
	}
	//good
	for {
		//  每次空循环, 让出 cpu
		runtime.Gosched()
	}

	// better
	select {} // 空的 select 语句将永远阻塞, 同时不会占住整个 cpu
}


```

### if 和 for 循环

```go


func conditionControl() {

	// if 条件判断
	//条件判断语句里面允许声明一个变量，这个变量的作用域只能在该条件逻辑块内
	// 开根号
	// func sqrt(x float64) string { //这里只是演示 if 用法
	// 	if x < 0 {
	// 		return sqrt(-x) + "i"
	// 	}
	// 	// 输出到字符串
	// 	return fmt.Sprint(math.Sqrt(x)) //1.4142135623730951 2i
	// }

	//if 后面可以跟短句
	// if v := math.Pow(x, n); v < lim { // 如果小于 lim 返回结果
	// 	return v
	//   }

	// for loop 循环
	sum := 0
	for i := 0; i < 10; i++ { // The init and post statements are optional.首尾可选
		sum += i
	}
	fmt.Println(sum) // 45

	// 没有 while, 只有 for
	for sum < 1000 {
		sum += sum
	}
	fmt.Println(sum)

	//Forever
	// 死循环
	// for {
	// }

	// 另一种死循环
	// ch := make(chan int)
	// do sth
	// go goroutine
	// <-ch // 这里会阻塞住


	//
	// switch 就是 if else 的简便写法
	//Switch evaluation order: Switch cases evaluate cases from top to bottom, stopping when a case succeeds.
	fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os { // 跟 if 一样, 条件前可跟 一条语句
	case "darwin":
		fmt.Println("OS X.")
		// 这里无需跟break
	case "linux":
		fmt.Println("Linux.")
	// case f() // 可以是函数
	default:
		// freebsd, openbsd,
		// plan9, windows...
		fmt.Printf("%s.", os)
	}

	// switch 不带条件, 相当于 switch true
	// 可以用来代替 long if-then-else chains
	t := time.Now()
	switch {
	case t.Hour() < 12:
		fmt.Println("Good morning!")
	case t.Hour() < 17:
		fmt.Println("Good afternoon.")
	default:
		fmt.Println("Good evening.")
	}

```

### 标签 goto break

```go

	//
	//goto
	//用goto跳转 必须跳转到 在当前函数内定义的标签
	//标签名是大小写敏感的
	i := 0
Here: //这行的第一个词，以冒号结束作为标签
	println("goto ->", i)
	i++
	if i < 3 {
		goto Here //跳转到Here去
	}

	
```

### defer

```go
	//
	// defer
	// 语法
	// defer xxxStatement
	// 
	// defer xxxfunc(arguments)
	//推迟执行, 但是 arguments 会被立即正常执行, 但是 这个func会被推迟执行(until the surrounding function returns.)
	// 
	// Stacking defers: 推迟执行的func都存储到哪里了?
	//  都被存储到一个 stack 中 , 遵循 last-in-first-out order
	// 
	// defer 仅在函数返回时才会执行，在循环的结尾或其他一些有限范围的代码内不会执行
	// 
	deferParam := func() string {
		fmt.Println("参数被执行")
		return "世界"
	}
	defer fmt.Println("world")      // 先进后出
	defer fmt.Println(deferParam()) // 参数立即执行, 即deferParam() 立即运行

	fmt.Println("hello")
	//参数被执行
	// hello
	// 世界
	// world




func main() {
  for i := 0; i < 4; i++ {
	  // defer 一条语句, 不是函数
    defer fmt.Print(i)
  }
}
/*
3
2
1
0
*/

for i := 0; i < 3; i++ {
	// defer 一个自动执行的闭包
  defer func() {
   fmt.Println(i) // 捕获的是变量地址, 即 i 的地址, 不是拷贝, i 最终变为 3
				// 循环结束, defer 闭包内的语句开始执行
   				//所有的延迟函数会查看相同的 i ，循环结束（值变成了3)，因此它们查看到的都是 3 。

  }()
}
/*
3
3
3
*/

for i := 0; i < 3; i++ {
  defer func(i int) {
   fmt.Println(i)
  }(i)//直接向延迟函数传参数。
}
/*
2
1
0
*/


// 获取 defer 函数的返回值

type Atype struct {}

func (a Atype) Close() error {
	return errors.New("error off close")
}

func TestDefer(t *testing.T) {

	f := func(a Atype) (err error) {
		defer func() {
			// err 变量赋值会创建一个全新的变量, 不再是返回值定义中的 err 了, 也就是 "作用域屏蔽了参数"
			// 若希望 defer 中的错误被返回回去, 使用 = 不要使用 :=
			if err := a.Close(); err != nil {

			}
		}()
		return
	}
	err := f(Atype{})
	if err != nil {
		log.Printf("%v\n", err)
	}
}






// 不要在循环中直接使用defer
for {
	...
	defer xxx
	//由于这是一个死循环，defer代码不会被执行到，所以申请的内存得不到释放，然后会导致程序占满整个内存，死机
}

// 但是可以封装到匿名函数中使用
for {

	...

    go func (){
        conn, err := grpc.Dial(address, grpc.WithInsecure())
        if err != nil {
            log.Fatalf("did not connect: %v", err)
        }
		//这里的defer会在匿名函数结束的时候得到执行，所以这样写就不会出现之前的资源没有释放的情况。
        defer conn.Close()
    }()
}

```

## sort 包

```go
// 实现这个接口
type Sorter interface {
    Len() int
    Less(i, j int) bool
    Swap(i, j int)
}

// 想对一个 int 数组进行排序，所有必须做的事情就是：为数组定一个类型并在它上面实现 Sorter 接口的方法
type IntArray []int
func (p IntArray) Len() int           { return len(p) }
func (p IntArray) Less(i, j int) bool { return p[i] < p[j] }
func (p IntArray) Swap(i, j int)      { p[i], p[j] = p[j], p[i] }
```

## http

### 原理

```go
// 路由如何实现的?
// 默认路由器中有个 map[string]muxEntry, muxEntry {pattern, Handler}, Handler 接口 就是处理业务逻辑的
// Handler包含一个 ServeHTTP(ResponseWriter, *Request) 方法, 只有实现这个方法, 才是 Handler

// 最关键的点:
type HandlerFunc func(ResponseWriter, *Request) 
// ServeHTTP calls f(w, r).
func (f HandlerFunc) ServeHTTP(w ResponseWriter, r *Request) {
	f(w, r)
}
// 这样, 我们实现自己的 Handler 时就无需手动实现 ServeHTTP 方法了
```

### 案例:客户端超时取消

```go

// server端，随机出现慢响应

func indexHandler(w http.ResponseWriter, r *http.Request) {
	number := rand.Intn(2)
	if number == 0 {
		time.Sleep(time.Second * 10) // 耗时10秒的慢响应
		fmt.Fprintf(w, "slow response")
		return
	}
	fmt.Fprint(w, "quick response")
}

func main() {
	http.HandleFunc("/", indexHandler)
	err := http.ListenAndServe(":8000", nil)
	if err != nil {
		panic(err)
	}
} 


///////////////////////////////////////////////////

// 客户端

type RespData struct {
	resp *http.Response
	err  error
}

func doCall(ctx context.Context) {
	client := http.Client{
		Transport: &http.Transport{
			// 请求频繁可定义全局的client对象并启用长链接
			// 请求不频繁使用短链接
			DisableKeepAlives: true},
	}

	respChan := make(chan *RespData, 1)
	req, err := http.NewRequest("GET", "http://127.0.0.1:8000/", nil)
	if err != nil {
		fmt.Printf("new requestg failed, err:%v\n", err)
		return
	}
	req = req.WithContext(ctx) // 使用带超时的ctx创建一个新的client request
	var wg sync.WaitGroup
	wg.Add(1)
	defer wg.Wait()
	go func() {
		resp, err := client.Do(req)
		fmt.Printf("client.do resp:%v, err:%v\n", resp, err)
		rd := &RespData{
			resp: resp,
			err:  err,
		}
		respChan <- rd
		wg.Done()
	}()

	select {
	case <-ctx.Done():
		//transport.CancelRequest(req)
		fmt.Println("call api timeout")
	case result := <-respChan:
		fmt.Println("call server api success")
		if result.err != nil {
			fmt.Printf("call server api failed, err:%v\n", result.err)
			return
		}
		defer result.resp.Body.Close()
		data, _ := ioutil.ReadAll(result.resp.Body)
		fmt.Printf("resp:%v\n", string(data))
	}
}

func main() {
	// 定义一个100毫秒的超时
	ctx, cancel := context.WithTimeout(context.Background(), time.Millisecond*100)
	defer cancel() // 调用cancel释放子goroutine资源
	doCall(ctx)
}


```

## context

### context注意实现

- Context是线程安全的，可以放心的在多个goroutine中传递
- 给一个函数方法传递Context的时候，不要传递nil，如果不知道传递什么，就使用context.TODO()
- 以Context作为参数的函数方法，应该把Context作为第一个参数

### WithCancel

协调具有层级关系的 goroutine, 一旦 goroutine 有层级, 单纯使用 channel 就无法控制这些goroutine 了

用于优雅的通知子 goroutine 退出

```go

func main() {
	con, cancel := context.WithCancel(context.Background())
	// 在程序末尾调用 cancel, 会发送一个标志 到 Done() channel 里, 表示结束
	defer cancel()

	ch := make(chan int)
	n := 1
	go func(con context.Context) {
	LABEL:
		for true {
			select {
			case ch <- n:
				n++
			case <-con.Done(): // done()返回一个 channel, 这里表示从中接收结束标志
				break LABEL
			}
		}
	}(con)

	for n := range ch {
		println(n)
		if n == 3 {
			break
		}
	}

}

```


### WithDeadline

可以为 子 goroutine 设置一个退出截止时间

```go

func main() {
	deadline, cancelFunc := context.WithDeadline(context.Background(), time.Now().Add(time.Millisecond*50))
	// 尽管ctx会过期，但在任何情况下调用它的cancel函数都更保险一点
	defer cancelFunc()

	select {
	case <-time.After(time.Second):
		println("after 1 second")
	case <-deadline.Done():  // 会走这个分支, 因为 deadline 只设置了 50 ms, 没到一秒
		println("after 50ms")
		println(deadline.Err()) // 打印的是地址
		fmt.Println(deadline.Err()) // 打印字符串信息
	}

}
```

### WithTimeout

类似 withDeadline, 不过设置的是一个时间段, 到期子 goroutine 退出

```go

var waitG sync.WaitGroup

func main() {
	timeout, cancelFunc := context.WithTimeout(context.Background(), time.Second*3)
	// 加上这行更保险
	cancelFunc()
	waitG.Add(1)

	go func() {
	LABEL:
		for {
			println("do something 1s")
			time.Sleep(time.Second)

			select {
			case <-timeout.Done():
				println("heha")
				break LABEL
			default:
				// 一定要加 default, 否则 select 还是会和 range xxxChannel 一样阻塞住, 阻塞在第一个 case

			}
		}
		waitG.Done()
	}()

	waitG.Wait()

}

```

### WithValue

在父子 goroutine 传递数据

```go

var waitG sync.WaitGroup

type LogId string

func main() {

	timeout, cancelFunc := context.WithTimeout(context.Background(), time.Second*3)
	defer cancelFunc()

	id := LogId("logId")
	valueCon := context.WithValue(timeout, id, "123")

	waitG.Add(1)

	go func() {
		s, ok := valueCon.Value(id).(string)
		if !ok {
			fmt.Println("error of get log id value")
		}
	LABEL:
		for {
			println("do something 1s, log id value = " + s)
			time.Sleep(time.Second)

			select {
			case <-valueCon.Done():
				println("heha")
				break LABEL
			default:
				// 一定要加 default, 否则 select 还是会和 range xxxChannel 一样阻塞住, 阻塞在第一个 case

			}
		}
		waitG.Done()
	}()


	waitG.Wait()

}
```


## io 

### 文件操作

```go
/*
// io 包里的 Readers 和 Writers 都是不带缓冲的，
// bufio 包里提供了对应的带缓冲的操作，在读写 UTF-8 编码的文本文件时它们尤其有用
type Reader interface {
	//返回读取的字节数和一个 error 对象，如果没有错误发生返回 nil，如果已经到达输入的尾端，会返回 io.EOF("EOF")，
    Read(p []byte) (n int, err error)
}
type Writer interface {
    Write(p []byte) (n int, err error)
}
*/
func ioDemo() {

	// reader - The io package specifies the io.Reader interface
	//有一个方法: func (T) Read(b []byte) (n int, err error)
	r := strings.NewReader("Hello, Reader!")

	b := make([]byte, 8)
	for {
		// n 表示读取了多少长度
		n, err := r.Read(b)
		fmt.Printf("n = %v err = %v b = %v\n", n, err, b)
		fmt.Printf("b[:n] = %q\n", b[:n])
		if err == io.EOF {
			break
		}
	}
	// print
	/*
		n = 8 err = <nil> b = [72 101 108 108 111 44 32 82]
		b[:n] = "Hello, R"
		n = 6 err = <nil> b = [101 97 100 101 114 33 32 82]
		b[:n] = "eader!"
		n = 0 err = EOF b = [101 97 100 101 114 33 32 82]
		b[:n] = ""
	*/


}

```

### scanner

```go
/*
Scanner是有缓存的，意思是Scanner底层维护了一个Slice用来保存已经从Reader中读取的数据，

type SplitFunc func(data []byte, atEOF bool) (advance int, token []byte, err error)

	Scanner会调用我们设置SplitFunc，将缓冲区内容(data)和是否已经输入完了(atEOF)以参数的形式传递给SplitFunc，而SplitFunc的职责就是根据上述的两个参数返回下一次Scan需要前进几个字节(advance)，分割出来的数据(token)，以及错误(err)。


*/
func main() {
    input := "abcdefghijkl"
    scanner := bufio.NewScanner(strings.NewReader(input))
    split := func(data []byte, atEOF bool) (advance int, token []byte, err error) {
        fmt.Printf("%t\t%d\t%s\n", atEOF, len(data), data)
        return 0, nil, nil // 返回的前进字节数始终是 0, 所以每次输出都是从第一个字符输出
    }
    scanner.Split(split)
    buf := make([]byte, 2) //缓冲区的初始大小设置为了2，不够的时候会扩展为原来的2倍，最大为bufio.MaxScanTokenSize
    scanner.Buffer(buf, bufio.MaxScanTokenSize)
    for scanner.Scan() {
        fmt.Printf("%s\n", scanner.Text()) // 因为每次循环 split 函数返回的 token 都是 "", 这里不会打印内容, 只会打印换行符
    }
}
/*
false 2 ab
false 4 abcd
false 8 abcdefgh
false 12 abcdefghijkl
true 12 abcdefghijkl
*/

// 标准库里的ScanLines实现
func ScanLines(data []byte, atEOF bool) (advance int, token []byte, err error) {
    // 表示我们已经扫描到结尾了
    if atEOF && len(data) == 0 {
        return 0, nil, nil
    }
    // 找到\n的位置
    if i := bytes.IndexByte(data, '\n'); i >= 0 {
        // 把下次开始读取的位置向前移动i + 1位
        return i + 1, dropCR(data[0:i]), nil
    }
    // 这里处理的reader内容全部读取完了，但是内容不为空，所以需要把剩余的数据返回
    if atEOF {
        return len(data), dropCR(data), nil
    }
    // 表示现在不能分割，向Reader请求更多的数据
    return 0, nil, nil
}
```

## image 

```go


	// image -  Package image defines the Image interface
	// https://tour.golang.org/methods/24
	/*
	   有三个方法:
	   ColorModel() color.Model
	   Bounds() Rectangle
	   At(x, y int) color.Color
	   **/
```



## channel csp并发控制

### channel 使用

```go

// channel
//无缓冲 channel 是在多个 goroutine之间同步的好工具
//goroutine运行在相同的地址空间，因此访问共享内存必须做好同步
//
/**语法
 ch := make(chan int) // 声明&创建
 c chan int						// 声明
ch <- v    // Send v to channel ch.
v := <-ch  // Receive from ch, 
// 或者
v, ok := <-ch

close(ch) // 关闭 channel
*/
// 默认情况下, channel接收和发送数据都是阻塞的
// 比如, 任何发送动作（如 ch<-5）将会被阻塞，直到前一个数据被读出; 任何读出动作 (如 value := <-ch) 将会被阻塞, 直到下一个数据被发送
//发送和接收块会在另一侧准备好的情况下进行(如果对方还没准备好, 就 block)。这样就允许goroutine在没有显式锁或条件变量的情况下进行同步
//
//Buffered Channels 缓冲 channel
// 语法: ch := make(chan int, 100)
//
//sender 可以关闭 channel 通过 close(xxxChannel), 表示传输终止
// receiver 可以检测 channel是否被关闭通过 v, ok := <-ch
// 只有 sender 可以 close channel, 而不是 receiver
// channel不是 文件, 一般无需关闭, 只有 receiver 需要被告知 "没有更多的 value 会被传过来了" 才需要关闭(比如: 终结 range channel)
func channelDemo() {
	sum := func(s []int, c chan int) {
		sum := 0
		for _, v := range s {
			sum += v
		}
		c <- sum // send sum to c
	}

	////对切片中的数字求和，在两个goroutine之间分配工作。两个goroutine完成计算后，它会计算最终结果
	s := []int{7, 2, 8, -9, 4, 0}

	c := make(chan int)
	go sum(s[:len(s)/2], c) // 用一个 goroutine 计算前半部分
	go sum(s[len(s)/2:], c) // 计算后半部分
	// receive from c ; x 为后半段和, y 为前半段和
	x, y := <-c, <-c // 阻塞在这里, 直到新开的 goroutine 将计算结构塞入 chan

	fmt.Println(x, y, x+y) //-5 17 12

	// 缓冲队列
	ch := make(chan int, 2)
	ch <- 1
	ch <- 2
	fmt.Println(<-ch) //1
	fmt.Println(<-ch) //2



}
```

### 利用 nil channel 实现动态 的 select case 

```go


	// 使用了值为 nil 的 channel, 即 在一个值为 nil 的 channel 上发送和接收数据将永久阻塞：
	// 利用这个死锁的特性, 在 select 中动态的打开和关闭 case 语句块
	inCh := make(chan int)
    outCh := make(chan int)

    go func() {
        var in <-chan int = inCh // in 是 <-chan int 类型, 只能往外拿
        var out chan<- int  // out 只能往里塞
        var val int

        for {
            select {
            case out <- val:
                println("--------")
                out = nil
                in = inCh
            case val = <-in:
                println("++++++++++")
                out = outCh
                in = nil
            }
        }
    }()

    go func() {
        for r := range outCh {
            fmt.Println("Result: ", r)
        }
    }()

    time.Sleep(0)
    inCh <- 1
    inCh <- 2
    time.Sleep(3 * time.Second)
```

### 迭代 channel 元素

#### 使用 for range

```go

	//
	// range 循环读取 channel
	//
	// 被 select 替代了, 因为 range channel不是异步的, 是顺序的会阻塞,
	//而且 如果channel中没有数据流动了, 会一直阻塞, 而 select 提供了 default 选项
	//
	fibonacci := func(n int, c chan int) {
		x, y := 0, 1
		for i := 0; i < n; i++ {
			c <- x
			x, y = y, x+y
		}
		close(c) // 关闭 channel
	}

	c1 := make(chan int, 10)
	go fibonacci(cap(c1), c1)
	for i := range c1 { //// range xxxChan 会循环接收 channel中的元素, 直到 sender 关闭 channel
		fmt.Print(i, " ") //0 1 1 2 3 5 8 13 21 34
	}
	println()

```

#### 使用 for select

```go


	//
	//
	// select -------- 循环读取 channel 更好的选择
	//
	//select 用于选择不同类型的通讯
	// 通过select可以监听多个channel上的数据流动
	// select默认是阻塞的，每个case的IO事件都是阻塞的, 只有当监听的channel中有发送或接收可以进行时才会运行
	//当多个channel都准备好的时候，select是随机的选择一个执行的
	// default就是当监听的channel都没有准备好的时候，默认执行（select不再阻塞等待channel）
	fibonacci1 := func(c, quit chan int) {
		x, y := 1, 1
		for {
			select {
			case c <- x: // 如果成功将 x 塞入 c 中
				x, y = y, x+y
			case <-quit: // 如果接受到结束标志
				fmt.Println("quit")
				return
			default: // 当所有 channel block时执行, 
			//一定要加 default, 否则 select 还是会和 range xxxChannel 一样阻塞住, 阻塞在第一个 case
				fmt.Println(">>> all channel block")
			}

		}
	}
	cha := make(chan int)
	quit := make(chan int)
	go func() {
		for i := 0; i < 10; i++ {
			fmt.Println(<-cha)
		}
		quit <- 0 // 发出结束标志
	}()
	fibonacci1(cha, quit)



	// 一个永远无法结束的 goroutine
func TestWaitGroup(t *testing.T) {
	var wg sync.WaitGroup
	wg.Add(1)
	defer func() {
		println("wait")
		wg.Wait()
	}()
	go func() {
		for true {
			select {
			// 永远无法结束, 因为存在 default 分支, select 变为非阻塞, 会有多次循环,每次for循环, 都会新建一个 after channel, 永远不会 timeout
			// 正确做法是将 time.After(time.Second*2) 提到 for 循环外部, 或者将 default 注释, 变 select 为阻塞式
			case <-time.After(time.Second*2):
				println("timeout")
				wg.Done()
			default:
				
			}
		}
	}()
}

}
```

### 使用回调而不是返回 channel

```go
// 遍历目录, 对每个文件执行某个操作

// 方式 1: 查出所有文件名
// 		问题:可能会阻塞很长时间, 分配大量内存
func ListDirectory(dir string) ([]string, error)
// 方式 2: 返回一个 chan, 元素是文件名
//		问题: 遍历目录可能出现异常, 调用者无法知道获取到的文件是不是全的
// 		问题: 调用者必须持续从通道中读取，直到它被关闭，因为这是调用者知道此通道的是否停止的唯一方式
func ListDirectory(dir string) chan string
// 方式 3: 传递回调函数 (这就是 filepath.WalkDir 函数的工作方式)
func ListDirectory(dir string, fn func(string))


```

### 仅需任意任务完成-利用 buffered channel 实现

```go
// 必须使用带缓存的 channel, 
// 因为如果不带缓存, 此时有个 task 先完成了, 放入数据到 chan, 那么 channel 中的数据只要还没被拿走, , 其他任务goroutine 还是会阻塞在那里不会结束, 这会造成资源的浪费


func MultiTask() string {
	runTask := func(i int) string {
		time.Sleep(time.Second)
		return fmt.Sprintf("result from %d", i)
	}

	ret := make(chan string) // bad
	//ret := make(chan string, 3) // good

	taskNum := 3
	for i := 0; i < taskNum; i++ {
		go func(i int) {
			ret <- runTask(i)
		}(i)
	}
	return <-ret
}

func TestMethod1(t *testing.T) {
	t.Logf("before task run, goroutine count: %v\n", runtime.NumGoroutine())//before task run, goroutine count: 2
	t.Log(MultiTask())//result from 0
	time.Sleep(time.Second) // 做一些其他耗时任务
	t.Logf("after: %v\n", runtime.NumGoroutine())//after: 4, 证明即使有一个 goroutine 完成任务了, 但是剩余 goroutine 还没终结
}

```

### 需要所有任务完成-利用 buffered channel 实现

```go
// 使用 waitGroup 也可以实现, 这里使用 channel 实现
func MultiTask() string {
	runTask := func(i int) string {
		time.Sleep(time.Second)
		return fmt.Sprintf("result from %d", i)
	}

	ret := make(chan string) // bad
	//ret := make(chan string, 3) // good

	taskNum := 3
	for i := 0; i < taskNum; i++ {
		go func(i int) {
			ret <- runTask(i)
		}(i)
	}

	resp := ""
	for i:=0, i<taskNum; i++ {
		resp += <-ret + "\n"
	}

	return resp
}
```

### 利用 close channel 实现广播

```go

// 若发送者关闭了 channel, 所有的接收者在这里会 立刻从阻塞恢复返回, 且v为零值,ok为 false (可以实现广播机制)
// v, ok := <-ch
// 
// close(ch) // 关闭 channel
```

### 对象池

#### 利用 no buffered channel 实现对象池


```go
// 对需要经常使用过的对象进行缓存, 防止回收
// 
// 		

type Obj struct{}
type ObjPool struct {
	bufChan chan *Obj
}
func New(numOfObj int) *ObjPool {
	ret := ObjPool{}
	ret.bufChan = make(chan *Obj, numOfObj)
	for i := 0; i < numOfObj; i++ {
		ret.bufChan <- &Obj{}
	}
	return &ret
}
func (o *ObjPool) GetObj(d time.Duration) (*Obj, error) {
	select {
	case obj:=<-o.bufChan:
		return obj, nil
	case <-time.After(d):
		return nil, errors.New("timeout")
	}
}
func (o ObjPool) ReleaseObj(obj *Obj) error {
	select {
	case o.bufChan <- obj:
		return nil
	default:
		return errors.New("overflow")
	}
}



```

#### sync.pool 对象缓存


```go
// 对象会这样顺序获取
// 1. 首先尝试从当前 processor 的私有对象获取 (协程安全)
// 2. 私有对象不存在, 尝试从 processor 的共享池获取 (协程不安全,会加锁)
// 3. 如果共享池空的, 尝试去其他 processor 共享池获取
// 4. 若所有子池都是空的, 调用用户指定的 New 函数返回新对象

// 特点:
// - 无法当做对象池用, 因为 gc 会清除 缓存的对象, 所以对象的缓存有效期是下一次 gc 之前 (可使用 runtime.GC() 触发 gc 来验证)
// - sync.Pool 是可伸缩的，高负载时会动态扩容，存放在池中的对象如果不活跃了会被自动清理, 其大小仅受限于内存的大小
// - 也是并发安全的，


// 使用 场景: 
// - 用于存储那些被分配了但是没有被使用，而未来可能会使用的值。这样就可以不用再次经过内存分配，可直接复用已有对象，减轻 GC 的压力

// 标准库中的例子
// 例如 fmt 和 encoding/json


// 示例:
// bad
type Student struct {
	Name   string
	Age    int32
	Remark [1024]byte
}
var buf, _ = json.Marshal(Student{Name: "Geektutu", Age: 25})
func unmarsh() {
	// 当程序并发度非常高的情况下，短时间内需要创建大量的临时对象。而这些对象是都是分配在堆上的，会给 GC 造成很大压力
	stu := &Student{}
	json.Unmarshal(buf, stu)
}

// good
// 所以最好通过 pool 获取
var studentPool = sync.Pool{
    New: func() interface{} { 
        return new(Student) 
    },
}
stu := studentPool.Get().(*Student)
json.Unmarshal(buf, stu)
// 对象使用完毕后，返回对象池
studentPool.Put(stu)
```

### 优雅关闭 channel

```go
/*

情形一：M个接收者和一个发送者，发送者通过关闭用来传输数据的通道来传递发送结束信号。
情形二：一个接收者和N个发送者，此唯一接收者通过关闭一个额外的信号通道来通知发送者不要再发送数据了。
情形三：M个接收者和N个发送者，它们中的任何协程都可以让一个中间调解协程帮忙发出停止数据传送的信号。

或者:
使用 sync.Once 或互斥锁(sync.Mutex)确保 channel 只被关闭一次。
// 
type MyChannel struct {
	C    chan T
	once sync.Once
}
func NewMyChannel() *MyChannel {
	return &MyChannel{C: make(chan T)}
}
func (mc *MyChannel) SafeClose() {
	mc.once.Do(func() {
		close(mc.C)
	})
}
*/
```

## goroutine


### goroutine原理 

#### 如何理解协程

[相关面试题](https://yushuangqi.com/blog/2017/golang-mian-shi-ti-da-an-yujie-xi.html?from=groupmessage&isappinstalled=0)

https://www.cnblogs.com/wdliu/p/9272220.html

每个 system thread 对应一个 golang 实现的协程处理器 processor, processor 会随机在关联的协程队列里挑选协程执行 (如果processor 一直在执行某个 goroutine, 有个守护线程会对每个 processor 完成的协程的数量进行记录, 一旦发现一直没变化, 会...)


多协程可以有效利用单核心计算，避免过多的 IO 等待 , 因为 io 等待时, 这个单核cpu可以去运行其他协程;
多进程（线程）可以有效利用多核心计算，避免单核负载过高，多个线程可以使用不同的 cpu

 协程其调度过程类似 cpu 对于系统线程的调度, 只不过调度人从 CPU 换为了程序员, 所以协程也称为用户态线程


举个不恰当的例子，你是个打工人，你每天工作 8 小时，要做的事情有编译程序 A 、编译程序 B 、帮老板端茶倒水、收发邮件。

你相当于一个线程（或进程），老板交给你的工作相当于系统分配线程的任务。

而协程就是，你自己怎么去更高效完成自己的任务。如果没有协程，就相当于“编译 A->编译 B->帮老板端茶倒水->收发邮件”，而协程就相当于“编译 A 开始->跑去给老板倒水->收发邮件->编译 B 开始->编译 A 结束->编译 B 结束”，可以节省你大量你坐在电脑前但是没有实际工作的时间去做其他事情。（对应协程中就是，比如遇到 HTTP API 请求，需要 0.5 秒，可以让这个进程继续先干别的，请求后回来继续当前处理完 HTTP API 请求的上下文）。

#### 和线程对比


和线程的异同：

- 创建时默认的 stack 大小:
  - 协程初始内存占用远小于线程, 2k 
  - java thread 为 1M

- 和操作系统线程对应关系:
  - java thread 是 1:1
  - 协程是 m:n

- 线程进程都是同步机制，而协程则是异步

- 协程能保留上一次调用时的状态，每次过程重入时，就相当于进入上一次调用的状态， 所以上下文的切换非常快

- 多个线程相对独立，有自己的上下文，`切换受系统控制`；而协程也相对独立，有自己的上下文，但是`其切换由程序员手动控制`，如: 若从当前协程切换到其他协程则由当前协程来控制。因此，没有线程切换的开销

- 协程不需要多线程的锁机制，因为只有一个线程，也不存在同时写变量冲突，在协程中控制共享资源不加锁，只需要判断状态就好了


因为协程是一个线程执行，那怎么利用多核CPU呢？最简单的方法是多进程+协程，既充分利用多核，又充分发挥协程的高效率，可获得极高的性能

### 协程在内存层面的实现

协程是可以被暂停/恢复的函数, 所以暂停时需要将函数上下文(在函数栈区)复制一份保存到一个安全的地方 (堆)

或者进一步, 省掉复制的步骤, 为协程分配空间时, 直接在堆中分配


### goroutine基本使用

```go

//Goroutines
//go routine 轻量级的thread, 十几个goroutine可能体现在底层就是五六个线程
//Go语言内部帮你实现了这些goroutine之间的内存共享 // 也就是说 goroutine运行在相同的地址空间
// 语法: go f(x, y, z)
func goroutines() {
	say := func(s string) {
		for i := 0; i < 5; i++ {
			time.Sleep(100 * time.Millisecond)
			fmt.Println(s)
		}
	}

	go say("world")
	say("hello")

	/* runtime包中有几个处理goroutine的函数:
	   Goexit

	   退出当前执行的goroutine，但是defer函数还会继续调用

	   Gosched

	   让出当前goroutine的执行权限，调度器安排其他等待的任务运行，并在下次某个时候从该位置恢复执行。

	   NumCPU

	   返回 CPU 核数量

	   NumGoroutine

	   返回正在执行和排队的任务总数

	   GOMAXPROCS

	   用来设置可以并行计算的CPU核数的最大值，并返回之前的值。

	*/
}

```

### goroutine 捕获外部变量

```go

func main() {
	// 限制单核
	runtime.GOMAXPROCS(1)
	wg := sync.WaitGroup{}
	wg.Add(20)
	for i := 0; i < 10; i++ {
		go func() {
			//golang 中匿名函数捕获外部变量捕获的是"引用"
			fmt.Println("A: ", i) //i打印出来是最终值 10,
			wg.Done()
		}()
	}
	for i := 0; i < 10; i++ {
		go func(i int) {
			fmt.Println("B: ", i) // 通过参数传递进来, 值拷贝
			wg.Done()
		}(i)
	}
	fmt.Println("C")
	wg.Wait()
}
/*
B:  9
A:  10
A:  10
A:  10
A:  10
A:  10
A:  10
A:  10
A:  10
A:  10
A:  10
B:  0
B:  1
B:  2
B:  3
B:  4
B:  5
B:  6
B:  7
B:  8
*/


func main() {
	var a int = 10
	wg := sync.WaitGroup{}
	wg.Add(1)
	go func() {
		fmt.Printf("&a = %v\n", &a)
		wg.Done()
	}()

	fmt.Printf("&a = %v\n", &a)
	wg.Wait()
}
// 地址相同
/*
&a = 0xc000126010
&a = 0xc000126010
*/


func main() {
	runtime.GOMAXPROCS(1)
	wg := sync.WaitGroup{}
	wg.Add(20)
	for i := 0; i < 10; i++ {
		go func() {
			fmt.Println("A: ", i)
			wg.Done()
		}()
		
		runtime.Gosched()
	}
	for i := 0; i < 10; i++ {
		go func(i int) {
			fmt.Println("B: ", i)
			wg.Done()
		}(i)
	}
	fmt.Println("C")
	wg.Wait()
}
//因为, runtime.Gosched() 主动让出了CPU时间片给刚刚创建的goroutine
/*
A:  0
A:  1
A:  2
A:  3
A:  4
A:  5
A:  6
A:  7
A:  8
A:  9
hello
B:  9
B:  0
B:  1
B:  2
B:  3
B:  4
B:  5
B:  6
B:  7
B:  8
*/
```


### 使用select 处理超时

```go
//
	//// 使用 select  处理 goroutine 超时
	//
	ch1 := make(chan int)
	ch2 := make(chan bool)
	go func() {
		for {
			select {
			case v := <-ch1:
				println(v)

			case <-time.After(2 * time.Second): // 等待 2s后执行
				//time.After(2 * time.Second) 返回一个channel, 等待2s 后塞入数据
				println("timeout")
				ch2 <- true
				break
			}
		}
	}()
	<-ch2 // block until 2s later
```



### 优雅退出 goroutine

#### 通过全局变量 waitGroup

```go

// 通过全局变量

//等待组, 类似java 的 countdownLunch
var wg sync.WaitGroup

func main() {
	fmt.Println("start")

	// 设置等待倒数的任务数量
	wg.Add(1)

	go work()
	time.Sleep(time.Second * 3)
	exit = true

	wg.Wait()

	fmt.Println("over")
}

//控制是否退出
var exit bool

func work() {
	// 任务结束需要给 wg 一个结束标志
	defer wg.Done()
	for true {
		fmt.Println("working...")
		time.Sleep(time.Second)
		if exit {
			break
		}
	}
}

```


#### 通过 channel 的方式



```go

// 通过 channel

//等待组, 类似java 的 countdownLunch
var wg sync.WaitGroup

func main() {
	// 更好的方式是 make(chan struct{}, 1) // 不占空间
	var ch = make(chan bool, 1)
			//建议创建有缓冲区的 channel, 防止父 goroutine 结束造成子 goroutine 阻塞在 channel 发送上

	fmt.Println("start")

	wg.Add(1)

	go work(ch)
	time.Sleep(time.Second * 3)
	ch <- true

	wg.Wait()

	fmt.Println("over")
}

func work(ch <-chan bool) {
	defer wg.Done()

LABEL:
	for true {
		select {
		case <-ch:
			//do not use "break", "break" can only break "select", cannot break "for"
			//return
			
			// or use break标签
			//return
			break LABEL
		default:
			fmt.Println("working...")
			time.Sleep(time.Second)
		}

	}
}

```


#### 通过 context 官方推荐

官方帮我们创建了channel: make(chan struct{}), 空 struct 仅仅是一个标识, 输入进 channel 时, 传 struct{}{}

```go
// 通过 context


//等待组, 类似java 的 countdownLunch
var wg sync.WaitGroup

func main() {
	con, cancel := context.WithCancel(context.Background())

	fmt.Println("start")

	wg.Add(1)

	go work(con)

	time.Sleep(time.Second * 3)
	cancel()

	wg.Wait()

	fmt.Println("over")
}

func work(con context.Context) {
	defer wg.Done()

LABEL:
	for true {
		fmt.Println("working...")
		time.Sleep(time.Second)

		select {
		case <-con.Done():
			break LABEL
		default:
		}

	}
}


```

### 限制并发数量

https://github.com/Jeffail/tunny
https://github.com/panjf2000/ants

```go
func main() {
	// sync.WaitGroup 并不是必须的，例如 http 服务, 这里只是为了让 main 不要退出
	var wg sync.WaitGroup
	// 保证并发任务最多为 3 , 也就是实现协程池的效果
	ch := make(chan struct{}, 3)
	for i := 0; i < 10; i++ {
		ch <- struct{}{} // 若缓存区满，则阻塞
		wg.Add(1)
		go func(i int) {
			defer wg.Done()
			log.Println(i)
			time.Sleep(time.Second)
			<-ch
		}(i)
	}
	wg.Wait()
}
```

### 案例-分段执行任务的退出

```go
// 将任务拆分为多段，只检测第一段是否超时，若没有超时，后续任务继续执行，超时则终止
// (好处: 超时后即时退出，避免 goroutine 无用的执行过多，浪费资源)

func do2phases(phase1, done chan bool) {
	time.Sleep(time.Second) // 第 1 段
	select {
	case phase1 <- true:
	default:
		return
	}
	time.Sleep(time.Second) // 第 2 段
	done <- true
}

func timeoutFirstPhase() error {
	phase1 := make(chan bool)
	done := make(chan bool)
	go do2phases(phase1, done)
	select {
	case <-phase1:
		<-done
		fmt.Println("done")
		return nil
	case <-time.After(time.Millisecond):
		return fmt.Errorf("timeout")
	}
}

func Test2phasesTimeout(t *testing.T) {
	for i := 0; i < 1000; i++ {
		timeoutFirstPhase()
	}
	time.Sleep(time.Second * 3)
	t.Log(runtime.NumGoroutine())
}
```

## 锁 共享内存下的并发控制


### Mutex 互斥锁 

```go

//
///////////////////////////////////////////
//
// sync.Mutex ---------- 加锁
//
// 实现 goroutine 互斥, 有两个方法: Lock(), Unlock()
//sync.Mutex一旦被锁住，其它的Lock()操作就无法再获取它的锁，只有通过Unlock()释放锁之后才能通过Lock()继续获取锁。
// SafeCounter is safe to use concurrently.
type SafeCounter struct {
	v   map[string]int
	mux sync.Mutex
}

// Inc increments the counter for the given key.
func (c *SafeCounter) Inc(key string) {
	c.mux.Lock() // 开始锁定
	// Lock so only one goroutine at a time can access the map c.v.
	c.v[key]++
	c.mux.Unlock() // 释放锁
}

// Value returns the current value of the counter for the given key.
func (c *SafeCounter) Value(key string) int {
	c.mux.Lock() // 开始锁定
	// Lock so only one goroutine at a time can access the map c.v.
	defer c.mux.Unlock() // 释放锁
	return c.v[key]
}

func syncMutexDemo() {
	c := SafeCounter{v: make(map[string]int)} // mux 无需初始化
	for i := 0; i < 1000; i++ {
		go c.Inc("somekey")
	}
	time.Sleep(time.Second)
	fmt.Println(c.Value("somekey"))
}

```

### 锁的公平性

```go
/*
在正常状态下，所有等待锁的 goroutine 按照FIFO顺序等待, 如果一个等待的 goroutine 超过 1ms 没有获取锁，那么它将会把锁转变为饥饿模式

在饥饿模式下，锁的所有权将从 unlock 的 goroutine 直接交给交给等待队列中的第一个。新来的 goroutine 将不会尝试去获得锁

如果一个等待的 goroutine 获取了锁，并且满足一以下其中的任何一个条件：(1)它是队列中的最后一个；(2)它等待的时候小于1ms。它会将锁的状态转换为正常状态
*/
```

### RWMutex读写锁

```go

///////////////////////////////////////////
//读写锁
// 解决读多写少时的性能问题
//
//RWMutex是基于Mutex的，在Mutex的基础之上增加了读、写的信号量，并使用了类似引用计数的读锁数量
// 可以同时申请多个读锁
// 有读锁时申请写锁将阻塞，有写锁时申请读锁将阻塞
// 只要有写锁，后续申请读锁和写锁都将阻塞
//
//func (rw *RWMutex) Lock()
// func (rw *RWMutex) Unlock() //Lock()和Unlock()用于申请和释放写锁, 如果不存在写锁，则Unlock()引发panic
//
// func (rw *RWMutex) RLock()
// func (rw *RWMutex) RUnlock() // RLock()和RUnlock()用于申请和释放读锁  // 一次RUnlock()操作只是对读锁数量减1，即减少一次读锁的引用计数, 如果不存在读锁，则RUnlock()引发panic
//
// func (rw *RWMutex) RLocker() Locker  // RLocker()用于返回一个实现了Lock()和Unlock()方法的Locker接口


```

### sync.Once只允许执行一次

```go
////////////////////////////////////
//
//sync.Once 执行一次
// 作用与包的 init 函数类似, 但是更安全方便, 可以在代码的任意位置初始化和调用，因此可以延迟到使用时再执行，并发场景下是线程安全的。
//
// 使用:
// var once sync.Once
		// once.Do(fn1)// fn1执行一次
		// once.Do(fn1) // 再 do 一次, 不会执行
/*
原理实现: 
	- 有个标志来判断变量是否已初始化过, 
	
		为什么将 done 置为 Once 的第一个字段：done 在热路径中，done 放在第一个字段，能够减少 CPU 指令

		为什么放在第一个字段就能够减少指令呢？因为结构体第一个字段的地址和结构体的指针是相同的，如果是第一个字段，直接对结构体的指针解引用即可。如果是其他的字段，除了结构体指针外，还需要计算与第一个值的偏移(calculate offset)

	- 需要互斥锁来实现
*/
// 实现单例模式
func TestSingle(t *testing.T) {
	type Single struct {
	}

	var once sync.Once
	f := func() *Single {
		var ret *Single
		once.Do(func() {
			println("create")
			ret = &Single{}
		})
		return ret
	}

	for i := 0; i < 5; i++ {
		single := f()
		fmt.Println(single)
	}
	time.Sleep(time.Second)
}
/*
create
&{}
<nil>
<nil>
<nil>
<nil>

*/


// 案例: 读取全局配置文件
type Config struct {
	Server string
	Port   int64
}

var (
	once   sync.Once
	config *Config
)

func ReadConfig() *Config {
	once.Do(func() {
		var err error
		config = &Config{Server: os.Getenv("TT_SERVER_URL")}
		config.Port, err = strconv.ParseInt(os.Getenv("TT_PORT"), 10, 0)
		if err != nil {
			config.Port = 8080 // default port
        }
        log.Println("init config")
	})
	return config
}
```

### sync.Cond 多个观察者等待某个任务完成 广播

```go
/*
作用: 当共享资源的状态发生变化的时候，它可以用来通知被互斥锁阻塞的多个 goroutine

	sync.Cond 经常用在多个 goroutine 等待，一个 goroutine 通知（事件发生）的场景。如果是一个通知，一个等待，使用互斥锁或 channel 就能搞定了

实现:基于互斥锁/读写锁

// 如果自己实现: 需要有个全局的变量来标志第一个协程数据是否接受完毕，剩下的协程，反复检查该变量的值，直到满足要求。或者创建多个 channel，每个协程阻塞在一个 channel 上，由接收数据的协程在数据接收完毕后，逐个通知


func NewCond(l Locker) *Cond  创建 Cond 实例
	每个 Cond 实例都会关联一个锁 L（互斥锁 *Mutex，或读写锁 *RWMutex），修改条件或者调用 Wait 方法时，需要手动加锁
Broadcast 广播唤醒所有等待这个条件变量 c 的 goroutine，无需锁保护
Signal 只唤醒任意 1 个等待条件变量 c 的 goroutine，无需锁保护
Wait 等待, 会自动释放锁 c.L，并挂起调用者所在的 goroutine
	如果其他协程调用了 Signal 或 Broadcast 唤醒了该协程，那么 Wait 方法在结束阻塞时，会重新给 c.L 加锁，并且继续执行 Wait 后面的代码
	
对条件的检查，使用了 for !condition() 而非 if
	是因为当前协程被唤醒时，条件不一定符合要求，需要再次 Wait 等待下次被唤醒。为了保险起见，使用 for 能够确保条件符合要求后，再执行后续的代码。
*/


var done = false //即互斥锁需要保护的条件变量

func read(name string, c *sync.Cond) {
	c.L.Lock() // 调用 wait 需要 手动加锁
	for !done {
		c.Wait()
	}
	log.Println(name, "starts reading")
	c.L.Unlock()
}

func write(name string, c *sync.Cond) {
	log.Println(name, "starts writing")
	time.Sleep(time.Second)
	c.L.Lock() // 修改条件, 需要手动加锁 
	done = true
	c.L.Unlock()
	log.Println(name, "wakes all")
	c.Broadcast()
}

func main() {
	cond := sync.NewCond(&sync.Mutex{})

	go read("reader1", cond)
	go read("reader2", cond)
	go read("reader3", cond)
	write("writer", cond)

	time.Sleep(time.Second * 3)
}
```

### waitGroup 等待多个任务全部必须完成

```go
waitGroup 作为方法形参时, 必须是指针, 否则如果形参只是普通变量类型, 传递给方法形参的会是值拷贝, 是不同 等待组

所以只能作为 全局变量 或者  指针方法形参 使用

wg.Add(1) 必须要在 goroutine 外部 (也就是main goroutine 上调用), 不能在goroutine内部调用, 否则 main goroutine 即使调用 wg.wait() 也不会阻塞

```

### 锁相关案例

#### 单例模式

此外, 也能使用 Once 实现

```go

// 在 singleton 包这么写
var (
	config      *Config
	configMutex sync.Mutex
)

type Config struct {
	Debug bool   `envconfig:"debug"`
	DBURL string `envconfig:"db_url"`
}

func GetConfig() *Config {
	if config != nil {
		return config
	}

	configMutex.Lock()
	defer configMutex.Unlock()

	// double check
	if config != nil {
		return config
	}

	config = &Config{}
	envconfig.Process("APP_NAME", config)

	return config
}
// ------------------------------------------------
// 在 main 中初始化
func main() {
    // init config
	_ = singleton.GetConfig()

}
// ------------------------------------------------
// 在别的包就可以直接使用了
var (
	config = singleton.GetConfig()
)

func Haha() {
    println(config.DBURL)
}
```

## atomic 原子操作

```go

// 原子操作是Go语言提供的方法它在用户态就可以完成，因此性能比加锁操作更好


// 读取
func LoadInt32(addr int32) (val int32)

// 写入
func StoreInt32(addr *int32, val int32)

// 	加法
func AddInt32(addr *int32, delta int32) (new int32)

// 交换
func SwapInt32(addr *int32, new int32) (old int32)

// 比较&交换
func CompareAndSwapInt32(addr *int32, old, new int32) (swapped bool)
```

## 反射 reflect

### 反射基本使用

#### 获取函数名称

```go
func getFunctionName(i interface{}) string {
  return runtime.FuncForPC(reflect.ValueOf(i).Pointer()).Name()
}
```

#### 实现类型断言

```go

func CheckType (v interface{}) {
	t : = reflect.TypeOf (v) // 得到 reflect 包内定义的类型
	switch t.Kind(){
	case reflect.Float32, reflect.Float64:
		fmt.Println("Float")
	case reflect.Int, reflect.Int32, reflect.Int64
		fmt.Println("Integer")
	default:
		fmt.Printin("Unknown", t)
	} 
}

func TestTypeAndValue (t *testing. T) {
	var fint64 = 10
	t.Log(reflect.Type0f(f), reflect.ValueOf (f))
	t.Log(reflect.ValueOf (f) .Type() )
}

```

#### 为任何 struct 设置值

```go

// 
func TestReflect(t *testing.T) {
	f:= func(target interface{}, props map[string]interface{}) error {
		// terget 必须为struct 或者指向 struct 的指针
		if reflect.TypeOf(target).Kind() != reflect.Ptr {
			// 拿到 target 值的实际类型
			if reflect.TypeOf(target).Elem().Kind() != reflect.Struct {
				return errors.New("1st param should be a struct or a ptr pointing to a struct")
			}
		}

		// 遍历 props
		for k, v := range props {
			// 若 k 在 target 中不存在, continue
			field, fieldOk := reflect.ValueOf(target).Elem().Type().FieldByName(k)
			if !fieldOk {
				continue
			}
			//若 props 中的属性类型 能和 field 匹配上, 则设置值
			if field.Type == reflect.TypeOf(v) {
				reflect.ValueOf(target).Elem().FieldByName(k).Set(reflect.ValueOf(v))
			}

		}
		return nil
	}

	type Aa struct {
		Name string // 必须导出
		Age int
	}
	var aa = new(Aa)
	f(aa, map[string]interface{}{
		"Name": "aa",
		"Age":  11,
	})
	fmt.Println(aa)
}
```

#### 从环境变量读取配置

```go
// 如果使用硬编码，Config 结构发生改变，例如修改 json 对应的字段，删除或新增了一个配置项，这块逻辑也需要发生改变
// 使用反射就方便了
func readConfig() *Config {
	// read from xxx.json，省略
	config := Config{}
	typ := reflect.TypeOf(config)
	value := reflect.Indirect(reflect.ValueOf(&config))
	for i := 0; i < typ.NumField(); i++ {
		f := typ.Field(i)
		if v, ok := f.Tag.Lookup("json"); ok {
			key := fmt.Sprintf("CONFIG_%s", strings.ReplaceAll(strings.ToUpper(v), "-", "_"))
			if env, exist := os.LookupEnv(key); exist {
				value.FieldByName(f.Name).Set(reflect.ValueOf(env))
			}
		}
	}
	return &config
}

func main() {
	os.Setenv("CONFIG_SERVER_NAME", "global_server")
	os.Setenv("CONFIG_SERVER_IP", "10.0.0.1")
	os.Setenv("CONFIG_SERVER_URL", "geektutu.com")
	c := readConfig()
	fmt.Printf("%+v", c)
}
```

### 反射性能优化

```go
// 创建对象
// 通过反射创建对象的耗时约为 new 的 1.5 倍，相差不是特别大
func BenchmarkNew(b *testing.B) {
	var config *Config
	for i := 0; i < b.N; i++ {
		config = new(Config)
	}
	_ = config
}
func BenchmarkReflectNew(b *testing.B) {
	var config *Config
	typ := reflect.TypeOf(Config{})
	b.ResetTimer()
	for i := 0; i < b.N; i++ {
		config, _ = reflect.New(typ).Interface().(*Config)
	}
	_ = config
}

// -----------------------------------

// 修改字段的值
// 一种是 FieldByName，另一种是 Field(按照下标)
// 		FieldByName 的性能相比 Field 劣化 10 倍
// 
// 底层实现上, FieldByName 中使用 for 循环，逐个字段查找，字段名匹配时返回。也就是说，在反射的内部，字段是按顺序存储的，因此按照下标访问查询效率为 O(1)，而按照 Name 访问，则需要遍历所有字段，查询效率为 O(N)。结构体所包含的字段(包括方法)越多，那么两者之间的效率差距则越大。
// 
func BenchmarkSet(b *testing.B) {

	config := new(Config)
	b.ResetTimer()
	for i := 0; i < b.N; i++ {
		config.Name = "name"
		config.IP = "ip"
		config.URL = "url"
		config.Timeout = "timeout"
	}
}

func BenchmarkReflect_FieldSet(b *testing.B) {
	typ := reflect.TypeOf(Config{})
	ins := reflect.New(typ).Elem()
	b.ResetTimer()
	for i := 0; i < b.N; i++ {
		ins.Field(0).SetString("name")
		ins.Field(1).SetString("ip")
		ins.Field(2).SetString("url")
		ins.Field(3).SetString("timeout")
	}
}

func BenchmarkReflect_FieldByNameSet(b *testing.B) {
	typ := reflect.TypeOf(Config{})
	ins := reflect.New(typ).Elem()
	b.ResetTimer()
	for i := 0; i < b.N; i++ {
		ins.FieldByName("Name").SetString("name")
		ins.FieldByName("IP").SetString("ip")
		ins.FieldByName("URL").SetString("url")
		ins.FieldByName("Timeout").SetString("timeout")
	}
}


// 如果确实需要使用 FiledByName, 可以可以利用字典将 Name 和 Index 的映射缓存起来
func BenchmarkReflect_FieldByNameCacheSet(b *testing.B) {
	typ := reflect.TypeOf(Config{})
	cache := make(map[string]int)
	for i := 0; i < typ.NumField(); i++ {
		cache[typ.Field(i).Name] = i
	}
	ins := reflect.New(typ).Elem()
	b.ResetTimer()
	for i := 0; i < b.N; i++ {
		ins.Field(cache["Name"]).SetString("name")
		ins.Field(cache["IP"]).SetString("ip")
		ins.Field(cache["URL"]).SetString("url")
		ins.Field(cache["Timeout"]).SetString("timeout")
	}
}
```

### 反射实现 filter map reduce

```go
// 实现 map

// 有两个版本的函数，一个是返回一个全新的数组 – Transform()，一个是“就地完成” – TransformInPlace()
func Transform(slice, function interface{}) interface{} {
  return transform(slice, function, false)
}

func TransformInPlace(slice, function interface{}) interface{} {
  return transform(slice, function, true)
}

func transform(slice, function interface{}, inPlace bool) interface{} {
 
  //check the <code data-enlighter-language="raw" class="EnlighterJSRAW">slice</code> type is Slice
  sliceInType := reflect.ValueOf(slice)
//   用 Kind() 方法检查了数据类型是不是 Slice，函数类型是不是Func
  if sliceInType.Kind() != reflect.Slice {
    panic("transform: not slice")
  }

  //check the function signature
  fn := reflect.ValueOf(function)
  elemType := sliceInType.Type().Elem()
  if !verifyFuncSignature(fn, elemType, nil) {
    panic("trasform: function must be of type func(" + sliceInType.Type().Elem().String() + ") outputElemType")
  }

  sliceOutType := sliceInType
  if !inPlace {
	//   需要新生成一个Slice，会使用 reflect.MakeSlice() 来完成
    sliceOutType = reflect.MakeSlice(reflect.SliceOf(fn.Type().Out(0)), sliceInType.Len(), sliceInType.Len())
  }
  for i := 0; i < sliceInType.Len(); i++ {
    sliceOutType.Index(i).Set(fn.Call([]reflect.Value{sliceInType.Index(i)})[0])
  }
  return sliceOutType.Interface()

}

func verifyFuncSignature(fn reflect.Value, types ...reflect.Type) bool {

  //Check it is a funciton
  if fn.Kind() != reflect.Func {
    return false
  }
  // NumIn() - returns a function type's input parameter count.
  // NumOut() - returns a function type's output parameter count.
  if (fn.Type().NumIn() != len(types)-1) || (fn.Type().NumOut() != 1) {
    return false
  }
  // In() - returns the type of a function type's i'th input parameter.
  for i := 0; i < len(types)-1; i++ {
    if fn.Type().In(i) != types[i] {
      return false
    }
  }
  // Out() - returns the type of a function type's i'th output parameter.
  outType := types[len(types)-1]
  if outType != nil && fn.Type().Out(0) != outType {
    return false
  }
  return true
}


// =============

// reduce

func Reduce(slice, pairFunc, zero interface{}) interface{} {
  sliceInType := reflect.ValueOf(slice)
  if sliceInType.Kind() != reflect.Slice {
    panic("reduce: wrong type, not slice")
  }

  len := sliceInType.Len()
  if len == 0 {
    return zero
  } else if len == 1 {
    return sliceInType.Index(0)
  }

  elemType := sliceInType.Type().Elem()
  fn := reflect.ValueOf(pairFunc)
  if !verifyFuncSignature(fn, elemType, elemType, elemType) {
    t := elemType.String()
    panic("reduce: function must be of type func(" + t + ", " + t + ") " + t)
  }

  var ins [2]reflect.Value
  ins[0] = sliceInType.Index(0)
  ins[1] = sliceInType.Index(1)
  out := fn.Call(ins[:])[0]

  for i := 2; i < len; i++ {
    ins[0] = out
    ins[1] = sliceInType.Index(i)
    out = fn.Call(ins[:])[0]
  }
  return out.Interface()
}



// ===========

// filter

func Filter(slice, function interface{}) interface{} {
  result, _ := filter(slice, function, false)
  return result
}

func FilterInPlace(slicePtr, function interface{}) {
  in := reflect.ValueOf(slicePtr)
  if in.Kind() != reflect.Ptr {
    panic("FilterInPlace: wrong type, " +
      "not a pointer to slice")
  }
  _, n := filter(in.Elem().Interface(), function, true)
  in.Elem().SetLen(n)
}

var boolType = reflect.ValueOf(true).Type()

func filter(slice, function interface{}, inPlace bool) (interface{}, int) {

  sliceInType := reflect.ValueOf(slice)
  if sliceInType.Kind() != reflect.Slice {
    panic("filter: wrong type, not a slice")
  }

  fn := reflect.ValueOf(function)
  elemType := sliceInType.Type().Elem()
  if !verifyFuncSignature(fn, elemType, boolType) {
    panic("filter: function must be of type func(" + elemType.String() + ") bool")
  }

  var which []int
  for i := 0; i < sliceInType.Len(); i++ {
    if fn.Call([]reflect.Value{sliceInType.Index(i)})[0].Bool() {
      which = append(which, i)
    }
  }

  out := sliceInType

  if !inPlace {
    out = reflect.MakeSlice(sliceInType.Type(), len(which), len(which))
  }
  for i := range which {
    out.Index(i).Set(sliceInType.Index(which[i]))
  }

  return out.Interface(), len(which)
}
```

## 泛型

### 泛型使用

```go

```

### go generation

https://coolshell.cn/articles/21179.html

## unsafe 不安全编程

```go

func TestUnsage(t *testing.T) {
	type MyInt int
	slice := []int{1, 2, 3}
	// unsafe.Pointer 接收一个地址, 返回一个指针
	ints := *(*[]MyInt)(unsafe.Pointer(&slice))
	fmt.Println(ints)
}

```

## http 服务

### http 包

基本使用:

```go

func TestHttp(t *testing.T) {
	/*
	handleFunc 接收一个 pattern 和 Handler, 
			Handler 类型如下, 
			type Handler interface {
				ServeHTTP(ResponseWriter, *Request)
			}
			HandlerFunc 已经实现了这个接口
	
	*/
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		fmt.Fprint(w, "hello.")
	})
	http.HandleFunc("/time", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte(fmt.Sprintf("time: %s", time.Now())))
	})
	http.ListenAndServe(":8080", nil) // nil 表示使用默认路由规则, 若末尾有 /, 表示严格匹配, 若没有 / 会从坐往右匹配, 匹配上就返回



	// 可以通过Server结构体对服务器进行更详细的配置
	 s := &http.Server{
     Addr:           ":8082",
     Handler:        myHandler, // 开源包的 router 就是从这里传入
     ReadTimeout:    10 * time.Second,
     WriteTimeout:   10 * time.Second,
     MaxHeaderBytes: 1 << 20,
 }
 s.ListenAndServe(":8080", nil)
}
```

### 自定义复用器

虽然默认的多路复用器很好用，但仍然不推荐使用，因为它是一个全局变量，所有的代码都可以修改它。有些第三方库中可能与默认复用器产生冲突。所以推荐的做法是自定义

```go
func main() {
     mux := http.NewServeMux()
     mux.HandleFunc("/", newservemux)
     mux.HandleFunc("/happy", newservemuxhappy)
     mux.HandleFunc("/bad", newservemuxbad)
     s := &http.Server{
         Addr:    ":8080",
         Handler: mux,
     }
 ​
     s.ListenAndServe()
 }
```

ServeMux的一个缺陷是无法使用变量实现URL模式匹配。而HttpRouter可以，HttpRouter是一个高性能的第三方HTTP路由包，弥补了net/http包中的路由不足问题


### 自定义中间件

https://segmentfault.com/a/1190000040343360

### 获取 ip 地址

```go
dial, err := net.Dial("udp", "8.8.8.8:80")
if err != nil {
	log.Fatal(err)
}
defer dial.Close()

addr := dial.LocalAddr()
fmt.Println(addr)
udpAddr := addr.(*net.UDPAddr)
fmt.Println(udpAddr.IP.String())

println("------------------------")

addrs, _ := net.InterfaceAddrs()
for _, addr := range addrs {
	ip, ok := addr.(*net.IPNet)
	if !ok {
		continue
	}
	if ip.IP.IsLoopback() {
		continue
	}
	if ip.IP.IsGlobalUnicast() {
		continue
	}
	println(ip.IP.String())
}
```

### 更好用的路由 router

https://github.com/julienschmidt/httprouter

## json 包

### json基本使用

```go
// encoding/json
// 不推荐了 , 反射性能低, 推荐 Easyjson, 或者 https://github.com/json-iterator/go
type Person struct {
	Name string `json:"name"`
	Age int `json:"age"`
}

func TestReadLog(t *testing.T) {
	jsonStr := `{
		"name": "hel",
		"age": 11
	}`
	p := new(Person)
	err := json.Unmarshal([]byte(jsonStr), p)
	if err != nil {
		fmt.Printf(">>> error of unmarshall json str: %v, err: %v\n", jsonStr, err)
		return
	}
	fmt.Printf(">>> Person: %#v\n", p)

}


```

### 临时忽略json 字段

```go
json.Marshal(struct {
    *User
	// 临时忽略掉空Password字段,可以用omitempty
	// 不会忽略某个字段，而是忽略空的字段，当字段的值为空值的时候，它不会出现在JSON数据中
	// 如果想临时忽略掉Password字段不管空不空,可以用 - 
    Password bool `json:"password,omitempty"`
}{
    User: user,
})
```

### 临时粘合两个struct

```go
type BlogPost struct {
    URL   string `json:"url"`
    Title string `json:"title"`
}
type Analytics struct {
    Visitors  int `json:"visitors"`
    PageViews int `json:"page_views"`
}
json.Marshal(struct{
    *BlogPost
    *Analytics
}{post, analytics})

```

### 一个json切分成两个struct

```go
json.Unmarshal([]byte(`{
  "url": "attila@attilaolah.eu",
  "title": "Attila's Blog",
  "visitors": 6,
  "page_views": 14
}`), &struct {
  *BlogPost
  *Analytics
}{&post, &analytics})
```

### 用字符串传递数字

```go
type TestObject struct {
    Field1 int    `json:",string"`
}
// {"Field1": "100"} 100会被转为int 

```

### 使用 json的RawMessage


```go
// 如果部分json文档没有标准格式，我们可以把原始的信息用[]byte保存下来。

type TestObject struct {
    Field1 string
    Field2 json.RawMessage // 用来接收 [1,2,3]
} 
var data TestObject
json.Unmarshal([]byte(`{"field1": "hello", "field2": [1,2,3]}`), &data)
should.Equal(` [1,2,3]`, string(data.Field2))

```


## socket 编程

### tcp

#### 粘包问题

```go
// 粘包是指网络通信中，发送方发送的多个数据包在接收方的缓冲区黏在一起，多个数据包首尾相连的现象
/*
原因: (https://studygolang.com/articles/25874)
原因主要是由tcp协议本身造成的

	tcp协议是面向连接，面向流，提供高可靠性服务的, tcp数据包转发使用Nagle算法(Nagle算法是为了提高tcp的传输效率)，当应用层有一个数据包要发送时，Nagle算法并不会立刻发送，而是继续收集要发送的消息，直到收到 server 对上一个包的确认ack时，才会发送数据，此时Nagle算法会将累积收集的多个的数据包形成一个分组，将这个分组一次性转发出去, 形成粘包

	udp协议不会出现粘包，因为udp是无连接，面向消息，提供高效服务的. 无连接意味着当有数据包要发送时，udp会立即发送，数据包不会积压; 因此，udp不会出现粘包，只可能会出现丢包

什么时候需要考虑处理半包和粘包？

	TCP连接是长连接，即一次连接多次发送数据

解决思路:

	- 定长分隔(每个数据包最大为该长度，不足时使用特殊字符填充) ，但是数据不足时会浪费传输资源
	- 使用特定分割字符来分割数据包，但是若要传输的数据中本身就含有分割字符则会出现Bug
	- 在数据包中添加长度字段，弥补了以上两种思路的不足，				[推荐]
*/



```

bad 示例

```go
// server

func serverUp(port int) {
	portStr := strconv.Itoa(port)
	listener, err := net.Listen("tcp", ":"+portStr)
	if err != nil {
		log.Fatal(err)
	}
	defer func() {
		_ = listener.Close()
		log.Println("the server is down")
	}()
	log.Println("the server is up and listening on port: ", portStr)

	for {
		accept, err := listener.Accept()
		if err != nil {
			log.Println("accept client conn failed: ", err)
			continue
		}
		go func() {
			addrClient := accept.RemoteAddr()
			defer func() {
				_ = accept.Close()
				log.Println("client conn closed: ", addrClient)
			}()
			log.Println("client conn established: ", addrClient)

			for {
				var buf [512]byte
				readN, err := accept.Read(buf[:])
				if err == io.EOF {
					//log.Println("read EOF")
					continue
				}
				if err != nil {
					log.Println("read err: ", err)
					break
				}
				log.Println("read msg: ", string(buf[:readN]))
			}

		}()
	}
}
/*
打印:
2021/12/23 23:52:11 read msg:  [这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf][这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf][这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf][这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf][这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf][这是一个完整的数据包, x
2021/12/23 23:52:11 read msg:  sdfsfsfsfsfsdffsfsdf][这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf]

可以看到
- 多个数据包“粘”在了一起
- 一个数据包被“拆”开，形成一个破碎的包
*/


// client
func clientUp(targetPort int) {
	conn, err := net.Dial("tcp", ":"+strconv.Itoa(targetPort))
	if err != nil {
		log.Fatal("the client cannot start, err: ", err)
	}
	defer func() {
		_ = conn.Close()
		log.Println("the client is down")
	}()

	for i := 0; i < 20; i++ {
		_, err := conn.Write([]byte("[这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf]"))
		if err != nil {
			log.Fatal(err)
		}
	}
}
```

#### 解决粘包 scanner

good 示例 (使用 scanner 实现)

```go
// server

func serverUp(port int) {
	listener, err := net.Listen("tcp", ":"+strconv.Itoa(port))
	if err != nil {
		log.Fatalln(err)
	}
	defer func() {
		_ = listener.Close()
		log.Println("the server is down")
	}()
	log.Println("the server is up and listening on port: ", port)

	for {
		accept, err := listener.Accept()
		if err != nil {
			log.Println("accept client conn failed: ", err)
			continue
		}
		go func(accept net.Conn) {
			addr := accept.RemoteAddr()
			log.Println("client conn is established: ", addr)
			defer func() {
				_ = accept.Close()
				log.Println("client conn is closed: ")
			}()

			var buf [512]byte
			for {
				readN, err := accept.Read(buf[:])
				if err == io.EOF {
					continue
				}
				if err != nil {
					log.Println("read from client failed: ", err)
					break
				}

				scanner := bufio.NewScanner(bytes.NewReader(buf[:readN]))
				scanner.Split(func(data []byte, atEOF bool) (advance int, token []byte, err error) {
					// 检查 atEOF 参数 和 数据包头部的四个字节是否 为 0x123456(我们定义的协议的魔数)
					if !atEOF && len(data) > 6 && binary.BigEndian.Uint32(data[:4]) == 0x123456 {
						var l int16
						// 读出 数据包中 实际数据 的长度(大小为 0 ~ 2^16)
						binary.Read(bytes.NewReader(data[4:6]), binary.BigEndian, &l)
						pl := int(l) + 6
						if pl <= len(data) {
							return pl, data[:pl], nil
						}
					}
					return
				})

			}
		}(accept)
	}
}


// client

func clientUp(target int) {
	conn, err := net.DialTimeout("tcp", ":"+strconv.Itoa(target), time.Second*10)
	if err != nil {
		log.Fatalln("connect to server failed: ", err)
	}

	content := []byte("[这是一个完整的数据包, xsdfsfsfsfsfsdffsfsdf]")
	var pack bytes.Buffer

	//往数据包写入魔数, 占位 4 字节
	var magicNum uint32 = 0x12345
	magicNumBytes := make([]byte, 4)
	binary.BigEndian.PutUint32(magicNumBytes, magicNum) // 按照 bigEndian 方式写入字节序列
	pack.Write(magicNumBytes)

	//往数据包写入数据体长度, 占位 2 字节
	bodyLenBytes := make([]byte, 2)
	binary.BigEndian.PutUint16(bodyLenBytes, uint16(len(content)))
	pack.Write(bodyLenBytes)

	//写入实际数据
	pack.Write(content)

	for i := 0; i < 30; i++ {
		_, err := conn.Write(pack.Bytes())
		if err != nil {
			log.Println("write to server failed: ", err)
			break
		}
	}
}
```

#### 解决粘包 自定义编解码

```go
// proto.go

func Encode(msg string) ([]byte, error) {
	pack := new(bytes.Buffer)

	//write the msg header
	err := binary.Write(pack, binary.LittleEndian, int32(len(msg)))
	if err != nil {
		return nil, err
	}

	err = binary.Write(pack, binary.LittleEndian, []byte(msg))
	if err != nil {
		return nil, err
	}
	return pack.Bytes(),nil

}

func Decode(reader *bufio.Reader) (string, error) {
	headerBytes, _ := reader.Peek(4) //  读取前4个字节的数据, 即消息体长度
	var msgLen int32
	err := binary.Read(bytes.NewBuffer(headerBytes), binary.LittleEndian, &msgLen)
	if err != nil {
		return "", err
	}

	//若读取出来的消息总共长度大于实际长度
	if msgLen+4 > int32(reader.Buffered()) {
		return "", err
	}

	// 读取消息体
	pack := make([]byte, int(4+msgLen))
	reader.Read(pack)

	return string(pack[4:]), nil
}


// server

type Server struct {
}

func (s *Server) Up()  {
	listener, _ := net.Listen("tcp", ":30000")
	defer func() {
		_ = listener.Close()
		log.Println("server is down")
	}()

	log.Println("server is up")

	for {
		accept, _ := listener.Accept()


		go func() {
			defer func() {
				_ = accept.Close()
			}()
			log.Println("new conn: ", accept.RemoteAddr())

			reader := bufio.NewReader(accept)
			//var buf [1024]byte
			//for {
			//	offset, err := reader.Read(buf[:])
			//	if err == io.EOF {
			//		break
			//	}
			//	if err != nil {
			//		log.Println("read from client failed, err: ", err)
			//		break
			//	}
			//
			//	log.Println("msg from client: ", string(buf[:offset]))
			//}

			for {
				decode, err := Decode(reader)
				if err == io.EOF {
					break
				}
				if err != nil {
					log.Println("read from client failed, err: ", err)
					break
				}
				log.Println("msg from client: ", decode)
			}
		}()
	}
}


// client

type Client struct {

}

func (c Client) Up() {
	conn, _ := net.Dial("tcp", "127.0.0.1:30000")
	defer conn.Close()
	for i := 0; i < 10; i++ {
		//conn.Write([]byte("hello1, hello2"))
		encode, _ := Encode("hello1, hello2")
		conn.Write(encode)
	}
}
```

### udp

```go
/*
在golang中的UDPConn分为connected和unconnected.
如果*UDPConn是connected,读写方法是Read和Write。
如果*UDPConn是unconnected,读写方法是ReadFromUDP和WriteToUDP（以及ReadFrom和WriteTo)。
DialUDP中的UDPConn为connected是不能调用WriteToUDP发送给某个地址.
ListenUDP中的UDPCon为unconnected,直接可以调用WriteToUDP发送给某个地址.
Go的这种设计和Unix/Linux设计一致,
*/
```

## websocket

https://github.com/joewalnes/websocketd


## Unicode 包

Unicode 是一种字符集(code point), 其他还有 ISO8859-1...

utf8是 Unicode 的存储实现 (转换为字节数组的规则)

```go
// 字符处理函数
判断是否为字母： unicode.IsLetter(v)
判断是否为十进制数字： unicode.IsDigit(v)
判断是否为数字： unicode.IsNumber(v)
判断是否为空白符号： unicode.IsSpace(v)
判断是否为Unicode标点字符 :unicode.IsPunct(v)
```

## time 包

### 定时器

```go

func TestTime(t *testing.T) {
	// 定时闹钟, 获取一个 chan Time, 从当前开始, 过 3s 取一个 time
	for range time.Tick(time.Second*3) {
		println("hello")
	}

	// 或者通过  time.After(xxx)
}


```

### 统计运行时间

```go

// 统计函数执行时间
start := time.Now()
longCalculation()
end := time.Now()
delta := end.Sub(start)

// 或者
defer func(t time.Time) {
	fmt.Printf("--- Time Elapsed (%s): %v ---\n", 
		getFunctionName(f), time.Since(t))
}(time.Now())

```

### 时间初始化

```go
 // func Now() Time
      fmt.Println(time.Now())

      // func Parse(layout, value string) (Time, error)
      time.Parse("2016-01-02 15:04:05", "2020-10-23 12:24:51")

      // func ParseInLocation(layout, value string, loc *Location) (Time, error) (layout已带时区时可直接用Parse)
      time.ParseInLocation("2006-01-02 15:04:05", "2020-10-23 14:06:06", time.Local)

      // func Unix(sec int64, nsec int64) Time
      time.Unix(1e9, 0)

      // func Date(year int, month Month, day, hour, min, sec, nsec int, loc *Location) Time
      time.Date(2018, 1, 2, 15, 30, 10, 0, time.Local)

      // func (t Time) In(loc *Location) Time 当前时间对应指定时区的时间
      loc, _ := time.LoadLocation("America/Los_Angeles")
      fmt.Println(time.Now().In(loc))

      // func (t Time) Local() Time
```

### 时间格式化 时区 加减

```go

// 格式化, 只能使用固定的几个数组, 即 2006 01 02 15 04 05 (0 可以去掉), 若果希望 12 小时制, 15 改成 03
// 
// 接收字符串, 也接收 time 包中也给了一些我们常用的格式
/*
				const (
						ANSIC       = "Mon Jan _2 15:04:05 2006"
						UnixDate    = "Mon Jan _2 15:04:05 MST 2006"
						RubyDate    = "Mon Jan 02 15:04:05 -0700 2006"
						RFC822      = "02 Jan 06 15:04 MST"
						RFC822Z     = "02 Jan 06 15:04 -0700" // RFC822 with numeric zone
						RFC850      = "Monday, 02-Jan-06 15:04:05 MST"
						RFC1123     = "Mon, 02 Jan 2006 15:04:05 MST"
						RFC1123Z    = "Mon, 02 Jan 2006 15:04:05 -0700" // RFC1123 with numeric zone
						RFC3339     = "2006-01-02T15:04:05Z07:00"
						RFC3339Nano = "2006-01-02T15:04:05.999999999Z07:00"
						Kitchen     = "3:04PM"
						// Handy time stamps.
						Stamp      = "Jan _2 15:04:05"
						StampMilli = "Jan _2 15:04:05.000"
						StampMicro = "Jan _2 15:04:05.000000"
						StampNano  = "Jan _2 15:04:05.000000000"
				)     
*/
fmt.println(now.format("2006-01-02 15:04:05"))
fmt.println(now.format("2006-01-02 03:04:05 PM"))
// 精确到毫秒
fmt.println(now.format("2006-01-02 03:04:05.000 PM"))



// 时间转换格式
beforeTimeS := beforeTime.Unix() // 秒时间戳
beforeDate := time.Unix(beforeTimeS, 0).Format("20060102150405") // 固定格式的日期时间戳



// 时区
// 根据字符串即系符合本地时区的时间
locale, err := time.loadLocale("Asia/Shanghai")
t :=time.parseInLocation("2006-01-02 03:04:05 pm", timeStr, locale)
// 时区
	//timeZone, _ := time.LoadLocation(ServerInfo["timezone"])
	timeZone := time.FixedZone("CST", 8*3600) // 东八区



// 前21天
	nowTime := time.Now().In(timeZone)
	beforeTime := nowTime.AddDate(0, 0, 21)


// Add 时间相加
	now := time.Now()
	// ParseDuration parses a duration string.
	// A duration string is a possibly signed sequence of decimal numbers,
	// each with optional fraction and a unit suffix,
	// such as "300ms", "-1.5h" or "2h45m".
	//  Valid time units are "ns", "us" (or "µs"), "ms", "s", "m", "h".
	// 10分钟前
	m, _ := time.ParseDuration("-1m")
	m1 := now.Add(m)
	fmt.Println(m1)

	// 8个小时前
	h, _ := time.ParseDuration("-1h")
	h1 := now.Add(8 * h)
	fmt.Println(h1)

	// 一天前
	d, _ := time.ParseDuration("-24h")
	d1 := now.Add(d)
	fmt.Println(d1)

	printSplit(50)

	// 10分钟后
	mm, _ := time.ParseDuration("1m")
	mm1 := now.Add(mm)
	fmt.Println(mm1)

	// 8小时后
	hh, _ := time.ParseDuration("1h")
	hh1 := now.Add(hh)
	fmt.Println(hh1)

	// 一天后
	dd, _ := time.ParseDuration("24h")
	dd1 := now.Add(dd)
	fmt.Println(dd1)

```

## math 包

### 随机值

```go
// 随机字符串
func main() {
    fmt.Println(RandString(10))
}

var source = rand.NewSource(time.Now().UnixNano())

const charset = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"

func RandString(length int) string {
    b := make([]byte, length)
    for i := range b {
        b[i] = charset[source.Int63()%int64(len(charset))]
    }
    return string(b)
}



// 或者
rand.Seed(time.Now().UnixNano())
nums := make([]int, 0, n)
for i := 0; i < n; i++ {
	nums = append(nums, rand.Int())
}
```

### 精密计算和 big 包

```
如果对精度没有要求，float32 或者 float64 可以胜任, 返回结果将精确到 15 位，，但如果对精度有严格要求的时候
```

## 数据库操作

```go

```

## runtime包

```go
// 显式的触发 GC
runtime.GC() 
//只在某些罕见的场景下才有用，比如当内存资源不足时, 它会在此函数执行的点上立即释放一大片内存，此时程序可能会有短时的性能下降（因为 GC 进程在执行）



// 获取当前代码执行的位置
func TestLog(t *testing.T) {
	writeLog := func(format string, params ...interface{}) {
		_, file, line, _ := runtime.Caller(1) // skip 决定从哪一层 stack frame 开始记录
												// 0 表示记录最底层, 也就是 writeLog 定义的地方, 这是无效的
												// 1 表示记录第一次调用的地方, 这个才是合适的

		var formatNew strings.Builder
		formatNew.WriteString("%v:%d")
		formatNew.WriteString(format)

		log.Printf(formatNew.String(), append([]interface{}{file, line}, params...))
	}

	for {
		i := "hello"
		writeLog("%v", i)
		time.Sleep(time.Second*3)
	}
}




// 当前内存状态
var m runtime.MemStats
runtime.ReadMemStats(&m)
fmt.Printf("%d Kb\n", m.Alloc / 1024)



// 在一个对象 obj 被从内存移除前执行一些特殊操作，比如写到日志文件中
runtime.SetFinalizer(obj, func(obj *typeObj))


// 让出CPU时间片，重新等待安排任务
runtime.Gosched()

// 退出当前协程
// runtime.goexit() 只是退出当前的goroutinue  os.exit()会退出主进程
/*
os.Exit跳过延迟函数的执行
使用os.Exit，可以指定退出代码0, 1
panic 会打印堆栈

一般推荐 panic
*/
 runtime.Goexit()

// 确定需要使用多少个OS线程来同时执行Go代码, 默认值是机器上的CPU核心数
 runtime.GOMAXPROCS(n)
```

## flag包

```go
// flag库支持三种命令行选项格式:
// -和--都可以使用，它们的作用是一样的

-flag		// 只支持布尔类型的选项，出现即为true，不出现为默认值
-flag=x
-flag x     // 不支持布尔类型的选项

所以最保险的用法还是推荐 `--flag=xxx`



// 示例
var (
	debug bool
	conf string
)

//go run main.go -conf=xx -debug=true -- aa bb cc 
func main() {
	flag.StringVar(&conf, "conf", "./config.toml", "config file")
	flag.BoolVar(&debug, "debug", false, "debug mode")

	flag.Parse()

	log.Println(debug) // true
	log.Println(conf) // xx

	args := flag.Args()
	count := flag.NArg()
	log.Println(args) //  [aa bb cc]
	log.Println(count) // 3
}


// 自定义解析类型
// https://darjun.github.io/2020/01/10/godailylib/flag/

```

## embed 包

https://www.flysnow.org/2021/02/28/golang-embed-for-web.html

https://github.com/rakyll/statik 开源包

https://github.com/tmc/reactssr 服务端渲染

https://github.com/dstotijn/golang-nextjs-portable 和 nextjs 结合

### 内嵌 react 页面

新建 ui 包

```go

// 将 ui 包下 build 文件夹添加到 uiFs 内嵌文件系统下
//go:embed build
var uiFs embed.FS

// https://github.com/gin-gonic/gin/issues/1044
// https://juejin.cn/post/7016538957231947813
// https://github.com/gin-contrib/static/issues/19
type embedFileSystem struct {
	http.FileSystem
}

// 确保 自定义 struct 实现 ServeFileSystem接口
var _ static.ServeFileSystem = embedFileSystem{}

func (efs embedFileSystem) Exists(prefix string, path string) bool {
	_, err := efs.Open(path)
	return err == nil
}

func NewEmbedFileSystem() static.ServeFileSystem {
	f, err := fs.Sub(uiFs, "build")
	if err != nil {
		logx.Fatal("get embed fs sub failed, err: %v", err)
	}
	return embedFileSystem{
		FileSystem: http.FS(f),
	}
}

```

然后在 router 中 (需要和 gin 的 static 中间件配合)

```go

// 静态文件
	r.Use(static.Serve("/", ui.NewEmbedFileSystem()))

```

## 编译时生成 编译时约束 go-generate go-build

TODO

```
go:generate

go:build
```

# 工程实践 编程思维

## 设计模式

### 创建型

#### 简单工厂

```go
// NewXXX 函数返回接口时就是简单工厂模式
// Golang的一般推荐做法就是简单工厂。

//API is interface
type API interface {
	Say(name string) string
}

//NewAPI return Api instance by type
func NewAPI(t int) API {
	if t == 1 {
		return &hiAPI{} // hiApi 实现接口
	} else if t == 2 {
		return &helloAPI{} // 实现了接口
	}
	return nil
}
```

#### 单例

```go
/*
单例模式采用了 饿汉式 和 懒汉式 两种实现，个人其实更倾向于饿汉式的实现，简单，并且可以将问题及早暴露，懒汉式虽然支持延迟加载，但是这只是把冷启动时间放到了第一次使用的时候，并没有本质上解决问题，并且为了实现懒汉式还不可避免的需要加锁。
*/
// Singleton 饿汉式单例
// 
type Singleton struct{}

var singleton *Singleton

func init() {
	singleton = &Singleton{}
}

// GetInstance 获取实例
func GetInstance() *Singleton {
	return singleton
}

// =================

// GetLazyInstance 懒汉式
// 
import "sync"

var (
	lazySingleton *Singleton
	once          = &sync.Once{}
)

func GetLazyInstance() *Singleton {
	if lazySingleton == nil {
		once.Do(func() {
			lazySingleton = &Singleton{}
		})
	}
	return lazySingleton

```


### 行为型

#### 观察者

##### 基本示例

```go
package observer

import "fmt"

// ISubject subject
type ISubject interface {
	Register(observer IObserver)
	Remove(observer IObserver)
	Notify(msg string)
}

// IObserver 观察者
type IObserver interface {
	Update(msg string)
}

// Subject Subject
type Subject struct {
	observers []IObserver
}

// Register 注册
func (sub *Subject) Register(observer IObserver) {
	sub.observers = append(sub.observers, observer)
}

// Remove 移除观察者
func (sub *Subject) Remove(observer IObserver) {
	for i, ob := range sub.observers {
		if ob == observer {
			sub.observers = append(sub.observers[:i], sub.observers[i+1:]...)
		}
	}
}

// Notify 通知
func (sub *Subject) Notify(msg string) {
	for _, o := range sub.observers {
		o.Update(msg)
	}
}

// Observer1 Observer1
type Observer1 struct{}

// Update 实现观察者接口
func (Observer1) Update(msg string) {
	fmt.Printf("Observer1: %s", msg)
}

// Observer2 Observer2
type Observer2 struct{}

// Update 实现观察者接口
func (Observer2) Update(msg string) {
	fmt.Printf("Observer2: %s", msg)
}
```

##### 实现 event bus

```go
// 我们实现一个支持以下功能的事件总线

// 异步不阻塞
// 支持任意参数值


// Bus Bus
type Bus interface {
	Subscribe(topic string, handler interface{}) error
	Publish(topic string, args ...interface{})
}

// AsyncEventBus 异步事件总线
type AsyncEventBus struct {
	// 存储 topic  和 function 的映射
	handlers map[string][]reflect.Value
	lock     sync.Mutex
}

func NewAsyncEventBus() *AsyncEventBus {
	return &AsyncEventBus{
		handlers: map[string][]reflect.Value{},
		lock:     sync.Mutex{},
	}
}

// Subscribe 订阅
func (bus *AsyncEventBus) Subscribe(topic string, f interface{}) error {
	bus.lock.Lock()
	defer bus.lock.Unlock()

	v := reflect.ValueOf(f)
	if v.Type().Kind() != reflect.Func {
		return fmt.Errorf("handler is not a function")
	}

	handler, ok := bus.handlers[topic]
	if !ok {
		handler = []reflect.Value{}
	}
	handler = append(handler, v)
	bus.handlers[topic] = handler

	return nil
}

// Publish 发布
// 这里异步执行，并且不会等待返回结果
func (bus *AsyncEventBus) Publish(topic string, args ...interface{}) {
	handlers, ok := bus.handlers[topic]
	if !ok {
		fmt.Println("not found handlers in topic:", topic)
		return
	}

	params := make([]reflect.Value, len(args))
	for i, arg := range args {
		params[i] = reflect.ValueOf(arg)
	}

	for i := range handlers {
		go handlers[i].Call(params)
	}
}

```

### 结构型

#### 代理模式

```go
// 静态代理

package proxy

import (
	"log"
	"time"
)

// IUser IUser
type IUser interface {
	Login(username, password string) error
}

// User 用户
type User struct {
}

// Login 用户登录
func (u *User) Login(username, password string) error {
	// 不实现细节
	return nil
}

// UserProxy 代理类
type UserProxy struct {
	user *User
}

// NewUserProxy NewUserProxy
func NewUserProxy(user *User) *UserProxy {
	return &UserProxy{
		user: user,
	}
}

// Login 登录，和 user 实现相同的接口
func (p *UserProxy) Login(username, password string) error {
	// before 这里可能会有一些统计的逻辑
	start := time.Now()

	// 这里是原有的业务逻辑
	if err := p.user.Login(username, password); err != nil {
		return err
	}

	// after 这里可能也有一些监控统计的逻辑
	log.Printf("user login cost time: %s", time.Now().Sub(start))

	return nil
}



// 动态代理
// 可用 go generate 实现

```

## 调试 debug

https://github.com/go-delve/delve

## 模块拆分

### 按照 mvc 模式拆分

Ruby(ruby on Rails) 和 Java (springMVc) 是按照 mvc 模式拆分, 将服务中的不同组件分成了 Model、View 和 Controller 三层

golang 中, Beego 框架就是按照 mvc 模式划分模块的


### 按照职责对进行拆分 

这样有一个巨大的好处: 非常容易对微服务进行拆分，我们可以直接将一个负责独立功能的 package 拆出去，对这部分性能热点单独进行扩容；

```sh
# 例如对于一个比较常见的博客系统, golang 会这么划分
$ tree pkg
pkg
├── comment
├── post
│   ├── handler.go
│   └── post.go
└── user

# 如果我们在 Go 语言中使用 model、view 和 controller 来划分层级，你会在其他的模块中看到非常多的 model.Post、model.Comment 和 view.PostView, 显得非常冗余
```

### 按依赖拆分



## 项目目录结构规范

另一种在 Go 语言中组织代码的方式就是项目的根目录下放项目的代码(平铺)，这种方式在很多框架或者库中非常常见, 减少了引用依赖包 import 语句的长度

若果是开发的顶层应用, 则是下面这种布局:

```sh
# https://github.com/golang-standards/project-layout

├── LICENSE.md
├── Makefile
├── README.md
├── api			# 对外提供的各种不同类型的 API 接口定义文件
├── assets		#与存储库一起使用的其他资产(图像、徽标等)。
├── build		# 打包和持续集成, 将你的云( AMI )、容器( Docker )、操作系统( deb、rpm、pkg )包配置和脚本放在 /build/package 目录下, 将你的 CI (travis、circle、drone)配置和脚本放在 /build/ci 目录中
├── cmd			# 当前项目中的可执行文件，该目录下的每一个子目录都应该包含我们希望有的可执行文件
├── configs     # 配置文件模板或默认配置
├── deployments	# IaaS、PaaS、系统和容器编排部署配置和模板(docker-compose、kubernetes/helm、mesos、terraform、bosh)。注意，在一些存储库中(特别是使用 kubernetes 部署的应用程序)，这个目录被称为 /deploy。
├── docs
├── examples
├── githooks
├── init		# System init（systemd，upstart，sysv）和 process manager/supervisor（runit，supervisor）配置。
├── internal	# 私有代码 (真正的项目代码, 当我们在其他项目引入包含 internal 的依赖时，Go 语言会在编译时报错)
├── pkg			# 项目中可以被外部应用使用的代码库 (其他的项目可以直接通过 import 引入这里的代码, 不过如果我们开发的是 HTTP 或者 RPC 的接口服务或者公司的内部服务，将私有和公有的代码都放到 /pkg 中也没有太多的不妥，因为作为最顶层的项目来说很少会被其他应用直接依赖)
├── scripts		# 脚本文件, 由 Makefile 触发, 执行各种构建、安装、分析等操作
├── test		# 额外的外部测试应用程序和测试数据
├── third_party
├── tools		#这个项目的支持工具。注意，这些工具可以从 /pkg 和 /internal 目录导入代码
├── vendor  # go mod vendor 生成
├── web      # 静态 Web 资产
└── website  	# 如果你不使用 Github 页面，则在这里放置项目的网站数据

```

## package 导入自定义包

```go

package main //Programs start running in package main.
// main 包 和 main 函数 告诉 go编译器: 这是一个可执行程序, 需要编译为二进制文件

// 远程包: import "github.com/xiaoyureed/xxx" ; 会先搜索 gopath, 如果没有, 会使用 go get github.com/xiaoyureed/xxx 下载到本地
// 包重命名: import myfmt "mylib/fmt"
// 特殊的重命名: import _ "mylib/fmt" 不使用这个包, 但是执行包的init()
// import . "fmt" - 允许包内的内容不加fmt前缀而被被直接引用
//
// import "xxx_package" --------- 单个包导入
import (
	"bytes"
	"fmt"
	"io"
	"math"
	"math/cmplx" // 代码中用到的只是 cmplx, 而不是 math/cmplx, by convention, package name == last element of "import path"
	"runtime"
	"strings"
	"sync"
	"time"

	"xiaoyureed.github.io/hello/xx" //go代码文件名没有出现, 直接通过包名调用导出的函数
)

// 每个package 中的 init() 总是最先执行
func init() {
	fmt.Println("init() executed")
}


// 编译生成的二进制文件名: main 函数 所在 的go文件 的名字
func main() {
	fmt.Println("hello", "world")
	xx.Hello() // 使用自定义包

	// beego.Run()

	basicType()

	funcDemo() // 变量or方法都必须大写才能在包外访问

}


如何导入自定义包

这就要说到模块名称的作用: 用来引用当前项目内的其他包, 如: 在项目下新建目录 utils，创建一个utils.go文件. 那么 在 main.go 中就能使用 `import "utils"` 来引用 utils 包

```

## init 方法

### init使用

golang 中, 导入包时, 会自动执行 init 方法, 一个包将只初始化一次(init 仅仅执行一次)

不推荐在 init 中初始化资源, 因为这是隐式的, 不够直观

一个包可以有多个 init 函数 (在单个文件中或分布在多个文件中)，并且按照它们呈现给编译器的顺序被调用

一些框架会在 init 中判断是否满足使用的前置条件, 如:

```go
func init() {
    if user == "" {
        log.Fatal("$USER not set")
    }
    if home == "" {
        home = "/home/" + user
    }
    if gopath == "" {
        gopath = home + "/go"
    }
    // gopath may be overridden by --gopath flag on command line.
    flag.StringVar(&gopath, "gopath", gopath, "override default GOPATH")
}
```

### 执行顺序

初始化包的顺序: import --> const --> var --> init()


```
如果一个包导入了其他包，则首先初始化导入的包。

然后初始化当前包的常量。

接下来初始化当前包的变量。

最后，调用当前包的 init() 函数。

```



## go mod

### go mod 简介

https://xuanwo.io/2019/05/27/go-modules/
https://xuanwo.io/2019/08/22/go-modules-migrate/
TODO

包管理: Golang的包管理经过了多种工具的演变，从go vendor，到 godep，再到dep. 从go v1.11开始支持的go Modules。

推荐 go mod, 告别 GOPATH


go modules 好处:

- 不必须将项目目录放在GOPATH中
- 项目内会生成一个go.mod文件，列出包依赖, 自动下载依赖包
- 不使用vendor目录，而是统一安装到$GOPATH/pkg/mod/cache
- 所有引入进来的第三方包会准确的指定版本号
- 对于已经转移的包，可以用replace 申明替换，不需要改代码
	- 在国内访问golang.org/x的各个包都需要翻墙，你可以在go.mod中使用replace替换成github上对应的库。如 `replace golang.org/x/text v0.3.0 => github.com/golang/text v0.3.0` 将引入正确的依赖


### 使用方法 相关命令

1. 在 gopath 外部新建一个 folder 作为模块目录(名称不限, 一般指定为 模块名称 如 hello)

1. 进入后 `go mod init xiaoyureed.github.io/hello` (xiaoyureed.github.io 表示模块发布的路径, hello 表示模块名), 生成 go.mod 文件, 内容包含: module name (即xiaoyureed.github.io/hello), go version, requires, 类比 package.json (一般不用手动修改 go.mod)

1. 新建 main 文件, 引入 `import "github.com/astaxie/beego"`, 然后 `go mod tidy -v`(整理依赖包到 go.mod), 可能需要 `go mod download`, 然后 main 函数中 `beego.Run()`, 直接运行 `go run main.go` 

    或者先编译 `go build` (可以 先 `go mod tidy` 去除不要的依赖), 生成 main 文件, ./main 执行 (同时, go build 后产生一个名为go.sum的文件, 类比 package.lock)

    依赖包会下载到 `$GOPATH/pkg/mod` 下



三方库版本号规则?  就是包发布到 github 标记的 tag，格式为 vn.n.n (n代表数字), 在 github 仓库的release 可以看到. 如果包的作者还没有标记版本，默认为 v0.0.0, 在 go.mod 中指定, 若没有指定, 默认 为 latest

依赖地址失效怎么办: 在 go.mod 中 `replace golang.org/x/text => github.com/golang/text latest` (前者表示要替换的地址, 后者表示新的有效地址). 原理就是下载http://github.com/golang/text 的最新版本到 $GOPATH/pkg/mod/golang.org/x/text下

引入的依赖在本地不在 github怎么办? 同样使用 `replace`, 首先在 required 下正常导入 `require xxx/xx v0.0.0`, 再通过 `replace xxx/xx => /usr/local/xxx` 即可


```
module xiaoyureed.github.io/log_collection

go 1.16

require github.com/Shopify/sarama v1.19.0

```

```sh


# 生成模块, 就是在当前目录下生成一个 go.mod
# go.mod 文件的出现定义了它所在的目录为一个模块。一个项目中，不同文件夹都可以有go.mod 
# 包括 mod name, go version
go mod init <mod name>

#  下载依赖的module到本地cache（默认为$GOPATH/pkg/mod目录）
# 下载modules到本地$GOPATH/pkg/mod和 ​$GOPATH/pkg/sum
go mod download

# 下载指定 mod, 没有 version 就是下载最新版, 
# GO111MODULE="auto" | "off", 会下载到 go_path/src 下
# GO111MODULE="on"会安装在GOPATH/pkg/mod/下，import导入非标准包的时候是从这个目录搜索，不会去GOPATH/src目录下找包。 此时等价于 go mod download
go get github.com/gogf/gf@version
# 指定分支
go get github.com/gogf/gf@master



# 编辑 go.mod
go mod edit
# 查看帮助
go help mod edit

# 验证依赖是否正确
go mod verify
# 以文本模式打印模块依赖图
go mod graph
# 会检测该文件夹目录下所有引入的依赖,写入 go.mod 文件
# 此时依赖还是没有下载的 , 需要 go mod download 才会下载
# 删除错误或者不使用的modules
# -v 表示打印详细过程
go mod tidy [-v]
# 生成vendor目录 , 将依赖复制到vendor下
go mod vendor

go mod verify      校验依赖
# 查找依赖
#   解释为什么需要依赖
go mod why
# 清理moudle 缓存
go clean -modcache

# 查看可下载版本
go list -m -versions github.com/gogf/gf
go list -m -u all # 来检查可以升级的package，
go get -u <need-upgrade-package> #升级后会将新的依赖版本更新到go.mod * 
go get -u #升级所有依赖
```


### GO111MODULE

可以把项目放在$GOPATH/src下吗? 可以, go会根据GO111MODULE的值而采取不同的处理方式
- auto 自动模式下 (默认)，项目在$GOPATH/src里会使用$GOPATH/src的依赖包，在$GOPATH/src外，就使用go.mod 里 require的包
- on 开启模式，1.12后，无论在$GOPATH/src里还是在外面，都会使用go.mod 里 require的包
- off 关闭模式，就是老规矩。


### 依赖 间接依赖

https://blog.csdn.net/juzipidemimi/article/details/104441398

```sh
# 被添加注释的包肯定是间接依赖的包，而没有添加// indirect注释的包则是直接依赖的包，即明确的出现在某个import语句中
# 
# 为什么需要间接依赖: Go module需要精确地记录软件的依赖情况, 由于Go 语言从v1.11版本才推出module的特性，众多开源软件迁移到go module还需要一段时间，在过渡期必然会出现间接依赖，但随着时间的推进，在go.mod中出现// indirect的机率会越来越低
# 
# 间接依赖出现在go.mod文件的情况，可能符合下面所列场景的一种或多种: (间接依赖出现在go.mod中，可以一定程度上说明依赖有瑕疵)
# 	直接依赖未启用 Go module 
# 		Module A 依赖 B，但是 B 还未切换成 Module，也即没有go.mod文件，此时，当使用go mod tidy命令更新A的go.mod文件时，B的两个依赖B1和B2将会被添加到A的go.mod文件中	
# 	直接依赖go.mod 文件中缺失部分依赖


go mod tidy # 会自动整理go.mod 文件，如果有必要会在部分依赖包的后面增加// indirect注释

go mod why -m all #则可以分析所有依赖的依赖链
go mod why -m <pkg> #查看某个间接依赖是被哪个依赖引入的


```

## 编码套路

### 面向接口编程

```go
//bad
package post
var client *grpc.ClientConn
func init() {
    var err error
	// 在 init 函数中隐式地初始化了 grpc 连接这种全局变量, 不好
    client, err = grpc.Dial(...）
    if err != nil {
        panic(err)
    }
}
// 没有将 ListPosts 通过接口的方式暴露出去，这会让依赖 ListPosts 的上层模块难以测试
func ListPosts() ([]*Post, error) {
    posts, err := client.ListPosts(...)
    if err != nil {
        return []*Post{}, err
    }
    
    return posts, nil
}



// good
// 这种使用接口组织代码的方式在 Go 语言中非常常见:
	// 使用大写的 Service 对外暴露方法；
	// 使用小写的 service 实现接口中定义的方法；
	// 通过 NewService 函数初始化 Service 接口, 返回 Service 的指针；
package post
// 通过接口 Service 暴露对外的 ListPosts 方法
// 简单点, 也可以吧 Service interface 省掉, 直接为 service struct 实现方法
type Service interface {
    ListPosts() ([]*Post, error)
}
type service struct {
    conn *grpc.ClientConn
}
// 使用 NewService 函数初始化 Service 接口的实现并通过私有的结构体 service 持有 grpc 连接
func NewService(conn *grpc.ClientConn) Service {
    return &service{
        conn: conn,
    }
}
func (s *service) ListPosts() ([]*Post, error) {
	// ListPosts 不再依赖全局变量，而是依赖接口体 service 持有的连接；
    posts, err := s.conn.ListPosts(...)
    if err != nil {
        return []*Post{}, err
    }
    
    return posts, nil
}

// 这样使用
func main() {
    conn, err = grpc.Dial(...）
    if err != nil {
        panic(err)
    }
    // 显式的初始化 grpc 连接、创建 Service 接口的实现并调用 ListPosts 方法
    svc := post.NewService(conn)
    posts, err := svc.ListPosts()
    if err != nil {
        panic(err)
    }
    
    fmt.Println(posts)
}

```

### functional options 构造对象

```go
// 等待构造的对象类型
type Server struct {
    Addr     string
    Port     int
    Protocol string
    Timeout  time.Duration
    MaxConns int
    TLS      *tls.Config
}

// 定义构造选项
type Option func(*Server)

func Protocol(p string) Option {
    return func(s *Server) {
        s.Protocol = p
    }
}
func Timeout(timeout time.Duration) Option {
    return func(s *Server) {
        s.Timeout = timeout
    }
}
func MaxConns(maxconns int) Option {
    return func(s *Server) {
        s.MaxConns = maxconns
    }
}
func TLS(tls *tls.Config) Option {
    return func(s *Server) {
        s.TLS = tls
    }
}

func NewServer(addr string, port int, options ...func(*Server)) (*Server, error) {

  srv := Server{
    Addr:     addr,
    Port:     port,
    Protocol: "tcp",
    Timeout:  30 * time.Second,
    MaxConns: 1000,
    TLS:      nil,
  }
  for _, option := range options {
    option(&srv)
  }
  //...
  return &srv, nil
}

// 使用
s1, _ := NewServer("localhost", 1024)
s2, _ := NewServer("localhost", 2048, Protocol("udp"))
s3, _ := NewServer("0.0.0.0", 8080, Timeout(300*time.Second), MaxConns(1000))
```

### 控制反转

```go
// 有这样一个 int set
// 现在要为他加入 undo 功能
type IntSet struct {
    data map[int]bool
}
func NewIntSet() IntSet {
    return IntSet{make(map[int]bool)}
}
func (set *IntSet) Add(x int) {
    set.data[x] = true
}
func (set *IntSet) Delete(x int) {
    delete(set.data, x)
}
func (set *IntSet) Contains(x int) bool {
    return set.data[x]
}


// ======= 完整实现


// 先声明一种函数接口，表现我们的Undo控制可以接受的函数签名是什么样的
// 
// 这个就是控制反转，不再由 控制逻辑 Undo 来依赖业务逻辑 IntSet，而是由业务逻辑 IntSet 来依赖 Undo 。其依赖的是其实是一个协议，这个协议是一个没有参数的函数数组。我们也可以看到，我们 Undo 的代码就可以复用了
type Undo []func()

func (undo *Undo) Add(function func()) {
  *undo = append(*undo, function)
}
// undo 就是执行最末尾的一步操作
func (undo *Undo) Undo() error {
  functions := *undo
  if len(functions) == 0 {
    return errors.New("No functions to undo")
  }
  index := len(functions) - 1
  if function := functions[index]; function != nil {
    function()
    functions[index] = nil // For garbage collection
  }
  *undo = functions[:index]
  return nil
}

// IntSet里嵌入 Undo，然后，再在 Add() 和 Delete() 里使用上面的方法，就可以完成功能
type IntSet struct {
    data map[int]bool
    undo Undo
}
 
func NewIntSet() IntSet {
    return IntSet{data: make(map[int]bool)}
}

func (set *IntSet) Undo() error {
    return set.undo.Undo()
}
 
func (set *IntSet) Contains(x int) bool {
    return set.data[x]
}

func (set *IntSet) Add(x int) {
    if !set.Contains(x) {
        set.data[x] = true
        set.undo.Add(func() { set.Delete(x) })
    } else {
        set.undo.Add(nil)
    }
}
 
func (set *IntSet) Delete(x int) {
    if set.Contains(x) {
        delete(set.data, x)
        set.undo.Add(func() { set.Add(x) })
    } else {
        set.undo.Add(nil)
    }
}
```

### 修饰器

```go
func WithServerHeader(h http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        log.Println("--->WithServerHeader()")
        w.Header().Set("Server", "HelloServer v0.0.1")
        h(w, r)
    }
}
func WithAuthCookie(h http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        log.Println("--->WithAuthCookie()")
        cookie := &http.Cookie{Name: "Auth", Value: "Pass", Path: "/"}
        http.SetCookie(w, cookie)
        h(w, r)
    }
}
func WithBasicAuth(h http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        log.Println("--->WithBasicAuth()")
        cookie, err := r.Cookie("Auth")
        if err != nil || cookie.Value != "Pass" {
            w.WriteHeader(http.StatusForbidden)
            return
        }
        h(w, r)
    }
}
func WithDebugLog(h http.HandlerFunc) http.HandlerFunc {
    return func(w http.ResponseWriter, r *http.Request) {
        log.Println("--->WithDebugLog")
        r.ParseForm()
        log.Println(r.Form)
        log.Println("path", r.URL.Path)
        log.Println("scheme", r.URL.Scheme)
        log.Println(r.Form["url_long"])
        for k, v := range r.Form {
            log.Println("key:", k)
            log.Println("val:", strings.Join(v, ""))
        }
        h(w, r)
    }
}
func hello(w http.ResponseWriter, r *http.Request) {
    log.Printf("Recieved Request %s from %s\n", r.URL.Path, r.RemoteAddr)
    fmt.Fprintf(w, "Hello, World! "+r.URL.Path)
}
func main() {
    http.HandleFunc("/v1/hello", WithServerHeader(WithAuthCookie(hello)))
    http.HandleFunc("/v2/hello", WithServerHeader(WithBasicAuth(hello)))
    http.HandleFunc("/v3/hello", WithServerHeader(WithBasicAuth(WithDebugLog(hello))))
    err := http.ListenAndServe(":8080", nil)
    if err != nil {
        log.Fatal("ListenAndServe: ", err)
    }
}

// 改进
// 多个修饰器的 Pipeline
type HttpHandlerDecorator func(http.HandlerFunc) http.HandlerFunc
func Handler(h http.HandlerFunc, decors ...HttpHandlerDecorator) http.HandlerFunc {
    for i := range decors {
        d := decors[len(decors)-1-i] // iterate in reverse
        h = d(h)
    }
    return h
}

// 使用
http.HandleFunc("/v4/hello", Handler(hello,
                WithServerHeader, WithBasicAuth, WithDebugLog))
```

### pipeline 模式

```go
// 类似 Unix 中的管道操作, 实际上, 也正是使用 go channel 实现的

// 需要一个吧序列转为 channel 的方法
func echo(nums []int) <-chan int {
  out := make(chan int)
  go func() {
    for _, n := range nums {
      out <- n
    }
    close(out)
  }()
  return out
}

// 求平方
func sq(in <-chan int) <-chan int {
  out := make(chan int)
  go func() {
    for n := range in {
      out <- n * n
    }
    close(out)
  }()
  return out
}

// 过滤出奇数
func odd(in <-chan int) <-chan int {
  out := make(chan int)
  go func() {
    for n := range in {
      if n%2 != 0 {
        out <- n
      }
    }
    close(out)
  }()
  return out
}

// 求和
func sum(in <-chan int) <-chan int {
  out := make(chan int)
  go func() {
    var sum = 0
    for n := range in {
      sum += n
    }
    out <- sum
    close(out)
  }()
  return out
}

// 使用
var nums = []int{1, 2, 3, 4, 5, 6, 7, 8, 9, 10}
for n := range sum(sq(odd(echo(nums)))) {
  fmt.Println(n)
}


// 不想有那么多的函数嵌套
type EchoFunc func ([]int) (<- chan int) 
type PipeFunc func (<- chan int) (<- chan int) 

func pipeline(nums []int, echo EchoFunc, pipeFns ... PipeFunc) <- chan int {
  ch  := echo(nums)
  for i := range pipeFns {
    ch = pipeFns[i](ch)
  }
  return ch
}
```

### visitor 模式

```go

// Kubernetes 的 kubectl 命令中的使用到到的一个编程模式 – Visitor
// 是一种将算法与操作对象分离的一种方法, 能够在不修改操作对象添加新操作

type Visitor func(shape Shape)
type Shape interface {
    accept(Visitor)
}
type Circle struct {
    Radius int
}
func (c Circle) accept(v Visitor) {
    v(c)
}
type Rectangle struct {
    Width, Heigh int
}
func (r Rectangle) accept(v Visitor) {
    v(r)
}


// 使用
// 实现两个Visitor，一个是用来做JSON序列化的，另一个是用来做XML序列化
// 操作对象有点像一个数据库，而各个Visitor会成为一个个小应用
func JsonVisitor(shape Shape) {
    bytes, err := json.Marshal(shape)
    if err != nil {
        panic(err)
    }
    fmt.Println(string(bytes))
}

func XmlVisitor(shape Shape) {
    bytes, err := xml.Marshal(shape)
    if err != nil {
        panic(err)
    }
    fmt.Println(string(bytes))
}

// ==============
func main() {
  c := Circle{10}
  r :=  Rectangle{100, 200}
  shapes := []Shape{c, r}

  for _, s := range shapes {
    s.accept(JsonVisitor)
    s.accept(XmlVisitor)
  }

}

```

### microKernel 架构

微内核模式

## 单元测试

### 开源测试库

```
goconvey, 代替 testify, GoConvey 和其他 Stub/Mock 框架的兼容性相比 Testify 更好


testify 提供非常多的断言, 自带 Mock 框架，但是用这个框架 Mock 类需要自己写。像这样重复有规律的部分在 GoMock 中是一键自动生成的



```

### 通用 mock


https://github.com/golang/mock  最标准的也是最被鼓励的方式

https://github.com/bouk/monkey 猴子补丁, 能够通过替换函数指针的方式修改任意函数的实现, 用来 Mock 依赖, 万能的方法，但是只在万不得已时使用，类似的代码写起来非常冗长而且不直观, 然而这种方法的使用其实有一些限制，由于它是在运行时替换了函数的指针，所以如果遇到一些简单的函数，例如rand.Int63n和time.Now，编译器可能会直接将这种函数内联到调用实际发生的代码处并不会调用原有的方法，所以使用这种方式往往需要我们在测试时额外指定-gcflags=-l禁止编译器的内联优化 `go test -gcflags=-l ./...`


### 数据层 mock测试

https://github.com/DATA-DOG/go-sqlmock mock 数据库, 处理依赖的数据库

https://github.com/alicebob/miniredis mock redis

### web层测试

net/http/httptest 标准库 , 测试自己编写的 api

https://github.com/h2non/gock mock 外部的第三方 api

https://github.com/jarcoal/httpmock HTTP mocking, 处理依赖的 http 请求


```go
func setupServerPostHandler(t *testing.T) *gin.Engine {
    engine := gin.New()
    //engine.Use(middleware.Logger())
    engine.Use(gin.Recovery())
    PostDaoMock,issql:= GetPostDAO(t)
    if !issql {
        ... mock 初使化
        
    }
    RedisClient,isTrue:= GetRedisClient(t)
    if !isTrue {
        ... mock 初使化
        
    }
    server := NewServer()
    // 唯一依赖
    server.SetPostService(PostDaoMock,RedisClient)
    
    engine.POST("/AddPost", server.GetPosts)
    return engine
}

func TestPostHandler(t *testing.T) {
    router := setupServerPostHandler(t)
    Convey("Post Handler接口测试",t, func() {
        req_content := &Post{
            ... 内容
        }
        type Data_resp struct {
            Post_id int `json:Post_id`
        }
        type resp_json struct {
            Data  Data_resp `json:data`
            Err_msg  string `json:err_msg`
            Err_no   int `json:err_no`
        }

        req_content.Type = "AddPost"
        Convey("AddPost 测试", func() {

            Convey("AddPost 测试1", func() {

                req_new := req_content
                req_string, _ := json.Marshal(req_new)
                req := httptest.NewRequest(http.MethodPost, "/AddPost", strings.NewReader(string(req_string)))
                req.Header[global.HEADER_TRACEID] = []string{"testTrace"}
                req.Header[global.HEADER_SPANID] = []string{"testSpan"}
                req.Header[global.HEADER_USER] = []string{"testUser"}
                req.Header.Set("Content-Type","application/json")

                w := httptest.NewRecorder()
                router.ServeHTTP(w, req)
                resp := w.Result()
                resp_json1 := &resp_json{}
                _ = json.Unmarshal(w.Body.Bytes(), resp_json1)
                So(resp_json1.Data.Post_id,ShouldHaveSameTypeAs,1)
                So(resp.StatusCode,ShouldEqual,http.StatusOK)
            })
        })
    })
}
```


### testing 包

#### 命令行基本使用

对于普通test, `go test .` 或者 `go test xxx_test.go`

1. 文件名以 "_test.go"结尾 （规范，否则 `go test` 不会执行测试), 不会被编译到可执行文件中
1. 文件必须包含测试函数, 测试函数名以 "Test"开头, 接受一个 "*testing.T" 类型的参数 (必须,否则不执行这个 test case), 有三种类型的函数，单元测试函数、基准测试函数和示例函数(前缀为Example)

对于 benchmark test 是特殊的test, 用于测试性能, `go test -bench=.`

1. 函数 以 "Benchmark" 开头
2. benchmark函数一般会跑 b.N 次(不是确定的), 以每次花费的时间代表性能

```go
go test <module name>/<package name> // 用来运行某个 package 内的所有测试用例

go test //默认执行当前目录下以xxx_test.go的测试文件
// or
go test <current module name>
// or
go test .

go test -v //可以看到详细的输出信息。
go test -v xxx_test.go //指定测试单个文件，但是该文件中如果调用了其它文件中的模块会报错
go test -v xxx_test.go xxx.go //指定测试单个文件和被测文件

go test -v -run=Testxxx //指定某个测试函数运行, Testxxx 不必指定全称
go test -v -run Testxxx //指定某个测试函数运行, Testxxx 不必指定全称

go test -v -cover //查看测试覆盖率。
go test -cover -coverprofile=c.out // 将覆盖率相关的记录信息输出到一个文件
go tool cover -html=c.out // 打开本地的浏览器窗口生成一个HTML报告


// 运行子 package 内的用例
go test <cur_package_name>/<sub_package name> 
// or
go test ./<sub_package name>
// 递归测试当前目录下的所有的 package
go test ./... 或 go test example/...


// 跳过单元测试，执行所有benchmark,同时生成一个cpu性能描述文件
// go test 命令默认不运行 benchmark 用例的，如果我们想运行 benchmark 用例，则需要加上 -bench 参数 (可以不加等号)
go test -run=xxx -bench=. -benchtime="3s" -cpuprofile profile_cpu.out
// 支持正则
go test -bench='Fib$' .

```

#### testing 通用方法

```go
/*
T结构内部是继承自common结构，common结构提供集中方法，是我们经常会用到的:

遇到一个断言错误的时候，判断这个测试用例失败:
	Fail  : case失败，测试用例继续
	FailedNow : case失败，测试用例中断
希望断言失败的时候，测试用例失败，打印出必要的信息，但是测试用例继续:
	Error : Log + Fail
希望断言失败的时候，测试用例失败，打印出必要的信息，测试用例中断:
	Fatal : Log + FailNow
遇到一个断言错误，只希望跳过这个错误，但是不希望标示测试用例失败
	SkipNow : case跳过，测试用例不继续
	Skip : Log + SkipNow
*/
package main

import (
  "fmt"
  "testing" // 测试包
)


// 可以通过 TestMain做一些初始化工作, 数据库连接, 文件打开, restful登陆...
// TestMain 不是必须的
func TestMain(m *testing.M) {

  fmt.Println("TestMain 最先执行")
  m.Run() // 必须调用, 否则其他test不会执行
}

func  TestAdd(t *testing.T) {
    s:=Add(1,2)
    if s!=3{
        t.Error("Expected 3, got ", s)
    }
    
}

// 跳过某些测试
// 
func TestTimeConsuming(t *testing.T) {
	// go test -short 则这里的 short() 返回 true
    if testing.Short() {
        t.Skip("short模式下会跳过该测试用例")
				// or
  			// t.SkipNow// 跳过当前 方法, 必须在第	一行

    }
    ...
}



// 方法名必须大写, 以 Test开头
// 		sub test
func TestXxx(t *testing.T) {

  // 可以保证 test 的顺序
  t.Run("sub test1", func(t *testing.T) {
    fmt.Println("sub test1")
  })
  t.Run("sub test2", func(t *testing.T) {
    fmt.Println("sub test2")
  })

  if false {
    t.Errorf("stm goes wrong")
  }
}

// 小写不会执行
// 小写的test一般作为 sub test
func testXxx(t *testing.T) {
  t.Errorf("testXxx 没执行")
}


// 并行测试
// 
// 遍历测试用例
	for _, tt := range tests {
		tt := tt  // 注意这里重新声明tt变量（避免多个goroutine中使用了相同的变量）
		t.Run(tt.name, func(t *testing.T) { // 使用t.Run()执行子测试
			t.Parallel()  // 将每个测试用例标记为能够彼此并行运行
			got := Split(tt.input, tt.sep)
			if !reflect.DeepEqual(got, tt.want) {
				t.Errorf("expected:%#v, got:%#v", tt.want, got)
			}
		})
	}


// -------------- 基准测试 -------------

// 待 性能测试的函数
func btest() int {
  xx := 20 + 30
  return xx
}

// benchmark 性能测试
func BenchmarkXxx(b *testing.B) {
	time.Sleep(time.Second * 3) // 模拟耗时准备任务
	b.ResetTimer() // 重置定时器, 计时清零从新开始
				// 其他还有:
				// b.StopTimer() 停止计时
				// b.StartTimer() 重新开始计时

	b.ReportAllocs() // 在report中包含内存分配信息

  for n := 0; n < b.N; n++ { // b.N 为默认提供的数值 不是定值, 会根据测试代码的执行时间动态调整直到执行时间达到稳态, 最后打印出的实践是每次执行的平均时间
    btest() // 测试代码的执行时间必须能够达到稳态, 否则benchmark会永远执行不完
  }
}


```

#### 表格测试 http测试


https://github.com/cweill/gotests 生成表格测试模板代码

net/http/httptest 标准库, 网络 http测试

```go


func main() {
	http.HandleFunc("/double", doubleHandler)
	log.Fatalln(http.ListenAndServe(":4000", nil))
}

func doubleHandler(w http.ResponseWriter, r *http.Request) {
	text := r.FormValue("v")

	if text == "" {
		http.Error(w, "missing value", http.StatusBadRequest)
		return
	}

	v, err := strconv.Atoi(text)
	if err != nil {
		http.Error(w, "not a number: "+text, http.StatusBadRequest)
		return
	}

	if _, err = fmt.Fprintln(w, v*2); err != nil {
		http.Error(w, "cannot write to response", http.StatusBadRequest)
		return
	}

}


// 符合Go语言单元测试风格的表格测试
func TestDoubleHandler(t *testing.T) {

	testCases := []struct {
		name   string
		input  string
		result int
		status int
		err    string
	}{
		{name: "double of two", input: "2", result: 4, status: http.StatusOK, err: ""},
		{name: "double of nine", input: "9", result: 18, status: http.StatusOK, err: ""},
		{name: "double of nil", input: "", status: http.StatusBadRequest, err: "missing value"},
	}

	for _, testCase := range testCases {
		testCase := testCase
		t.Run(testCase.name, func(t *testing.T) {
			req, err := http.NewRequest(http.MethodGet, "localhost:4000/double?v="+testCase.input, nil)
			if err != nil {
				t.Fatalf("could not create a new request: %v, err: %v", req, err)
			}

			rec := httptest.NewRecorder()
			doubleHandler(rec, req) // 待测试函数
			res := rec.Result()

			if res.StatusCode != testCase.status {
				t.Errorf("received status code %d, expect %d", res.StatusCode, testCase.status)
				return
			}

			respBytes, err := io.ReadAll(res.Body)
			if err != nil {
				t.Fatalf("cannot read all from the response body, err: %v", err)
			}
			defer res.Body.Close()

			trimedResult := strings.TrimSpace(string(respBytes))

			if res.StatusCode != http.StatusOK {
				// check the error message
				if trimedResult != testCase.err {
					t.Errorf("received error message %s, expect %s", trimedResult, testCase.err)
				}
				return
			}

			// compare the returned value
			doubleVal, err := strconv.Atoi(trimedResult)
			if err != nil {
				t.Errorf("cannot convert response body to int, err: %v", err)
				return
			}

			if doubleVal != testCase.result {
				t.Errorf("received result %d, expected %d", doubleVal, testCase.result)
			}
		})
	}
}
```

## 错误处理

https://mytechshares.com/2021/11/22/go-error-best-practice/
https://xuanwo.io/2020/05-go-error-handling/
https://coolshell.cn/articles/21140.html#%E5%8C%85%E8%A3%85%E9%94%99%E8%AF%AF
https://lailin.xyz/post/go-training-03.html
https://go.dev/blog/error-handling-and-go

虽然 Go 语言中也有类似 Java 或者 Ruby try/catch 关键字，但是很少有人会在代码中使用 panic 和 recover 来实现错误和异常的处理

### 以闭包的形式封装错误检测

```go
func httpRequestHandler(w http.ResponseWriter, req *http.Request) {
    err := func () error {
        if req.Method != "GET" {
            return errors.New("expected GET")
        }
        if input := parseInput(req); input != "command" {
            return errors.New("malformed command")
        }
        // 可以在此进行其他的错误检测
    } ()

        if err != nil {
            w.WriteHeader(400)
            io.WriteString(w, err)
            return
        }
        doSomething() ...
```

### panic recover 机制

```go
// panic 程序退出, 用于不可恢复的错误, 退出前会执行 defer 内容
// os.exit 也会退出, 不会执行 defer, 不会输出调用栈信息

// err := recover() 会捕获异常
// 但是不要这样做, 因为这样强行不让程序 crash, 但是实际引起 error 的原因还是存在, 也就是 程序好存活着, 但是无法正常工作, 其他的健康检查一看程序还活着, 也不会报警

defer func() {
	if err := recover(); err != nil {
		log.error(err)
	}
}()

```

### 对错误进行比较 

```go
// 错误的 error比较方法
func TestA(t *testing.T) {
	_, err := doSth("a1")
	if err != nil {
		if err == errors.New("flag is not a") {
			println(">>> 相同")
		} else {
			// 代码会走这里
			// errors.new(xx) 返回的是指针, 两个指针比较, 总是会不等
			//为什么这么设计? 防止错误字符串相等就判断两个错误相等
			println(">>> 不同")
		}
	}
}
func doSth(flag string) (string, error) {
	if flag != "a" {
		return "hello", errors.New("flag is not a")
	}
	return flag, nil
}

//////////////////////////

// 正确的方式是提前定义好error变量
var flagErr = errors.New("flag error")

func TestA(t *testing.T) {
	_, err := doSth("a1")
	if err != nil {
		if err == flagErr {
			//这次就好了, 走这里了
			println(">>> 相同")
		} else {
			println(">>> 不同")
		}
	}
}


```

### 对错误进行包装 erros包 Is As Unwrap 自定义错误


```go

// Is


var flagErr = errors.New("flag error")

func TestA(t *testing.T) {
	err := parentMethod("a1")
	//Is() 错误值比较, 可以判断 err 的错误链条是否存在 目标错误
	//它递归调用 Unwrap 并判断每一层的 err 是否相等，如果有任何一层 err 和传入的目标错误相等，则返回 true, 如果一直到底都不行就返回 false
	//
	if errors.Is(err, flagErr) {
		fmt.Printf("err: %v\n", err)
		//print
		//error of parent method, orginal err: error of flag
		// 可见, 打印顺序是从外层到内层
	}
}


func parentMethod(flag string) error {
	_, err := doSth(flag)
	if err != nil {
		//包装错误时, 使用 %w
		return fmt.Errorf("error of parent method, orginal err: %w", err)
	}
	return nil
}

func doSth(flag string) (string, error) {
	if flag != "a" {
		return "hello", flagErr
	}
	return flag, nil
}


///////////////////
// As
// 
//在Go 1.13之前没有wrapping error的时候，我们要把error转为另外一个error，一般都是使用type assertion 或者 type switch，其实也就是类型断言
// 
// 遍历err嵌套链，从里面找到类型符合的error，然后把这个error赋予target,这样我们就可以使用转换后的target了，这里有值得赋予，所以target必须是一个指针

func TestA(t *testing.T) {
	err := grandParentMethod("a1")
	var e flagErr
	// As 第二个参数是用来存放提取出来的 err 的指针
	// 会把最内层的 error 提取出来
	if errors.As(err, &e) {
		fmt.Printf("err: %v, e: %v\n", err, e)
		//print
		//err: error of grand parent method, orginal: error of parent method, orginal err: error of flag, e: error of flag

		// 解开包装
		err := errors.Unwrap(err)
		fmt.Printf("unwrap1: %v\n", err)
		//unwrap1: error of parent method, orginal err: error of flag
		err = errors.Unwrap(err)
		fmt.Printf("unwrap2: %v\n", err)
		//unwrap2: error of flag
		err = errors.Unwrap(err)
		fmt.Printf("unwrap3: %v\n", err)
		// unwrap3: <nil>
	}
}


type flagErr struct {
	Msg string
}

func (e flagErr) Error() string {
	return e.Msg
}

func grandParentMethod(flag string) error {
	err := parentMethod(flag)
	if err != nil {
		err := fmt.Errorf("error of grand parent method, orginal: %w", err)
		fmt.Printf("grandParentMethod: type: %T, value: %v\n", err, err)
		//print
		//grandParentMethod: type: *fmt.wrapError, value: error off grand parent method, orginal: error of parent method, orginal err: error of flag
		return err
	}
	return nil
}

func parentMethod(flag string) error {
	_, err := doSth(flag)
	if err != nil {
		//包装错误时, 使用 %w
		err := fmt.Errorf("error of parent method, orginal err: %w", err)
		fmt.Printf("parentMethod: type: %T, value: %v\n", err, err)
		//print
		//parentMethod: type: *fmt.wrapError, value: error of parent method, orginal err: error of flag
		return err
	}
	return nil
}

func doSth(flag string) (string, error) {
	if flag != "a" {
		err := flagErr{"error of flag"}
		fmt.Printf("doSth: type: %T, value: %v\n", err, err)
		//print
		//doSth: type: main.flagErr, value: error of flag
		return "hello", err
	}
	return flag, nil
}

```

### if err错误处理优化套路

```go
// 套路 1: 在定义的 struct 内部声明一个字段用来保存操作过程中的错误
// 参考 bufio.Scanner()


// 文件读写例子
type errWriter struct {
	io.Writer
	err error
}
func (e *errWriter) Write(buf []byte) (int, error) {
	if e.err != nil {
		return 0, e.err
	}
	var n int
	n, e.err = e.Writer.Write(buf)
	return n, nil
}
func WriteResponse(w io.Writer, st Status, headers []Header, body io.Reader) error {
	ew := &errWriter{Writer: w}
	fmt.Fprintf(ew, "HTTP/1.1 %d %s\r\n", st.Code, st.Reason)

	for _, h := range headers {
		fmt.Fprintf(ew, "%s: %s\r\n", h.Key, h.Value)
	}

	fmt.Fprint(ew, "\r\n")
	io.Copy(ew, body)
	return ew.err
}
```

### 使用 pkg-errors库

```go
// 要新生成一个错误
func New(message string) error

//只附加新的信息
func WithMessage(err error, message string) error

//只附加调用堆栈信息
func WithStack(err error) error

//同时附加堆栈和信息
func Wrap(err error, message string) error

// 找到最内层错误
func Cause(err) error


%s,%v //功能一样，输出错误信息，不包含堆栈
%q //输出的错误信息带引号，不包含堆栈
%+v //输出错误信息和堆栈
fmt.Printf("%+v\n", err)


// 实例
func main() {
	_, err := ReadConfig()
	if err != nil {
		fmt.Printf("original error: %T %v\n", errors.Cause(err), errors.Cause(err))
		fmt.Printf("stack trace:\n%+v\n", err)
		os.Exit(1)
	}
}
/*
original error: *os.PathError open /Users/dfc/.settings.xml: no such file or directory
stack trace:
open /Users/dfc/.settings.xml: no such file or directory
open failed
main.ReadFile
        /Users/dfc/devel/practical-go/src/errors/readfile2.go:16
main.ReadConfig
        /Users/dfc/devel/practical-go/src/errors/readfile2.go:29
main.main
        /Users/dfc/devel/practical-go/src/errors/readfile2.go:35
runtime.main
        /Users/dfc/go/src/runtime/proc.go:201
runtime.goexit
        /Users/dfc/go/src/runtime/asm_amd64.s:1333
could not read config
*/
```

## 日志

### 自带日志包

没有级别功能, 需要自己封装

```go
package main

import (
    "io"
    "log"
    "os"
    "sync/atomic"
)

// log level
const (
    LDEBUG = iota + 1 // 1
    LWARN             // 2
    LINFO             // 3
    LERROR            // 4
    LFATAL            // 5
)

type myLogger struct {
    level       int64
    w           io.Writer
    debugLogger *log.Logger
    warnLogger  *log.Logger
    infoLogger  *log.Logger
    errLogger   *log.Logger
    fatalLogger *log.Logger
}

func New(w io.Writer, level int64, flag int) *myLogger {
    if w == nil {
        w = os.Stderr
    }

    if flag <= 0 {
        flag = log.LstdFlags
    }

    return &myLogger{
        w:           w,
        level:       level,
        debugLogger: log.New(w, "[DEBUG] ", flag|log.Lmsgprefix),
        warnLogger:  log.New(w, "[WARN] ", flag|log.Lmsgprefix),
        infoLogger:  log.New(w, "[INFO] ", flag|log.Lmsgprefix),
        errLogger:   log.New(w, "[ERROR] ", flag|log.Lmsgprefix),
        fatalLogger: log.New(w, "[FATAL] ", flag|log.Lmsgprefix),
    }
}

func (l *myLogger) SetLevel(level int64) {
    if level < LDEBUG || level > LFATAL {
        return
    }

    atomic.StoreInt64(&l.level, level)
}

func (l *myLogger) Debugln(v ...interface{}) {
    if atomic.LoadInt64(&l.level) > LDEBUG {
        return
    }
    l.debugLogger.Println(v...)
}

func (l *myLogger) Debugf(format string, v ...interface{}) {
    if atomic.LoadInt64(&l.level) > LDEBUG {
        return
    }
    l.debugLogger.Printf(format, v...)
}

func (l *myLogger) Infoln(v ...interface{}) {
    if atomic.LoadInt64(&l.level) > LINFO {
        return
    }
    l.infoLogger.Println(v...)
}

func (l *myLogger) Infof(format string, v ...interface{}) {
    if atomic.LoadInt64(&l.level) > LINFO {
        return
    }
    l.infoLogger.Printf(format, v...)
}

func main() {
    logger := New(nil, LWARN, 0)
    logger.Infoln("info level log demo")
    logger.Debugln("debug level log demo")
}


```

### 日志切分 

https://github.com/natefinch/lumberjack 推荐

https://github.com/lestrrat-go/file-rotatelogs

### 日志全局配置


https://stackoverflow.com/questions/30257622/golang-logrus-how-to-do-a-centralized-configuration 日志全局化配置
https://stackoverflow.com/questions/29538668/logging-globally-across-packages


### zerolog

### zap

推荐

https://github.com/uber-go/zap


### logrus

```go
// logrus
// https://github.com/Sirupsen/logrus
// 有大量反射, 性能相对低, 推荐 zerolog, zap
func main() {
   customFormatter := new(logrus.TextFormatter)
   customFormatter.FullTimestamp = true                    // 显示完整时间
   customFormatter.TimestampFormat = "2006-01-02 15:04:05" // 时间格式
   customFormatter.DisableTimestamp = false                // 禁止显示时间
   customFormatter.DisableColors = false                   // 禁止颜色显示
 
   logrus.SetFormatter(customFormatter)
   logrus.SetOutput(os.Stdout)
   logrus.SetLevel(logrus.DebugLevel)
 
   logrus.Debug("Debug日志")
   logrus.Info("Info日志")
   logrus.Warn("Warn日志")
   logrus.Error("Error日志")
   logrus.Fatal("Fatal日志") //log之后会调用os.Exit(1)
   logrus.Panic("Panic日志") //log之后会panic()
}


```

### 日志文件切分

https://github.com/natefinch/lumberjack

## 依赖注入

实际上是否需要依赖注入，取决于编程风格。依赖注入是一种编程模式。比较适合面向对象编程，在函数式编程中则不需要

uber 开源的 dig (https://pkg.go.dev/go.uber.org/dig) 
 
,elliotchance 开源的 dingo、sarulabs 开源的 di、google 开源的 wire 和 facebook 开源的 inject (最受欢迎的是 dig 和 wire)

 https://juejin.cn/post/6898514836100120590

 "Go语言的接口可以迟于struct实现来定义这一独一无二的语言特性，使得我们在使用依赖注入的时可以先方便的注入具体类型；而在后续需要扩展为“接口”，提供多个实现的时候，无需修改模块代码。 可以说，go语言与依赖注入范式是相当绝妙的搭配"


https://lailin.xyz/post/go-training-week4-wire.html
TODO

# 性能优化调优

## 计算内存占用

```go
// 使用 unsafe.Sizeof 计算出一个数据类型实例需要占用的字节数
```

## 内存对齐对性能影响

```go
/*
为什么需要内存对齐 (https://geektutu.com/post/hpg-struct-alignment.html)
CPU 访问内存时，并不是逐个字节访问，而是以字长（word size）为单位访问。比如 32 位的 CPU ，字长为 4 字节，那么 CPU 访问内存的单位也是 4 字节, 这么设计的目的，是减少 CPU 访问内存的次数

*/

// 一个结构体实例所占据的空间等于各字段占据空间之和，再加上内存对齐的空间大小
type Args struct {
    num1 int
    num2 int
}

type Flag struct {
    num1 int16
    num2 int32
}

func main() {
    fmt.Println(unsafe.Sizeof(Args{})) // 16
						// Args 由 2 个 int 类型的字段构成，在 64位机器上，一个 int 占 8 字节，因此存储一个 Args 实例需要 16 字节。
    fmt.Println(unsafe.Sizeof(Flag{})) //8
						// Flag 由一个 int32 和 一个 int16 的字段构成，成员变量占据的字节数为 4+2 = 6，但是 unsafe.Sizeof 返回的结果为 8 字节，多出来的 2 字节是内存对齐的结果
}
```



## 通过相关工具查看性能瓶颈

go 自带了 pprof 工具/包

此外还有 Graphviz 生成火焰图, go-torch 也是生成火焰图

```sh
# cpu
go tool pprof cpu.pprof
# 内存
go tool pprof mem.pprof


# 调用图
# 火焰图



```

方法 1: 直接在代码 本地生成 prof 文件, 分析粒度更细, 适合在本地分析

方法 2: 通过 http 输出 profile, 适合线上持续运行的程序, 主函数中导入 `import _ "net/http/pprof"` 然后启动 http server 即可, 然后访问 `http://ip:port/dubug/pprof` or `go tool pprof _http://ip:port/debug/pprof/profile?seconds=10`(默认采样时间间隔为 30s)

```go
// 先看方法 1:
// 除此之外, go test -bench=. -cpuprofile=cpu.prof 也能输出 prof 文件
const (
	row = 10000
	col = 10000
)

//填充矩阵
func fillMatrix(m *[row][col]int) {
	r := rand.New(rand.NewSource(time.Now().UnixNano()))
	for i := 0; i < row; i++ {
		for j := 0; j < col; j++ {
			m[i][j] = r.Intn(100000)
		}
	}
}

//模拟耗时计算
func calculate(m *[row][col]int) {
	for i := 0; i < row; i++ {
		tmp := 0
		for j := 0; j < col; j++ {
			tmp += m[i][j]
		}
	}
}
func main() {
	f, _ := os.Create("cpu.prof")
	defer f.Close()
	pprof.StartCPUProfile(f)
	defer pprof.StopCPUProfile()

	i := [row][col]int{}
	fillMatrix(&i)
	calculate(&i)

	memProf, _ := os.Create("mem.prof")
	defer memProf.Close()
	// 先回收一个再 dump 内存快照
	//runtime.GC()
	pprof.WriteHeapProfile(memProf)

	goroutineProf, _ := os.Create("goroutine.prof")
	defer goroutineProf.Close()
	lookup := pprof.Lookup("goroutine") // lookup 可以记录不同 tag, "goroutine"是代表协程信息的 tag
	if lookup != nil {
		lookup.WriteTo(goroutineProf, 0)
	}

}
/*
# 进入交互窗口
go tool pprof cpu.prof
	#接着输入, 查看 cpu 占用状态
	top [-cum]
	#输出依次是:
	函数本身执行时间  所占比例 [sum%存疑]  函数本身时间+调用的子函数执行时间(cumulation)   所占比例
      flat  flat%   sum%        cum   cum%
     1.91s 97.95% 97.95%      1.91s 97.95%  main.fillMatrix
     0.02s  1.03% 98.97%      0.03s  1.54%  main.calculate (inline)

	# 查看指定方法每一行的详细耗时信息 (不必指定全名, 会自动做最大程度的匹配)
	list fillMatrix

 */
```

## 编译优化

### 优化编译体积

### 逃逸分析友好的代码

```go
/*
变量会存储在两个地方
- 全局的堆(heap)空间用来动态分配内存，函数执行结束时自动回收
- 另一个是每个 goroutine 的栈(stack)空间 , 函数结束后还会留存一段时间, 经过 GC 算法分析, 某个时间点进行垃圾回收

逃逸分析:
编译器决定内存分配位置的方式，就称之为逃逸分析(escape analysis)。逃逸分析由编译器完成，作用于编译阶段
通过 go build -gcflags=-m main_pointer.go  查看逃逸情况

逃逸的分类

指针逃逸: 即在函数中创建了一个对象，返回了这个对象的指针。这种情况下，函数虽然退出了，但是因为指针的存在，对象的内存不能随着函数结束而回收，因此只能分配在堆上。

interface{} 动态类型逃逸:如果函数参数为 interface{}，编译期间很难确定其参数的具体类型，也会发生逃逸

闭包造成的逃逸: 闭包函数访问了外部变量 n，那变量 n 将会一直存在，直到 in 被销毁。很显然，变量 n 占用的内存不能随着函数 Increase() 的退出而回收，因此将会逃逸到堆上。
*/


```

## 编程实践

```
使用 strconv.Itoa() 会比 fmt.Sprintf() 要快一倍左右

使用StringBuffer 或是StringBuild 来拼接字符串，会比使用 + 或 += 性能高三到四个数量级

尽可能地避免把String转成[]Byte

在使用map的时候，使用整型的key会比字符串的要快，因为整型比较比字符串比较要快

避免在热代码中进行内存分配，这样会导致gc很忙。尽可能的使用 sync.Pool 来重用对象。

如果在for-loop里对某个slice 使用 append()请先把 slice的容量很扩充到位，这样可以避免内存重新分享以及系统自动按2的N次方幂进行扩展但又用不到，从而浪费内存。

尽可能的使用并发的 go routine，然后使用 sync.WaitGroup 来同步分片操作

避免使用 mutex，尽可能使用 sync/Atomic包(无锁编程)。

使用 I/O缓冲，I/O是个非常非常慢的操作，使用 bufio.NewWrite() 和 bufio.NewReader() 可以带来更高的性能

频繁使用的固定的正则表达式，一定要使用 regexp.Compile() 编译再使用。性能会得升两个数量级。
```

# GC

## gc 算法

```
标记清除算法，并且在此基础上使用了三色标记法和写屏障技术，提高了效率
```

## gc 分析

方法 1: 带上环境变量 `GODEBUG=gctrace=1 go test/run ....` , 运行会输出 gc 次数, 内存变化信息

方法 2: 使用 go tool trace; 包括在代码中 `tarce.start(f), tarce.stop()`, 或者在测试程序中输出 `go test -trace trace.out`, 最后通过 `go tool trace xxx.out` 可视化输出

## 写GC 友好代码的原则

- 避免内存分配(也就减少了 gc 负担), 
  - 比如使用指针作为方法参数, 避免拷贝
  - 为 slice, map 初始化合适的大小, 避免扩容

- 复用内存

# golang runtime 运行时

https://mp.weixin.qq.com/s/gTb9p0WpJ37M5_k9e6xUiQ

TODO

# golang 命令工具使用
https://hyper0x.github.io/go_command_tutorial/#/0.13

## 有哪些命令

`go <cmd> <args>`

```sh
# 编译当前目录 (会自动查找当前目录下的 main 方法作为待编译文件)
# 输出物名称为目录名称
go build
# or
go build .
# -o 指定输出物名字
go build -o xxx 
# 编译指定文件, 同时指定输出名字, 若不指定, 默认使用文件名
go build -o xxx aaa/bb.go

go build hello.go
go build github.com/xiaoyureed/stringutil

go env # 环境变量 GOARCH=amd64 GOOS=windows ...

# 跨平台编译需要先设定 env 值
env GOOS=linux GOARCH=amd64 go build

go clean # 清除编译文件... 用法类似 go build

go run main.go  # 运行, 必须是 package main, 有 main 函数

go install  # 编译同时安装到 gopath 下的 bin, 配合 export PATH="$PATH:$(go env GOPATH)/bin" 使用
go install google.golang.org/protobuf/cmd/protoc-gen-go@v1.26

# 下载github第三方包到 gopath, 末尾不带版本号则使用最新, 默认 master 分支上的代码, -u 更新 -v 显示进度
go get -u github.com/xiaoyureed/xxx 

go fmt  # 格式化 用法类似 go build
go vet  # 错误检查 用法类似 go build
go test # 单元测试 用法类似 go build； -v 同时打印信息

```



## 交叉编译

 (ref: https://studygolang.com/articles/13760)

```
GOOS：目标平台的操作系统（darwin、freebsd、linux、windows） 
GOARCH：目标平台的体系架构（386、amd64、arm） 
交叉编译不支持 CGO 所以要禁用它

# Windows 下编译 Mac 和 Linux 64位可执行程序
SET CGO_ENABLED=0
SET GOOS=darwin
SET GOARCH=amd64
go build main.go
 
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go


# Linux 下编译 Mac 和 Windows 64位可执行程序
CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go

# Mac 下编译 Linux 和 Windows 64位可执行程序
CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go
CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build main.go

```


# 开源自己的类库

https://zhuanlan.zhihu.com/p/354147069

```sh
# 先创建github 仓库 https://github.com/vsixz/common-go.git
git clone https://github.com/vsixz/common-go.git
cd common-go
# module名称需要与github仓库一致
go mod init github.com/vsixz/common-go
...

# 发行版本
# 最佳实践是创建对应的版本发布分支，然后使用发布分支创建tag
git checkout -b release/v1.x
git push -u origin release/v1.x
git tag v1.0.0 
git push --tags # 此时，在github仓库release中可以看到发布的版本



```


# 开发restful api


## 项目结构

```
├── conf                    #项目配置文件目录
│   └── config.toml         #大家可以选择自己熟悉的配置文件管理工具包例如：toml、xml、ini等等
├── requests                #定义入参即入参校验规则
│   └── user_request.go
│   └── food_request.go
├── responses                #定义响应的数据
│   └── user_response.go
│   └── food_response.go
├── services                #服务定义目录
|	└── v1					#服务v1版本
│   |	└── user_service.go
│   |	└── food_service.go
|	└── v2					#服务v2版本
│   |	└── user_service.go
│   |	└── food_service.go
├── api             		#api目录，按模块存放控制器（或者叫控制器函数），必要的时候可以继续划分子目录。
│   └── v1					#apiv1版本
│   |	└── user.go
│   |	└── food.go
│   └── v2					#apiv2版本
│   |	└── user.go
│   |	└── food.go
├── router					#路由目录
│   └── v1					#路由v1版本
│   |	└── user.go
│   |	└── food.go
│   └── v2					#路由v2版本
│   |	└── user.go
│   |	└── food.go
├── init.go					#路由初始化
├── pkg						#自定义的工具类等
│   └── e					#项目统一的响应定义，如错误码，通用的错误信息，响应的结构体
│   └── util				#工具类目录
├── models                  #模型目录，负责项目的数据存储部分，例如各个模块的Mysql表的读写模型。
│   ├── food.go
│   ├── user.go
│	└── init.go				#模型初始化
├── repositories            #数据操作层，定义各种数据操作。
│   └── user_repository.go
│   └── food_repository.go
├── logs                    #日志文件目录，主要保存项目运行过程中产生的日志。
├── main.go                 #项目入口，这里负责Gin框架的初始化，注册路由信息，关联控制器函数等。
```

## gin 中的 json

https://www.flysnow.org/2019/12/29/golang-gin-json-rendering.html
https://www.flysnow.org/2019/12/29/golang-gin-json-rendering.html

## 中间件

```go
// 跨域
func Cors() gin.HandlerFunc {
	config := cors.DefaultConfig()
	config.AllowAllOrigins = true
	config.AllowHeaders = append(config.AllowHeaders, "Authorization")
	return cors.New(config)
}



// 错误处理

func AppErrorJsonReporter() gin.HandlerFunc {
	return func(c *gin.Context) {
		c.Next()

		collectedErrors := c.Errors.ByType(gin.ErrorTypeAny)
		if len(collectedErrors) > 0 {
			var errResp AppError

			err := collectedErrors[0].Err
			switch errTyped := err.(type) {
			case AppError:
				errResp = errTyped
			default:
				errResp = AppError{
					Code: http.StatusInternalServerError,
					Msg:  err.Error(),
				}
			}
			c.AbortWithStatusJSON(errResp.Code, errResp)
		}
	}
}

type AppError struct {
	Code int
	Msg  string
}

var _ error = (*AppError)(nil)

func (a AppError) Error() string {
	return fmt.Sprintf("%d: %s", a.Code, a.Msg)
}



// ============

// api 层日志记录

func HttpApiLogRecord() gin.HandlerFunc {
	return func(c *gin.Context) {
		start := time.Now()

		c.Next()

		elapse := time.Now().Sub(start)
		reqMethod := c.Request.Method
		reqUri := c.Request.RequestURI
		reqAgent := c.Request.UserAgent()
		respStatusCode := c.Writer.Status()
		reqIp := c.ClientIP()
		logx.Info("elapse: %v, reqMethod: %v, reqUri: %v, reqIp: %v, reqAgent: %v, respCode: %v",
			elapse.Milliseconds(), reqMethod, reqUri, reqIp, reqAgent, respStatusCode)
	}
}


```


# 开发单体app

https://github.com/sipin/gorazor 视图引擎
https://github.com/mjibson/esc 静态资源内嵌


# 开发微服务 microservice

## 服务之间通信

```
Twirp grpc 取舍 https://taoshu.in/twirp.html

https://ghz.sh/ 压测工具
https://github.com/crossoverJie/ptg/

```

## 微服务框架选型

第三代微服务直接用 k8s 做负载均衡，k8s etcd 做注册中心，k8s configmap 做配置中心
https://jishuin.proginn.com/p/763bfbd6b81b

kratos 设计理念不错, b 站

腾讯 tars-go

阿里 dubbo-go

https://github.com/asim/go-micro go-micro

go-kit

kite, 
kitex 字节

Gizmo 的使用场景在于 Go Micro 和 Go Kit 中间。它不像 Go Micro 那样是一个完整的『黑匣子』。同时，它也不像 Go Kit 那样原始

https://blog.csdn.net/qq2942713658/article/details/112721577


## go-micro

- micro api

## 网关

traefik


# 开源库

## 监听文件改动

https://github.com/fsnotify/fsnotify
fsnotify 的一点不足在于侦听文件夹并不会递归进行， 也就是当使用它侦听了某一文件夹时，这个文件夹子目录下的修改并不会被捕捉到，因此我们必须手动完成这一工作。

## Python 解释器

https://github.com/sbinet/go-python

## 权限管理

```
casbin
```

## 网络

```

https://github.com/valyala/fasthttp 比标准库更快 http client


https://github.com/panjf2000/gnet 底层网络框架, 比标准库 net 更好用

tcp 服务器框架 https://github.com/aceld/zinx

```


## 热加载 live-reloading hot reload

https://github.com/cosmtrek/air

https://github.com/codegangsta/gin

https://github.com/gravityblast/fresh

## 容器

```
https://github.com/wagoodman/dive 查阅镜像每层的内容, 优化...
```

## 数据库

https://github.com/go-gorm/gorm orm 框架, 类比 hibernate

https://github.com/jmoiron/sqlx 简化 SQL 操作, 类比 mybatis

https://github.com/go-sql-driver/mysql 驱动, 配合 database/sql 使用

https://github.com/hashicorp/go-memdb 内存数据库支持事务


## 缓存

go-redis

golang/groupcache

golang.org/x/sync/singleflight 防止缓存击穿  (https://www.huolg.net/backend/702)


## 解析库

```

https://github.com/spf13/cobra 命令行解析


https://github.com/pelletier/go-toml  配置文件解析
github.com/go-ini/ini

https://github.com/spf13/viper 处理配置文件, 支持多格式, 也能处理环境变量

https://github.com/kelseyhightower/envconfig 环境变量解析
github.com/joho/godotenv
```

## 颜色

https://github.com/fatih/color

## 好的编程体验

### 数据库表转 struct

https://github.com/gohouse/converter

### struct 解析

https://github.com/fatih/structs

https://github.com/fatih/structtag tag解析

https://github.com/mitchellh/mapstructure

https://github.com/jinzhu/copier 克隆复制

### 格式化日期

https://github.com/dustin/go-humanize 人类友好的格式化库(比如格式化成 xxx hours ago ...)


### 流式处理 流式编程

https://github.com/reugn/go-streams 流式处理 流式编程 附带滑动窗口实现


### 池

goroutine 池 https://github.com/panjf2000/ants


### 依赖注入

```

https://github.com/google/wire 编译时注入(使用代码生成实现)


 依赖反射实现的运行时依赖注入：inject、uber、dig

```


## 定时任务 

https://github.com/robfig/cron

```go
package main

import (
	"github.com/robfig/cron/v3"
	"log"
	"time"
)

func main() {
	c := cron.New()
	entryId, _ := c.AddFunc("@every 1s", func() {
		log.Println("hello")
	})
	c.Start()
	after := time.After(time.Second * 3)
	<-after
	c.Remove(entryId)
	select {
	}
}

```

## api 和文档

gin

https://github.com/go-swagger/go-swagger

参数校验 github.com/go-playground/validator/v10



## 系统信息 运维

```

https://github.com/shirou/gopsutil psutil 的 golang 版本

https://github.com/yudai/gotty 暴露 terminal 成为 web 服务
```



## 时间工具

```
https://github.com/jinzhu/now
```


## 持续追踪读取日志


github.com/hpcloud/tail 日志文件读取

## 分布式

https://github.com/yedf/dtm 分布式事务管理

https://github.com/kelseyhightower/confd 配置文件管理


## 实现插件机制

https://wangbjun.site/2021/coding/golang/go-rpc-plugin.html
TODO




## 和其他语言交互

```
https://github.com/rogchap/v8go 执行 js 脚本
https://github.com/kuoruan/v8go-polyfills

https://github.com/robertkrimen/otto

https://github.com/gopherjs/gopherjs




```

## 音频视频图片处理

```
https://github.com/h2non/bimg 图片
```

## 常用工具库

```
https://github.com/kakuilan/kgo
```

## 代码生成

```
https://github.com/smallnest/gen 生成 rest api

https://github.com/ent/ent
```

## 注解编程

https://github.com/MarcGrol/golangAnnotations

https://github.com/u2takey/go-annotation

## 生成假数据

https://github.com/aszhc/go-faker-cn

https://github.com/bxcodec/faker

https://github.com/brianvoe/gofakeit


## 网络抓包

https://github.com/google/gopacket


## gui框架

https://github.com/fyne-io/fyne


# 参考链接


https://github.com/LearnGolang/LearnGolang

https://github.com/shockerli/go-awesome

https://github.com/golang-design/Go-Questions

https://www.geekclub.cc/2020/06/1160 技术栈

https://github.com/overnote/over-golang

https://github.com/0voice/Introduction-to-Golang

https://blog.51cto.com/u_13283759/3187086

<!-- <<go 程序设计语言>> -->
<!-- <<面向模式的软件架构(模式系统)>> -->

https://github.com/golang101/golang101

https://github.com/yongxinz/gopher

https://github.com/kirintang/go-read-recommend

https://github.com/shockerli/go-awesome

https://github.com/wh211212?after=Y3Vyc29yOnYyOpK5MjAxOS0wOS0wN1QxMjoyODowOSswODowMM4LDi9E&tab=stars 星星还行
https://cloud.tencent.com/developer/article/1904240?from=article.detail.1196581 腾讯工程部入门好文章

https://go.dev/doc/faq go faq 官方
https://github.com/golang/go/wiki/Articles 精华文章
https://github.com/golang/go/wiki/Blogs 博客集合
https://github.com/golang/go/wiki/GoTalks 访谈

代码规范
https://github.com/golang/go/wiki/CodeReviewComments
https://go.dev/doc/effective_go

https://github.com/eachain/Gotchas 小技巧
https://github.com/eachain

https://github.com/wangbjun 小工具 学习

https://draveness.me/golang-101/ golang 工程化实践


https://talkgo.org/ golang 夜读

https://github.com/yifhao?tab=stars golang java 大牛
https://github.com/yifhao/share 大牛分享

https://dave.cheney.net/practical-go/presentations/qcon-china.html 最佳实践
https://github.com/llitfkitfk/go-best-practice 翻译

https://github.com/gocn 中文社区组织
https://github.com/gocn/translator 翻译的英文文章

https://github.com/gwuhaolin/blog/issues/12 教你写 shadowsocks

https://github.com/ma6254/FictionDown 笔趣阁小说爬取清洗

https://github.com/jiujuan/go-collection 资料搜集

https://github.com/halfrost/LeetCode-Go 算法

https://github.com/hackstoic/golang-open-source-projects  中文版awesome-go
https://github.com/avelino/awesome-go
https://github.com/jobbole/awesome-go-cn

official doc: http://docs.studygolang.com/doc/
中文 http://docscn.studygolang.com/

dev web app by golang: https://slides.com/akshaydeo/writing-web-apps-in-golang

https://github.com/unknwon/the-way-to-go_ZH_CN

实现一个简单的 video server : https://github.com/xiaoyureed/video_server

tips: https://zhuanlan.zhihu.com/p/27518650, https://blog.gaobinzhan.com/category/22/

https://github.com/astaxie/build-web-application-with-golang

https://github.com/wyh267/FalconEngine 简单搜索引擎


https://github.com/TimothyYe 小工具

https://github.com/geektutu/7days-golang 手写中间件

https://awesome-go.com/

https://github.com/geektutu/high-performance-go性能分析
