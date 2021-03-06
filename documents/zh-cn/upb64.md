# 上传 base64

```Javascript
Tunnel.prototype.upb64
```

Docs: https://developer.qiniu.com/kodo/kb/1326/how-to-upload-photos-to-seven-niuyun-base64-code


## 使用

```Javascript
import { Tunnel } from 'qiniup'

let tunnel = new Tunnel()
let base64Image = 'data:image/gif;base64,R0lGODlhAQABAAAAACH5BAEKAAEALAAAAAABAAEAAAICTAEAOw=='

tunnel.upb64(base64Image, { size: base64Image.length, token, key, mimeType, crc32, userVars }, {}, function (error, response) {
  if (error) {
    console.error(error)
    return
  }

  let { ctx, checksum, crc32, offset, host, expired_at } = response
  // doing something...
})
```


## 参数

### token

- 类型: `String`
- 必填

七牛上传凭证, 通过七牛 SDK 通过后端接口返回的 Token. <br/>
Docs: https://developer.qiniu.com/kodo/manual/1208/upload-token


### size

- 类型: `SafeInteger`
- 默认值: `-1`
- 必填

文件大小, 默认值为 `-1`, 则为自动获取文件大小


### key

- 类型: `String`
- 非必填

如果没有指定则：如果 uptoken.SaveKey 存在则基于 SaveKey 生产 key，否则用 hash 值作 key。EncodedKey 需要经过 base64 编码


### mimeType

- 类型: `String`
- 默认值: `application/octet-stream`
- 非必填

文件的 MIME 类型


### crc32

- 类型: `String`
- 非必填

文件内容的 crc32 校验值，不指定则不进行校验


## 配置

## useHttps

- 类型: `Boolean`
- 默认值: `true`

是否使用 `https` 协议进行请求; 如果不配置 `host` 属性, `useHttps` 会改变默认 `host` 配置.


## host

- 类型: `String`
- 默认值: `'up.qbox.me'` 或 `'up-z0.qiniu.com'`

七牛云服务器上传地址, 默地址为中国华南地区服务器
默认值会受到 `useHttps`, `useHttps:true` 则会使用 `up.qbox.me` 否则使用 `up-z0.qiniu.com`. 其他七牛地址可以[查看这里](https://developer.qiniu.com/kodo/manual/1671/region-endpoint)


### tokenPrefix

- 类型: `String`
- 默认值: `'UpToken'`

七牛云上传令牌前缀, 固定为 `UpToken`, 不需要修改, 若用于其他服务可以进行配置


### progress

- 类型: `Function`
- 默认值: `undefined`

上传进度回调函数; 根据该函数可以获取当前上传的进度;


## tokenGetter

- 类型: `Function`
- 默认值: `undefined`

获取 token, 通过 `callback` 实现异步获取 `token`. 同时也可以设置过期时间(在 0.2.0 版本以上才适用); 七牛云文档表示: 若为超过过期时间, token 可以继续使用
