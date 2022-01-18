<template>
  <div class="home">
    <p>生成aesKey:{{ aesKey }}</p>
    <p>加密数据:{{ encryptedData }}</p>
    <p>加密aesKey:{{ encryptedAesKey }}</p>
    <p>解密aesKey:{{ decryptedAesKey }}</p>
    <p>解密数据:{{ decryptedData }}</p>
  </div>
</template>

<script>
import encry from '@/utils/encryUtils'
export default {
  name: 'Home',
  data() {
    return {
      aesKey: '',
      encryptedData: '',
      encryptedAesKey: '',
      encrypted: '',
      decryptedAesKey: '',
      decryptedData: '',
      //RSA公钥
      rsaPublicKey: `-----BEGIN PUBLIC KEY-----
        MIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQC80LjZJDlrfw42evV0Zaz4FxqC
        mGpoPlnq0CiZ0Nx1pTr8xhAWDaWsAYn6wgHrxxcXGqIG1qE7bItcUSgKTnnt5qQA
        4X7t3/qFrXlzv0TatCT4OISuGCiicftGPzVpY8DsRerkgBRdZ1Ard7FZMwdMaV8V
        eeXzNWifSIUA8q2jEwIDAQAB
        -----END PUBLIC KEY-----`,
      //RSA私钥
      rsaPrivateKey: `-----BEGIN PRIVATE KEY-----
        MIICdgIBADANBgkqhkiG9w0BAQEFAASCAmAwggJcAgEAAoGBALzQuNkkOWt/DjZ6
        9XRlrPgXGoKYamg+WerQKJnQ3HWlOvzGEBYNpawBifrCAevHFxcaogbWoTtsi1xR
        KApOee3mpADhfu3f+oWteXO/RNq0JPg4hK4YKKJx+0Y/NWljwOxF6uSAFF1nUCt3
        sVkzB0xpXxV55fM1aJ9IhQDyraMTAgMBAAECgYAaj3XhPcJCB9509Xj/xam+QGm/
        Qzd8sICvklaTxJiuh+6zTh1HLOZIOvMw7gedJiVuX5W5RonptQwpkVUDliR6f5im
        xNv88gJqvIYM7WA23atWiPpJb6yS4s5ReLK46fApvDHVkgCk4k5cHiUbdo/8wMJ5
        N+F9fbx5bAhHrfzASQJBAPJK+8Qu4zcT85miqUMUyBiAi8JiiRm7dr9YH7SuIPur
        wrBJAPMi6/ce3h0DX6jE3xkFxdi7SzypAo9o2JqU3dcCQQDHfz9U1EEH8WhQoXZj
        uDdSTKQZ6xhqazYZvKmNt2q13FtO8fPiE32hTwfc4YZA4ch1OC79z6zogTYhnK3n
        gqUlAkA2ykYMox22gsh/YY0tIjHteIQiPO4L55x+wIrK7OWAg+LOwnN4h9kcVNqd
        bPngzEQ3AFsxG4lz+jQeAfOZYTiZAkBCl2MYedFLSXW8lGjkWHV+7z5HuIXp3+er
        J6KhP3xLQEbqTzFNYZwp4CuLu2wI9FTpa9ujtVLOOXNMPPR/tshRAkEAkB7V90Pp
        iBZnYvv44pJvEKDyTy/c8d1zDFV6VdYrwDxkSnf44AaIh/r/RHMPC5d5cfrTZ9ZD
        /vleNiEOfq6/jw==
        -----END PRIVATE KEY-----
`, //RSA密钥
    }
  },
  created() {
  console.log('encry',encry);
    // 生产AES密钥
    this.aesKey = encry.createAesKey()
    // const aesKey = '21jgsi1a3paulr78'; //密钥格式为长度16得字符串
    console.log('生成AES密钥:', this.aesKey)

    // 用生成的 AES 密钥加密数据
    this.encryptedData = encry.encryptByECB('你快乐吗?', this.aesKey)
    // this.encryptedData = `HKY6FLv2apfWCPTaDBaPTy7zxRLRJZCbMbv75tvJGOM=`;
    // 用 RSA 公钥加密 AES密钥
    this.encryptedAesKey = encry.publicEncrypt(this.aesKey, this.rsaPublicKey)
    // this.encryptedAesKey = `YUxi/pWfkPeERjptnhpGjHLm04nVKunr6fZeiJ0RZ2CmqVITtrDgOX1gFJSQGweeqZ2y2TT3fYn+WDmrRwck99qSb3rzuYLHKV763twWyl1GQySrbwW23Veckz4vdioZCz6/3v78IPX8bHxmeEyTkm4RgU0vXB+zL6BvLCasTzc=`;
    console.log('加密AES密钥:', this.encryptedAesKey)

    this.encrypted = {
      aesKey: this.aesKey, //AES密钥
      encryptedAesKey: this.encryptedAesKey, //加密的AES密钥
      encryptedData: this.encryptedData, //加密后的data
    }
    console.log('encrypted:', JSON.stringify(this.encrypted))

    // 用RSA密钥解码 AES 密钥
    this.decryptedAesKey = encry.privateDecrypt(this.encryptedAesKey, this.rsaPrivateKey)
    console.log('解码AES 密钥:', this.decryptedAesKey)

    // 用解码的AES密钥  解码数据
    this.decryptedData = encry.decryptByECB(this.encryptedData, this.decryptedAesKey)

    console.log('解码数据:', this.decryptedData)

    // this.decrypted = {
    //   decryptedAesKey,
    //   decryptedData,
    // };
  },
  methods: {},
}
</script>
<style>
p {
  word-wrap: break-word;
}
</style>
