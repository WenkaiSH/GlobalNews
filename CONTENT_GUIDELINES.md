# GlobalNews 内容制作规范

> 本文档规定了英语学习网站文章的格式标准，所有新文章必须遵循。

## 文件结构

每篇文章包含以下文件：
```
content/YYYY-MM-DD/
├── meta.json          # 文章索引
├── article-1.json     # 初级文章
├── article-2.json     # 中级文章
└── article-3.json     # 进阶文章
```

## JSON 格式规范

### 基础字段

```json
{
  "id": "YYYYMMDD-N",           // 格式: 日期-序号, 如 20260404-1
  "date": "YYYY-MM-DD",          // 发布日期
  "level": "beginner|intermediate|advanced",
  "level_label": "初级|中级|进阶",
  "title": "英文标题",
  "title_cn": "中文标题",
  "source": "来源名称",
  "source_url": "原文链接",
  "topic": "分类 / 子分类",       // 如 "国际新闻 / 军事冲突"
  "word_count": 520,             // 英文词数
  "reading_time": 5              // 预计阅读时间(分钟)
}
```

### content 字段

- 完整英文正文
- 段落之间用 `\n\n` 分隔
- 保持原文段落结构

### translation 字段（⚠️ 重点规范）

**必须采用逐句中英对照格式**：

```json
{
  "translation": [
    {
      "en": "英文句子1",
      "cn": "中文翻译1"
    },
    {
      "en": "英文句子2", 
      "cn": "中文翻译2"
    }
  ]
}
```

**规则**：
1. 每个 `translation` 对象对应一句完整的英文和对应的中文翻译
2. 英文句子不宜过长（建议控制在30词以内）
3. 中文翻译应准确、通顺，符合中文表达习惯
4. 句子编号按数组索引自动生成（从1开始）
5. 确保 `translation` 数组长度与可读性匹配，不要过多或过少

**错误示例**（不要这样）：
```json
// ❌ 错误的段落对应
{
  "translation": [
    "中文段落1",
    "中文段落2"
  ]
}

// ❌ 过长句子
{
  "en": "This is a very long sentence with many clauses that goes on and on making it hard to read and understand for language learners.",
  "cn": "这是一个很长的句子..."
}
```

### vocabulary 字段

每篇文章包含 8-12 个重点词汇：

```json
{
  "vocabulary": [
    {
      "word": "单词",
      "phonetic": "/音标/",
      "pos": "词性",              // 如 noun, verb, adjective
      "meaning": "中文释义",
      "example": "英文例句",
      "synonyms": ["同义词1", "同义词2"]
    }
  ]
}
```

**词汇选择原则**：
1. 选择文章中出现的重要词汇
2. 优先选择学术/商务/新闻常用词汇
3. 初级文章词汇难度适中（高中-四级水平）
4. 进阶文章可包含专业术语
5. 每个词汇提供实用例句

## 级别划分标准

| 级别 | 词数范围 | 句式复杂度 | 词汇难度 | 适合水平 |
|------|----------|------------|----------|----------|
| 初级 | 400-600 | 简单句为主 | 高中-四级 | 英语学习初期 |
| 中级 | 600-900 | 复合句为主 | 四级-六级 | 有一定基础 |
| 进阶 | 900-1200 | 复杂长句 | 六级-雅思 | 高级学习者 |

## meta.json 格式

```json
{
  "date": "2026-04-04",
  "total_articles": 3,
  "articles": [
    {
      "id": "20260404-1",
      "level": "beginner",
      "level_label": "初级",
      "title": "英文标题",
      "title_cn": "中文标题",
      "topic": "分类 / 子分类",
      "word_count": 520,
      "file": "article-1.json"
    }
  ]
}
```

## 质量控制清单

发布前检查：

- [ ] JSON 格式有效（可用 jsonlint 验证）
- [ ] 所有必填字段已填写
- [ ] translation 数组格式正确（每个元素有 en 和 cn）
- [ ] translation 数量合理（8-15句为宜）
- [ ] 词汇数量 8-12 个
- [ ] 词汇音标使用标准 IPA 格式
- [ ] 原文链接可访问
- [ ] 文章发布于 24 小时内

## 工作流程

1. **选题**：从 Reuters, BBC, Guardian 等选择 24 小时内热点新闻
2. **分级**：根据难度将同一主题改编为初/中/进阶三个版本
3. **生成**：按本规范生成 4 个 JSON 文件
4. **验证**：检查 JSON 格式和内容完整性
5. **部署**：推送到 GitHub，自动部署到 Pages

---

*文档版本*: v1.0  
*最后更新*: 2026-04-04
