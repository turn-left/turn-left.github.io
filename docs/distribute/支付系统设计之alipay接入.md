## 支付系统设计之alipay接入

### 支付宝支付产品

![支付宝 支付产品.png](/docs/distribute/img/支付宝支付产品.png)

### 最佳架构

商户或系统商在对接支付宝时，通常有两种形式：门店直连和商户后台转发。

- 门店直连，即门店收银终端直接通过公网请求支付宝。
- 商户/系统商后台转发，即商户/系统商开发并部署独立的服务端（支付中台），门店收银终端先请求到商户服务端，再由服务端请求支付宝。
  <br>
  支付宝官方建议第二种转发模式，这样可以方便日志记录、问题排查，同时将支付逻辑和原有业务逻辑尽量解耦。

![original.png](/docs/distribute/img/original.png)
<br>([来自支付宝开放平台官方文档](https://opendocs.alipay.com/open/194/105322))

### 商户接入流程

支付宝提供了[沙箱环境](https://open.alipay.com/platform/appDaily.htm) 以供商户侧开发与调试。沙箱环境不同于正式环境，门槛低，无需签约等繁琐步骤，可以直接下载demo到本地调试接口。
<br>这部分以当面付产品为例，探讨商户后台从无到有，接入alipay的步骤。

1. [**沙箱环境调试**](https://opendocs.alipay.com/common/02kkv7)
2. **接口开发与调试**
3. **应用创建及配置**
4. [**商户接入准备**](https://opendocs.alipay.com/open/01csp3)
5. **商户应用发布**
6. **商户线上验证**

#### [扫码支付接入](https://opendocs.alipay.com/open/194/106078)

扫码支付适合有各类自助终端的商家，用户在自助终端通过扫码完成支付。当面付扫码支付采用 商家/系统服务商后台转发 方式接入，商家先预下单到商家后台，再请求到支付宝。

- 扫码支付流程图

![扫码支付流程.png](/docs/distribute/img/扫码支付流程.png)

- 扫码支付接口时序

![扫码支付接口调用时序.png](/docs/distribute/img/扫码支付接口调用时序.png)

#### [付款码支付接入](https://opendocs.alipay.com/open/194/106039)

商户/系统商后台转发方式接入即商家收银台先向商家后台发起收款请求，商家后台再将请求转发给支付宝后台。建议由多家门店的商户或大型商户这类有能力开发自有后台的商户采用。

- 付款码支付流程
  ![付款码支付流程.png](/docs/distribute/img/付款码支付流程.png)

- 付款码支付接口时序
  ![付款码支付接口时序.png](/docs/distribute/img/付款码支付接口时序.png)

- 核心交互接口
  <br>商户后台在接入支付宝的全流程中涉及几个核心接口,涵盖
  [预付单](https://opendocs.alipay.com/open/02ekfg?scene=19)
  、
  [交易查询](https://opendocs.alipay.com/open/02ekfh?scene=23)
  、
  [交易撤销](https://opendocs.alipay.com/open/02ekfi)
  、
  [退款](https://opendocs.alipay.com/open/02ekfk)
  、
  [对账](https://opendocs.alipay.com/open/02ekfm)
  等环节。
  <br>![核心交互接口.png](/docs/distribute/img/核心交互接口.png)

### 参考资源

- [支付宝能力接入文档](https://opendocs.alipay.com/open/01zuoj)
- [支付宝沙箱环境](https://open.alipay.com/platform/appDaily.htm)
- [支付宝沙箱环境文档](https://opendocs.alipay.com/common/02kkv7)
- [沙箱环境当面付接入](https://open.alipay.com/platform/appDaily.htm?tab=info)
- [当面付接入流程](https://opensupport.alipay.com/support/helpcenter/99/201602490909?ant_source=opendoc_recommend)
- [alipay-sdk-java-all](https://github.com/alipay/alipay-sdk-java-all)
- [二维码指南及如何扫描二维码](https://www.kaspersky.com.cn/resource-center/definitions/what-is-a-qr-code-how-to-scan)
- [支付宝二维码生成工具](https://opensupport.alipay.com/support/tools/convert/qrcode?ant_source=opendoc)
- [关于第三方支付，看这篇文章就够了](http://www.ityouknow.com/payment/2019/03/30/third-payment.html)