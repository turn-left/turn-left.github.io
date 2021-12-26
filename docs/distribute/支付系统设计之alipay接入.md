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
这部分以当面付产品为例，探讨商户后台从无到有，接入alipay的步骤。

- [沙箱环境调试](https://opendocs.alipay.com/common/02kkv7)
- 接口开发与调试
- 应用创建及配置
- 商户签约
- 应用发布
- 线上验证

### 参考资源

- [支付宝能力接入文档](https://opendocs.alipay.com/open/01zuoj)
- [支付宝沙箱环境](https://open.alipay.com/platform/appDaily.htm)
- [支付宝沙箱环境文档](https://opendocs.alipay.com/common/02kkv7)
- [沙箱环境当面付接入](https://open.alipay.com/platform/appDaily.htm?tab=info)
- [alipay-sdk-java-all](https://github.com/alipay/alipay-sdk-java-all)
- [二维码指南及如何扫描二维码](https://www.kaspersky.com.cn/resource-center/definitions/what-is-a-qr-code-how-to-scan)
- [支付宝二维码生成工具](https://opensupport.alipay.com/support/tools/convert/qrcode?ant_source=opendoc)
- [关于第三方支付，看这篇文章就够了](http://www.ityouknow.com/payment/2019/03/30/third-payment.html)