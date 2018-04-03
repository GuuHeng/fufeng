· [homebrew](https://brew.sh)

## MAC安装步骤：
1、打开终端 复制粘贴
    
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

2、遇到问题
 
    error: RPC failed; curl 18 transfer closed with outstanding read data remaining
    fatal: The remote end hung up unexpectedly
    fatal: early EOF
    fatal: index-pack failed
    
处理方法-终端输入命令行：

    git config --global http.postBuffer 524288000

查看修改后配置-命令行：
    
    git config --list
