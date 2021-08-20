---
title: 2020-07-31领读《反脆弱》第十九章 炼金石与反炼金石
author: Carlxu
type: post
date: 2020-07-31T12:12:09+00:00
url: /202007/709/
categories:
  - 个人日记
  - 生活笔记
tags:
  - 读书

---
<div class="markdown-here-wrapper" data-md-url="carlxu.cn">
  <p style="margin: 0px 0px 1.2em !important;">
    本章更多的是对前面概念的数学化阐述，即通过简单的数学方法判断哪些事物是线性的、非线性的或脆弱性（反脆弱性）的，作者说，已经明白前面几章的可以跳过这章（领读是不是也可跳过，&#x1f604;&#xfe0f;）
  </p>
  
  <p id="-">
    题外话：既然领读，还是要认真对待的。自己泛读、精读、联系上下章读，看了有好些遍，也查阅补充了一些背景知识和他人读书笔记，只能说有了基本了解，下面尝试领读。（以下部分内容引自他人笔记）
  </p>
  
  <p>
    <!--more-->
  </p>
  
  <hr />
  
  <h3 id="-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.3em;">
    一、核心内容
  </h3>
  
  <p style="margin: 0px 0px 1.2em !important;">
    标题所指的炼金石，就是验证反脆弱性的方法和技术，即变量函数的平均值高于变量平均值的函数。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    具体来说，判断一个事物的模式是线性的、非线性的或脆弱性（反脆弱性）的，就看Y=F(x) 的对应关系是否是呈现出指数关系。增加x一个单位的偏差，对比Y的相应增量是多少，如果x和Y不成比例，那就说明是非线性的，如果x增大给Y带来更大的损失或更大的收益，则说明其具有脆弱性或反脆弱性。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    房利美的赢利模式是脆弱的，祖母的健康对天气来说是脆弱的，挑战自身极限的锻炼是反脆弱的。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    这章给我们的启示是，如果你拥有有利的不对称性，或正凸性（选择权是特例），从长远来看，你会做得相当不错，在不确定的情况下表现优于平均数。不确定性越强，可选择的作用越大，你的表现就越好。
  </p>
  
  <h3 id="-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.3em;">
    二、通过一个例子引出炼金石概念
  </h3>
  
  <p style="margin: 0px 0px 1.2em !important;">
    汽车数量每时每刻都在发生变化，是一个变量。交通时间是汽车数量的函数。在交通这种非线性下，变量的行为和函数的行为会有很大差别。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    非线性越大，变量的函数和变量本身的行为差异就越大。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    变量越不稳定，也就是不确定性越强，函数和变量本身的区别就越大。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    比如：变量是8万辆车，到达机场的交通时间是30分钟，变量为10万辆，交通时间会增加到45分钟，但是，变量12万辆后，交通时间会变成70分钟。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    变量增加＝(12－8)÷8×100%＝50%
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    函数增加＝(70－30)÷30×100%＝133%
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    交通时间（函数）更取决于围绕车辆（变量）平均数的波动性。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    如果汽车数量分布均匀，交通情况就会缓解，比如：路上一直保持着平均10万辆的情况。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    如果汽车数量分布越不确定，虽然平均下来还是10万辆，但第一个小时8万，第二个小时12万，交通时间会变得很糟糕。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    到达机场时间＝(30+70)/2＝50分钟，大于平均10万辆的45分钟，交通成本增加，收益降低了。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    且比8万增加到10万，再增加到12万，交通更混乱、函数值更大。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    结论：<strong>如果函数呈现凸性（反脆弱性），变量函数的平均值将比变量平均值的函数要高。</strong><br /> 这就是塔勒布所说的炼金石——<strong>炼石为金</strong>。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    如果函数呈现凹性（脆弱性），情况相反，变量函数的平均值将比变量平均值的函数要低。<br /> 这便是反炼金石——化金为土。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    （这里有个疑问，感觉凸性和凹性更多的是对个人收益来主观判断的。按作者的计算方法，车辆波动相对平均情况的时间函数值是增加了，对人来说是损失，对车来说就不是，比如增加了和车主的陪伴时间，这个怎么理解？）
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    文中提到的掷骰子，平方函数和平方根函数的收益对比，也就是指数增长和指数下降，相信大家都能看懂和理解，就不详述了。
  </p>
  
  <h3 id="-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.3em;">
    三、收获和启示
  </h3>
  
  <h4 id="1-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.2em;">
    1. 不要相信平均数
  </h4>
  
  <p style="margin: 0px 0px 1.2em !important;">
    国外有名谚语：如果一条河的平均深度是4英尺，就千万不要过河。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    它就像有人告诉你，一个地方的全年平均气温是21摄氏度。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    很多人会认为，这个地方是人间天堂，因为21摄氏度是最适宜人类的温度。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    但是，它很可能是第一个小时零下8度，第二小时则为60度。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    平均数往往会掩盖极端值，就谚语所说的河，它确实平均深度是4英尺，也就1.2米。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    可是，如果真要过河，这个数值根本就没意义，必须要明确地知道河水最深多少。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    因为，只要有小小的一段水深2米，你就可能遭遇淹死的巨大风险。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    显然，平均数没有太大意义，数据的分布更重要。
  </p>
  
  <h4 id="2-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.2em;">
    2. 多做正面非对称性的事物
  </h4>
  
  <p style="margin: 0px 0px 1.2em !important;">
    所谓的正面、或者有利的不对称性，就是你一旦做对了或者运气好时的收益要大于你做错或者运气差时的代价，而且，事情最好不是一次性的，是可以多次重复的。这样，时间一长，积累下来，你有好结果的概率很大。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    文中讲到，事物有三类：喜欢干扰（或者错误）的事物，中性，以及厌恶干扰的事物。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    你最好的策略就是多次、重复的做第一类事情，避免第三类。
  </p>
  
  <h4 id="3-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.2em;">
    3. 见微知著，快速嗅出风险
  </h4>
  
  <p style="margin: 0px 0px 1.2em !important;">
    古人说：见微知著。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    曾有人说，不用看什么数据，对于经济，只要到街头走一走，你就能知道。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    比如：早餐的油条、包子突然涨价了， 说明通货膨胀有点高。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    因为制作早餐的商人是经济大链条中最微小的毛细血管，他们也最敏感，也最具脆弱性。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    第一，他们知道最鲜活的价格；第二，他们不会轻易随便涨价。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    当他们都受到影响不得不涨价时，说明前面那些个环节早就变化完成了。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    脆弱的经济，收入增加10%带来的利润增加额，绝对低于收入下降10%带来的利润减少额。
  </p>
  
  <h4 id="4-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.2em;">
    4. 读书有益
  </h4>
  
  <p style="margin: 0px 0px 1.2em !important;">
    为什么读书被绝大部分人看作是一个积极的爱好？
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    任何时候劝别人读书，推荐好书给他人，都不会特别的遭人恨。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    罗胖的每天一本书还搞了大型的发布会，有人称其在制造知识焦虑，但这种反对的声音浪花不大。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    原因很简单，读书是典型的正面非对称性，你的损失就是时间成本，书籍本身的成本几乎
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    可以忽略，尤其你不读书的话，那个时间很可能贡献给微信了，所以甚至可以认为代价为零。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    而你读了一本坏书的代价也不高，反正大部分人其实是很难有如此强的学习能力和执行能力的，但是读到一些好书时，至少也算开阔了眼界，增加了谈资。
  </p>
  
  <p style="margin: 0px 0px 1.2em !important;">
    如果碰巧打通了任督二脉，认知模式升级，那就赚大了。
  </p>
  
  <h3 id="-" style="margin: 1.3em 0px 1em; padding: 0px; font-weight: bold; font-size: 1.3em;">
    四、延伸阅读
  </h3>
  
  <ol style="margin: 1.2em 0px; padding-left: 2em;">
    <li style="margin: 0.5em 0px;">
      <a href="https://m.sohu.com/a/271536930_778083">房利美商业模式及启示</a>
    </li>
    <li style="margin: 0.5em 0px;">
      <a href="https://m.sohu.com/a/383136783_378683">坤鹏论：非线性的世界里 规模越大麻烦越大</a>
    </li>
    <li style="margin: 0.5em 0px;">
      <a href="https://www.jianshu.com/p/592f0498080c">《反脆弱》读书笔记 第19章 炼金石与反炼金石</a>
    </li>
  </ol>
  
  <div style="height: 0; width: 0; max-height: 0; max-width: 0; overflow: hidden; font-size: 0em; padding: 0; margin: 0;" title="MDH:PHA+IyMg44CK5Y+N6ISG5byx44CL56ys5Y2B5Lmd56ugIOeCvOmHkeefs+S4juWPjeeCvOmHkeef
