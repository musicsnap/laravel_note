##### 安装 vagrant box 后，up 的时候出现下面错误：
```bash
==> default: Clearing any previously set forwarded ports...
==> default: Clearing any previously set network interfaces...
==> default: Preparing network interfaces based on configuration...
    default: Adapter 1: nat
    default: Adapter 2: bridged
==> default: Forwarding ports...
    default: 22 => 2222 (adapter 1)
==> default: Booting VM...
==> default: Waiting for machine to boot. This may take a few minutes...
    default: SSH address: 127.0.0.1:2222
    default: SSH username: vagrant
    default: SSH auth method: private key
    default: Error: Connection timeout. Retrying...
    default: Error: Connection timeout. Retrying...
    default: Error: Connection timeout. Retrying...
    default: Error: Connection timeout. Retrying...
    default: Error: Authentication failure. Retrying...
    default: Error: Authentication failure. Retrying...
    default: Error: Authentication failure. Retrying...
    default: Error: Authentication failure. Retrying...
    default: Error: Authentication failure. Retrying...
```
##### 解决办法：
- 先查看我们的 `ssh-config`(应该是up以后才能查看) ，找到 `insecure_private_key` 的路径
- 找到后，先关闭该项目，`vagrant halt`
```bash
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile C:/Users/xxxx/.vagrant.d/insecure_private_key
  IdentitiesOnly yes
  LogLevel FATAL
```
- 如果发现 `insecure_private_key` 内容为空，删掉该文件
- 然后我们再执行 `vagrant up` 启动机器，发现这个文件又重新生成了，而且内容也不为空了，就能正常登录了。
