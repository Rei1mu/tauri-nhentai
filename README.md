### 第一步
cargo tauri android init

### 第二步
#### 将src-tauri/init/ 目录下的
```
upload-keystore.jks
key.properties
build.gradle.kts
```
复制并放入init生成的
```
src-tauri/gen/android/app/
```
目录下

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
cargo tauri icon