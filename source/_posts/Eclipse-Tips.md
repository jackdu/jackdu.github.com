title: Eclipse Tips
date: 2014-09-08 11:50:41
categories: 折腾
tags: [eclipse, 有意思, tips]
---

保存时发现 Android 代码的缩进每次都有变化
===

```Java
// Original
new ArrayAdapter<String>(actionBar.getThemedContext(),
    android.R.layout.simple_list_item_1, android.R.id.text1, new String[] {
    (R.string.title_section1), (R.string.title_section2), (R.string.title_section3), }), this);
```

第一次保存：

```Java
// First Sava Action
new ArrayAdapter<String>(actionBar.getThemedContext(),
                        android.R.layout.simple_list_item_1, android.R.id.text1, new String[] {
                                getString(R.string.title_section1),
                                getString(R.string.title_section2),
                                getString(R.string.title_section3), }), this);
```

随便改动一下，比如在最后加个空格，再一次保存：

```Java
// Second Sava Action
new ArrayAdapter<String>(actionBar.getThemedContext(),
                        android.R.layout.simple_list_item_1, android.R.id.text1, new String[] {
                        getString(R.string.title_section1),
                        getString(R.string.title_section2),
                        getString(R.string.title_section3), }), this);
```

原因是在`首选项 -> Java -> 保存操作`中既选中了`格式化源代码 -> 格式化所有行`，又在选中了`其他操作 -> 配置 -> 代码组织 -> 更正缩进`，而两者的标准不一样导致了每次保存时代码缩进的变化，去掉后面那个即可。

