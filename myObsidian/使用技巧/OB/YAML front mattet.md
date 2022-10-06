YAML front matter 是 Obsidian 储存文档级元信息的方法。

Front matter 是由纯文本构成的、放置于文件开头的属性信息。这是将元数据放入 Markdown 文件中的好方法。

Front matter 在开头和结尾处都有三个 `-`。它需要放置在文件开头才能被识别。

示例：

```
---
key: value
key2: value2
key3: [one, two, three]
key4:
- 4
- 5
- 6
---
```

从 0.9.17 版本开始，[笔记的别名](https://publish.obsidian.md/help-zh/%E4%BD%BF%E7%94%A8%E6%8C%87%E5%8D%97/%E4%B8%BA%E7%AC%94%E8%AE%B0%E6%B7%BB%E5%8A%A0%E5%88%AB%E5%90%8D)可以在 Front matter 中出现。未来，我们将让开发者更容易访问 Front matter，同时也会让 Front matter 对用户更加友好。

当前 Obsidian 包含三个原生的 key：`tags`、`aliases` 以及 `cssclass`。****

aliases: 别名属性 这个是可以在引用中直接搜索的， 不同于｜ 后面的别名 只能用于显示
tags： 标签属性 分类用 
Spaces are not allowed in tags. So, to differentiate two or more words in a tag, you can use these case styles/formats:
他们都是一样的
-   camelCase: [#twoWords](https://publish.obsidian.md/#twoWords)
-   PascalCase: [#TwoWords](https://publish.obsidian.md/#TwoWords)
-   snake_case: [#two_words](https://publish.obsidian.md/#two_words)
-   kebab-case: [#two-words](https://publish.obsidian.md/#two-words)

