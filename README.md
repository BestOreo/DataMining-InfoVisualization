
### Display Entry:
http://120.77.220.71:8090/DM/index.html

# DataMining-InfoVisualization (Course Project, Zhejiang University)
This is the couse design for Course Information Visualization. The source data comes from Hacking Team  which is a Hacker Company in Italy. This company is hacked in 2015 and hackers upload all the emails records in this company. We are asked to dig worthwhile information from it and display it by information visualization philosophy and techinique.
Luckily, I got 99 scores from this course.

**This project is displayed by html, please click the index.html**
**本工程展示利用了html，请点击index.html**

One of charts in html:
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/10.png)


### HackingTeam Email data Source Download: https://pan.zju.edu.cn/share/7c368fa0035c2aab14919fbd9e


## Data Mining and Visualization of Emails in Hacking Team
### Chapter I Abstract
Hacking Team is an information technology company from Milan, Italy, which provides information systems intrusion and surveillance services to government agencies and law enforcement agencies. It helps customers to intercept Internet users, decrypt files, monitor to Internet calls such as Skype, and even turn on the microphone and camera remotely. On July 5, 2015, Hacking Team's official Twitter account was compromised by unidentified individuals, who used it to reveal many of the company's insider information and informed the company that its internal data had been leaked. The first notice states: "Anyway, we have nothing to hide, and we have to publish our emails, files, and source code ..." along with a download link for nearly 400G of data, including the intruder's alleged Internal e-mail, various related documents and source code.<br/> 

This particular data breach has aroused widespread concern in the community. One of the hot topics is how to decrypt Hacking Team's organizational structure and development process. Hacking Team's in-house email data is an important data source to understand the company, not only reflecting the complex communications network between employees and business partners, but also understanding the company's business content from email content and attachments. We did a preliminary formatting of the original mail data, but analyzing and understanding the mail data is still a very difficult task. Therefore, we provide formatted mail data provided, hope that participants as a data analyst, the use of visual analysis technology to analyze e-mail data to help us understand the history of Hacking Team Company and the various stages of business characteristics, identify the Inside the company's key figures and reasoning about their role and job responsibilities.

#### Chapter II Thought Introduction
This question is given to 59 csv files, a total of more than 10 million e-mail, so a huge amount of unstructured chaotic data. As the saying goes, see the issue from a different perspective. Our group decided to cut into topics from multiple dimensions, digging through the information in the email from different perspectives and then using reasonable visualization to show the data. We mainly use python for data mining, data visualization using html / css / javascript and third-party libraries d3.js, NVD, and Echart.

##### 2.1 classification work, the classification of personnel, the establishment of topological relations

This work is time-consuming and tedious. We carefully analyzed the mail address and display, found that if the address stage '/ 0 = HACKINGTEAM' is at the beginning, then this mail must be internal mail. Second, I found that if not, this format can not rule out the possibility of internal mail, because there is still a '@ hackingteam' for the domain name of the mailbox. We find it very puzzling to find out that '/ 0 = HACKINGTEAM' can be classified as '@ hackingteam.com' and '@ hackingteam.it' as it is Italian domain name, so this is also internal mails.<br/> 

Therefore, an e-mail is separated from the recipient, copying email, the sender, then the e-mail is divided into many e-mails. We believe that the recipient and the sender are internal staff is the internal mail.<br/> 

Then staff classification. First of all, we can confirm that the list of 59 csv personnel must be insiders. But after rough screening I found that there are many internal staff. This step is the basis for future work, so need to have both: 1 full name, 2 mailbox list was considered a legitimate internal staff. The screening process is divided into three steps: 1. Filter out all the address columns starting with '/ O = HACKINGTEAM', find the names of the people they contain, and convert them to the '@ hackingteam.com' mailbox. 2. Re-filter the address column, will be processed in addition to the first step into a list of mail. 3. Re-filter the display column, pulled into a list. Finally, the most important merge operation, I first go to the address list to find, if it contains 'hackingteam', then extract the name (this step is likely abbreviation), and then go to the display to find the full name (abbreviation need to match The first letter), if you can match, add this person, or add the mailbox.<br/> 

