# ygk

### 配置文件

- 下面的注释在运行环境中需要删掉

```c
{
  "setting": {
    "daemon": false, // 默认值: false
    "uid": 0, // setuid()，无默认值
    "gid": 0, // setgid(), 无默认值
    "pid_file": "ygk.pid" // 无默认值
  },
  "tun": {
    "name": "tun3", // 默认值: tun3
    "address": "10.5.5.1", // 填IP或者域名，仅支持ipv4，无默认值且为必填项
    "netmask": "255.255.255.0", // 默认值: 255.255.255.0
    "mtu": "1500", // 默认值: 1500
    "path": "/dev/net/tun" // 默认值: /dev/net/tun
  },
  "server": { // 表示客户端，当此项存在时listen失效
    "address": "1.2.3.4", // 填IP或者域名，仅支持ipv4，无默认值且为必填项
    "port": 80, // 无默认值且为必填项
    "password": "abcdef", // 无默认值且为必填项
    "ch": "", // custom header，默认值: GET / HTTP/1.1\\r\\nHost: biadu.com\\r\\n\\r\\n
    "timeout": 300 // 单位：秒，默认值: 300
  },
  "listen": { // 表示服务端
    "address": "0.0.0.0", //  填IP或者域名，仅支持ipv4，默认值: 0.0.0.0
    "port": 80, // 无默认值且为必填项
    "password": "abcdef", // 无默认值且为必填项
    "timeout": 300 // 单位：秒，默认值: 300
  }
}
```
