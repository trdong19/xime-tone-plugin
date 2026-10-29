# xime-tone-plugin — Xime 输入法拼音声调标注插件

给 [Xime（曦码）输入法](https://github.com/ximeiorg/Xime) 的候选注释加上**带声调拼音**：`ni hao` → `nǐ hǎo`。

- 纯插件（`.xipk`），**不需要修改/重编译输入法本体**
- 完全离线：内置 GB2312 一级常用字（3755 字）带调拼音表，无网络请求
- 基于 Xime 官方 `candidate_transform` 插件能力（候选词变换，15ms 硬超时，失败自动回退）

## 安装

1. 下载本仓库 Release（或 Actions 构建产物）里的 `tone-comment-<版本>.xipk`
2. Xime 输入法 → 扩展商店 → 右上角**本地管理** → 导入该文件
3. 打字时候选下方注释自动变为带声调拼音

> 声调标注规则：注释带数字调（`ni3`）时精确转换；注释无调时用候选汉字查内置字表对齐标注（多音字读音与注释不一致时保守原样，不乱标）。

## 已知限制（重要）

- **当前仅全键盘模式生效**。九键（T9）模式的候选面板在宿主 v3.4.2 中不渲染候选注释、且 T9 变换路径不支持覆盖引擎候选注释（`CandidateTransformCoordinator.transformForT9` 只注入插件自有候选）——这需要上游支持，已验证机制并整理了实现建议，待 Xime 上游更新后本插件自动受益。

## 开发

```bash
# 测试（内嵌 QuickJS，无需真机）
xipm test plugins/tone-comment

# 打包（输出 build/plugin-release/*.xipk）
xipm pack
```

字表生成：pypinyin（GB2312 一级字库），数据在 `plugins/tone-comment/libs/tone-data.ts`。

## License

MIT