Segmentation of internal staff is difficult because we do not have specific email content, which can only be guessed based on titles. If a person has a large number of emails and received and he/she also has a lot of people contacting with him/her, the person must has high status in this company.<br/> 

By counting up the the mails within the company can we get the topology.

##### 2.2 Timing of mail statistics

According to the employee category cross-reference table and employee name table previously obtained, we can easily filter out the 10 million e-mail to find who are internal staff and outsiders. The internal staff mail by monthly statistics, if the person sent the original month, then that the company has an employee this month, thus get the statistics of the development of the company.

##### 2.3 stage keyword statistics

According to the segmentation point of the company's general plan as a critical point for stage division, and then statistics for each stage of the high frequency words, draw stage theme cloud, dig some from the cloud to some of the key information, as a breakthrough in the re- E-mail screening and keyword related mail.

##### 2.4 Industrial Business Statistics

Hacking Team is a hacker technology company, then the company's internal mail there will inevitably be a large number of operating systems, hacking techniques related vocabulary. We filter out these terms for statistics and classification to determine Hacking Team's work business, business changes, means of attack and the target platform and other information.

#### Chapter III Introduction to Visual Engineering

##### 3.1 Hacking Team Development Overview

Hacking Team is a hacker technology company in Italy that provides hacking services to the governments. The company was firstly founded in 2001, when the company only had two founders.<br/> 

In the next series of diagrams, each point represents a mailbox suffix, and the connection between the two points represents the connection between the companies. The coarsest connection means the closer the relationship is. We tested the Hacking Team's business scale and the trading partner's service status between 2001 and 2015, and it is clear that Hacking Team's size has evolved over time. Since 2005, Hacking Team has started to grow quickly. By 2009, it has already had a relatively large number of customers. After that, it has entered its first period of upward development. The result of 2011 has surprised us very much. Afterwards, the customers The number is even more huge.<br/> 
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/%E5%9B%BE%E7%89%87%201.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/2.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/3.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/4.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/5.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/6.png)

##### 3.2 Working hours
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/7.png)

According to the company's internal staff to send mail time we found Hacking Team's staff usually work from 17:00 to 24:00. **Why? Is this because programmers are night owls?<br/> **

We found in the following mining of customer sources, the United States is Hacking Team's largest source of customers and business countries. The 17 o'clock Italian time is just 8 o'clock local time in San Francisco, New York local time 11 o'clock. Therefore, we speculate that the business relationship between Hacking Team and a large number of U.S. clients during this time period is the reason why the Hacking Team is in a day and night timetable.

##### 3.3 Hacking Team Mail Overview
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/8.png)

Through this picture, we can overview the development process of Hacking Team. The blue bar represents the total amount of emails in the current month, and the yellow line represents the number of active internal staffs in the current month. The total number of internal staff at the time of the start-up only two people, after the gradual expansion of the size of the ranks of development, at its highest reached more than 90 people. From the company's mail growth situation, there are four main stages, three turning points.<br/> 
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/9.png)

##### 3.4 Stage Business Overview

Based on the previous time-series analysis of internal mail and external mail, we divided hacking team's business development into four phases. Therefore, for each stage, we calculated the number of repetitions of each mail subject during the period through the way of Python data analysis to identify those topics that are more frequently repeated, and then filtered the first 15 topics to display the word cloud.

According to the advice of the TA, we revised the general email map to improve the interaction.
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/10.png)

Click on different time points will display the corresponding stage keywords.
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/11.png)


The first stage: 2001 / 01-2013 / 06 start-up period
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/12.png)

From the first phase of the company word cloud you can find:

