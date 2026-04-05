# GlobalNews 每日更新手册

> **任务**: 每周二、四、六 16:00-18:00 更新3篇英文新闻文章
> 
> **路径**: `/projects/GlobalNews/`
> **GitHub**: https://github.com/WenkaiSH/GlobalNews
> **网站**: https://wenkaish.github.io/GlobalNews/

---

## 📋 执行标准

- [ ] 3篇文章均发布于24小时内
- [ ] 分级：初级(1篇)、中级(1篇)、进阶(1篇)
- [ ] 每篇含：原文、逐句翻译、重点单词释义
- [ ] 文件格式：JSON，存放于 `content/YYYY-MM-DD/`
- [ ] 18:00前完成推送并通知用户

---

## 📝 内容格式

### 文件结构
```
content/YYYY-MM-DD/
├── meta.json       # 文章索引
├── article-1.json  # 初级文章
├── article-2.json  # 中级文章
└── article-3.json  # 进阶文章
```

### meta.json 格式
```json
{
  "date": "2026-04-05",
  "articles": [
    {"id": "article-1", "level": "beginner", "topic": "科技 / 人工智能"},
    {"id": "article-2", "level": "intermediate", "topic": "商业 / 市场"},
    {"id": "article-3", "level": "advanced", "topic": "国际 / 政治"}
  ]
}
```

### article-X.json 格式
```json
{
  "id": "article-1",
  "date": "2026-04-05",
  "level": "beginner",
  "title": "英文标题",
  "title_cn": "中文标题",
  "source": "Reuters",
  "source_url": "https://...",
  "topic": "科技 / 人工智能",
  "word_count": 550,
  "reading_time": 3,
  "translation": [
    {"en": "完整英文句子1", "cn": "中文翻译1"},
    {"en": "完整英文句子2", "cn": "中文翻译2"},
    {"en": "完整英文句子3", "cn": "中文翻译3"}
  ],
  "vocabulary": [
    {
      "word": "example",
      "phonetic": "/ɪɡˈzæmpl/",
      "pos": "n.",
      "meaning": "例子，实例",
      "example": "This is an example sentence.",
      "synonyms": ["instance", "sample"]
    }
  ]
}
```

**关键要求**：`translation` 数组必须包含**完整原文的每一句**，逐句中英对照，不允许节选或摘要。

---

## 🔄 更新流程

```bash
# 1. 进入项目目录
cd /projects/GlobalNews

# 2. 创建当天内容目录
mkdir -p content/2026-04-05

# 3. 生成/编辑文章 JSON 文件
# ...

# 4. 提交并推送
git add content/2026-04-05/
git commit -m "Add articles for 2026-04-05"
git push origin main

# 5. 等待自动部署（约2-3分钟）
```

---

## 📚 内容规范

### 文章选择标准
1. **时效性**：24小时内发布的全球热点新闻
2. **来源**：Reuters, BBC, Guardian, AP 等权威媒体
3. **主题**：国际新闻、科技、商业、环境、文化
4. **避坑**：避免过于敏感的政治争议内容

### 难度分级标准

| 级别 | 词数 | 特点 |
|------|------|------|
| 🟢 初级 | 400-700 | 短句、常用词、单一段落 |
| 🟡 中级 | 700-1200 | 复合句、专业术语适中 |
| 🔴 进阶 | 1000-1800 | 复杂句式、专业词汇多 |

### 词汇选择原则
- 每篇 8-12 个重点词汇
- 优先选择：高频实用词、考试词汇、新闻常用词
- 包含：音标、词性、简明释义、例句、同义词

### 逐句翻译生成标准（重要）

**原则**：依赖 AI 能力完成完整拆分，不缩减原文。

1. **获取完整原文**：从来源网站获取文章完整正文（不删减段落）
2. **句子拆分**：按原文句号、问号、感叹号拆分句子
3. **逐句翻译**：每一句英文必须对应一句中文翻译
4. **数组格式**：`translation` 为对象数组，每个对象含 `en` 和 `cn` 字段
5. **完整性检查**：确保 translation 句子数量与原文句子数量一致

**示例工作流程**：
```
原文 → AI 分析句子边界 → 逐句翻译 → 生成 translation 数组 → 校验完整性
```

**禁止事项**：
- ❌ 只翻译部分句子（节选）
- ❌ 合并多个句子为一个翻译单元
- ❌ 删减原文段落或内容

---

*创建于 2026-04-05*
*更新于 2026-04-05 - 增加完整原文逐句翻译要求*
