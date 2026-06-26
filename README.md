# 汉英词典 Chinese-English Dictionary

一个覆盖 **271,712** 个汉语词条的开放词典数据集，以 CSV 格式分发，字段涵盖释义、拼音、词性、例句、近义词、HSK 等级、词书来源等。

> **免责声明**：本数据集中的例句、释义、用法说明等内容**均由 AI 大语言模型自动生成**，不代表作者或任何机构的立场、观点或意见。词汇的入选与 AI 生成内容无关，仅供学习与研究使用。

---

## 数据来源

词头（词形 + 拼音）来自以下公开资料的合并去重：

| 来源 | 词条数 |
|------|--------|
| CC-CEDICT（MDBG） | 主体词库 |
| 现代汉语大词典 | 100,805 |
| 中華語文大辭典 | 97,614 |
| 现代汉语规范词典 | 78,656 |
| 现代汉语词典（第7版）-拼音 | 74,494 |
| 现代汉语词典（第7版） | 58,559 |
| 近代汉语词典 | 48,291 |
| 古代汉语词典（第1版） | 36,217 |
| 臺灣台語常用詞辭典 | 25,063 |
| 兩岸差異用詞 | 5,433 |

词头确定后，**释义、词性、例句、近义词、搭配、语域等语义字段全部由 AI（大语言模型）批量生成**，并经过敏感词过滤清洗（参见下方说明）。

HSK 等级数据来自 [ivankra/hsk30](https://github.com/ivankra/hsk30) 和 [drkameleon/complete-hsk-vocabulary](https://github.com/drkameleon/complete-hsk-vocabulary)，按 `simplified + pinyin` 对齐合并。

---

## 文件说明

```
clean_dict.csv   # 主数据文件，UTF-8 with BOM，271,712 行
```

---

## 字段说明

| 字段名 | 类型 | 说明 |
|--------|------|------|
| `word_id` | 整数 | 唯一主键 |
| `simplified` | 文本 | 简体中文词形 |
| `pinyin_display` | 文本 | 带声调符号的拼音（xuéxí） |
| `pinyin` | 文本 | 机读拼音，音调用数字表示（xue2 xi2） |
| `hsk_level` | 文本 | HSK 等级（旧1–6级、旧7-9级、新1–7级），无则为空 |
| `part_of_speech` | 文本 | 词性（名词、动词、形容词…） |
| `brief` | 文本 | 简短英文释义（一行） |
| `meaning` | 文本 | 详细英文释义 |
| `usage` | 文本 | 用法说明（英文） |
| `simple_example` | 文本 | 中英双语例句 |
| `origin` | 文本 | 词源说明 |
| `tags` | 文本 | 主题标签 |
| `synonyms` | 文本 | 同义词 |
| `antonyms` | 文本 | 反义词 |
| `near_synonyms` | 文本 | 近义词 |
| `near_synonym_distinction` | 文本 | 近义词辨析 |
| `collocations` | 文本 | 常见搭配 |
| `register` | 文本 | 语域（正式、口语、书面语…） |
| `measure_word` | 文本 | 量词 |
| `grammar_pattern` | 文本 | 语法结构 |
| `valency` | 文本 | 动词配价 |
| `frequency_rank` | 整数 | 词频排名（数字越小越常用） |
| `cedict_definitions` | 文本 | CC-CEDICT 原始英文释义 |
| `status` | 文本 | 数据状态（filled / cedict 等） |
| `src_xiandai_da` | 0/1 | 收录于「现代汉语大词典」 |
| `src_zhonghua` | 0/1 | 收录于「中華語文大辭典」 |
| `src_guifan` | 0/1 | 收录于「现代汉语规范词典」 |
| `src_xiandai7_py` | 0/1 | 收录于「现代汉语词典第7版-拼音」 |
| `src_xiandai7` | 0/1 | 收录于「现代汉语词典第7版」 |
| `src_jindai` | 0/1 | 收录于「近代汉语词典」 |
| `src_gudai` | 0/1 | 收录于「古代汉语词典第1版」 |
| `src_taiwan` | 0/1 | 收录于「臺灣台語常用詞辭典」 |
| `src_liangan` | 0/1 | 收录于「兩岸差異用詞」 |

---

## 快速使用

### Python 直接读取

```python
import pandas as pd

df = pd.read_csv('clean_dict.csv', encoding='utf-8-sig')
print(df[['simplified', 'pinyin_display', 'brief']].head())
```

### 转换为 SQLite 数据库

```python
import pandas as pd, sqlite3

df = pd.read_csv('clean_dict.csv', encoding='utf-8-sig')
con = sqlite3.connect('dict.db')
df.to_sql('word', con, if_exists='replace', index=False)

# 建索引加速查询
con.execute('CREATE INDEX IF NOT EXISTS idx_simplified ON word(simplified)')
con.execute('CREATE INDEX IF NOT EXISTS idx_pinyin ON word(pinyin)')
con.commit()
con.close()
print('数据库已生成：dict.db')
```

### SQLite 查询示例

```python
import sqlite3

con = sqlite3.connect('dict.db')

# 查单词
row = con.execute("SELECT * FROM word WHERE simplified='学习'").fetchone()

# 查 HSK 旧4级词汇
hsk4 = con.execute("SELECT simplified, pinyin_display, brief FROM word WHERE hsk_level='旧4级'").fetchall()

# 查同时收录于多本词书的词
multi = con.execute("""
    SELECT simplified, (src_xiandai_da+src_zhonghua+src_guifan+src_xiandai7
                        +src_jindai+src_gudai+src_taiwan+src_liangan) AS n
    FROM word WHERE n >= 5 ORDER BY n DESC LIMIT 20
""").fetchall()
```

---

## 敏感词过滤说明

数据集在发布前经过多轮敏感词扫描，使用以下开源词库进行匹配删除：

- [cjh0613/tencent-sensitive-words](https://github.com/cjh0613/tencent-sensitive-words)（41,560 词）
- [konsheng/Sensitive-lexicon](https://github.com/konsheng/Sensitive-lexicon)（~51,000 词）

共删除 **1,112** 个匹配词条，涉及政治人名、政治机构、政治事件、色情词汇等类别。

---

## 许可证

数据集以 [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) 许可证发布，允许自由使用、修改和再分发，需注明来源。

AI 生成内容可能存在错误，**请勿将本数据集用于任何商业出版或正式教育考试材料**，使用前请自行核实关键字段的准确性。
