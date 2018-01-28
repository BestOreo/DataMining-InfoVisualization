# DataMining-InfoVisualization (Course Project, Zhejiang University)
This is the couse design for Course Information Visualization. The source data comes from Hacking Team  which is a Hacker Company in Italy. This company is hacked in 2015 and hackers upload all the records about emails of staff in this company. We are asked to dig worthwhile information from it and display it by information visualization techinique.
Luckily, I got 99 scores from this course.

** This project is displayed by html, please click the index.html **
本工程展示利用了html，请点击index.html

### HACKING TEAM 邮件信息可视化

##### ——信息可视化课程大作业

小组成员： 郭爽  沈锴  葛帅琦 

#### 第一章、题目概览与背景介绍

Hacking Team 是一家来自意大利米兰的信息技术公司，该公司向政府部 门及执法机构提供信息系统入侵与监视服务，它帮助客户截获 Internet 用户 间的通信、解密文件、监听 Skype 等网络通话、甚至还可以远 程开启麦克风 和摄像头。2015 年 7 月 5 日， Hacking Team 公司的官方 Twitter 帐号 遭到不明人士入侵，入 侵者用此帐号公布了该公司许多内幕信息并通告该公司 的内部数据已经泄露。首条通告写道：“反正我们 也没什么东西好藏，那就把 我们的电子邮件、文件、源代码都发布出来…”，并附有近 400G 数据的下载 链 接，其中包含入侵者所称的内部电子邮件、各种相关文件和源代码。

这次特殊的数据泄露事件引起了社会各界的广泛关注，其中一项热门议题 是如何解密 Hacking Team 公 司的组织结构和发展历程。Hacking Team 公司内部电子邮件数据是了解该公司的重要数据源，它不但能反映公司员工间 及与业务对象间的复杂通信网络，还可以从邮件内容与附件中了解公司经营的 业务内容。我 们对原邮件数据进行了初步的格式化处理，但分析和理解这批邮 件数据仍然是一项非常艰巨的任务。因此， 我们将格式化后的邮件数据提供出 来，希望参赛者以数据分析师的身份，采用可视分析技术来分析邮件数 据，帮 助我们了解 Hacking Team 公司发展历程及各阶段业务特点，找出该公司内 部的重要人物并推理其担任的角色与工作职责。

#### 第二章、思路介绍

本问题所给 59 个 csv 文件中，共计邮件一千余万封，如此海量的数据用 三个字来概括难、繁、杂。古人云：横看成岭侧成峰，我们组决定从多个维度 切入题目，从不同的角度去挖掘邮件中的信息然后用合理的可视化手段将数据 显示出来。我们主要使用 python 进行数据挖掘，用 html/css/javascript 以 及第三方封装库 d3.js，NVD 以及 Echart 进行数据可视化显示。

##### 2.1 分类工作、人员分类、人员拓扑关系的建立

这部分工作耗时繁琐。我们仔细分析了邮件的 address 和 display，发 现 address 阶段如果以’/0=HACKINGTEAM’开头，那么这个邮件一定是内部 邮件。其次发现如果不是这种格式也不能排除内部邮件的可能，因为还存 在’@hackingteam’为域名的邮箱。我们觉得很疑惑，经过查找资料，认 为’/0=HACKINGTEAM’可以归为’@hackingteam.com’， 而’@hackingteam.it’的 it 是意大利的域名，因此这个也是内部邮件。

因此将一封邮件按照接受者、抄送者、密送者分开，将一封邮件分成很多 份邮件，认为接受者和发送者都为内部人员才是内部邮件。

然后是人员分类。首先我们可以确认，由 59 个 csv 组成的人员列表一定 是内部人员。但我经过粗粗筛选发现内部人员还有很多。这一步的工作是以后 的工作的基础，因此需要同时具备：1.全名，2.邮箱列表 才认为是一个合法的 内部员工。筛选工作分成三步：1. 筛选出 address 列的所有 以’/O=HACKINGTEAM’开头的邮箱地址，找出包含的人名，然后将其转换成’@hackingteam.com’的邮箱。2. 重新筛选 address 列，将除了第一步处 理过的邮箱都拉成一个列表。3. 重新筛选 display 列，拉成一个列表。4. 最 后是最关键的合并操作，我先去地址列表中寻找，如果包含’hackingteam’， 就提取出人名（这一步很可能是人名缩写），然后去 display 中寻找完整的人 名（缩写需要匹配第一个字母），如果能匹配到，就新增这个人，或者新增邮 箱。

内部员工的细分很困难，因为我们没有具体的邮件内容，只能做到根据特 征猜测。我们从认为一个人如果在收发邮件总量、和他有邮件联系的人总量、 平均每一个人的邮件数都有很高的占比的话，就可以认为这个人不会是一个小 员工。

