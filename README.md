# 留刻 · 手绘互动叙事画面

将情侣回忆、人物照片和互动机制，扩写为适合生成图片的手绘互动叙事游戏画面。

这个 Skill 面向「留刻」情侣回忆小游戏，参考 Florence 式互动叙事气质，但只提取抽象的视觉规律，不复制具体角色、剧情、镜头或关卡布局。

## 核心能力

- 根据场景描述自动扩写完整生图提示词
- 有人物照片时，分别提取左右人物的身份特征
- 保持人物数量、左右关系、发型、脸型、肤色、服装和显著标记
- 使用数值化的线宽、颜色、留白、尺寸和交互热区规范
- 支持点击、长按、拖拽、拼合、擦除、密码和拆封等互动机制
- 生成粗钴蓝线、平涂、低细节背景、轻微错版的手绘互动叙事画面
- 严格执行「先输出完整提示词，再生成图片」的流程

## 使用方式

提供一个具体的场景描述，例如：

> 两个人在周末早晨一起做早餐，女生把草莓递给男生，用户需要点击正确的食物完成互动。

Skill 会按照以下流程处理：

1. 提取人物、动作、地点、关键道具和互动目标
2. 判断是否存在人物参考图
3. 建立人物身份卡和画面设计规格
4. 选择背景模式、色彩模式和互动组件
5. 输出完整生图提示词
6. 使用同一份提示词生成图片
7. 按人物身份、构图、线条、交互和视觉风格进行验收
8. 失败时针对具体问题自动修订并重试一次

## 输入变量

### 必填变量

- `scene_description`：场景描述，包含人物、动作、地点、物件和叙事重点

### 可选变量

- `character_reference`：人物参考照片
- `character_reference_mode`：`PHOTO_TO_GAME_ART` 或 `IDENTITY_IN_NEW_SCENE`
- `interaction_mechanic`：点击、长按、拖拽、拼合、擦除、密码或拆封
- `interaction_state`：`idle`、`hint`、`pressed`、`dragging`、`success` 等
- `composition`：景别、人物位置、视角和画面分层
- `background_mode`：纸面留白、彩色场景板、完整场景或记忆拼贴
- `palette_mode`：纸面舞台、彩色面板、完整场景或单色记忆
- `aspect_ratio`：默认 `9:16`
- `resolution`：默认 `1080×1920px`

## 视觉规范

- 基准画布：`360×640px`
- 高清输出：`1080×1920px`
- 人物外轮廓：逻辑画布约 `4.8px`
- 人物内部线：逻辑画布约 `2.3px`
- 道具和普通控件：逻辑画布约 `3.8px`
- 大型 UI 外框：逻辑画布约 `5.2px`
- 可操作区域：不小于 `48×48px`
- 组件最小间距：`12px`
- 默认纸面颜色：`#FBFDF8`
- 默认主轮廓颜色：`#202796`

完整参数请查看 [references/component-system.md](generate-memory-game-art/references/component-system.md)。

## 人物参考图规则

人物参考图只决定人物身份，不决定画风。固定风格参考图只决定线条、色彩、构图密度、道具和 UI 语言。

Skill 会重点检查：

- 人物数量和左右关系
- 脸型、五官轮廓和发型长度
- 肤色、体型、服装和显著标记
- 眼镜、胡须、痣、耳饰等身份锚点
- 两个人的特征是否发生交换
- 是否被生成成相似的通用卡通脸

详细规则请查看 [references/character-identity.md](generate-memory-game-art/references/character-identity.md)。

## 目录结构

```text
generate-memory-game-art/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── assets/
│   └── icon.svg
└── references/
    ├── approved-style-calibration.md
    ├── character-identity.md
    ├── component-system.md
    ├── prompt-contract.md
    ├── style-reference-index.md
    └── style-images/
        ├── 01–16 早期风格参考图
        └── 17–18 已验收风格参考图
```

## 重要限制

- 不生成图片内文字、字幕、水印、品牌名或 Logo
- 不复制 Florence 的具体角色、对白、地图、镜头或关卡布局
- 不生成干净商业 AI 插画、半日漫精致脸或 Q 版比例
- 不使用全局黄色滤镜、完整摄影透视或高密度背景
- 未提供清晰人物参考图时，不猜测人物身份
- 除非用户明确要求，否则默认生成温暖、亲密、积极的情侣回忆场景

## 相关文件

- [Skill 主说明](generate-memory-game-art/SKILL.md)
- [数值化组件系统](generate-memory-game-art/references/component-system.md)
- [人物身份规范](generate-memory-game-art/references/character-identity.md)
- [提示词契约](generate-memory-game-art/references/prompt-contract.md)
- [风格参考图索引](generate-memory-game-art/references/style-reference-index.md)
