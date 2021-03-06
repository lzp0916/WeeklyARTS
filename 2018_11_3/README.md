# Weekly ARTS

- 动态规划一题
- 使用显式模板特化的资源管理
- 模板技术在C++中实现观察者模式的应用
- 急需一门表达课

## Algorithm [343. Integer Break](https://leetcode.com/problems/integer-break/)

这个题目怎么说呢,我做的过程中心情是比较复杂的,先看一下题目:

题目要求给定正整数`n`,将其拆分成最少两个正整数的和,求出能够得到的最大乘积是多少.

所以,这是个动态规划问题?

之前动态规划做过十几题了,摸清套路的我开始各种拆分找规律,譬如,计算`10`的最大乘积:

- 以2开始拆分,`2*8=16`、`2*3*5=30`、`2*3*3*2=36`
- 以3开始拆分,`3*7=21`、`3*3*4=36`
- 以4开始拆分,`4*6=24`
- 以5开始拆分,`5*5=25`
- ......

即使是根据提示从`7`拆分到`10`,只能发现说`7`能拆分出`2*2*3`和`3*4`,`8`能够拆分成`2*2*2*2`、`2*2*4`和`4*4`,`9`能够拆分出`3*3*3`,`10`则可以拆分出`2*2*3*3`、`3*3*4`.

而动态规划问题不是说`dp[i]`与`dp[j]`之间的关系么?百思不得其解......

直到看了`discuss`才知道这个......不是那种动态规划套路.这个`n`会被拆解成很多整数之和,但是从数学角度(别问我我也不懂)讲,在特定限制条件下最终被3拆分才能获取最大乘积,譬如`6`,`3*3>2*2*2`,只要`n>4`都会满足这种场景.因而解决方法很简单:

```C++
int integerBreak(int n) {
    if (n == 2) return 1;
    if (n == 3) return 2;
    //if (n == 4) return 4;
    int result = 1;

    while (n > 4) {
        n -= 3;
        result *= 3;
    }
    return result * n;
}
```

注意`2,3,4`均为特定情况,需要单独处理,而只要`n>4`即可将`n`拆分成尽可能多的3和最终剩余的`1,2,3,4`,这样能够获得最大乘积.

动态规划问题已经练习了十几题,题题套路都不一样,摸不着头脑啊.

## Review [使用显式模板特化的资源管理](ACCU2086.md)

文中展示了一种RAII包裹方法,用来解决智能指针应对非内存资源类型时存在的问题,其中用到的技术值得琢磨.

## Technique [模板技术在C++中实现观察者模式的应用](Observer.md)

感受一下模板的魅力.

## Share 急需一门表达课

周末参加了一下公司的黑客马拉松活动,最终要参加“路演”,需要PPT,原本也是做的要应用到产品上的东西,干货是有的,可临到要写材料要表达自己的设计和设想时,却哑火了.

是的,我学过UML,没怎么用,也看不出来能够提供多少表达上的帮助,临阵抱佛脚,用google搜索`how to describe software design`,找到了一些描述:

- [4+1 architectural view model](https://en.wikipedia.org/wiki/4%2B1_architectural_view_model)
- [The C4 model for software architecture](https://c4model.com/)

看了半天,应该是了解得太浅,依然没多少头绪,怎么才能恰当地表达业务,设计及实现?换句话说,如何表达想法?

不知道其它人是否也有相同的困惑,能有什么办法解决这个问题?