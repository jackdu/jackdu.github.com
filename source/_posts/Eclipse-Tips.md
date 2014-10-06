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

原因是在`首选项 -> Java -> 保存操作`中既选中了`格式化源代码 -> 格式化所有行`，又选中了`其他操作 -> 配置 -> 代码组织 -> 更正缩进`，而两者的标准不一样导致了每次保存时代码缩进的变化，去掉后面那个即可。


Updated: 2014-10-06 20:10:04

Eclipse 重新导入包含 jni 的 Android 工程时出现"Unresolved inclusion"错误
===

在`Eclipse`上创建一个新的含有 jni 内容的 Android 工程(也就是需要使用`Android NDK`工具编译动态库或者静态库的工程)时，`Eclipse`可以正确解析诸如`jni.h/stdio.h`等头文件。但是如果在另外一台电脑上导入此工程时，`Eclipse`会提示这些头文件无法解析，并标出黄色的警告。可以按照如下步骤消除这些警告：

1. 关闭打开的`Eclipse`工程
2. 删除工程所在文件夹中的`.cproject`文件
3. 打开工程所在文件夹中的`.project`文件
    * 删除`name`为`org.eclipse.cdt.managedbuilder.core.genmakebuilder`和`org.eclipse.cdt.managedbuilder.core.ScannerConfigBuilder`的`buildCommand`节点
    * 删除四个`CDT`相关的`nature`:
        * <nature>org.eclipse.cdt.core.cnature</nature>
        * <nature>org.eclipse.cdt.core.ccnature</nature>
        * <nature>org.eclipse.cdt.managedbuilder.core.managedBuildNature</nature>
        * <nature>org.eclipse.cdt.managedbuilder.core.ScannerConfigNature</nature>
4. 打开`Eclipse`工程，使用`Android Tools -> Add Native Support...`功能重新添加库，注意名称要和以前的相同。因为`jni`目录下的文件都没有变动过，所以`Android Tools`不会再次添加同名的`C/C++`文件。