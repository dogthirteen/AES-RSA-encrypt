# AES-RSA-encrypt

## Project setup
```
yarn install
```

### Compiles and hot-reloads for development
```
yarn dev
```

### 简介
```
AES 加解密类型使用 ECB；CBC方法需要提供IV偏移量
后端
  1、生成 AES密钥（密钥长度16的字符串，格式:128;本项目工具包函数有提供生成AES密钥方法）加密data数据（加密方法使用AES）; 
  2、使用RSA密钥 加密AES密钥（加密方法使用RSA） 
  3、接口返回 加密ASE密钥  加密data
前端 
  1、使用RSA密钥（后端提供）对 加密ASE密钥 进行解密（解密方法使用RSA）
  2、使用解密的AES密钥 对 加密数据进行解密（解密密方法使用AES）
```

