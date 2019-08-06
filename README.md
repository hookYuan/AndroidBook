## 前言
> 没有规矩不成方圆，良好的代码规范，能够在项目当中发挥举足轻重的作用；它不仅能使你们的开发更加高效，而且还会减少BUG产生的几率，增强代码可维护性及稳定性。
>
>本文将引用[《阿里巴巴Java开发手册（详尽版）》](https://snailclimb.gitee.io/javaguide/#/java/Java%E7%BC%96%E7%A8%8B%E8%A7%84%E8%8C%83?id=%e5%9b%a2%e9%98%9f])中的标记方式。依据约束力强弱及故障敏感性，规约依次分为【强制】、【推荐】、【参考】三大类。在延伸信息中，“说明”对规约做了适当扩展和解释；【正例】提倡什么样的编码和实现方式；【反例】说明需要提防的雷区，以及真实的错误案例。
>
>本文将提供长期更新并同步上传[ github ](https://github.com/hookYuan/AndroidBook),如有不合理的地方欢迎指正。同时希望更多的Android开发者加入进来维护。

## 编程规约
### （一）、Java命名风格（参考[《阿里巴巴Java开发手册》](https://snailclimb.gitee.io/javaguide/#/java/Java%E7%BC%96%E7%A8%8B%E8%A7%84%E8%8C%83?id=%e5%9b%a2%e9%98%9f])）
1. 【强制】代码中的命名均不能以下划线或美元符号开始，也不能以下划线或美元符号结束。
【反例】_name / __name / $name / name_ / name$ / name__ 
<br/>

2. 【强制】代码中的命名严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。
【说明】正确的英文拼写和语法可以让阅读者易于理解，避免歧义。注意，纯拼音命名方式更要避免采用。
【正例】renminbi / alibaba / taobao / youku / hangzhou 等国际通用的名称，可视同英文。
【反例】DaZhePromotion [打折] / getPingfenByName() [评分] / int 某变量 = 3
<br/>

3. 【强制】类名使用UpperCamelCase风格，但以下情形例外：DO / BO / DTO / VO / AO / PO / UID等。 
【正例】JavaServerlessPlatform / UserDO / XmlService / TcpUdpDeal / TaPromotion
【反例】javaserverlessplatform / UserDo / XMLService / TCPUDPDeal / TAPromotion
<br/>


4. 【强制】方法名、参数名、成员变量、局部变量都统一使用lowerCamelCase风格，必须遵从驼峰形式。
【正例】 localValue / getHttpMessage() / inputUserId
<br/>

5. 【强制】常量命名全部大写，单词间用下划线隔开，力求语义表达完整清楚，不要嫌名字长。 
【正例】MAX_STOCK_COUNT / CACHE_EXPIRED_TIME 
【反例】MAX_COUNT / EXPIRED_TIME
<br/>

6. 【强制】抽象类命名使用Abstract或Base开头；异常类命名使用Exception结尾；测试类命名以它要测试的类的名称开始，以Test结尾。 
<br/>

7. 【强制】类型与中括号紧挨相连来表示数组。 
【正例】定义整形数组int[] arrayDemo;
【反例】在main参数中，使用String args[]来定义。
<br/>

8. 【强制】POJO类中布尔类型变量都不要加is前缀，否则部分框架解析会引起序列化错误。
【说明】在本文MySQL规约中的建表约定第一条，表达是与否的值采用is_xxx的命名方式，所以，需要在<resultMap>设置从is_xxx到xxx的映射关系。 
【反例】定义为基本数据类型Boolean isDeleted的属性，它的方法也是isDeleted()，RPC框架在反向解析的时候，“误以为”对应的属性名称是deleted，导致属性获取不到，进而抛出异常。
<br/>

9. 【强制】包名统一使用小写，点分隔符之间有且仅有一个自然语义的英语单词。包名统一使用单数形式，但是类名如果有复数含义，类名可以使用复数形式。
【正例】应用工具类包名为com.alibaba.ai.util、类名为MessageUtils（此规则参考spring的框架结构）
<br/>

 10. 【强制】避免在子父类的成员变量之间、或者不同代码块的局部变量之间采用完全相同的命名，使可读性降低。 
【说明】子类、父类成员变量名相同，即使是public类型的变量也是能够通过编译，而局部变量在同一方法内的不同代码块中同名也是合法的，但是要避免使用。对于非setter/getter的参数名称也要避免与成员变量名称相同。
【反例】
```
public class ConfusingName {
    public int age;

    // 非setter/getter的参数名称，不允许与本类成员变量同名
    public void getData(String alibaba) {
        if (condition) {
            final int money = 531;
            // ...
        }
        for (int i = 0; i < 10; i++) {
      // 在同一方法体中，不允许与其它代码块中的money命名相同
            final int money = 615;
      // ...
        }
    }
}

class Son extends ConfusingName {
    // 不允许与父类的成员变量名称相同
    public int age;
}
```
<br/>

11. 【强制】杜绝完全不规范的缩写，避免望文不知义。
【反例】AbstractClass“缩写”命名成AbsClass；condition“缩写”命名成 condi，此类随意缩写严重降低了代码的可阅读性。
<br/>

12. 【推荐】为了达到代码自解释的目标，任何自定义编程元素在命名时，使用尽量完整的单词组合来表达其意。 
【正例】在JDK中，表达原子更新的类名为：AtomicReferenceFieldUpdater。
【反例】int a的随意命名方式。
<br/>

13. 【推荐】在常量与变量的命名时，表示类型的名词放在词尾，以提升辨识度。
【正例】startTime / workQueue / nameList / TERMINATED_THREAD_COUNT 
【反例】startedAt / QueueOfWork / listName / COUNT_TERMINATED_THREAD
<br/>

14. 【推荐】如果模块、接口、类、方法使用了设计模式，在命名时需体现出具体模式。 
【说明】将设计模式体现在名字中，有利于阅读者快速理解架构设计理念。
【正例】 public class OrderFactory; public class LoginProxy; public class ResourceObserver;
<br/>

15. 【推荐】接口类中的方法和属性不要加任何修饰符号（public 也不要加），保持代码的简洁性，并加上有效的Javadoc注释。尽量不要在接口里定义变量，如果一定要定义变量，肯定是与接口方法相关，并且是整个应用的基础常量。
【正例】接口方法签名 void commit(); 接口基础常量 String COMPANY = "alibaba"; 【反例】接口方法定义 public abstract void f();
【说明】JDK8中接口允许有默认实现，那么这个default方法，是对所有实现类都有价值的默认实现。

16. 接口和实现类的命名有两套规则： 
1）【强制】对于Service和DAO类，基于SOA的理念，暴露出来的服务一定是接口，内部的实现类用Impl的后缀与接口区别。
      &ensp; &ensp;&ensp;【正例】CacheServiceImpl实现CacheService接口。

 &ensp;&ensp;&ensp;2）【推荐】如果是形容能力的接口名称，取对应的形容词为接口名（通常是–able的形容词）。
        &ensp; &ensp;&ensp; &ensp;&ensp;【正例】AbstractTranslator实现 Translatable接口。

（一）、Res命名风格

