### 第一步
```npm i
npm build
cargo tauri android init
```

### 第二步
#### 将src-tauri/init/ 目录下的
```
key.properties
build.gradle.kts
upload-keystore.jks
```
文件复制并放入init生成的src-tauri/gen/android/app/目录下



#### 生成icon，按照根目录的app-icon.png

```
cargo tauri icon
```

### 第三步 编译
#### android 无target则universe(x86,arm通用).apk安装包
```
cargo tauri android build --target aarch64
```

#### windows x64 编译.msi安装包
```
cargo tauri build --target=x86_64-pc-windows-msvc
```

#### windows arm64 编译nsis安装包
```
cargo tauri build --target aarch64-pc-windows-msvc --bundles nsis
```

#### linux 安装包
自己填


### 安卓签名生成
#### 生成sign,jks/keystore格式
在src-tauri目录下执行cmd
```
cd src-tauri
keytool -genkey -v -keystore .\init\upload-keystore.jks -storetype JKS -keyalg RSA -keysize 2048 -validity 10000 -alias upload
```

#### pkcs12标准
```
keytool -importkeystore -srckeystore .\init\upload-keystore.jks -destkeystore .\init\upload-keystore.jks -deststoretype pkcs12
```
