# iOS Loon 与懒猫微服共存配置

## 一、Loon 基础配置

### 1. 打开 Loon 高级配置

打开 **Loon**，进入：

**底部 → 配置 → 高级配置**

需要修改以下三项设置：

* **IP Stack**
* **绕过路由**
* **代理模式**

![Loon 高级配置](https://pic1.imgdb.cn/item/6936bc4a2a4ee13cb951c8cf.png)

![Loon 高级配置](https://pic1.imgdb.cn/item/6936bc4a2a4ee13cb951c8cd.png)

---

### 2. IP Stack 设置

进入 **IP Stack**，进行以下配置：

* **查询模式**：`IPv4&IPv6`
* **TUN IPV6**：开启

![IP Stack 设置](https://pic1.imgdb.cn/item/6936bc4a2a4ee13cb951c8ce.png)

![TUN IPV6 设置](https://pic1.imgdb.cn/item/6936bc4a2a4ee13cb951c8d0.png)

---

### 3. 绕过路由设置

返回上一级，进入 **绕过路由**，添加以下地址：

```text
6.6.6.6/32
2000::6666/128
```

也可以直接添加为：

```text
6.6.6.6/32,2000::6666/128
```

![绕过路由设置](https://pic1.imgdb.cn/item/6936bc4a2a4ee13cb951c8cc.png)

---

### 4. 懒猫微服网络模式设置

保存 Loon 配置后，进入 **懒猫微服**：

**网络模式 → 将 VPN 切换为 Proxy**

切换完成后，**重启懒猫微服手机客户端**，即可实现直连。

![懒猫微服网络模式](https://pic1.imgdb.cn/item/6936bc4a2a4ee13cb951c8d1.png)

---

## 二、Loon 与懒猫微服共存

完成上述配置后，如果希望在 **Loon 客户端外部直接打开懒猫微服应用**，还需要进行以下配置。

### 1. 添加本地节点

首先添加两个本地节点：

![本地节点 1](https://pic1.imgdb.cn/i/034UCnIFrghSC7b4EYVGw5.jpg)

![本地节点 2](https://pic1.imgdb.cn/i/034UCnIDcaOpCtMBQTj0lu.jpg)

---

### 2. 创建策略组

进入 Loon 底部的 **策略**，新增一个策略组。

将刚才创建的两个**本地节点**加入该策略组。

![策略组设置](https://pic1.imgdb.cn/i/034UCq4gzeQoBu415GaB08.jpg)

> 策略组名称可以根据自己的习惯设置，例如：`懒猫微服`

---

### 3. 添加本地规则

进入：

**底部 → 配置 → 规则**

新增一条**本地规则**。

配置：

* **策略**：选择刚才创建的策略组
* **匹配方式**：域名后缀匹配
* **域名后缀**：

```text
heiyu.space
```

![本地规则设置](https://pic1.imgdb.cn/i/034UCtkc6Mqn8mY2rqnGT.jpg)

---

### 4. 完成配置

添加完成后，Loon 会将 `heiyu.space` 域名的流量按照刚才创建的策略组进行处理。

完成以上配置后，即可在**不关闭 Loon 的情况下，从客户端外部正常打开懒猫微服应用**。

## 三、配置总结

整体配置流程如下：

```text
Loon
  ↓
配置 → 高级配置
  ↓
IP Stack
  ├─ 查询模式：IPv4&IPv6
  └─ TUN IPV6：开启
  ↓
绕过路由
  └─ 6.6.6.6/32
     2000::6666/128
  ↓
懒猫微服
  └─ 网络模式：Proxy
  ↓
重启懒猫微服客户端
  ↓
添加两个本地节点
  ↓
创建策略组
  ↓
添加 heiyu.space 域名后缀规则
  ↓
完成 Loon 与懒猫微服共存配置
```