(1) Azerbaijan, India, Kuwait, Oman, Israel, Georgia, HT are the main communication countries, indicating that the key clients of the hacking team in the business start-up are likely to come from India, Azerbaijan, Kuwait, Oman, Israel, Georgia, Haiti and other countries .<br/> 
(2) It can also be seen from keywords such as Expression of Interest, Delivery Azerbaijan, Azerbaijan Delivery Confirmation, Presentations and Demonstrations, etc. The company is expressing its interest to partners, confirming information transmission and delivery, and demonstrating and demonstrating the company's capabilities. Seen in this light, the stage of the company more focused on external business development and customer contact.<br/> 
(3) There are also some specific projects carried out by the company. It can be seen from Corsi prossima settimana, Rosso Pomodoro and Prototipo valigetta that the company has conducted a series of courses entitled "Lessons for next week", "red tomatoes" and "prototype briefcase" Business projects, because of the specific security issues involved, therefore using the action code to represent a business.<br/> 
(4) In the specific business forms, the company's main business is still RCS.<br/> 

The second stage: 2013 / 07-2014 / 01 rapid development period

From the second phase of the company word cloud can be found:
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/13.png)


(1) From the key words such as Mobile Hacking, AV Monitor, hardware test, BIOS, Mac and PC, the company conducts business invasion through these forms.<br/> 
(2) From the DAP, it can be found that the way the company attacks is mainly data acquisition and processing.<br/> 
(3) From Moldova, Slovacchia, Guatemala, HT, it can be seen that the companies in this phase of the company's business are located in the country of the company.<br/> 
(4) Noting Delivery and Training is an important topic, the company is likely to focus on project delivery and software usage training for business members during this time.<br/> 
(5) There are also some action codes that we can not infer from specific business, such as: sulcorriere<br/> 

The third stage: 2014 / 02-2014 / 05
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/14.png)

The third phase of the company in the state of the business is slightly tightened, the word cloud can be found in its business as follows:<br/> 

(1) There are some specific business projects, the action code: compagni di pranzo, Italian Lasagna, Olimpia Marcon.<br/> 
(2) The main business countries are: Puma, Indonesia, Ecuador, Malaysia, Azerbaijan, Uzbeki, etc., indicating that the business scope has been expanded during this period.<br/> 
(3) For the specific business, note that the keywords delivery, Proposal, Situation, Payment, maintenance, training, Specifications, Tentative date indicate that the company in this period is expanding its business to more countries, taking over new projects, Communication Identify the characteristics of the project; deliver and train the ongoing project; maintain the previous project.<br/> 
(4) For the specific business forms, it is still dominated by RCS, and at the same time, the support for URLs has been added.<br/> 

The fourth stage: 2014 / 06-2016
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/15.png)
The fourth phase is the most important core business phase of the company, with a dramatic increase in the volume of mail at this stage.<br/> 

(1) First, the company's popular e-mail topics at this stage are largely related to life, Pranzo gioved (Thursday lunch), E Max si sposa! (Bride of Max Max), Arrivederci (goodbye) From the point of view of the number of e-mails, it is a well-deserved "big theme" in terms of the entire company's development history. But do not rule out the possibility of action code.<br/> 
(2) The countries contacted are mainly Puma, Kazakstan, BAJA (a Hungarian city), HT and so on.<br/> 
(3) In terms of business, the terms DAT document, demo, Urgent, Draft Contract, Delivery & Installation indicate that the company drafted a variety of businesses from document drafting to project delivery at this stage.<br/> 
(4) There are also many less understood topics during this period, such as Global Protect for Yosemite, Tramezzino, which is likely to be the action code for the project. <br/> 
(5) Campagna elettorale !!! The subject matter is likely to be related to the company's internal campaign.<br/> 

##### 3.5 business statistics (means of attack and platform)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/16.png)

