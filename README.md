# Claw cloud容器搭建3x-ui面板
>`日本、新加坡人太多不稳定，不建议该地区`


[注册地址](https://console.run.claw.cloud/signin?link=WQSAZFMXPOVF)

## 创建应用程式
名称随意

## 镜像

```
metaligh/3x-ui
```

## 端口
开启`80``2053`
>`80`**出入站端口**
>`2053`**面板访问地址**

## 路径配置Mount Path ：
```
/etc/x-ui/
```

`再加一条`
```
/etc/letsencrypt/
```

## 示例图
![123.png](https://img.996399.xyz/file/1745946057497_123.png)

访问2053端口地址
默认账号密码`admin`
```
admin
```

# 添加入站规则
**照着填**
![image.png](https://img.996399.xyz/file/1745946297054_image.png)

名称`随意填写`

协议`vlass`

流量出入站端口`80`

传输选择第三个`wedsocket`

其他设置默认

完成

## 开始使用节点

`导入到客户端（不可以直接使用ping不通，需要设置出站流量）

IP地址需要替换`80`端口分配的域名

端口填写`443`

TLS：选择`tls`

all `false`

配置好后就可以翻墙了`


[idx免费vps](https://idx.google.com)
```
bash <(wget -qO- https://raw.githubusercontent.com/yonggekkk/argosb/main/argosb.sh)
```

## 翻墙客户端下载地址

[V2rayN下载](https://github.com/2dust/v2rayN)win Linux macOS
[nekoray下载](https://github.com/MatsuriDayo/nekoray)win Linux
[Clash for Windows下载](https://github.com/MatsuriDayo/nekoray/releases)



