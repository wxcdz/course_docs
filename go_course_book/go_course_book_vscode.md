
## 00.Go环境配置和快捷键设置

### Vscode配置插件

#### 配置用户环境变量
GOPATH变量设置用户工作目录。如果写代码时要用到第三方库，然后使用go get xxx时，xxx就下载到这个目录。

```
变量 GOPATH        值 C:\Program Files\Go\bin
```

GOROOT变量设置Go编译器的安装位置
```
变量 GOROOT        值 C:\Program Files\Go
```

#### 配置go的环境变量
在命令行下使用go env命令可以看到所有关于go的环境变量。
```
go env -w GOPROXY=https://goproxy.io,direct
go env -w GOPRIVATE=*.corp.example.com
go env -w GO111MODULE=on
```

#### 安装第三方库
```
go get -u gorm.io\gorm
```

| 安装的组件                                                  | 默认安装状态 | 组件备注                                         | github.com->golang.org          |
| ----------------------------------------------------------- | ------------ | ------------------------------------------------ | ------------------------------- |
| go get -u -v github.com/nsf/gocode                          | SUCCEEDED    | 自动补全                                         |                                 |
| go get -u -v github.com/uudashr/gopkgs/cmd/gopkgs           | SUCCEEDED    | 自动补全未导入的包                               |                                 |
| go get -u -v github.com/ramya-rao-a/go-outline              | SUCCEEDED    | 当前文件中按符号搜索                             | https://github.com/golang/tools |
| go get -u -v github.com/acroca/go-symbols                   | SUCCEEDED    | 当前workspace中按符号搜索                        |                                 |
| go get -u -v golang.org/x/tools/cmd/guru                    | SUCCEEDED    | 查找所有引用组件                                 |                                 |
| go get -u -v golang.org/x/tools/cmd/gorename                | SUCCEEDED    | 重命名符号                                       |                                 |
| go get -u -v github.com/fatih/gomodifytags                  | SUCCEEDED    | 修改结构上的标签                                 |                                 |
| go get -u -v github.com/haya14busa/goplay/cmd/goplay        | SUCCEEDED    | for running current file in the Go playground    |                                 |
| go get -u -v github.com/josharian/impl                      | SUCCEEDED    | for generating stubs for interfaces              |                                 |
| go get -u -v github.com/davidrjenni/reftools/cmd/fillstruct | SUCCEEDED    | for filling a struct literal with default values |                                 |
| go get -u -v github.com/rogpeppe/godef                      | SUCCEEDED    | 转到定义2                                        |                                 |
| go get -u -v golang.org/x/tools/cmd/godoc                   | SUCCEEDED    | 鼠标悬停显示文档注释2                            |                                 |
| go get -u -v sourcegraph.com/sqs/goreturns                  | SUCCEEDED    | 格式化代码2                                      |                                 |
| go get -u -v github.com/golang/lint/golint                  | SUCCEEDED    | for linting                                      | https://github.com/golang/lint  |
| go get -u -v github.com/cweill/gotests/...                  | SUCCEEDED    | 生成单元测试                                     |                                 |
| go get -u -v github.com/derekparker/delve/cmd/dlv           | SUCCEEDED    | 调试                                             |                                 |
| go get -u -v github.com/zmb3/gogetdoc                       |              | 转到定义2/鼠标悬停显示注释2                      |                                 |
| go get -u -v golang.org/x/tools/cmd/goimports               |              | 格式化代码2                                      |                                 |