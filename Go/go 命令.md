
#### go build：编译包和依赖项。 
如果是main包，默认编译执行命令时所在目录的所有包，生成可执行文件。也可指定要编译的文件，在命令后加上文件即可。

#### go get :下载并安装包和依赖。
分为两步，下载所需的依赖包，编译并安装。下载依赖源码下载工具。在go get之前，必须安装必要的下载工具，更详细介绍可见http://www.jb51.net/article/56781.htm

#### go install:编译并且安装包和依赖。
分两步，编译生成结果文件，将结果文件移到GOPATH/pkg或者GOPATH/binmulu xia .

#### gofmt

gofmt –w program.go

会格式化该源文件的代码然后将格式化后的代码覆盖原始内容（如果不加参数 -w 则只会打印格式化后的结果而不重写文件）；

gofmt -w *.go 会格式化并重写所有 Go 源文件；

gofmt map1 会格式化并重写 map1 目录及其子目录下的所有 Go 源文件。

gofmt 也可以通过在参数 -r 后面加入用双引号括起来的替换规则实现代码的简单重构，规则的格式：<原始内容> -> <替换内容>。

#### go doc pkgname：可以用来查看pkgname手册。
尝试了下，在ubuntu14.04上面，go1.5.1情况下，执行apt-get install golang-go.tools即可安装go doc工具。

apprtc的信令服务器collider编译安装的步骤为 
#### go get collidermain 作用是下载依赖项 
#### go install collidermain 
作用是编译和安装，最后在GOPATH/bin下生成可执行文件。