统计内部员工的邮件往来总数就可以得到拓扑图。

##### 2.2 邮件时序的统计

根据之前得到的员工类别对照表和员工名字对照表，可以轻松筛选出一千 万条邮件中哪些是内部人员哪些是外部人员。将内部人员的邮件按每个月统 计，如果该人员在这个月发送过原件，则认为该公司这个月有一个员工，从而 统计出公司发展总图。

##### 2.3 阶段关键词的统计

根据公司发展总图的分段点作为临界点进行阶段划分，然后统计每个阶段 中出现的高频词，绘制阶段主题云图，从云图中挖掘一些到一些关键信息，以 此为突破口在重新从邮件中筛选和关键词相关的邮件。

##### 2.4 工业业务的统计

Hacking Team 是一家黑客技术公司，那么这家公司的内部邮件中必然会有大量的和操作系统，黑客攻击技术相关的词汇。我们把这些词汇筛选出来进行统计和分类，从而确定 Hacking Team 的工作业务，业务变迁，攻击手段 和目标平台等信息。

#### 第三章、可视化工程介绍

##### 3.1 Hacking Team 发展概览

Hacking Team 是一家位于意大利的黑客技术公司，为政府提供黑客服 务。这家公司最早创立于 2001 年，公司创始人仅有两人。

在接下来一系列的关系图中，每个点代表一种邮箱后缀，两点之间的连线 代表公司之间的联系，连线越粗意味着关系越为密切。我们测试了 2001 年到 2015 年 Hacking Team 的业务规模、交易伙伴的服务状况，可以很明显的看 到 Hacking Team 公司的规模随时间发展的状况。从 2005 年开始， Hacking Team 公司开始发展，到 09 年的时候已经有了比较可观的客户数 量，之后则进入了第一个上升发展期，到 2011 年的结果已经让我们十分惊 讶，之后的客户数量则更为庞大。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/%E5%9B%BE%E7%89%87%201.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/2.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/3.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/4.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/5.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/6.png)

##### 3.2 工作时间 
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/7.png)

按照公司内部人员发送邮件的时间我们发现 Hacking Team 公司的员工 都会在 17 点到零点工作。这是为什么呢，是因为程序员都是夜猫子？

我们在之后的客户来源挖掘中发现，美国是 Hacking Team 最大的客户 来源以及业务往来国家。而意大利时间的 17 点正好是美国旧金山当地时间的 8 点，纽约当地时间的 11 点。所以我们猜测，这个时间段内 Hacking Team 和美国客户的大量邮件往来，存在的业务关系是 Hacking Team 昼夜颠倒的 时间表的原因。

##### 3.3 Hacking Team 邮件人员总览 
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/8.png)

通过这张图可以总览 Hacking Team 的发展流程，其中蓝色条代表当月 邮件总量，黄线代表当月活跃的内部员工数。公司内部人员总数在初创时仅有 两人，在之后的发展中队伍规模逐渐扩张，在最高的时候达到了 90 余人。从 公司的邮件增长情况来看，主要有四个阶段，三个转折点。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/9.png)

##### 3.4 阶段业务总览

根据前面关于内部邮件与外部邮件的时序分析，我们将 hacking team 公 司的业务发展分成了四个阶段。因此对于每个阶段，我们通过 Python 数据分 析的方式统计出每个邮件主题在该阶段内重复的次数，从而确定出那些重复频 率较高的主题，然后筛选前 15 个主题进行词云的展示。

根据助教的意见我们对邮件总图进行了修改，提高交互性。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/10.png)

点击不同的时间点会显示对应阶段的关键词。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/11.png)


第一阶段：2001/01-2013/06 初创时期
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/12.png)

从第一阶段的公司词云中可以发现：

（1） Azerbaijan、India、Kuwait、Oman、Israel、Georgia、HT 是主 要的沟通国家，说明业务初创时期 hacking team 公司的主要客户很可 能来自印度、阿塞拜疆、科威特、阿曼、以色列、格鲁吉亚、海地等国 家。 
（2） 同时还可以从 Expression of Interest，Delivery Azerbaijan， Azerbaijan Delivery Confirmation，Presentations and Demonstrations 等关键词看到，公司在向合作伙伴表达利益诉求，进 行信息传送与传送确认，展现和证明公司的能力。由此看来，该阶段公 司更多的着重于对外进行业务拓展与客户联系。 
（3） 公司也开展了一些具体的项目，由 Corsi prossima settimana， Rosso Pomodoro，Prototipo valigetta 可知，公司开展了一些代号 为“下一周的课程”、“红色的西红柿”、“原型的公文包”的业务项 目，由于涉及到具体的安全问题，因此采用行动代号的方式来表示一项业务。
（4） 在具体的业务形式方面，公司主要的业务还是 RCS。

