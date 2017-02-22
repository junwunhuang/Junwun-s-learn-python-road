##### 1、用git下载安装pyenv

进入root模式：

```linux
git clone git://github.com/yyuu/pyenv.git .pyenv
```

##### 2、设置环境变量

我按照github上pyenv作者所写的环境变量设置在centos7.3上弄就出现了各种问题，而在centos6.5上设置就没问题。

所以推荐下面这种方法：

```linux
vim /etc/profile.d/pyenv.sh

#!/bin/bash
# File Name: /etc/profile.d/pyenv.sh
# Define environment variable

export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval"$(pyenv init -)"
```

pyenv在github的[官网地址](https://github.com/yyuu/pyenv) ：https://github.com/yyuu/pyenv

