# 用于 Rime 输入法 (五笔方案) 的词库

目前缺乏权威汉语词语数据，各大厂商在线词库，冗余紊乱，因此，做了一个轻量版的五笔词库，由“一个单字词库”和“三个扩展词库”组成。

其中，单字词库由 25 个一级简码、613 个二级简码和 8105 个《通用规范汉字表》组成。

## 一个单字词库

- `wubi86.dict.yaml`，删除了 [rime-wubi](https://github.com/rime/rime-wubi) 社区方案，根据[《通用规范汉字表》](http://www.gov.cn/zwgk/2013-08/19/content_2469793.htm)做了一份简体单字库。

另外配置了 `import_tables` key，以引入扩展词库。

```yaml
import_tables:
  - wubi86_dict_chengyu      # 成语词库
  - wubi86_dict_ciyu         # 词语词库
  - wubi86_dict_xzqh         # 中国行政区划词库
  - wubi86_dict_it           # IT 相关词库
  # - wubi86_dict_extra        # 个人扩展词库
  # - wubi86_dict_work         # 个人工作相关词库
  # - wubi86_dict_user         # 个人私有词库 (生活)
```

## 多个扩展词库

- `wubi86_dict_chengyu.dict.yaml`，包含 32,642 个成语
- `wubi86_dict_ciyu.dict.yaml`，包含 316,757 个词语
- `wubi86_dict_it.dict.yaml`，包含 1,522 个 IT 行业常用词语
- `wubi86_dict_it.dict.yaml`，包含 481 个 中国行政区划词库 (省份/城市)，无“省、市、区/地区、县、盟、新区、林区、经济开发区、<民族>自治州/自治县”等行政单位，仅地名。

其中成语和词语来自[汉典网](https://www.zdic.net/)，已去除冗余。

## 建议配置 `wubi86.schema.yaml`

```yaml
translator:
  dictionary: wubi86                 # 翻译器将调取此字典文件
  enable_charset_filter: true        # 开启字符集过滤
  enable_completion: true            # 显示编码未输入完整的词条

  enable_user_dict: true             # 开启用户词典，记录动态字频和用户词频
  enable_sentence: true              # 句子输入模式
  enable_encoder: false              # 自动造词
  encode_commit_history: true        # 对已上屏词自动造词 (仅 table_translator 有效)

  max_phrase_length: 2               # 自动生成词的最大长度
  user_dict: user                    # 用户词典名
  db_class: tabledb                  # 用户词典类型 (二进制/userdb, 人类语言/tabledb)
  disable_user_dict_for_patterns:    # 不需要录入用户词典的编码
    - "^z.*$"                        # 禁止拼音反查调频
    - ^[a-y]{1,2}$                   # 禁止单码字调频
  comment_format:                    # 提示码自定义
    - xform/.+//                     # 当前默认不提示编码，消除所有候选词后的提示码
```

建议维护自己其它方面的词库。

## Feature

1. 未来会将词频部分分享出来，大部分人中的一部分，输入应是具有共性的；
2. 商务印馆有出版《现代汉语常用词表》（第2版），本打算基于它做一套词典方案的，找了一圈没有找到 PDF 文件，未来有机会再整。

## Resources

- [YAML 入门教程](https://www.runoob.com/w3cnote/yaml-intro.html) / [The Official YAML Web Site](https://yaml.org/)
- [深蓝词库转换](https://github.com/studyzy/imewlconverter)
- [五笔码表助手 for Rime](https://github.com/KyleBing/wubi-dict-editor)
- [百度输入法-词库](https://shurufa.baidu.com/dict)
- [搜狗输入法-词库](https://pinyin.sogou.com/dict/)
- [QQ 输入法-词库](http://cdict.qq.pinyin.cn/)
