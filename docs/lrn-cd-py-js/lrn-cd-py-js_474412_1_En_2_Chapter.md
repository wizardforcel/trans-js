© 作者，独家授权给Springer Fachmedien Wiesbaden GmbH，隶属于Springer Nature 2024 J. L. Zuckarelli 使用Python和JavaScript学习编程 [https://doi.org/10.1007/978-3-658-42912-6_2](https://doi.org/10.1007/978-3-658-42912-6_2)

# 2. 为什么学习编程？

Joachim L. Zuckarelli^([1](#Aff2) )(1)德国慕尼黑概述

你已经决定阅读这本书，因此显然不需要再说服你去学习编程。然而，在这一章中，回顾一下学习编程的意义仍然是值得的。

尽管（职业）程序员在我们现代社会中有时看起来像是知识工作者中的超级明星，但他们常常面临一些充满夸张成见的偏见。即使作为一名业余程序员，你也会遇到这些偏见。我们将在本章中讨论这些偏见和刻板印象。

## 2.1 很多值得学习的理由

学习编程值得的原因包括以下几点：

### 2.1.1 让你的日常生活更轻松！

会编程意味着你可以自动化那些原本需要手工完成、既繁琐又容易出错的任务。这不仅提高了你的生产力，而且让工作变得更加轻松，因为通常是那些乏味、单调、重复的——简而言之：令人烦恼的任务，最能通过程序实现自动化。

微软 Excel 是今天办公室工作人员的瑞士军刀。除了少数例外情况，例如以撰写详细的法律文书、合同和其他法律文件为主要业务模式的律师事务所，Excel（以及其他供应商的电子表格，如 Google 的电子表格）现在几乎在各个领域和各种用途上都有应用，从预算规划和商业案例到项目计划和待办事项列表。许多用户不知道，Excel（像其他微软办公软件一样）内置了一个强大的编程语言——*Visual Basic for Applications*，简称 *VBA*。这个编程语言使你能够自动化甚至是复杂的过程。举个例子，假设你有多个客户或员工调查问卷的 Excel 文件，并且现在想将它们合并成一个工作簿。当然，你可以手动打开每个文件，读取或复制值，然后粘贴回合并后的工作簿。更快且更安全的做法（即，减少错误的风险）是编写一个小的 VBA 程序，自动完成这个任务。现在你可能会反驳，开发和测试 VBA 程序需要时间，直到它正常工作。的确，开发这样一个小的宏，VBA 程序的另一种叫法，通常比你最初估计的时间要长。然而，自动化任务的挑战要比枯燥的手动复制数据更加激动人心。VBA 程序的优势在于，当你稍后需要重复这个任务时，尤其是因为有新的调查结果时，它的优势显现得淋漓尽致。

尝试让你的同事，甚至是你的老板，印象深刻，展示你如何迅速而轻松地完成许多看起来像是耗时的噩梦项目。云服务 *Dropbox* 的创始人之一德鲁·休斯顿曾说过：“编程是我们最接近超能力的东西。” 这一说法表达了编程中蕴含的神奇之感，这种观念在许多其他程序员的言论中也有所体现。但当然，这种感觉对外行人来说才显得神秘。那些“魔法师”自己知道这些“魔法”是如何运作的，他们的“能力”根本不是什么超自然的。

微软创始人比尔·盖茨在年轻时就证明了，知道如何编程有时能让生活变得更加愉快。他和他的朋友、后来成为微软联合创始人的保罗·艾伦，干预了盖茨高中时间表软件的设计方式，结果他突然发现自己进入了一门几乎全是女孩的班级。正如他自己所说，他与任何一位女同学都相处不好，这至少不是因为他的编程技能。

### 2.1.2 说“IT”！

这是一个已经被重复了千百遍的观察，但即便如此，它依然是真实的，那就是：信息技术（IT）在公司和其他组织中，包括公共部门，变得越来越重要。几乎没有一个现代组织的商业运作不受数字化进程的影响。有时，甚至商业模型本身也在这个过程中发生了变化。当然，结果是，IT部门在内部变得越来越重要，正因为有越来越多的问题和挑战只能通过与内部IT部门或外部IT顾问的合作来解决。即使你自己不在IT部门工作，而是在一个传统的“专业部门”里，比如销售部门或财务部门，你也会接触到一些项目和计划，其中IT会做出重要的贡献。因此，了解“IT”基本是如何运作的，什么是技术上可解决的，什么是无法解决的，以及大致需要哪些步骤来解决问题，这些都具有巨大的优势。特别是当你紧密参与涉及IT组成部分的项目时，这一点尤为重要。过去那种写上百页复杂商业概念的时代已经过去，那些商业概念往往被IT部门或多或少地误解并转化为技术解决方案。如今，敏捷方法如SCRUM正日益兴起，其开发周期更短，而且（内部）“客户”，即定义技术解决方案商业需求的人员，参与到设计、实施和测试中的程度远远超过过去。换句话说，与IT的合作变得更加密切和重要，互相理解也变得至关重要。作为一名编程专家，你会比其他人更具备这一点，而有了这种理解，即使你对他们使用的具体技术毫无头绪，你也能更轻松地与IT同事平等地讨论问题。实际上，比起精通某一特定技术，更重要的是认识到哪些问题是可以解决的（例如自动化方面），哪些是无法解决的，理解解决问题的思路，并能够预见出解决问题的最重要步骤。这样，你就能成为IT同事的宝贵技术伙伴，有效推动你的技术问题！

顺便提一下，如果你有志于更高层次的职位：过去，由于IT在运营中的不重要性，管理层直到包括执行董事会成员在内的管理人员可以对IT话题视而不见的时代已经结束。未来，几乎没有人能在没有IT实现方案的理解下，仅仅凭借在华丽的演示幻灯片上展示狂野的战略而轻松过关。

### 2.1.3 赚钱！

我们刚刚提到，IT变得越来越重要，并且今天已经具有极大的重要性。

这一点在劳动力市场数据中也得到了体现。根据*美国劳工统计局*的《职业前景手册》，在2021年，美国有1,425,900人从事软件开发工作。这个职业群体的年薪中位数为120,730美元，明显高于美国员工的平均收入（45,760美元）。如果你还没有决定职业方向，或者想要重新调整方向，显然这是一个具有吸引力的领域。劳工统计局预计，在2021至2031年间，这一行业的就业将增长26%。

当然，你不一定非得争取一个永久职位才能将编程技能转化为收入。自由职业者可以在各种互联网平台上提供服务。以流行的网站*Upwork*为例，写作时，平台上在“桌面软件开发”、“移动开发”和“网页开发”类别中显示了27,333个项目，客户将这些项目交给自由职业者进行承接。当然，许多来自低工资国家的软件开发者也在这些平台上交易，他们愿意接受较低的报酬，尽管他们通常是经过良好培训并具备技能的劳动者。要在像Upwork这样的平台注册并取得成功，你需要建立良好的声誉，因为你部分通过以前客户的评价来获取新客户。当然，这使得一开始尤其困难。然而，这里有一种方法是，最初接受较低的费用，并通过展示其他方式（例如私人编程项目）来证明自己的技能，这些项目你可以通过像*GitHub*这样的平台展示给潜在客户。尽管通过此类互联网平台做自由职业可能会带来许多困难，尤其是在初期，但它依然是一个绝佳的机会，可以让你实践并测试自己新获得的技能，几乎没有风险，并且无需离开你的主职工作。

最后，你还可以从为单个客户做合同工作中脱离出来，开发自己的软件或网络服务，并将其提供给更广泛的受众。是否可以在保持日常工作的同时做到这一点（无论是实践上还是法律上），只能逐个案例决定，并且肯定需要一些关于风险偏好的深思熟虑。然而，多个实例表明，即使在有限的时间内，凭借企业活动在软件和互联网业务中取得成功也是可能的。毕竟，你的产品不一定非要是下一个Facebook。

### 2.1.4 理解支撑世界核心的力量！

到目前为止，我们谈论的更多是生活中平凡的事情，关于如何通过编程让你的生活变得更轻松，推进你的职业项目并赚取金钱。如果你对这些不太感兴趣，而是有着学习更多关于我们复杂世界运作的崇高目标，那么你无法避开编程。

如果歌德的《浮士德》活在今天，他不会与魔鬼签订契约，而是会学习编程。

我们的世界正日益被所谓神秘的算法力量所主导。尽管如此，许多人对于算法是什么以及它们如何工作缺乏理解，而希望你在阅读上一章之后已经建立起了这种理解。根据*Bertelsmann Foundation*发布的2018年研究《欧洲对算法的认知与看法》，在10,960名欧洲调查对象中，48%的人承认他们要么没听说过算法（15%），要么不知道它是什么（33%）。有趣的是，研究发现，能够理解算法的人更能看到算法所提供的机会。

所以，我们生活在一个越来越被技术和问题解决方法所塑造的世界，而这些许多人并不理解。过去情况不同。学校曾经让每个人或多或少地掌握了当时主要技术的工作原理。任何在学校里用心的人都知道一辆车是如何工作的，电力是从哪里来的，以及基于劳动分工的工业生产为何具有效率优势。然而，现在公共教育已经失去了方向。我们稍后会回到这个话题。

如果你想形成一个关于算法的机会与风险的有根据的观点，并参与到关于这一话题的社会讨论中，那么根据Bertelsmann的调查，你需要比许多欧洲人了解更多关于算法的知识。你必须能够自己编程吗？不，当然不必。但是任何曾经自己开发过一个小程序的人，都会有更深的理解。

### 2.1.5 训练你的逻辑思维和解决问题的能力！

常有人说，学习拉丁语能更好地理解语法，尽管它的纯粹交流功能（除了或许在梵蒂冈，那里的意大利语可能也行）相当有限。学习拉丁语意味着更好地理解语法，是因为如果你想翻译拉丁文文本，你必须比在其他语言中更多地涉及语法问题，例如英语。通过这种方式，你学习了语法的基本概念，比如不同的格及其用法，这些可以被应用到其他语言中。因此，学习拉丁语有其益处，即使你不是那些因职业原因需要掌握至少基础拉丁语的人，比如历史学家或医生。

编程也类似。在很少的其他领域，你能学会如何系统地处理问题，将问题拆解成更简单的子问题，为每个子问题制定解决方案，最终将子问题的解决方案拼接起来，得到原始问题的答案。系统化解决问题的能力不仅在编程中有用，在生活的*各个方面*都能帮助你。如果你学会了编程，你会以不同的方式看待这个世界，并且以更有结构和更注重解决方案的方式去应对各种问题。也许，这种逻辑思维方式是最值得学习编程的原因。

## 2.2 陈词滥调与偏见

现在我们已经讨论了为什么学习编程有意义的几个好理由，接下来我们花点时间澄清一下许多人对编程的陈词滥调和偏见。

### 2.2.1 编程只是书呆子做的事

有些人依然有一种印象，认为编程者是那种长了青春痘、戴着眼镜的男少年，他们的主食是披萨和可乐，整晚不停地敲击键盘。是的，这种程序员确实存在。而且不难看出，这种夸张的刻板印象为什么会有一些真实性。首先有“上瘾潜力”。如果你有这种倾向，你很容易被一个编程问题完全“吸引住”，以至于忘记周围的一切，因为你完全专注于解决这个难题。而在这种情况下，时间很快变得不那么重要。你只想解决它，因为如果不解决这个问题，感觉是完全不满足的，尽管根据经验，通常最好先休息一下，等第二天精神焕发地再来解决这个问题。

除了上面提到的上瘾潜力外，第二个隐含的方面是编程作为替代真实社交互动的方式。编程的伟大之处在于，你开发了一些东西，然后从计算机那里得到反馈：程序运行，或者它不运行。很容易想象，这对那些在社交场合内向和内敛的人来说是一个有趣的激励因素。再加上完美的可控性：如果你编写正确，计算机将完全按照你的指令执行，且不会做任何其他事情。而社交互动则不可控，总是充满了不可预见、令人惊讶，甚至可能是随机的元素。这些社交互动的核心要素可以在编程中轻松消除。你发现自己处于一个完全可控的环境中。

关于上瘾潜力和可控性的问题，只对一小部分程序员有影响。大多数程序员都是完全正常的人。那些通过VBA自动化一些Excel工作步骤，以简化日常工作流程的商业员工，正处在人生的中段，可能与您并无太大区别。那些从事软件开发工作的人也是如此。所以，您完全不需要担心，如果您更深入地参与编程，自己会成为社会边缘群体的一员。

### 2.2.2 软件及其编程只是时尚，炒作而已

有些人可能认为软件行业不过是现代炒作的产物。最终，重要的不是程序，而是一个好的、可用的实物产品，或者说，这样的观点在一些人中流行。但那些这么想的人低估了软件在我们生活中所扮演的重要角色。如今，许多完全由软件组成的产品应运而生（例如办公应用和社交网络），而且由于软件的存在，实物产品的设计、制造、分发和变现方式正在发生深刻变化。例如，想想*亚马逊*对书籍交易的影响。在一些行业中，如汽车行业，已经有强烈迹象表明，软件在整体产品中相较于物理组件的重要性正在显著增加。也许在未来，您的汽车能做什么，因为它运行的软件，而不再是它是否配有铝合金轮圈和运动座椅，才会变得更有趣。特别是对于那些将汽车主要视为交通工具的人来说，物理车体可能会变得越来越像一个平台，真正有趣的功能则以软件的形式运行在其上。

是的，实物产品和非软件服务仍将继续占据重要地位，但它们将变得更加依赖软件，从而能够为用户提供更多的功能和好处。实物产品的创造和分发方式也将发生变化，有时甚至是根本性的，正如纯软件和互联网产品的重要性将显著增加一样。

### 2.2.3 编程仅仅是男性的专利

可能男性在技术类主题上，平均而言，比女性更感兴趣。但在编程领域，并没有理由相信女性不能成为同样出色的程序员，或者认为女性精通编程对职业发展不如男性有益。

事实上，女性在软件编程历史上一直扮演着特殊的角色。在19世纪，英国数学家*奥古斯塔·阿达·拜伦*是第一个为*查尔斯·巴贝奇*设计的打孔卡机描述完整程序的人。因此，她被广泛认为是世界上第一位女性程序员。（然而，巴贝奇的*分析机*由于资金困难，在拜伦和巴贝奇的生前从未建成。）她还意识到——这可能更为重要——像巴贝奇的系统这样的分析机，从根本上不仅仅能够处理数字，还能够处理其他类型的符号，如字母。此外，她还设计了诸如循环（程序语句的重复）等概念，这些概念现在几乎在所有现代编程语言中都是标准功能。为了纪念她，*Ada* 编程语言以她的名字命名。

除了奥古斯塔·阿达·拜伦，其他女性也对编程的发展做出了重要贡献。一个例子是计算机先驱*格雷斯·霍普*，她早在1940年代就提出了用一种直接为人类理解的语言编写程序的开创性想法，并在*COBOL*（*Common Business Oriented Language*，通用商业语言）的开发中发挥了重要作用，COBOL是最早的现代高级编程语言之一。她还被认为是编译器的发明人，编译器将用编程语言编写的程序（人类可理解的语言）转化为计算机能够直接执行的机器语言（更多内容将在下一章中介绍）。

还有美国数学家*玛格丽特·汉密尔顿*，她与她的团队共同开发了阿波罗11号计划的控制软件，并在某种意义上发明了帮助*尼尔·阿姆斯特朗*和*巴兹·奥尔德林*于1969年成功登月并安全返回地球的辅助系统。

女性对编程发展的贡献是决定性的，她们使得我们今天认为理所当然的许多事情在最初得以实现。纵观历史，编程一直是女性的世界。为什么今天会有所不同呢？