Hacking Team, a company that provides surveillance, hacking, and information security services primarily to governments, uses Rcs, virus and our common trojan, wap, malware, dos attacks and more. Its main operating platform skype, windowsphone, android, blackberry, synbian, windows, linux, ios and so on.

##### 3.6 Business Statistics (client)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/17.png)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/18.png)

These eight email suffixes are the eight email suffixes most relevant to the Hacking Team. Nice, an AI service and visual data company, guessed that the Hacking Team company had a lot of monitoring material available to nice companies for data visualization. (Haha ~) dhag is probably Marathi in India, and .vn is Vietnam's domain name, which should be Vietnam's mailbox. Gnse is an information security services company. Robottec is a robotics company.
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/19.png)

##### 3.7 Business Statistics (client time development)
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/20.png)

By 2010, Hacking Team was still small and took up a relatively small amount of international business. After 2010, it will take over a lot of international business. Among them, the United States has the largest volume of business, followed by Oman, Thailand, Azerbaijan and Italy.

Although the title only gave us 59 csv files, but according to the mining situation, we found that the number of people in the company actually more than 90 people, then how to show the importance of internal staff?

##### 3.8 The importance of company employees map
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/21.png)

We set the total amount of mail to be sent, the total amount of mail received, the total amount of mail sent and received, the total number of people sent, the total number of mail recipients sent, the total number of sent / sent, the total accepted / the total number of senders Seven dimensions are used thermographs to show all internal employees send and receive e-mail situation.
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/22.png)

We can find the top 11 individuals must be the company's executives.

##### 3.9 Internal staff diagram
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/23.png)

Based on the TA's advice, we re-ordered everyone, brought company executives together, and lowered the contrast of the whole image to improve observability.
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/24.png)

According to the previous decision of the senior management, internal relations of staff production, and senior executives separately out.
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/25.png)


The high level of communication among top executives shows that previous top-level speculation was correct and that senior executives would not have a well-balanced relationship if some of them were not executives.

### Chapter IV, workload

In order to deal with such a large amount of data, we mainly use python to process data mining. First of all need to send and receive mail when the classification of people, because a person may have more than one trumpet, multiple e-mail number may correspond to a person. We first classify and replace this part of the information. Then use python to mine and count the valuable information of more than 10 million messages. Three pre-python may write four or five thousand lines, the latter part of the drawing mainly used echart, d3.js template to modify and organize. Pro before showing some of the less suitable figure to re-take a more appropriate way to visualize.

After the show, despite the busy week of exams, we also modified several html based tutorials to improve interactivity. And think of several questions given by the TA, some of which we have given our thoughts and discussions have given our thoughts and mentioned in the report.

### Chapter V, Difficulties and Summary
When I did this project, I actually encountered a lot of difficulties.

In fact, initially we do not have a good command of some web languages such as HTML, CSS, JavaScript and the understanding of the websites is relatively limited. But fortunately these languages are not difficult to learn. Through the project, we finally got a better understanding of these languages.<br/>

Later in the process of doing the questions, we actually did not have a very good solution to the problem at the beginning, and the entire team was in a rather dizzy state. We just started from the Internet to find a lot of visual example, to see what can be used to our data, if you can try it, but later found only more fragmented analysis, did not form a good overall idea .<br/>

