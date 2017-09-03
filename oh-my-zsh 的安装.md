# oh-my-zsh 的安装

## 1. zsh 的安装

```shell
sudo yum install zsh
# 或者使用
# sudo apt-get install zsh
```

## 2. 下载 `oh-my-zsh` 来配置 `zsh`

```shell
# wget 自动安装
wget https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh -O - | sh
```

如果提示还没有安装 `git`，需要先安装 `git`。

## 3. 设置默认 `shell` 为 `zsh`

```shell
# 使用 chsh
chsh
# 或者在 su 管理员身份下修改 /etc/passwd 文件
```

## 4. 主题选择

在配置文件 `~/.zshrc` 文件修改 `ZSH_THEME`，主题推荐：

```shell
# ZSH_THEME="robbyrussell"
```

