# ssh_key_dispense

## 使用方法
### **1,环境准备**

**RHEL6/7、CENTOS6/7** 
``` bash
# 安装pip
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py

# 安装环境包
yum install gcc libffi-devel python-devel openssl-devel
pip install fabric
pip install pexpect
```
> python3 fabric版本需要更换，<code>pip install fabric3</code>

### **2,clone本程序到本地目录**
``` bash
git clone https://github.com/xiaotuanyu120/ssh-key-dispense.git
```

### **3,配置main.py**
将需要生成key的host及其密码写进main.py，格式为hosts={host: password, ...}

### **4,命令操作**
``` bash
# 执行下面命令列出可用操作
fab -f main.py -l
    
    Available commands:
        
        ssh_key_copy:     拷贝以host命名的key到相应host，并创建~/.ssh/config文件
        ssh_key_copy_rsa: 拷贝默认的id_rsa的key到所有的host
        ssh_key_gen:      在/root/.ssh/下生成相应host的key，key为"host"&"host.pub"
        ssh_key_gen_rsa:  在/root/.ssh/下生成默认id_rsa id_rsa.pub

# 执行方式
fab -f main.py command
```

### **5,连接方法**
程序中已经配置过~/.ssh/config，所以直接执行下面命令即可
``` bash
ssh host
```

> 如果host对应的key存在，keygen_ssh.py会将老key文件更名为"host.old"&"host.pub.old"
