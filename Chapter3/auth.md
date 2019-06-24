# 3.6: 三方认证

如果我们在第一步修改config.yaml中，修改了正确Authentication，那么其实在整个部署过程中，认证相关都是该是设置正确的，就是该直接可以正常的microsoft账号登录。

当然，我们后续会提供wechat等国内常用的第三方接入方法。

#### microsoft认证

在[微软官方](https://apps.dev.microsoft.com/)进行申请，得到clientId和clientSecret，

把这段key作为Authentication中加入到config.yaml中、

然后再在配置中加入当前域名的白名单，比如 <https://qjy-proxy02.zhejianglab.com/sign-microsoft>

完成以上两步即可。



tips：

如果是后期才操作，那么需要重启webui2。