The biggest challenge is how to extract and classify valid information from over 10 million pieces of messy e-mail messages. At the beginning of our thinking there was a incorrect deviation that emails should be grouped in accordance with the year and the title information, so there are 15 groups, which is  unintelligible. Second, in 2004 and 2005, for example, these two years are still the start-ups of the company. Therefore, it is unscientific to separate these into two years. The phased approach to science should be based on turning points. When we figure out the following figure, we take the turning point of the company's development as the dividing line to calculate the word frequency, and the statistical result is convincing.<br/>
![pic](https://github.com/BestOreo/Pic-for-README.md/blob/master/datamining%26%26infovisualization/26.png)

Later, we finally came to form our own thinking, that is, what kind of analysis we should carry out with these figures, and what conclusion we can draw, so that we can think further about new points for visualization.<br/>

Of course, there are some ideas from the final realization is still a long distance, in terms of implementation, we spent a lot of time for Python data analysis, we often use some statistical methods to find some of the data in the law, and then Sex with different maps for visualization.<br/>

One of the difficulties is that the title is mixed in Italian and English. After we screened the key words in different stages, we translated these related words (Italian) into Google Machine and identified some important information with the naked eye, such as the names of some countries (the same country in the mail may have English and Italian Two kinds of representation. Some of the hacking keywords are also carried out separately, and then re-search the massive data statistics.<br/>

Although we encountered a lot of difficulties in this project, we are very grateful to this project from which we have learned a lot. The project not only brought us a great improvement from the technical level, such as front-end, Python and other programming proficiency increases, but also for our data analysis, data visualization has greatly improved. In fact, the subject is still a relatively raw csv data, which requires us to work on a lot of effort in data processing. As for the selection and design of specific visualization models, a great deal of what teachers say in class is used. To tell the truth, the teacher told a lot about the principles and knowledge of visualization in class. At first glance, it feels very simple and natural. However, it is natural to learn how to visualize. After this process of application, we have a better understanding of basic principles of data visualization.<br/>

Finally, there is a deeper feeling that good visualization must be done after thinking and analyzing rather than directly from data to conclusion. Based on some preliminary analysis, depending on the specific goals, we hope to add some more detailed features and elements, and then generate more useful information. Good visualization is by no means obtained directly from the data, but rather continuously improved.<br/>


### HACKING TEAM 邮件信息可视化

##### ——信息可视化课程大作业

小组成员： 郭爽  沈锴  葛帅琦 

#### 第一章、题目概览与背景介绍

Hacking Team 是一家来自意大利米兰的信息技术公司，该公司向政府部 门及执法机构提供信息系统入侵与监视服务，它帮助客户截获 Internet 用户 间的通信、解密文件、监听 Skype 等网络通话、甚至还可以远 程开启麦克风 和摄像头。2015 年 7 月 5 日， Hacking Team 公司的官方 Twitter 帐号 遭到不明人士入侵，入 侵者用此帐号公布了该公司许多内幕信息并通告该公司 的内部数据已经泄露。首条通告写道：“反正我们 也没什么东西好藏，那就把 我们的电子邮件、文件、源代码都发布出来…”，并附有近 400G 数据的下载 链 接，其中包含入侵者所称的内部电子邮件、各种相关文件和源代码。

这次特殊的数据泄露事件引起了社会各界的广泛关注，其中一项热门议题 是如何解密 Hacking Team 公 司的组织结构和发展历程。Hacking Team 公司内部电子邮件数据是了解该公司的重要数据源，它不但能反映公司员工间 及与业务对象间的复杂通信网络，还可以从邮件内容与附件中了解公司经营的 业务内容。我 们对原邮件数据进行了初步的格式化处理，但分析和理解这批邮 件数据仍然是一项非常艰巨的任务。因此， 我们将格式化后的邮件数据提供出 来，希望参赛者以数据分析师的身份，采用可视分析技术来分析邮件数 据，帮 助我们了解 Hacking Team 公司发展历程及各阶段业务特点，找出该公司内 部的重要人物并推理其担任的角色与工作职责。

#### 第二章、思路介绍

本问题所给 59 个 csv 文件中，共计邮件一千余万封，如此海量的数据用 三个字来概括难、繁、杂。古人云：横看成岭侧成峰。我们组决定从多个维度 切入题目，从不同的角度去挖掘邮件中的信息然后用合理的可视化手段将数据 显示出来。我们主要使用 python 进行数据挖掘，用 html/css/javascript 以 及第三方封装库 d3.js，NVD 以及 Echart 进行数据可视化显示。

##### 2.1 分类工作、人员分类、人员拓扑关系的建立

这部分工作耗时繁琐。我们仔细分析了邮件的 address 和 display，发 现 address 阶段如果以’/0=HACKINGTEAM’开头，那么这个邮件一定是内部 邮件。其次发现如果不是这种格式也不能排除内部邮件的可能，因为还存 在’@hackingteam’为域名的邮箱。我们觉得很疑惑，经过查找资料，认 为’/0=HACKINGTEAM’可以归为’@hackingteam.com’， 而’@hackingteam.it’的 it 是意大利的域名，因此这个也是内部邮件。

因此将一封邮件按照接受者、抄送者、密送者分开，将一封邮件分成很多份邮件。我们认为接受者和发送者都为内部人员才是内部邮件。

然后是人员分类。首先我们可以确认，由 59 个 csv 组成的人员列表一定 是内部人员。但我经过粗粗筛选发现内部人员还有很多。这一步的工作是以后 的工作的基础，因此需要同时具备：1.全名，2.邮箱列表 才认为是一个合法的 内部员工。筛选工作分成三步：1. 筛选出 address 列的所有 以’/O=HACKINGTEAM’开头的邮箱地址，找出包含的人名，然后将其转换成’@hackingteam.com’的邮箱。2. 重新筛选 address 列，将除了第一步处 理过的邮箱都拉成一个列表。3. 重新筛选 display 列，拉成一个列表。4. 最 后是最关键的合并操作，我先去地址列表中寻找，如果包含’hackingteam’， 就提取出人名（这一步很可能是人名缩写），然后去 display 中寻找完整的人 名（缩写需要匹配第一个字母），如果能匹配到，就新增这个人，或者新增邮 箱。

内部员工的细分很困难，因为我们没有具体的邮件内容，只能做到根据特 征猜测。我们从认为一个人如果在收发邮件总量、和他有邮件联系的人总量、 平均每一个人的邮件数都有很高的占比的话，就可以认为这个人不会是一个小员工。

统计内部员工的邮件往来总数就可以得到拓扑图。

##### 2.2 邮件时序的统计

根据之前得到的员工类别对照表和员工名字对照表，可以轻松筛选出一千万条邮件中哪些是内部人员哪些是外部人员。将内部人员的邮件按每个月统 计，如果该人员在这个月发送过原件，则认为该公司这个月有一个员工，从而 统计出公司发展总图。

##### 2.3 阶段关键词的统计

根据公司发展总图的分段点作为临界点进行阶段划分，然后统计每个阶段 中出现的高频词，绘制阶段主题云图，从云图中挖掘一些到一些关键信息，以 此为突破口在重新从邮件中筛选和关键词相关的邮件。

##### 2.4 工业业务的统计

Hacking Team 是一家黑客技术公司，那么这家公司的内部邮件中必然会有大量的和操作系统，黑客攻击技术相关的词汇。我们把这些词汇筛选出来进行统计和分类，从而确定 Hacking Team 的工作业务，业务变迁，攻击手段 和目标平台等信息。

#### 第三章、可视化工程介绍

##### 3.1 Hacking Team 发展概览

Hacking Team 是一家位于意大利的黑客技术公司，为政府提供黑客服 务。这家公司最早创立于 2001 年，公司创始人仅有两人。

在接下来一系列的关系图中，每个点代表一种邮箱后缀，两点之间的连线 代表公司之间的联系，连线越粗意味着关系越为密切。我们测试了 2001 年到 2015 年 Hacking Team 的业务规模、交易伙伴的服务状况，可以很明显的看 到 Hacking Team 公司的规模随时间发展的状况。从 2005 年开始， Hacking Team 公司开始发展，到 09 年的时候已经有了比较可观的客户数 量，之后则进入了第一个上升发展期，到 2011 年的结果已经让我们十分惊讶，之后的客户数量则更为庞大。
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
