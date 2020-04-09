# serverless framework 初识

`serverless` 是各大云服务商提供出来的一种无服务的计算资源。为什么叫无服务呢，因为如果你使用 `serverless`，你只需要关注应用层，而无需关心底层基础设施，无需运维。简而言之，`serverless` 并不是真的无服务，而是关于有服务的不归你管，云服务商帮你搞定，比如 `google`，`aws` 或者 `aliyun`。

关注点分离，好呀好，有了 `serverless` 以后只需要也只能关心业务了，这也不知是喜是忧。但你也无需过于担心，这是对已有并且成熟的开发模式的挑战，解决痛点有限，因此很多团队对于替换为 `serverless` 也动力不足。

但是我仍然建议你学习 `serverless`，毕竟各大云厂商对于 `serverless` 有很多免费额度可以让你薅羊毛，对于个人开发者利好。

## serverless framework

`serverless` 是基于各大云服务商的产品，每一个云厂商对于 `serverless` 都有一套自己的 API。为了能够兼容这些 API，为了让你的代码 `Write Once, Run Everywhere`，于是 `serverless framework` 诞生了。

> 通常认为 serverless = faas + baas，然而 serverless framework 只兼容到了 faas，对于 baas，如各家提供的数据存储服务，要做到兼容还是很难。

## 快速开始

![serverless](https://camo.githubusercontent.com/0baf7ab6806be91afaeb587724fd734faf6656f5/68747470733a2f2f696d672e7365727665726c657373636c6f75642e636e2f32303139313231372f313537363537363134363431392d717569636b2d73746172742d6769662e676966)

`serverless framework` 与阿里云的函数计算来开始一个 `hello, world` 吧

``` bash
$ npm install -g serverless
```

``` bash
$ serverless create --template aliyun-nodejs --name hello

Serverless: Generating boilerplate...
 _______                             __
|   _   .-----.----.--.--.-----.----|  .-----.-----.-----.
|   |___|  -__|   _|  |  |  -__|   _|  |  -__|__ --|__ --|
|____   |_____|__|  \___/|_____|__| |__|_____|_____|_____|
|   |   |             The Serverless Application Framework
|       |                           serverless.com, v1.60.1
 -------'

Serverless: Successfully generated boilerplate for template: "aliyun-nodejs"
```

## 阿里云凭证

``` bash
$ vim ~/.aliyunrc
[default]
aliyun_access_key_id = xxxxxxxx
aliyun_access_key_secret = xxxxxxxxxxxxxxxxxxxx
aliyun_account_id = 1234567890
```

+ [`aliyun_access_key_id`](https://account.console.aliyun.com/?#/secure)
+ [`aliyun_access_key_secret`](https://ak-console.aliyun.com/?#/accesskey)
+ [`aliyun_account_id`](https://ak-console.aliyun.com/?#/accesskey)

## 部署

### `sls deploy`: 部署到目标云服务商上

``` bash
$ sls deploy

Serverless: Packaging service...
Serverless: Excluding development dependencies...
Serverless: Compiling function "hello"...
Serverless: Finished Packaging.
Serverless: Log project sls-1693442753428000-cn-shanghai-logs already exists.
Serverless: Creating log store sls-1693442753428000-cn-shanghai-logs/hello-dev...
Serverless: Created log store sls-1693442753428000-cn-shanghai-logs/hello-dev
Serverless: Creating log index for sls-1693442753428000-cn-shanghai-logs/hello-dev...
Serverless: Created log index for sls-1693442753428000-cn-shanghai-logs/hello-dev
Serverless: Creating RAM role sls-hello-dev-cn-shanghai-exec-role...
Serverless: Created RAM role sls-hello-dev-cn-shanghai-exec-role
Serverless: Creating RAM policy fc-hello-dev-cn-shanghai-access...
Serverless: Created RAM policy fc-hello-dev-cn-shanghai-access
Serverless: Attaching RAM policy fc-hello-dev-cn-shanghai-access to sls-hello-dev-cn-shanghai-exec-role...
Serverless: Attached RAM policy fc-hello-dev-cn-shanghai-access to sls-hello-dev-cn-shanghai-exec-role
Serverless: Creating service hello-dev...
Serverless: Created service hello-dev
Serverless: Creating bucket sls-1693442753428000-cn-shanghai...
Serverless: Created bucket sls-1693442753428000-cn-shanghai
Serverless: Uploading serverless/hello/dev/1586145092309-2020-04-06T03:51:32.309Z/hello.zip to OSS bucket sls-1693442753428000-cn-shanghai...
/root/Documents/hello/.serverless/hello.zip
Serverless: Uploaded serverless/hello/dev/1586145092309-2020-04-06T03:51:32.309Z/hello.zip to OSS bucket sls-1693442753428000-cn-shanghai
Serverless: Creating function hello-dev-hello...
Serverless: Created function hello-dev-hello
Serverless: Creating RAM role sls-hello-dev-cn-shanghai-invoke-role...
Serverless: Created RAM role sls-hello-dev-cn-shanghai-invoke-role
Serverless: Attaching RAM policy AliyunFCInvocationAccess to sls-hello-dev-cn-shanghai-invoke-role...
Serverless: Attached RAM policy AliyunFCInvocationAccess to sls-hello-dev-cn-shanghai-invoke-role
Serverless: Creating API group hello_dev_api...
Serverless: Created API group hello_dev_api
Serverless: Creating API sls_http_hello_dev_hello...
Serverless: Created API sls_http_hello_dev_hello
Serverless: Deploying API sls_http_hello_dev_hello...
Serverless: Deployed API sls_http_hello_dev_hello
Serverless: GET http://8ce117265ab748d49b16b18f7827e2ef-cn-shanghai.alicloudapi.com/foo -> hello-dev.hello-dev-hello
```

## 函数调用

``` bash
$ sls invoke --function hello
Serverless: Invoking hello-dev-hello of hello-dev
Serverless: {"statusCode":200,"body":"{\"message\":\"Hello!\"}"}
```

## http 调用

``` bash
$ curl http://8ce117265ab748d49b16b18f7827e2ef-cn-shanghai.alicloudapi.com/foo
{"message":"Hello!"}
```
