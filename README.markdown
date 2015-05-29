**写在前头:本插件只适用 android studio和 Intellij IDEA 工具,eclipse 的少年无视我吧!!!**
##这个跟 master最大的区别是使用 Public 来修饰成员变量,代替了传统的 Set 和 get 方法.##
这是一个根据JSONObject格式的字符串,自动生成实体类参数.


版本1.1.1

>1.1.1版本更新内容
 1.  修复了因为过滤//注释代码导致的出现的 Json 格式验证异常;
 * 支持解析 java 的关键字作为 key (支持字段:
default,abstract,null,final,void,implements,
this,instanceof,native,new,goto,const,volatile,return,finally)其余暂不支持;

版本1.1.0
>1.1.0 版本更新内容:
  1. 直接数组中嵌套数组的解析;
  * 支持过滤Json格式中的注释代码.



  #Usage#
安装方法:
~~~
     1.下载当前仓库下的GsonFormat_.jar ;
     2.Android studio  File->Settings..->Plugins -->
 install plugin from disk..导入下载的GsonFormat_.jar 
     3重启android studio 
~~~

##使用方式##
在实体类中使用Generate的快捷键.

快捷键:图中选中的部分
![72350A47-A21A-4505-817E-2CA8092F7B7D.png](http://upload-images.jianshu.io/upload_images/166866-45621bdaadaa177c.png)
我这边的快捷键是 command+n;




####简单的实体类:####

简单的 json 格式
~~~
{
    "name": "王五",
    "gender": "man",
    "age": 15,
    "height": "140cm",
}
~~~
实体类
~~~
**
 * Created by 轻微 on 15/1/9.
 */
public class Bean  extends JSONModel {


    
    /**
     * height : 140cm
     * age : 15
     * name : 王五
     * gender : man
     */
    public String height;
    public int age;
    public String name;
    public String gender;

}
~~~



#####复杂的实体类:
实体类不仅包含另外一个**实体**,还包含另外实体的**数组**.
![复杂.gif](http://upload-images.jianshu.io/upload_images/166866-38c1f99c6d097367.gif)
图中复杂的json 格式
~~~
{
    "name": "王五",
    "gender": "man",
    "age": 15,
    "height": "140cm",
    "addr": {
        "province": "fujian",
        "city": "quanzhou",
        "code": "300000"
    },
    "hobby": [
        {
            "name": "billiards",
            "code": "1"
        },
        {
            "name": "computerGame",
            "code": "2"
        }
    ]
}
~~~
图中的实体类
~~~
/**
 * Created by 轻微 on 15/1/9.
 */
public class Bean  extends JSONModel {


     /**
     * height : 140cm
     * age : 15
     * name : 王五
     * hobby : [{"name":"billiards","code":"1"},{"name":"computerGame","code":"2"}]
     * gender : man
     * addr : {"province":"fujian","code":"300000","city":"quanzhou"}
     */
    public String height;
    public int age;
    public String name;
    public List<HobbyEntity> hobby;
    public String gender;
    public AddrEntity addr;

    public class HobbyEntity {
        /**
         * name : billiards
         * code : 1
         */
        public String name;
        public String code;
    }

    public class AddrEntity {
        /**
         * province : fujian
         * code : 300000
         * city : quanzhou
         */
        public String province;
        public String code;
        public String city;
    }
}

~~~






