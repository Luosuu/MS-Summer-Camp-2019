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
    <Grid.RowDefinitions>
        <RowDefinition Height = "50" />
        <RowDefinition Height = "*"/>
        <RowDefinition Height = "2*"/>
    </Grid.RowDefinitions>

    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="50" />
        <ColumnDefinition Width="Auto" />
        <ColumnDefinition />
    </Grid.ColumnDefinitions>

    <StackPanel Orientation="Vertical" Grid.Row="1">
        <TextBlock Text="Hello"/>
        <TextBlock Text="world"/>
    </StackPanel>

</Grid>

```

*表示按比例分割区域，上面的代码就代表着第二行和第三行的比例是1：2

想要在Grid中布置组件，只需要在`<Grid></Grid>`中声明组件，然后在组件的属性中加入如`Grid.Row = "1"`表示组件在Grid中的位置。上面的代码就在第一行的位置上布置了一个组件StackPanel。

StackPanel能按照一定的方向排列组件。排列的方向由属性"Orientation"决定。

## 常用的结构

### UWP非常具有独特风格的NavigationView框架

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

    
    <NavigationView x:Name="nvSample">
        <NavigationView.MenuItems>
            <NavigationViewItem Icon="Play" Content="Menu Item1" Tag="SamplePage1" />
            <NavigationViewItem Icon="Save" Content="Menu Item2" Tag="SamplePage2" />
            <NavigationViewItem Icon="Refresh" Content="Menu Item3" Tag="SamplePage3" />
            <NavigationViewItem Icon="Download" Content="Menu Item4" Tag="SamplePage4" />
        </NavigationView.MenuItems>

        <Frame x:Name="contentFrame">
            <Grid>
            </Grid>
        </Frame>
    </NavigationView>
   
</Page>
```

`<Frame></Frame>`中就是除了框架的内容页面。

使用了NavigationView自然要进行页面跳转。页面跳转的实现部分要放在`MianPage.xaml.cs`中实现。

页面跳转有两种方法，一个是`ItemInvoked`，另外一个是`SelectionChanged`。前者只要发生NavigationView的item点击事件就会被检测到，后者只有当选择的item发生变化时才会发生。下面展示一个使用`ItemInvoked`的页面跳转的实现。

```C#
 private void NvSample_ItemInvoked(NavigationView sender, NavigationViewItemInvokedEventArgs args)
        {
            if (args.IsSettingsInvoked == true)
            {
                contentFrame.Navigate(typeof(SettingsPage), args.RecommendedNavigationTransitionInfo);
            }         
            else
            {
                TextBlock ItemContent = args.InvokedItem as TextBlock;
                switch (ItemContent.Tag)
                {
                    case "Recog_page":
                        {
                            contentFrame.Navigate(typeof(Recog_page));
                        }
                        break;
                    case "SP2":
                        {
                            contentFrame.Navigate(typeof(SamplePage2));
                        }
                        break;
                    case "SP3":
                        {
                            contentFrame.Navigate(typeof(SamplePage3));
                        }
                        break;
                    case "SP4":
                        {
                            contentFrame.Navigate(typeof(SamplePage4));
                        }
                        break;
                    default:
                        {
                            contentFrame.Navigate(typeof(MainPage));
                        }
                        break;                    
                }
            }
        }
```

上述的实现通过识别item的不同tag属性来进行跳转。由于NavigationView自带的Setting不具备tag属性，所以就先只好判断`IsSettingInvoked`。

使用`contentFrame.Navigate(typeof())`进行页面跳转，识别的是.xaml.cs文件中的类的名称，而不是xaml文件里的name。

xaml文件的地位并不高，只是方便我们搭建框架而已，实际上xaml文件完全可以不写，完全使用C#搭建框架，只是这样没有编辑xaml直观方便。

## 在UWP中使用图片

你可能需要使用到BitmapImage类，但是BitmapImage类默认不在UWP项目的引用列表里，所以需要手动添加

```C#
using windows.UI.Xaml.Media.Imaging;
using <MianPage的命名空间，一般是项目名>.Views;//有的时候不必要添加
```

BitmapImage类使用Uri进行加载资源文件，UWP的资源文件默认都放在项目里的Assets文件夹里。

```C#
BitmapImage picture = new BitmapImage();
picture.UriSource = new Uri("ms-appx:Assets/dog.jpg");
```

然后就可以把这个属性赋给一些图片，让他们重新加载资源图片。如果xaml文件里有一个Image组件，属性有`x:name = Sample`，那么就可以在.xaml.cs文件里，使用`Sample.Source=picture`来重新加载图片。
