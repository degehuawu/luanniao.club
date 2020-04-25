# LuanNiao Blazor 组件库
LuanNiao Blazor 组件库是**基于**Antd V4版本的CSS样式库开发的ASP.NET Core Blazor组件库.
我们的库的目标在于基于Antd的高复用样式以及高兼容性的基础上去制作一套中小型企业可以落地使用的,方便,快捷的组件库.

如果您对此感兴趣,您可以抽出几分钟来阅读我们的简介,以确定您是否决定使用/关注当前组件库.

## 当前项目状态
架构设计与前期框架搭建中,发布计划暂无,对于Blazor从落地到实际项目中而言,我们仍旧处于观察期,但这并不影响我们实现这个组件库,因为Blazor给予了我们无限大的想象空间.<br/>
另外,我们公司的实际使用中不仅需要这个UI组件库,更是需要一个Canvas组件的,目前您已经可以在Antd库中见到示例,但是确实如您所见那真的只是一个非常简单的实例,正常而言,我们会从Canvas2D开始制作我们需要的组件.

## 在您阅读一切之前,我希望能够在这里感谢一下给予我们帮助的人
这些无私且伟大的人有:<br/>
[diwu0510](https://github.com/orgs/luanniao/people/diwu0510)<br/>
[lucio-c](https://github.com/orgs/luanniao/people/lucio-c)<br/>
[shenbo1](https://github.com/orgs/luanniao/people/shenbo1)<br/>
[talabright](https://github.com/orgs/luanniao/people/talabright) <br/>
我们目前并没有过多的贡献者,不过这并不会影响我们的积极性,我们会尽可能的完善这个库并伴随着我们公司的项目落地这个组件库.<br/>
如果您愿意浪费您宝贵的时间在我们这个不起眼的项目上,那么您的帮助将是我至高的荣幸.<br/>
好了,不打扰您了,接下来让我给您介绍一下我们的库吧!(•́⌄•́๑)૭✧
<br/>

### 设计理念
##### **我们的组件风格并不局限于模拟Antd**
因此,您可能会发现,我们的API可能与您印象中Antd的并不相同.


## 库的设计背景
该仓库仓库是由一个完整的企业团队与一些值得我尊敬的朋友共同维护的,我们的每一个举措都是需要在我们的项目中实际使用的,所以我们可能与其他库并不大相同,我们的实现策略将受到下列内容影响,如果您无法接受这些内容,可能您需要考虑是否继续使用当前组件库.
1.  这是一个核心问题:Blazor目前是Preview版本,我们制作此库的目的在于尽可能的或者说尽早的得到我们的WASM开发组件库以应对前端人员缺失的问题(***这是一个悲伤的问题***),所以就目前情况下,如果我们没有发布Release版本的Nuget包或者我们的版本没有>1.0.0.0那么,请不要在您的生产环境使用,我们的测试必定是没有通过的.同样的,如果我们有任何新的关于版本的发布,我们会在这个网站进行同步更新.
1.  我们并不保证我们不破坏ANTD的原本实现思路
    例如Menu我们直接将其拆分为InlineMenu,DropdownMenu,HorizontalMenu3种,未来还会有其他扩展,但是ANTD并不是这样做的.
1.  我们的开发路线并是以实现现实项目会出现的实际应用(是的这可能会更加偏向于我们的项目,我们是制作企业内部应用的).
    这将可能会导致**我们会实现*****但并不是立即实现***那些在系统中不太常见的功能.
    例如:ANTD中的大块日历,很遗憾我们的产品中并没有类似于日程表的功能,所以我们暂时不考虑投入人员去支持它.
1.  我们可能会出现长时间的组件开发**停顿**,是的,我们目前虽然再尽快的开发更多的组件,但是如果您仔细翻看我们的提交记录(太多了,但是我保证是这样的)您会发现,在一段时间内,我们始终在修改Blazor.Core,而组件开发停滞不前,这是因为我们发现了Blazor的一个性能问题(虽然已经处理了),但是我们并不保证未来不会出现这样的情况.原因很简单,我们需要这个组件库用到我们的产品上,我们的客户是不可能接受**卡顿**的.

### 我们做出这些设计的原因
您在使用中会发现我们的组件从使用或者是设计角度上会与react或vue等主流前端框架有所不同,例如:
1.  我们的组件属性均为大写,
    这是因为我们是基于Blazor开发的,那么我们从设计上认为,您需要接受C#的代码风格,而C#的代码风格有一个约束**Property必须为大写字母开头**.
    因此您会看到如下组件:
    ```Html
      @("<Row Gutter=\"new MarginGutter() { Vertial = 10, Horizontal = 4 }\">")
      @("</Row>")
    ```
1.  我们可能会要求您传递非常多的子组件.
    这是因为,就目前而言,Blazor是无法做到在属性中传递对象的.当然,我们知道您可以编写如下类型的代码
    ```C#
        @("RenderFragment _filedName=@\"<X></X>\"")
    ```
    但是经过我们的实际测试,这样的组件您是无法做到完全使用所有组合可能的,例如您无法捕获***this***对象,以及会产生一些其他的奇奇怪怪的问题,具体您可以自行编写代码尝试一下,最核心的问题其实是无法捕获***this***对象.我们最开始也是这样编写的代码,但是后来放弃了,因为就目前的情况而言在实际的工作中您必然需要捕获***this***.
    所以,我们会出现类似下面样式的代码
    ```Html
        @("<LNCard CStyle=\"width:300px\" Actions=\"new[]{ a1,a2,a3}\">")
        @("     <Title>")
        @("         Default size card")
        @("     </Title>")
        @("     <Extra>")
        @("         <a href=\"#\">More</a>")
        @("     </Extra>")
        @("     <ChildContent>")
        @("        <p>Card content</p>")
        @("        <p>Card content</p>")
        @("        <p>Card content</p>")
        @("     </ChildContent>")
        @("     <Actions>")
        @("         <CardAction>")
        @("             <LuanNiao.Blazor.Component.Antd.Button.LNButton OnClickCallback=\"@(async ( a)=>{ Console.WriteLine(\"asd\"); })\" />")
        @("         </CardAction>")
        @("         <CardAction>")
        @("             <EditOutlined />")
        @("         </CardAction>")
        @("         <CardAction>")
        @("             <EllipsisOutlined />")
        @("         </CardAction>")
        @("     </Actions>")
        @("</LNCard>")
    ```
1.  我们目前有制作状态树的计划,但是后来***取消***了,因为我们认为,必然会有更厉害的**角色**来实现类似于***Redux***的功能,到时候,我们可以顺便搭车,毕竟强如ANTD也没有考虑过这个问题.所以我们可能在近期不会将**状态树**考虑到功能范围内.
1. 就目前而言,我们也暂时不会考虑加入**网页富文本编辑器**您如果需要这个功能,可能需要等上好一阵子了.经过我们团队在全网的搜罗而言,我们并没有找到合适于Blazor的**网页富文本编辑器**,当前的实现基本上偏向于两种极端,就拿Markdown而言:
    1. 完全使用C#来实现所有的内容,但是根本不可能存在,除非实现类似于C库的markdown功能,但是这依赖于大量的服务器渲染,这违背了WASM的基本初衷,假设我使用了C库,那么从WASM的安全性角度考虑,这时候我们并不保证我们所生成的所有.DLL,.SO库能够在各种平台上适用,并且我们可能也没有手段在任何情况下拿到当前的操作系统平台信息.
    1. MarkDown目前比较完善的支持是JavaScript/Type Script比较多,很遗憾,.NET的支持,只存在两种情况:依赖组件过多或生成的HTML没办法加入丰富的扩展组件.
    1. 您当前看到的内容,或者说LuanNiao组件库的Doc是Markdown编写的,但是我们也付出了惨痛的代价,我们无法支持flow,因为当我们引入flow时,它的依赖组件与Blazor的JS引起了冲突,这使得我们不得不放弃Markdown的支持.

## 关于我们在开发组件库时遇到的问题
未来我们会在其他地方建立专门的专区来分享这些内容,但截至目前(2020年4月24日)暂无具体计划.:blush:
>您可以关注本网站的更新来确定我们是否进行了此项更新

<br/>
<br/>
<br/>
<br/>
<br/>
<br/>

# 非常感谢您阅读到这里
感谢您对于当前库的阅读,我们为您为此浪费的几分钟表示感谢!您尽情在我们的文档库中玩转吧.

#### 小请求
如果出现BUG,我期望您能够在[GITHUB](https://github.com/luanniao/Blazor.Component.Antd)上给我们提出Issue,您的意见会给予我们极大的帮助! 