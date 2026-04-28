# weiqi-assets

围棋相关静态资源库，提供二维码分享、棋谱编解码等功能的 JavaScript 库。

## 项目结构

```
weiqi-assets/
├── js/
│   └── share.js          # 核心分享库（二维码生成、编解码）
├── share/
│   └── index.html        # 扫码后下载 SGF 的解码页面
├── css/                  # 预留
├── img/                  # 预留
└── index.html            # 本页（资源导航）
```

## 快速使用

### 1. 加载分享库

```html
<script src="https://weiqi-dev.github.io/weiqi-assets/js/share.js"></script>
```

### 2. 生成二维码分享

```javascript
// gameState: [{col, row, player, isPass}, ...]
WeiqiShare.generateQR(containerElement, gameState)
    .then(() => console.log('二维码生成成功'))
    .catch(err => console.error(err));
```

### 3. 扫码下载

二维码内容指向：
```
https://weiqi-dev.github.io/weiqi-assets/share/?d={encodedData}
```

扫码后自动下载 SGF 文件。

## API 文档

### WeiqiShare 对象

| 方法 | 说明 | 参数 |
|-----|------|-----|
| `isWechat()` | 检测微信浏览器 | - |
| `encode(gameState)` | 编码棋谱为紧凑格式 | gameState: 棋谱数组 |
| `decode(base64)` | 解码 base64 为棋谱数据 | base64: URL-safe Base64 |
| `toSGF(data)` | 棋谱数据转 SGF | data: {boardSize, moves} |
| `generateQR(container, gameState)` | 生成二维码 | container: DOM元素 |

### 数据格式

**紧凑二进制格式**（每手2字节）：
- 文件头：4字节（Magic + Version + BoardSize + Handicap）
- 手数：第1字节(颜色1bit + X坐标7bit)，第2字节(Y坐标8bit)
- 编码：Base64 URL-safe

**容量**：300手棋谱 ≈ 604字节 → Base64 ≈ 805字符

## 示例项目

- [weiqi-recorder](https://github.com/zhangbin2025/weiqi-skills/tree/main/weiqi-recorder) - 使用本库的围棋记谱工具

## License

MIT
