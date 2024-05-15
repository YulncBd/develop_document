## 创建package

Flutter Packages 的官方开发文档

https://docs.flutter.cn/packages-and-plugins/developing-packages#step-1-create-the-package

package 有两种：纯dart包和插件包（和原生交互）

这里创建的sliver_grid_view 是一个纯dart包

```shell
# 创建package
flutter create --template=package sliver_grid_view

# 添加example
flutter create example
```

创建完成的项目如下图所示：

![alt text](/assets/flutter/package/flutter_package1.png)

## 编写代码

在lib文件下新家一个src文件夹，存放代码

![alt text](/assets/flutter/package/flutter_package2.png)

在lib文件夹下的sliver_grid_view.dart中export需要公开的类

```dart
library sliver_grid_view;
export 'src/sliver_grid_view.dart';
```

## 完善项目

### 完善example

example 是告诉别人怎么使用插件

首先在example的pubspec.yaml中引入插件
```yaml
dependencies:
  flutter:
    sdk: flutter

  cupertino_icons: ^1.0.6
  # 引入插件
  sliver_grid_view:
    path: ../
```

然后在main.dart 中使用
```dart
import 'package:sliver_grid_view/sliver_grid_view.dart';

编写具体的使用代码
```

### 完善插件的pubspec.yaml

name: 插件名字
description：插件描述，不可太长也不可太短
version：插件版本，每次更新version要增加
homepage：项目的git地址

```yaml
name: sliver_grid_view
description: "you can set gird-view's header and footer, section's header and footer,and different grid delegate for each section "
version: 0.0.3
homepage: 'https://github.com/YulncBd/sliver_grid_view.git'
```

### 完善插件的CHANGELOG

CHANGELOG.md 记录插件的更新内容

### 完善插件的README

README 来介绍软件以及使用情况

### 完善插件的LICENSE

LICENSE 是许可证文件
```txt
sliver_grid_view

Copyright <2024> <irwin>

Redistribution and use in source and binary forms, with or without modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.

3. Neither the name of the copyright holder nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
```

注意，你需要将sliver_grid_view、2024和irwin替换成你自己的插件名称、年份和姓名。

## 发布

### 运行dry-run命令检验内容

```shell
flutter pub publish --dry-run
```

如果运行成功，输出以下内容

```shell
Package has 0 warnings.
The server may enforce additional checks.
```

如果运行失败，根据提示修改即可

### 提交到pub

提前准备好梯子，以及google账号

windows 请使用cmd（win + r），而不是powershell

运行下面的命令

```shell
flutter pub publish --server=https://pub.dartlang.org
```

上传成功后需要等几分钟才能搜索到项目


### 更新项目

修改代码

更改pubspec.yaml 中的version

修改CHANGELOG 和 README

将代码提交到git

将代码提交到pub

### 运行过程中遇到的问题

问题1：

```shell
Do you want to publish sliver_grid_view 0.0.1 to https://pub.dev (y/N)? 
```

输入 y 即可

问题2：

```shell
In a web browser, go to https://accounts.google.com/o/oauth2/auth? xxx...xxx.email
Then click "Allow access".
Waiting for your authorization...
```

复制链接在浏览器打开，输入google账号即可

问题3：

```shell
Authorization received, processing...
It looks like accounts.google.com is having some trouble.
Pub will wait for a while before trying to connect again.
OS Error: Operation timed out, errno = 60, address = accounts.google.com, port = 54374
pub finished with exit code 69
```

授权失败，需要打开梯子，并设置cmd代理

```shell
# 设置cmd代理，端口1080根据实际填写
set http_proxy=http://127.0.0.1:1080
set https_proxy=https://127.0.0.1:1080
```

powershell设置代理的方式与cmd不一样，请搜索引擎搜索