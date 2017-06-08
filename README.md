# haskell 在线实验环境

## 软件简介

Haskell是一种标准化的、通用纯函数式编程语言，有非限定性语义和强静态类型。它的命名源自美国逻辑学家Haskell Brooks Curry，他在数学逻辑方面的工作使得函数式编程语言有了广泛的基础。在Haskell中，函数是一等公民。作为函数式编程语言，主要控制结构是函数。Haskell语言是1990年在编程语言Miranda的基础上标准化的，并且以λ演算（Lambda-Calculus)为基础发展而来。具有“证明即程序、结论公式即程序类型”的特征。这也是Haskell语言以希腊字母「λ」（Lambda）作为自己标志的原因。Haskell语言的最主要的执行环境是GHC。

所属类别是编程语言

特点：

1.Haskell支持惰性求值、模式匹配、列表内包、类型类和类型多态

2.Haskell拥有一个强、静态类型系统

3.Haskell是现有的一门开放的、已发布标准的，且有多种实现的语言。

4.Haskell的主要实现——GHC——是个解释器，也是个原生代码编译器。它可以在大多数平台运行

## 软件官网

https://www.haskell.org/

## Dockerfile 使用方法

开始交互式口译会话ghci：
```
$ docker run -it --rm haskell:8
GHCi, version 8.0.2: http://www.haskell.org/ghc/  :? for help
Prelude>
```
将应用程序从Hackage中移植到一个Dockerfile：
```
FROM haskell:8
RUN stack install pandoc pandoc-citeproc
ENTRYPOINT ["pandoc"]
```
或者，使用cabal：
```
FROM haskell:8
RUN cabal update && cabal install pandoc pandoc-citeproc
ENTRYPOINT ["pandoc"]
```
Dockerfile使用构建缓存迭代开发Haskell应用程序：
```
FROM haskell:7.10

WORKDIR /opt/server

RUN cabal update

# Add just the .cabal file to capture dependencies
COPY ./snap-example.cabal /opt/server/snap-example.cabal

# Docker will cache this command as a layer, freeing us up to
# modify source code without re-installing dependencies
# (unless the .cabal file changes!)
RUN cabal install --only-dependencies -j4

# Add and Install Application Code
COPY . /opt/server
RUN cabal install

CMD ["snap-example"]
```
## 资源链接

- https://www.haskell.org/
