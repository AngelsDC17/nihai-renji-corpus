# 数据字段说明

## entries.jsonl（一行一条判语，共 19,294 条）

```json
{
  "book": "01-shanghan",
  "part_name": "伤寒论",
  "h2": "条12",
  "h3": "讲解判语",
  "quote": "倪师原话（单行字幕级引文）",
  "bvid": "BV17P84z8EPS",
  "ep": 1,
  "part": 1,
  "section": 3,
  "t_hms": "00:33:20",
  "source_file": "renji-01-伤寒-太阳病上篇",
  "note": ""
}
```

| 字段 | 含义 |
|---|---|
| `book` | 所属部：`01-shanghan` `02-jinkui` `03-bencao` `04-neijing` `05-zhongjing` `06-zhenjiu` |
| `part_name` | 部名中文 |
| `h2` / `h3` | 章目 / 子类（对应 `docs/` 各部的二、三级标题：条号、药名、篇名、穴位等） |
| `quote` | 倪师原话。**粒度为单行烧录字幕**（平均 13 字），照录 OCR 主源，不据残字臆改 |
| `bvid` | B 站视频号 |
| `ep` | 该部内的集号（伤01–15、金01–21、本01–14、内01–19、仲01–04、针01–44） |
| `part` | 视频分P号。人纪各集均为单 P，恒为 `1` |
| `section` | 集内语义段号（对应 `sections/`） |
| `t_hms` | 该判语在本集内的起始时间 |
| `source_file` | 抽取来源篇目（54 篇之一） |
| `note` | 考据标注；空串表示无 |

**回放 URL**：`https://www.bilibili.com/video/{bvid}?t={t_hms换算秒}`
（人纪单 P，无需 `?p=`；出处标签形如 `[伤01 §3 @00:33:20]`）

### 关于条目粒度

人纪判语是**逐行字幕级**引文（平均 13 字），与《天纪》语料库的段落级引文（平均 141 字）不同。
这个粒度为**逐句回放**设计：点任一条直达该句所在的那一秒，适合跟读与字幕导播。
若用于 RAG，建议改用按语义段聚合的 [`corpus-rag.md`](corpus-rag.md)，或按 `book + h2 + section` 自行合并。

## sections/{bvid}_p01.json（每集语义段索引，共 117 个）

```json
{ "section": 3, "t_start_ms": 1980000, "t_end_ms": 2350000, "topic": "太阳中风提纲" }
```

## corrections-ledger.jsonl（勘误账本，67 条）

OCR / ASR 错型的登记与裁决记录。产出方只登记不改主源，由监督方逐条裁决；
其中 `layer: g4_false_positive` 类为门禁误报裁决（如本草原文「黄连真黄」撞紫微「廉贞」崩字）。
