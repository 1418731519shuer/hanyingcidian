# 汉英词典 Chinese-English Dictionary

一个覆盖 **271,000+** 个汉语词条的开放词典数据集，以 CSV 格式分发，字段涵盖释义、拼音、词性、例句、近义词、HSK 等级、词书来源等。

---

# 数据集免责声明（完整版）

本数据集（以下简称"数据集"）由编纂方（以下简称"我方"）提供，旨在促进语言学习与研究。我方现将数据集**完全开放**，用户可**自由下载、复制、修改、分发、用于商业或非商业任何目的**，无需事先取得我方授权。但请您在使用前仔细阅读以下免责条款，一旦使用即视为完全接受。

---

## 一、使用自由与授权
我方明确授予所有用户**无限制的使用权**，包括但不限于：
- 个人学习、课堂教学、学术研究；
- 嵌入商业软件、训练AI模型、出版引用；
- 二次加工、再分发、转售（以数据集原样或修改后形态）。

我方不会对上述任何使用方式收取费用或追究侵权责任（涉及第三方版权的内容除外，见第三条）。

---

## 二、内容来源与不承担责任声明
1. **AI生成性质**：数据集中所有词条、释义、拼音、例句、词性、近义词、HSK等级等，均由人工智能大语言模型自动生成或辅助整理，**未经人工逐条审校**。我方**不对数据的准确性、完整性、可靠性、时效性、适用性作任何明示或暗示的保证**。
2. **使用后果自负**：用户因使用本数据集而产生的任何直接或间接损失（包括但不限于教学失误、考试失利、商业决策错误、法律纠纷、系统故障等），**我方概不负责**。用户应自行承担所有风险，并在关键场景中交叉验证权威来源。
3. **不构成专业建议**：数据集内容仅为参考，不构成语言教学、翻译、考试辅导或其他专业领域的正式建议，用户需自行判断其适用性。

---

## 三、第三方版权与知识产权
数据集中的个别释义、例句可能涉及受版权保护的文学片段、成语典故等，其版权归原作者或合法权利人所有。我方仅作汇编整理，**不对这些原始内容主张权利**。若用户在使用中涉及这些内容，应自行取得相应授权。我方整体汇编成果虽有一定独创性，但鉴于我方已开放免费使用，亦不主张对汇编结构的排他性权利。

---

## 四、爱国立场与内容合规承诺
1. **坚决拥护党的领导**：我方及数据集内容始终**坚决拥护中国共产党的领导，全面贯彻党的教育方针，坚持社会主义核心价值观**，弘扬中华优秀传统文化，积极传播正能量。
2. **内容合规性**：我方已尽最大努力确保数据集中不含任何违反中国法律法规、危害国家安全、破坏民族团结、宣扬暴力恐怖、淫秽色情、封建迷信或侮辱诽谤他人的信息。
3. **问题整改机制**：若用户在数据集中发现任何不当内容（包括但不限于政治表述偏差、历史文化错误、歧视性言论等），请及时通过官方渠道向我方反馈。我方承诺**在收到反馈后立即核查，并于第一时间进行下架、修改或删除等整改措施**，坚决维护国家利益和社会稳定。

---

## 五、法律适用与免责最终条款
本声明适用中华人民共和国法律。我方在任何情况下（包括但不限于疏忽、违约、侵权等）均不对用户因使用本数据集而产生的任何索赔、损害或损失承担责任，即使已被告知可能发生此类损害。本声明最终解释权归我方所有。

---

**使用本数据集即表示您已阅读、理解并完全接受上述所有条款。**
**如有异议，请勿使用。**

---

最后更新日期：2026年6月26日

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

词头确定后，**释义、词性、例句、近义词、搭配、语域等语义字段全部由 AI（大语言模型）批量生成**，并经过敏感词过滤清洗。HSK 等级数据来自 [ivankra/hsk30](https://github.com/ivankra/hsk30) 和 [drkameleon/complete-hsk-vocabulary](https://github.com/drkameleon/complete-hsk-vocabulary)，按 `simplified + pinyin` 对齐合并。

---

## 字段说明

| 字段名 | 类型 | 说明 |
|--------|------|------|
| `word_id` | 整数 | 唯一主键 |
| `simplified` | 文本 | 简体中文词形 |
| `pinyin_display` | 文本 | 带声调符号的拼音（xuéxí） |
| `pinyin` | 文本 | 机读拼音，音调用数字表示（xue2 xi2） |
| `hsk_level` | 文本 | HSK 等级（旧1–6级、旧7-9级、新1–7级），无则为空 |
| `part_of_speech` | 文本 | 词性 |
| `brief` | 文本 | 简短英文释义 |
| `meaning` | 文本 | 详细英文释义 |
| `usage` | 文本 | 用法说明 |
| `simple_example` | 文本 | 中英双语例句 |
| `origin` | 文本 | 词源说明 |
| `tags` | 文本 | 主题标签 |
| `synonyms` | 文本 | 同义词 |
| `antonyms` | 文本 | 反义词 |
| `near_synonyms` | 文本 | 近义词 |
| `near_synonym_distinction` | 文本 | 近义词辨析 |
| `collocations` | 文本 | 常见搭配 |
| `register` | 文本 | 语域 |
| `measure_word` | 文本 | 量词 |
| `grammar_pattern` | 文本 | 语法结构 |
| `valency` | 文本 | 动词配价 |
| `frequency_rank` | 整数 | 词频排名 |
| `cedict_definitions` | 文本 | CC-CEDICT 原始英文释义 |
| `status` | 文本 | 数据状态 |
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

# 查被5本以上词书收录的词
multi = con.execute("""
    SELECT simplified, (src_xiandai_da+src_zhonghua+src_guifan+src_xiandai7
                        +src_jindai+src_gudai+src_taiwan+src_liangan) AS n
    FROM word WHERE n >= 5 ORDER BY n DESC LIMIT 20
""").fetchall()
```

---

## 敏感词过滤说明

发布前经过多轮人工辅助 + 自动化敏感词扫描，使用以下开源词库：

- [cjh0613/tencent-sensitive-words](https://github.com/cjh0613/tencent-sensitive-words)
- [konsheng/Sensitive-lexicon](https://github.com/konsheng/Sensitive-lexicon)

共删除 **1,100+** 词条，并对近义词、反义词、例句字段进行额外扫描清理。
