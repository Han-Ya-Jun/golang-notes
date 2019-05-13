#### 什么是Go?
Go是一门 并发支持 垃圾回收的编译型系统编程语言，旨在创
造一门具有在静态编译语言的 高性能 和动态语言的 高效开发 之间拥有
良好平衡点的一门编程语言
#### Go语言发展历史
Go，全称golang，是Google开发的一种静态强类型、编译型、并发型并具有垃圾回收功能的编程语言。 Go从2007年末由Robert Griesemer、Rob Pike、Ken Thompson（C语言发明者）主持开发，于2009年11月正式宣布成为开放源代码项目，并在Linux及Mac OS X平台上进行了实现，后续增加了Windows平台的实现。2012年初，Go语言官方发布了Go 1.0稳定版本，目前Go语言基于1.x每半年发布一个版本。

![](http://cdn.hanyajun.com/20190513_234208_go_version.png)
#### 语言特性
- 静态类型和编译型
- 原生的并发编程
- 高效的垃圾回收机制  
- 快速编译和运行（同时解决C语言中头文件太多的问题）
- 跨平台
- 多编程范式：支持函数式编程，函数类型为第一类型，可以方便地传递和赋值。此外，还支持面向对象编程，有接口类型和实现类型的概念，但用嵌入替代了继承。
- 丰富的标准库。
#### Go语言优势
1. 脚本化的语法；开发效率高，容易上手
1. 静态类型+编译型，程序运行速度有保障；静态类型+编译型语言相对于动态类型+解释型语言的效率高
1. 原生的支持并发编程；降低开发、维护成本/程序可以更好的执行
1. 对于云原生支持比较好，容器化，微服务化比较容易。
#### Go擅长领域
Go 语言被设计成一门应用于搭载 Web 服务器，存储集群或类似用途的巨型中央服务器的系统编程语言。
对于高性能分布式系统领域而言，Go语言无疑比大多数其它语言有着更高的开发效率。它提供了海量并行的支持，这对于游戏服务端的开发而言是再好不过了。

Go语言主要用途如下：

1. 服务器编程，如处理日志、数据打包、虚拟机处理、文件系统等
1. 分布式系统，数据库代理器等
1. 网络编程，如Web应用、API应用、下载应用
1. 内存数据库，如groupcache、couchbase的部分组建
1. 云平台，目前国外很多云平台在采用Go开发，CloudFoundy的部分组建，前VMare的技术总监自己出来搞的apcera云平台。
#### GO语言的缺点
1. 它不支持泛型，即使有很多关于它的讨论。可能也在议程当中，期待那一天的到来。
1. 使用这种编程语言分发的软件包非常有用，但Go在传统意义上并不是面向对象的。
1. 缺少一些库，尤其是UI工具包。
#### 使用Go语言开发的流行应用
- [Docker](https://github.com/docker/docker-ce)：一组用于部署Linux容器的工具
- [Openshift](https://github.com/openshift/origin)：由Red Hat提供的云计算平台即服务。
- [Kubernetes](https://github.com/kubernetes/kubernetes/)：无缝自动化部署流程的未来
- [Tidb](https://github.com/pingcap/tidb)： 开源分布式关系型数据库。
- [InfluxDB](https://github.com/influxdata/influxdb)：是由InfluxData开发的开源时间序列数据库。
- [Etcd](https://github.com/etcd-io/etcd)：分布式的键值对数据存储系统，提供共享配置、服务的注册和发现。
#### 使用Go语言的公司
- **Google**
- **Facebook**
- **腾讯**（腾讯音乐）
- **百度**
- **蚂蚁金服**
- **京东**（消息推送系统、云存储）
- **小米**（http://open-falcon.com/）小米互娱、小米商城、小米视频、小米生态链等团队都在使用Golang。
- **七牛云**
- **bilibili**
- **今日头条**
- **美团**
- **滴滴**
- **快手**
- **英语流利说**
#### GOPATH
1. **src目录**： 用于以代码包的显示组织并保存go源码文件。
2. **pkg目录**: 用于存放通过go install 安装后的代码包的归档文件。
3. **bin目录**: 与pkg相似，在通过go install 命令安装后生成的可执行文件。
#### 包导入

```go
import(
. "github.com/Han-Ya-Jun/***"
_ "github.com/Han-Ya-Jun/***"
)

```
- **.** 导入表示我们不想加前缀而直接使用某个依赖包的程序实体。
- **_** 这种导入表示我们只想初始化这个代码包，包初始化时会自动执行init（）方法，所有的代码包的初始化函数都会在main函数执行前，并且只会执行一次。

#### 标准命令
##### go build
go build 命令主要是用于测试编译。在包的编译过程中，若有必要，会同时编译与之相关联的包。
-  如果是普通包，当你执行go build命令后，不会产生任何文件。
- 如果是main包，当只执行go build命令后，会在当前目录下生成一个可执行文件。如果需要在$GOPATH/bin木下生成相应的exe文件，需要执行go install 或者使用 go build -o 路径/a.exe。
- 如果某个文件夹下有多个文件，而你只想编译其中某一个文件，可以在 go build 之后加上文件名，例如 go build a.go；go build 命令默认会编译当前目录下的所有go文件。
- 你也可以指定编译输出的文件名。比如，我们可以指定go build -o myapp.exe，默认情况是你的package名(非main包)，或者是第一个源文件的文件名(main包)。
- go build 会忽略目录下以”_”或者”.”开头的go文件。

如果你的源代码针对不同的操作系统需要不同的处理，那么你可以根据不同的操作系统后缀来命名文件。例如有一个读取数组的程序，它对于不同的操作系统可能有如下几个源文件：

- array_linux.go 
- array_darwin.go 
- array_windows.go 
- array_freebsd.go

go build的时候会选择性地编译以系统名结尾的文件（Linux、Darwin、Windows、Freebsd）。例如Linux系统下面编译只会选择array_linux.go文件，其它系统命名后缀文件全部忽略。
<hr>

#####  go clean
go clean 命令是用来移除当前源码包里面编译生成的文件，这些文件包括

- _obj/ 旧的object目录，由Makefiles遗留
- _test/ 旧的test目录，由Makefiles遗留
- _testmain.go 旧的gotest文件，由Makefiles遗留
- test.out 旧的test记录，由Makefiles遗留
- build.out 旧的test记录，由Makefiles遗留
- *.[568ao] object文件，由Makefiles遗留
- DIR(.exe) 由 go build 产生
- DIR.test(.exe) 由 go test -c 产生
- MAINFILE(.exe) 由 go build MAINFILE.go产生

<hr>

##### go fmt

go fmt 命令主要是用来帮你格式化所写好的代码文件。

比如我们写了一个格式很糟糕的 test.go 文件，我们只需要使用 fmt go test.go 命令，就可以让go帮我们格式化我们的代码文件。但是我们一般很少使用这个命令，因为我们的开发工具一般都带有保存时自动格式化功能，这个功能底层其实就是调用了 go fmt 命令而已。

使用go fmt命令，更多时候是用gofmt，而且需要参数-w，否则格式化结果不会写入文件。gofmt -w src，可以格式化整个项目。

<hr>

##### go get 

go get 命令主要是用来动态获取远程代码包的，目前支持的有BitBucket、GitHub、Google Code和Launchpad。这个命令在内部实际上分成了两步操作：第一步是下载源码包，第二步是执行go install。下载源码包的go工具会自动根据不同的域名调用不同的源码工具，对应关系如下：


```
BitBucket (Mercurial Git)
GitHub (Git)
Google Code Project Hosting (Git, Mercurial, Subversion)
Launchpad (Bazaar)
```


所以为了go get 能正常工作，你必须确保安装了合适的源码管理工具，并同时把这些命令加入你的PATH中。其实go get支持自定义域名的功能，具体参见go help remote。
go get 命令本质上可以理解为：首先通过源码工具clone代码到src目录，然后执行go install。
<hr>

##### go install

go install 命令在内部实际上分成了两步操作：第一步是生成结果文件(可执行文件或者.a包)，第二步会把编译好的结果移到 $GOPATH/pkg 或者$GOPATH/bin。

.exe文件： 一般是 go install 带main函数的go文件产生的，有函数入口，所有可以直接运行。

.a应用包： 一般是 go install 不包含main函数的go文件产生的，没有函数入口，只能被调用。

<hr>

##### go test
go test 命令，会自动读取源码目录下面名为*_test.go的文件，生成并运行测试用的可执行文件。输出的信息类似


```
ok   archive/tar   0.011s
FAIL archive/zip   0.022s
ok   compress/gzip 0.033s
...
```


默认的情况下，不需要任何的参数，它会自动把你源码包下面所有test文件测试完毕，当然你也可以带上参数，详情请参考go help testflag

<hr>

##### go doc
go doc 命令其实就是一个很强大的文档工具。

如何查看相应package的文档呢？ 例如builtin包，那么执行go doc builtin；如果是http包，那么执行go doc net/http；查看某一个包里面的函数，那么执行godoc fmt Printf；也可以查看相应的代码，执行godoc -src fmt Printf；

通过命令在命令行执行 godoc -http=:端口号 比如godoc -http=:8080。然后在浏览器中打开127.0.0.1:8080，你将会看到一个golang.org的本地copy版本，通过它你可以查询pkg文档等其它内容。如果你设置了GOPATH，在pkg分类下，不但会列出标准包的文档，还会列出你本地GOPATH中所有项目的相关文档，这对于经常被限制访问的用户来说是一个不错的选择。

##### 详细的go标准命令
https://github.com/hyper0x/go_command_tutorial