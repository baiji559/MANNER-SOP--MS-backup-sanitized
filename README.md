# MS 脱敏备份

这是 `MS` 工作区的公开、脱敏备份。仓库用于保存可安全公开的项目源码，不包含原始 Git 历史、账号凭据或本机构建环境。

## 备份内容

| 文件 | 内容 | SHA-256 |
| --- | --- | --- |
| [`coffee-studio-source.zip`](./coffee-studio-source.zip) | Coffee Studio 网站、Cloudflare Worker、Supabase 迁移和 Android 源码 | `F85347AF7C6426F2E67E06B0E9DD5B98F3B151382FFDC665085351542E0887D5` |
| [`deployment-source.zip`](./deployment-source.zip) | Cloudflare 部署脚本和迁移说明 | `5376D22496D71BD10AB5F3D2FAA2FD7650A1B66872678C8C4C1A95D5348B4D6A` |
| [`shiguang-recipe-source.zip`](./shiguang-recipe-source.zip) | 时光配方静态站点源码 | `E6A7F72E5D88C885D1F2B904D66BA88A356A9A43C488DE9568B2076607AC2118` |

三个压缩包合计包含 31 个项目文件，并保留各项目内部的目录结构。

## 已移除或替换的内容

备份前已进行敏感信息检查和脱敏：

- 移除原始 Git 历史和嵌套仓库元数据；
- 移除依赖目录、Android SDK、构建缓存、APK 和原部署 ZIP；
- 移除调试签名私钥及其他密钥文件；
- 将个人邮箱替换为 `owner@example.invalid`；
- 将 Supabase 项目引用和可发布密钥替换为占位值；
- 将 OpenAI Hosting 项目 ID 替换为占位值；
- 不包含 `service_role`、Cloudflare Token、应急访问代码或数据库密码。

更完整的处理记录见 [`SANITIZATION.md`](./SANITIZATION.md)。

## 恢复方法

1. 下载所需的源码 ZIP 并解压。
2. 在部署前替换以下占位值：
   - `owner@example.invalid`
   - `YOUR_PROJECT_REF`
   - `sb_publishable_REPLACE_ME`
   - `REPLACE_WITH_HOSTING_PROJECT_ID`
3. 将服务端密钥、应急访问代码和部署令牌配置在对应平台的 Secret/环境变量中，不要写入源码。
4. 为正式 Android 发布生成并安全保存独立的 release keystore；不要使用仓库中的调试签名生成逻辑作为正式签名方案。
5. 安装依赖并运行项目测试后再部署。

## 完整性校验

PowerShell：

```powershell
Get-FileHash .\coffee-studio-source.zip -Algorithm SHA256
Get-FileHash .\deployment-source.zip -Algorithm SHA256
Get-FileHash .\shiguang-recipe-source.zip -Algorithm SHA256
```

将输出与上表中的 SHA-256 值比较即可确认文件未损坏。

## 安全提示

这是公开仓库。提交任何更新前，请重新扫描邮箱、私钥、访问令牌、数据库连接串、`.env` 文件和签名文件。仓库根目录的 `.gitignore` 提供基础防护，但不能替代提交前审查。

## 许可

此备份目前未附带开源许可证。除非版权所有者另行授权，否则公开可见不代表允许复制、修改或再分发。
