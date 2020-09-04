# ygk

### QQ 群

- 753621403

### 客户端配置文件

- 下面的注释在运行环境中需要删掉

```c
{
  "setting": { // 一些设置选项
    "daemon": true, // 是否后台运行，默认 false
    "uid": 1000, // 切换运行用户，需要 root 权限，无默认值
    "gid": 1000, // 切换运行用户组，需要 root 权限，无默认值
    "pid_file": "/home/ygk/ygk.pid", // 指定 pid 输出文件，无默认值
    "log_level": "fatal", // 日志级别，具体看下方介绍，默认 fatal
    "log_file": "/home/ygk/ygk.log", // 日志输出文件，默认标准输出（stdout）
    "log_file_max": 1024 // 日志文件大小的最大值，超出后会清空日志文件，单位 kb，默认 1024
  },
  "in": { // 客户端的入口设置
    "mode": "tun", // 入口模式，支持 tun，无默认值且为必填项
    "name": "tun3", // tun 模式的虚拟网卡名称，默认 tun3
    "netmask": "255.255.255.0", // tun 模式的子网掩码，默认 255.255.255.0
    "mtu": 1500, // tun 模式的 mtu 值，默认 1500
    "path": "/dev/net/tun", // tun 模式的 tun 路径，默认 /dev/net/tun 或 /dev/tun
    "tun_post": "echo hello world" // tun 模式的网卡变化后执行的 shell 命令，无默认值
  },
  "server": { // 客户端的服务端设置
    "address": "1.2.3.4", // 服务端地址，填 IP 或者域名，无默认值且为必填项
    "port": 11, // 服务端端口，无默认值且为必填项
    "password": "abc", // 服务端密码，无默认值且为必填项
    "ch": "GET / HTTP/1.1\r\nHost: qq.com\r\n\r\n", // custom header，自定义的 http 请求头部，无默认值且为必填项
    "tun_address": "", // 客户端的地址，必须处于服务端的子网内，默认从服务端获取
    "timeout": 30 // 连接超时时间，默认 30 秒
  }
}
```

### 服务端配置文件

- 下面的注释在运行环境中需要删掉

```c
{
  "setting": { // 一些设置选项
    "daemon": true, // 是否后台运行，默认 false
    "uid": 1000, // 切换运行用户，需要 root 权限，无默认值
    "gid": 1000, // 切换运行用户组，需要 root 权限，无默认值
    "pid_file": "/home/ygk/ygk.pid", // 指定 pid 输出文件，无默认值
    "log_level": "fatal", // 日志级别，具体看下方介绍，默认 fatal
    "log_file": "/home/ygk/ygk.log", // 日志输出文件，默认标准输出（stdout）
    "log_file_max": 1024 // 日志文件大小的最大值，超出后会清空日志文件，单位 kb，默认 1024
  },
  "tun": { // 服务端 tun 选项
    "name": "tun3", // 虚拟网卡名称，默认 tun3
    "address": "10.5.5.1", // 虚拟网卡地址，默认 10.5.5.1
    "netmask": "255.255.255.0", // 子网掩码，默认 255.255.255.0
    "mtu": 1500, // mtu 值，默认 1500
    "path": "/dev/net/tun", //  tun 路径，默认 /dev/net/tun 或 /dev/tun
    "tun_post": "echo hello world" // 网卡变化后执行的 shell 命令，无默认值
  },
  "listen": [ // 服务端监听选项，可配置多个
    {
      "address": "0.0.0.0", // 监听地址，默认 0.0.0.0
      "port": 11, // 监听端口，无默认值且为必填项
      "password": "abc", // 密码
      "ch": "HTTP/1.1 200 OK\r\n\r\n", //  custom header，自定义的 http 应答头部，默认 HTTP/1.1 200 OK\r\n\r\n
      "timeout": 60 // 连接超时，默认 60 秒
    },
    {
      "address": "0.0.0.0",
      "port": 12,
      "password": "abc",
      "ch": "HTTP/1.1 200 OK\r\n\r\n",
      "timeout": 60
    }
  ]
}
```

### 日志级别

- fatal 输出必定会使程序出错的信息
- error 输出可能会使程序出错的信息
- warning 输出不会影响程序正常运行但非期望的信息
- info 输出用户感兴趣的信息
- debug 输出开发者感兴趣的信息
