# 黄金点游戏学习

本篇主要是讲我如何学习根据微软的相关AI工具制作一个能参加微软黄金点游戏的AI。

[黄金点游戏的教案](https://github.com/microsoft/ai-edu/tree/master/B-教学案例与实践/B8-自构建－AI游戏开发案例－黄金点游戏/微软-方案1)

[微软黄金点游戏的介绍](https://github.com/microsoft/ai-edu/tree/master/C-开发工具与环境/微软黄金点程序工具/OnlineGame)

[微软AI教育共建平台](https://github.com/microsoft/ai-edu)

首先这个游戏已经提供了C#和python的基础框架。如果你使用这两个语言，那么只需要完成算法的核心部分，完成在`GeneratePridictionsNumbers`函数即可。

[BotDemolnCsharp](https://github.com/microsoft/ai-edu/tree/master/C-开发工具与环境/微软黄金点程序工具/OnlineGame/BotDemoInCSharp)

[BotDemolnPython](https://github.com/microsoft/ai-edu/tree/master/C-开发工具与环境/微软黄金点程序工具/OnlineGame/BotDemoInPython)

甚至有一个[依托于Azure Notebooks的版本](https://notebooks.azure.com/fatterbetter/projects/goldennumbernotebook)。可以免去配置环境，直接在线运行示例Bot。

如果你使用其他语言进行开发。那么可以自己到黄金点游戏的介绍中扎到RESTful API的介绍，自己搭建框架。

那么现在的问题就在与如何生成C#或者Python的AI代码。完成目标函数。

夏令营中使用的工具是不限的。这里列举一些常用的。

1. ML.NET
   * 使用C#，本意是为了C#开发者可以方便的学习和使用机器学习模型，可以在三大主流平台使用，Windows可以在Visual Studio中安装，有官方教程。
   * 内置了很多模型，并按照用处分类，可以按照分类方便的测试内置的模型并且排名，选择较高效率的模型直接生成代码。甚至有Auto ML功能，可以方便的处理数据。可以应对小型的场景化开发。
2. Azure AI
   * 可以在Visual Studio和Visual Studio Code中安装相关插件，提供认知和训练服务。需要有Azure账号并且有订阅。国内世纪互联的订阅疑似在VSC上识别不到。国外的订阅需要VISA信用卡。
   * 教程多，模型好，服务全面。不过由于是在网上跑模型，而且模型一般都比较大，速度不一定有保障，黄金点游戏要求每一局游戏开始后5s内上交数据。如果是基于过于的对局情况预测接下来的黄金点可能会比较慢吧。也有可能我没用明白。

由于没有任何限定，其实用任何框架和工具都可以。