第二阶段：2013/07-2014/01 迅速发展时期

从第二阶段的公司词云中可以发现：
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/13.png)


（1） 从 Mobile Hacking，AV Monitor，hardware test，BIOS，Mac and PC 等关键词看到，公司通过这些形式进行业务入侵。 
（2） 从 DAP 可以发现，公司在攻击时的方式主要是数据获取与处理。 
（3） 从 moldova，slovacchia，Guatemala，HT 可以看出该阶段公司的业务来往的公司所在国家。 
（4） 注意到 Delivery and Training 是一个重要的主题，因此该公司这段时间很可能着重于项目的交付与对业务成员的软件使用培训。 
（5） 同时也有一些行动代号，我们无法从中推断出具体的业务，如：sulcorriere

第三阶段：2014/02-2014/05
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/14.png)

第三阶段的公司处于业务稍有紧缩的状态，由词云可以发现其业务情况如下：

（1） 有一些具体的业务项目，其行动代号：compagni di pranzo，Italian Lasagna，Olimpia Marcon
（2） 业务来往的国家主要有：Puma，Indonesia，Ecuador，Malaysia， Azerbaijan，Uzbeki 等，说明该时期业务范围得到了扩大。 
（3） 对具体的业务来说，注意到关键词 delivery，Proposal，Situation， Payment，maintenance，training，Specifications，Tentative date 说明该时期公司：在进行业务对更多国家的扩展；接手新的项目， 交流确定项目的特征；交付与培训正在进行的项目；维护之前的项目。 
（4） 对于具体的业务形式，仍然以 RCS 为主，同时这段时间增加了对 URL 的支持功能。

第四阶段：2014/06-2016
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/15.png)
第四阶段为公司最核心最重要的业务阶段，该阶段邮件数量急剧增长。

（1） 首先，该公司在这个阶段邮件热门主题很大程度上与生活息息相关， Pranzo gioved（星期四的午餐）、E Max si sposa!（E Max 的新 娘）、Arrivederci（再见）这几个主题，从邮件数量的角度来说，从整 个公司的发展历程来看，是当之无愧的“大主题”。但也不排除可能是 行动代号。 
（2） 联系的国家主要有 Puma、Kazakstan、BAJA（匈牙利的一个城 市）、HT 等。 
（3） 在业务方面，DAT document，demo，Urgent，Draft Contract， Delivery & Installation 等词语，表明该阶段公司从文件起草到项目交 付各种各样的业务都有。 
（4） 这一时期也有许多不太能明白的主题，如 Global Protect for Yosemite，Tramezzino，很可能是项目的行动代号 （5） Campagna elettorale!!!主题很可能和公司内部的竞选有关。

##### 3.5 业务统计（攻击手段与平台）
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/16.png)

Hacking Team 作为一家主要为各国政府提供监控、黑客渗透以及信息安全服务的公司，其主要使用的攻击手段有 Rcs,virus 以及我们常见的 Trojan 木马，wap，malware，dos 攻击等等。其主要经营的平台有 skype， windowsphone，android，blackberry，synbian，windows，linux，ios 等。

##### 3.6 业务统计（服务对象）
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/17.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/18.png)

这八个邮箱后缀是与 Hacking Team 关系最为密切的 8 个邮箱后缀。 Nice 公 司是一家人工智能服务以及可视化数据公司，猜测是 Hacking Team 这家公 司把大量的监听材料给了 nice 公司做数据可视化。（haha~）dhag 可能是印度的马拉地语，.vn 是越南的域名，这应该是越南的邮箱。 Gnse 则是一家信息安全服务公司。Robottec 是一家机器人自动化公司。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/19.png)

##### 3.7 业务统计（服务对象时间发展）
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/20.png)

在 2010 年前，Hacking Team 公司规模还比较小，接手的国际业务数量 也比较少。2010 年后开始大量接手国际业务。其中美国的业务量是最多的， 其次是阿曼，泰国，阿塞拜疆，意大利等。

虽然题目只给了我们 59 个 csv 文件，但是根据挖掘的情况来看，我们发 现公司内部的人数其实最多的时候超过了 90 人，那么如何来显示内部人员的 重要性呢？

##### 3.8 公司员工职能重要性图
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/21.png)

我们设置了发送邮件总量、接受邮件总量，收发邮件总量，发送的人总 数，其发送的邮件接受人总数，发件总量/发送的人总数，接受总量/发件人总 数共七个维度用热力图的方式来显示所有内部员工的收发邮件的情况。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/22.png)