szwvcD48cD7mnKznq6Dmm7TlpJrnmoTmmK/lr7nliY3pnaLmpoLlv7XnmoTmlbDlrabljJbpmJDo
v7DvvIzljbPpgJrov4fnroDljZXnmoTmlbDlrabmlrnms5XliKTmlq3lk6rkupvkuovnianmmK/n
ur/mgKfnmoTjgIHpnZ7nur/mgKfnmoTmiJbohIblvLHmgKfvvIjlj43ohIblvLHmgKfvvInnmoTv
vIzkvZzogIXor7TvvIzlt7Lnu4/mmI7nmb3liY3pnaLlh6Dnq6DnmoTlj6/ku6Xot7Pov4fov5nn
q6DvvIjpoobor7vmmK/kuI3mmK/kuZ/lj6/ot7Pov4fvvIztoL3tuITvuI/vvIk8L3A+PHA+6aKY
5aSW6K+d77ya5pei54S26aKG6K+777yM6L+Y5piv6KaB6K6k55yf5a+55b6F55qE44CC6Ieq5bex
5rOb6K+744CB57K+6K+744CB6IGU57O75LiK5LiL56ug6K+777yM55yL5LqG5pyJ5aW95Lqb6YGN
77yM5Lmf5p+l6ZiF6KGl5YWF5LqG5LiA5Lqb6IOM5pmv55+l6K+G5ZKM5LuW5Lq66K+75Lmm56yU
6K6w77yM5Y+q6IO96K+05pyJ5LqG5Z+65pys5LqG6Kej77yM5LiL6Z2i5bCd6K+V6aKG6K+744CC
77yI5Lul5LiL6YOo5YiG5YaF5a655byV6Ieq5LuW5Lq656yU6K6w77yJPC9wPjxwPi0tPC9wPjxw
PiMjIyDkuIDjgIHmoLjlv4PlhoXlrrk8L3A+PHA+5qCH6aKY5omA5oyH55qE54K86YeR55+z77yM
5bCx5piv6aqM6K+B5Y+N6ISG5byx5oCn55qE5pa55rOV5ZKM5oqA5pyv77yM5Y2z5Y+Y6YeP5Ye9
5pWw55qE5bmz5Z2H5YC86auY5LqO5Y+Y6YeP5bmz5Z2H5YC855qE5Ye95pWw44CCPC9wPjxwPuWF
t+S9k+adpeivtO+8jOWIpOaWreS4gOS4quS6i+eJqeeahOaooeW8j+aYr+e6v+aAp+eahOOAgemd
nue6v+aAp+eahOaIluiEhuW8seaAp++8iOWPjeiEhuW8seaAp++8ieeahO+8jOWwseeci1k9Rih4
KSDnmoTlr7nlupTlhbPns7vmmK/lkKbmmK/lkYjnjrDlh7rmjIfmlbDlhbPns7vjgILlop7liqB4
5LiA5Liq5Y2V5L2N55qE5YGP5beu77yM5a+55q+UWeeahOebuOW6lOWinumHj+aYr+WkmuWwke+8
jOWmguaenHjlkoxZ5LiN5oiQ5q+U5L6L77yM6YKj5bCx6K+05piO5piv6Z2e57q/5oCn55qE77yM
5aaC5p6ceOWinuWkp+e7mVnluKbmnaXmm7TlpKfnmoTmjZ/lpLHmiJbmm7TlpKfnmoTmlLbnm4rv
vIzliJnor7TmmI7lhbblhbfmnInohIblvLHmgKfmiJblj43ohIblvLHmgKfjgII8L3A+PHA+5oi/
5Yip576O55qE6LWi5Yip5qih5byP5piv6ISG5byx55qE77yM56WW5q+N55qE5YGl5bq35a+55aSp
5rCU5p2l6K+05piv6ISG5byx55qE77yM5oyR5oiY6Ieq6Lqr5p6B6ZmQ55qE6ZS754K85piv5Y+N
6ISG5byx55qE44CCPC9wPjxwPui/meeroOe7meaIkeS7rOeahOWQr+ekuuaYr++8jOWmguaenOS9
oOaLpeacieacieWIqeeahOS4jeWvueensOaAp++8jOaIluato+WHuOaAp++8iOmAieaLqeadg+aY
r+eJueS+i++8ie+8jOS7jumVv+i/nOadpeeci++8jOS9oOS8muWBmuW+l+ebuOW9k+S4jemUme+8
jOWcqOS4jeehruWumueahOaDheWGteS4i+ihqOeOsOS8mOS6juW5s+Wdh+aVsOOAguS4jeehruWu
muaAp+i2iuW8uu+8jOWPr+mAieaLqeeahOS9nOeUqOi2iuWkp++8jOS9oOeahOihqOeOsOWwsei2
iuWlveOAgjwvcD48cD4jIyMg5LqM44CB6YCa6L+H5LiA5Liq5L6L5a2Q5byV5Ye654K86YeR55+z
5qaC5b+1PC9wPjxwPuaxvei9puaVsOmHj+avj+aXtuavj+WIu+mDveWcqOWPkeeUn+WPmOWMlu+8
jOaYr+S4gOS4quWPmOmHj+OAguS6pOmAmuaXtumXtOaYr+axvei9puaVsOmHj+eahOWHveaVsOOA
guWcqOS6pOmAmui/meenjemdnue6v+aAp+S4i++8jOWPmOmHj+eahOihjOS4uuWSjOWHveaVsOea
hOihjOS4uuS8muacieW+iOWkp+W3ruWIq+OAgjwvcD48cD7pnZ7nur/mgKfotorlpKfvvIzlj5jp
h4/nmoTlh73mlbDlkozlj5jph4/mnKzouqvnmoTooYzkuLrlt67lvILlsLHotorlpKfjgII8L3A+
PHA+5Y+Y6YeP6LaK5LiN56iz5a6a77yM5Lmf5bCx5piv5LiN56Gu5a6a5oCn6LaK5by677yM5Ye9
5pWw5ZKM5Y+Y6YeP5pys6Lqr55qE5Yy65Yir5bCx6LaK5aSn44CCPC9wPjxwPuavlOWmgu+8muWP
mOmHj+aYrzjkuIfovobovabvvIzliLDovr7mnLrlnLrnmoTkuqTpgJrml7bpl7TmmK8zMOWIhumS
n++8jOWPmOmHj+S4ujEw5LiH6L6G77yM5Lqk6YCa5pe26Ze05Lya5aKe5Yqg5YiwNDXliIbpkp/v
vIzkvYbmmK/vvIzlj5jph48xMuS4h+i+huWQju+8jOS6pOmAmuaXtumXtOS8muWPmOaIkDcw5YiG
6ZKf44CCPC9wPjxwPuWPmOmHj+WinuWKoO+8nSgxMu+8jTgpw7c4w5cxMDAl77ydNTAlPC9wPjxw
PuWHveaVsOWinuWKoO+8nSg3MO+8jTMwKcO3MzDDlzEwMCXvvJ0xMzMlPC9wPjxwPuS6pOmAmuaX
tumXtO+8iOWHveaVsO+8ieabtOWPluWGs+S6juWbtOe7lei9pui+hu+8iOWPmOmHj++8ieW5s+Wd
h+aVsOeahOazouWKqOaAp+OAgjwvcD48cD7lpoLmnpzmsb3ovabmlbDph4/liIbluIPlnYfljIDv
vIzkuqTpgJrmg4XlhrXlsLHkvJrnvJPop6PvvIzmr5TlpoLvvJrot6/kuIrkuIDnm7Tkv53mjIHn
nYDlubPlnYcxMOS4h+i+hueahOaDheWGteOAgjwvcD48cD7lpoLmnpzmsb3ovabmlbDph4/liIbl
uIPotorkuI3noa7lrprvvIzomb3nhLblubPlnYfkuIvmnaXov5jmmK8xMOS4h+i+hu+8jOS9hues
rOS4gOS4quWwj+aXtjjkuIfvvIznrKzkuozkuKrlsI/ml7YxMuS4h++8jOS6pOmAmuaXtumXtOS8
muWPmOW+l+W+iOezn+ezleOAgjwvcD48cD7liLDovr7mnLrlnLrml7bpl7TvvJ0oMzArNzApLzLv
vJ01MOWIhumSn++8jOWkp+S6juW5s+WdhzEw5LiH6L6G55qENDXliIbpkp/vvIzkuqTpgJrmiJDm
nKzlop7liqDvvIzmlLbnm4rpmY3kvY7kuobjgII8L3A+PHA+5LiU5q+UOOS4h+WinuWKoOWIsDEw
5LiH77yM5YaN5aKe5Yqg5YiwMTLkuIfvvIzkuqTpgJrmm7Tmt7fkubHjgIHlh73mlbDlgLzmm7Tl
pKfjgII8L3A+PHA+57uT6K6677yaKirlpoLmnpzlh73mlbDlkYjnjrDlh7jmgKfvvIjlj43ohIbl
vLHmgKfvvInvvIzlj5jph4/lh73mlbDnmoTlubPlnYflgLzlsIbmr5Tlj5jph4/lubPlnYflgLzn
moTlh73mlbDopoHpq5jjgIIqKjwvcD48cD7ov5nlsLHmmK/loZTli5LluIPmiYDor7TnmoTngrzp
h5Hnn7PigJTigJQqKueCvOefs+S4uumHkSoq44CCPC9wPjxwPuWmguaenOWHveaVsOWRiOeOsOWH
ueaAp++8iOiEhuW8seaAp++8ie+8jOaDheWGteebuOWPje+8jOWPmOmHj+WHveaVsOeahOW5s+Wd
h+WAvOWwhuavlOWPmOmHj+W5s+Wdh+WAvOeahOWHveaVsOimgeS9juOAgjwvcD48cD7ov5nkvr/m
mK/lj43ngrzph5Hnn7PigJTigJTljJbph5HkuLrlnJ/jgII8L3A+PHA+77yI6L+Z6YeM5pyJ5Liq
55aR6Zeu77yM5oSf6KeJ5Ye45oCn5ZKM5Ye55oCn5pu05aSa55qE5piv5a+55Liq5Lq65pS255uK
5p2l5Li76KeC5Yik5pat55qE44CC5oyJ5L2c6ICF55qE6K6h566X5pa55rOV77yM6L2m6L6G5rOi
5Yqo55u45a+55bmz5Z2H5oOF5Ya155qE5pe26Ze05Ye95pWw5YC85piv5aKe5Yqg5LqG77yM5a+5
5Lq65p2l6K+05piv5o2f5aSx77yM5a+56L2m5p2l6K+05bCx5LiN5piv77yM5q+U5aaC5aKe5Yqg
5LqG5ZKM6L2m5Li755qE6Zmq5Ly05pe26Ze077yM6L+Z5Liq5oCO5LmI55CG6Kej77yf77yJPC9w
PjxwPuaWh+S4reaPkOWIsOeahOaOt+mqsOWtkO+8jOW5s+aWueWHveaVsOWSjOW5s+aWueagueWH
veaVsOeahOaUtuebiuWvueavlO+8jOS5n+WwseaYr+aMh+aVsOWinumVv+WSjOaMh+aVsOS4i+mZ
je+8jOebuOS/oeWkp+WutumDveiDveeci+aHguWSjOeQhuino++8jOWwseS4jeivpui/sOS6huOA
gjwvcD48cD4jIyMg5LiJ44CB5pS26I635ZKM5ZCv56S6PC9wPjxwPiMjIyMgMS4g5LiN6KaB55u4
5L+h5bmz5Z2H5pWwPC9wPjxwPuWbveWkluacieWQjeiwmuivre+8muWmguaenOS4gOadoeays+ea
hOW5s+Wdh+a3seW6puaYrzToi7HlsLrvvIzlsLHljYPkuIfkuI3opoHov4fmsrPjgII8L3A+PHA+
5a6D5bCx5YOP5pyJ5Lq65ZGK6K+J5L2g77yM5LiA5Liq5Zyw5pa555qE5YWo5bm05bmz5Z2H5rCU
5rip5pivMjHmkYTmsI/luqbjgII8L3A+PHA+5b6I5aSa5Lq65Lya6K6k5Li677yM6L+Z5Liq5Zyw
5pa55piv5Lq66Ze05aSp5aCC77yM5Zug5Li6MjHmkYTmsI/luqbmmK/mnIDpgILlrpzkurrnsbvn
moTmuKnluqbjgII8L3A+PHA+5L2G5piv77yM5a6D5b6I5Y+v6IO95piv56ys5LiA5Liq5bCP5pe2
6Zu25LiLOOW6pu+8jOesrOS6jOWwj+aXtuWImeS4ujYw5bqm44CCPC9wPjxwPuW5s+Wdh+aVsOW+
gOW+gOS8muaOqeebluaegeerr+WAvO+8jOWwseiwmuivreaJgOivtOeahOays++8jOWug+ehruWu
nuW5s+Wdh+a3seW6puaYrzToi7HlsLrvvIzkuZ/lsLExLjLnsbPjgII8L3A+PHA+5Y+v5piv77yM
5aaC5p6c55yf6KaB6L+H5rKz77yM6L+Z5Liq5pWw5YC85qC55pys5bCx5rKh5oSP5LmJ77yM5b+F
6aG76KaB5piO56Gu5Zyw55+l6YGT5rKz5rC05pyA5rex5aSa5bCR44CCPC9wPjxwPuWboOS4uu+8
jOWPquimgeacieWwj+Wwj+eahOS4gOauteawtOa3sTLnsbPvvIzkvaDlsLHlj6/og73pga3pgYfm
t7nmrbvnmoTlt6jlpKfpo47pmanjgII8L3A+PHA+5pi+54S277yM5bmz5Z2H5pWw5rKh5pyJ5aSq
5aSn5oSP5LmJ77yM5pWw5o2u55qE5YiG5biD5pu06YeN6KaB44CCPC9wPjxwPiMjIyMgMi4g5aSa
5YGa5q2j6Z2i6Z2e5a+556ew5oCn55qE5LqL54mpPC9wPjxwPuaJgOiwk+eahOato+mdouOAgeaI
luiAheacieWIqeeahOS4jeWvueensOaAp++8jOWwseaYr+S9oOS4gOaXpuWBmuWvueS6huaIluiA
hei/kOawlOWlveaXtueahOaUtuebiuimgeWkp+S6juS9oOWBmumUmeaIluiAhei/kOawlOW3ruaX
tueahOS7o+S7t++8jOiAjOS4lO+8jOS6i+aDheacgOWlveS4jeaYr+S4gOasoeaAp+eahO+8jOaY
r+WPr+S7peWkmuasoemHjeWkjeeahOOAgui/meagt++8jOaXtumXtOS4gOmVv++8jOenr+e0r+S4
i+adpe+8jOS9oOacieWlvee7k+aenOeahOamgueOh+W+iOWkp+OAgjwvcD48cD7mlofkuK3orrLl
iLDvvIzkuovnianmnInkuInnsbvvvJrllpzmrKLlubLmibDvvIjmiJbogIXplJnor6/vvInnmoTk
uovnianvvIzkuK3mgKfvvIzku6Xlj4rljozmgbblubLmibDnmoTkuovnianjgII8L3A+PHA+5L2g
5pyA5aW955qE562W55Wl5bCx5piv5aSa5qyh44CB6YeN5aSN55qE5YGa56ys5LiA57G75LqL5oOF
77yM6YG/5YWN56ys5LiJ57G744CCPC9wPjxwPiMjIyMgMy4g6KeB5b6u55+l6JGX77yM5b+r6YCf
5ZeF5Ye66aOO6ZmpPC9wPjxwPuWPpOS6uuivtO+8muingeW+ruefpeiRl+OAgjwvcD48cD7mm77m
nInkurror7TvvIzkuI3nlKjnnIvku4DkuYjmlbDmja7vvIzlr7nkuo7nu4/mtY7vvIzlj6ropoHl
iLDooZflpLTotbDkuIDotbDvvIzkvaDlsLHog73nn6XpgZPjgII8L3A+PHA+5q+U5aaC77ya5pep
6aSQ55qE5rK55p2h44CB5YyF5a2Q56qB54S25rao5Lu35LqG77yMIOivtOaYjumAmui0p+iGqOiD
gOacieeCuemrmOOAgjwvcD48cD7lm6DkuLrliLbkvZzml6nppJDnmoTllYbkurrmmK/nu4/mtY7l
pKfpk77mnaHkuK3mnIDlvq7lsI/nmoTmr5vnu4booYDnrqHvvIzku5bku6zkuZ/mnIDmlY/mhJ/v
vIzkuZ/mnIDlhbfohIblvLHmgKfjgII8L3A+PHA+56ys5LiA77yM5LuW5Lus55+l6YGT5pyA6bKc
5rS755qE5Lu35qC877yb56ys5LqM77yM5LuW5Lus5LiN5Lya6L275piT6ZqP5L6/5rao5Lu344CC
PC9wPjxwPuW9k+S7luS7rOmDveWPl+WIsOW9seWTjeS4jeW+l+S4jea2qOS7t+aXtu+8jOivtOaY
juWJjemdoumCo+S6m+S4queOr+iKguaXqeWwseWPmOWMluWujOaIkOS6huOAgjwvcD48cD7ohIbl
vLHnmoTnu4/mtY7vvIzmlLblhaXlop7liqAxMCXluKbmnaXnmoTliKnmtqblop7liqDpop3vvIzn
u53lr7nkvY7kuo7mlLblhaXkuIvpmY0xMCXluKbmnaXnmoTliKnmtqblh4/lsJHpop3jgII8L3A+
PHA+IyMjIyA0LiDor7vkuabmnInnm4o8L3A+PHA+5Li65LuA5LmI6K+75Lmm6KKr57ud5aSn6YOo
5YiG5Lq655yL5L2c5piv5LiA5Liq56ev5p6B55qE54ix5aW977yfPC9wPjxwPuS7u+S9leaXtuWA
meWKneWIq+S6uuivu+S5pu+8jOaOqOiNkOWlveS5pue7meS7luS6uu+8jOmDveS4jeS8mueJueWI
q+eahOmBreS6uuaBqOOAgjwvcD48cD7nvZfog5bnmoTmr4/lpKnkuIDmnKzkuabov5jmkJ7kuobl
pKflnovnmoTlj5HluIPkvJrvvIzmnInkurrnp7DlhbblnKjliLbpgKDnn6Xor4bnhKbomZHvvIzk
vYbov5nnp43lj43lr7nnmoTlo7Dpn7PmtaroirHkuI3lpKfjgII8L3A+PHA+5Y6f5Zug5b6I566A
5Y2V77yM6K+75Lmm5piv5YW45Z6L55qE5q2j6Z2i6Z2e5a+556ew5oCn77yM5L2g55qE5o2f5aSx
5bCx5piv5pe26Ze05oiQ5pys77yM5Lmm57GN5pys6Lqr55qE5oiQ5pys5Yeg5LmO5Y+v5Lul5b+9
55Wl77yM5bCk5YW25L2g5LiN6K+75Lmm55qE6K+d77yM6YKj5Liq5pe26Ze05b6I5Y+v6IO96LSh
54yu57uZ5b6u5L+h5LqG77yM5omA5Lul55Sa6Iez5Y+v5Lul6K6k5Li65Luj5Lu35Li66Zu244CC
PC9wPjxwPuiAjOS9oOivu+S6huS4gOacrOWdj+S5pueahOS7o+S7t+S5n+S4jemrmO+8jOWPjeat
o+Wkp+mDqOWIhuS6uuWFtuWunuaYr+W+iOmavuacieWmguatpOW8uueahOWtpuS5oOiDveWKm+WS
jOaJp+ihjOiDveWKm+eahO+8jOS9huaYr+ivu+WIsOS4gOS6m+WlveS5puaXtu+8jOiHs+WwkeS5
n+eul+W8gOmYlOS6huecvOeVjO+8jOWinuWKoOS6huiwiOi1hOOAgjwvcD48cD7lpoLmnpznorDl
t6fmiZPpgJrkuobku7vnnaPkuozohInvvIzorqTnn6XmqKHlvI/ljYfnuqfvvIzpgqPlsLHotZrl
pKfkuobjgII8L3A+PHA+IyMjIOWbm+OAgeW7tuS8uOmYheivuzxicj4xLiBb5oi/5Yip576O5ZWG
5Lia5qih5byP5Y+K5ZCv56S6XShodHRwczovL20uc29odS5jb20vYS8yNzE1MzY5MzBfNzc4MDgz
KTxicj4yLiBb5Z2k6bmP6K6677ya6Z2e57q/5oCn55qE5LiW55WM6YeMIOinhOaooei2iuWkp+m6
u+eDpui2iuWkp10oaHR0cHM6Ly9tLnNvaHUuY29tL2EvMzgzMTM2NzgzXzM3ODY4Myk8YnI+My4g
W+OAiuWPjeiEhuW8seOAi+ivu+S5pueslOiusCDnrKwxOeeroCDngrzph5Hnn7PkuI7lj43ngrzp
h5Hnn7NdKGh0dHBzOi8vd3d3LmppYW5zaHUuY29tL3AvNTkyZjA0OTgwODBjKTwvcD4=">
    ​
  </div>
</div>

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->

<!--more-->