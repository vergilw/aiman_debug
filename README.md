### ReactNative配置

参考官方配置方案 https://reactnative.cn/docs/getting-started/

1. 确保WindowsOS下已安装如下，且环境变量配置正确。
   * Node 10.x版本+
   * Python2
   * JavaSDK 1.8

   * yarn
   * react-native-cli

   * AndroidStudio IDE


2. 环境配置完成后，用终端进入项目主目录:

   1. 执行 `yarn install`
   2. 执行 `./node_modules/.bin/rn-nodeify --hack --install`
   3. 打开Android模拟器
   4. 执行 `react-native run-android`


调试代码在主目录`App.js`内，aiman请求会报错，但是rpc请求不会，代码如下：
```javascript
  //debug aiman lib
  global.httpProvider = new HttpProvider('https://testnet.matrix.io');
  global.httpProvider.man.getBalance('MAN.35dDuaK7Pb42338pXq5a6shtsTDoZ', (error, result) => {
    console.log(error);
    console.log(result);
  });

  //debug rpc with axios 
  axios({
    method: 'post',
    url: 'https://testnet.matrix.io',
    data: { "jsonrpc": "2.0", "method": "man_getBalance", "params": ["MAN.35dDuaK7Pb42338pXq5a6shtsTDoZ", "latest"], "id": 1 }
  })
    .then((response) => {
      console.log(response);
    })
    .catch((error) => {
      console.error(error);
    });
```
注：ReactNative不支持同步网络请求，底层只有Javascript框架支持，没有NodeJS框架支持。