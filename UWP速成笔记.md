# UWP速成笔记

夏令营期间速成了一下微软家的前端工具UWP。

推荐环境：Blend for Visual Studio 2019 / Visual Studio 2019

需要安装Visual Studio的UWP开发组件。在`tools and extensions`里面安装。

如果你使用的是Visual Studio 2017，可能会出现无法使用实时preview功能，建议升级为2019版本。

## Quick Start

首先新建UWP项目。

然后你会看到`App.xaml`和`MainPage.xaml`，前面的不用管。后面的就是我们的主页面。

xaml文件类似于HTML文件，熟悉HTML的同学很快就能上手。

关于常用的组件，可以去Windows store里面下载`xaml Controls Gallery`。里面有几乎所有常用的组件及其基本代码，更重要的是它本身就是用UWP写的，所以里面的组件都有展示效果，很方便很强大，缺点就是不够详细。

比较详细的可以查阅文档，微软的UWP文档写的相当好。

[UWP doucumentation](https://docs.microsoft.com/en-us/windows/uwp/)

现在你可以看到`MainPage.xaml`的内容了。

```xaml
<Page
    x:Class="Github_example.MainPage"
    xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
    xmlns:local="using:Github_example"
    xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
    xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
    mc:Ignorable="d"
    Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">

    <Grid>

    </Grid>
</Page>
```

`<Page></Page>`中是页面的内容。

`<Grid></Grid>`是一个组件，能按照几行几列分割页面。其基本的使用是：

```xaml
<Grid>

</Grid>

```