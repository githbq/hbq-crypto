# 跨平台加解密操作 基于 js-crypto 同时支持 浏览器环境与 nodejs 环境

![my love](./logo.png) 

## 安装
```
yarn add cross-crypto
```
## 核心代码
1. AES 

```typescript 
const crypto = require("crypto-js");
  
// const content = `how old are you`;
// const secret = "ihP9cS6oqy24HAay";

export function encrypt(key, originStr) {
    const keyBuffer = crypto.enc.Utf8.parse(key);
    const encryptedData = crypto.AES.encrypt(originStr, keyBuffer, {
        mode: crypto.mode.ECB,
        padding: crypto.pad.Pkcs7,
    });
    const baseBuffer = crypto.enc.Base64.parse(encryptedData.toString());
    const hexData = crypto.enc.Hex.stringify(baseBuffer);
    return hexData.toString().toUpperCase();
}

export function decrypt(key, encryptedStr) {
    const keyBuffer = crypto.enc.Utf8.parse(key);
    const encryptedHexBuffer = crypto.enc.Hex.parse(encryptedStr);
    const encryptedBase64Str = crypto.enc.Base64.stringify(encryptedHexBuffer);
    const decryptedData = crypto.AES.decrypt(encryptedBase64Str, keyBuffer, {
        mode: crypto.mode.ECB,
        padding: crypto.pad.Pkcs7,
    });
    const decryptContent = decryptedData.toString(crypto.enc.Utf8);
    return decryptContent;
}

// const encryptResult = encrypt(secret, content);
// const decryptResult = decrypt(secret, encryptResult);


// console.log("\r\n原文:", content);
// console.log("\r\n解密后:", decryptResult);
// console.log("\r\n加密结果与原始密文一致:", decryptResult === content);


```

## 测试   
```
npm run test    
```
 