我们可以找到最前面的 11 个人必然是公司的高管。

##### 3.9 内部员工关系图
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/23.png)

根据助教的意见我们对所有人重新进行了排序，公司高管放到了一起，并且降 低了整张图的对比度，从而提高可观性。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/24.png)

我们按之前判定的高管情况，制作内部员工的关系图，并且把高管单独标注出来。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/25.png)


高管之间通信十分均匀，说明之前高管的猜测是正确的，如果其中有人不 是高管，高管的关系图不会如此均匀。

### 第四章、工作量

为了处理如此大量的数据，我们主要采用 python 来进行数据的处理挖 掘。首先需要对邮件收发时的人员进行归类，因为一个人可能会有多个小号， 多个邮件号可能对应一个人。我们首先对这部分信息进行了归类和替换。然后 用 python 去挖掘以及统计一千多万条邮件的有价值信息。三人前期 python 可能就写了四五千行，后期的绘图主要用了 echart，d3.js 的模板进行修改和 整理。临展示前又对一些不大合适的图重新采取更合适的方式来进行可视化。

展示后，尽管考试周很忙，我们还是按助教给的建议对几个 html 进行了 修改，提高交互性。并且思考助教给出的几个问题，其中几个问题的回答我们 经过思考和讨论都已经给出了自己的想法并在上述的报告中提及。

### 第五章、困难与总结
在做这个 project 时，其实遇到了很多困难。

其实最初的我们并不是很了解 HTML、CSS、JavaScript 这些语言和框 架，对前端的了解也比较少，所以这些语言几乎要从头学起。虽然工作量比较 大，但所幸这些语言学起来不是很难，后面 project 进行过程中，用起来也不 需要掌握很多高端的框架。经过一段时间的学习，我们最终对这些语言有了一 个基本的了解。

后来在做题的过程中，我们一开始其实对问题没有一个很好的解决思路， 整个团队都处于比较晕头转向的状态。一开始我们只是从网上找了很多可视化 的 example，看看有什么能用到我们的数据上的，如果可以就尝试一下，但后 来发现都只是比较零散的分析，没有形成一个很好的整体思路。

最大的困难是如何从杂乱无章的 1000 多万条邮件信息中提取出有效的信 息并进行分类。一开始我们思路上出现了偏差，觉得应该按照年份去分组标题 信息，这样出现 15 个组，每个组单独拎出来也是不知所云。其次例如 2004 年和 2005 年，这两年都还算是公司的初创期，所以把这两年给割裂开是不科 学的。科学的分阶段方式应该是按照转折点来分。当我们统计出下图后，以公 司发展的转折点为分界线进行词频的统计，统计出的结果才是有说服力的。
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/26.png)

后来我们终于渐渐地形成了我们自己的思路，即用这些图我们要进行怎样 的分析，得出怎样的结论，从而进一步思考新的点来进行可视化。

当然有了一些思路距离最终的实现其实还是有很远距离，在实现方面，我 们用了很多时间来进行 Python 数据分析，我们常常会先用一些统计的方法发 现数据中的一些规律，然后再针对性用不同图进行可视化。

这其中还有一个难点是：标题中意大利文和英文夹杂。我们筛选出不同阶 段的关键词后，把这些关系词（意大利文）用谷歌机器翻译了一遍，用肉眼确 定一些重要的信息，例如一些国家的名字（邮件中同一个国家可能有英文和意 大利文）两种表示。把一些黑客攻击的关键词也单独拎出来，然后再到海量的 数据中重新检索统计。

尽管这其中我们遇到了很多困难，但我们非常感谢这个 project，使我们 学到了很多。这个 project 不仅从技术层面带给了我们很大的提升，比如前 端、Python 等编程方面熟练度的增加，更使我们对于数据分析、数据可视化 方面有了很大的提升。题目给的 csv 其实总来说还是一个比较 raw 的 data， 这就需要我们在数据处理上下很多功夫。而对于具体可视化模型的选择与设计的过程中，则大量地用到了老师上课讲的东西。说实话，上课时老师讲了很多 有关可视化的原则和知识，咋一看总感觉很简单、很自然，但有没有学会心里 其实是没底的，但经过这个运用的过程后，自己就对上课讲的知识有了更加深 刻的理解，这种感觉其实非常好。

最后有一个比较深刻的感受就是，好的可视化一定边做边分析边思考得出 的，而不是从数据到结论一步到位的。基于一些初步的分析后，根据具体的目 标，我们希望会加一些更多功能和元素，然后产生更多有用的信息。好的可视 化作品绝不是由数据直接得到的，而是不断改进得到的。
