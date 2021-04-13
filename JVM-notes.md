

# JVM̽��

���ϸ������KuangShen JVM �ʼ���Դ��https://github.com/xudongyin1/Study-Notes/blob/master/Java/JVM.md

�ӽ�ԭ�ʼǣ���΢΢�Ķ���https://blog.csdn.net/weixin_45653314/article/details/111145660

- [JVM�ڴ�ģ��-��ϸ��](https://www.processon.com/view/5ea567b163768974669293f3)
- [jvm�ڴ�ģ��](https://www.processon.com/view/5c31d6e2e4b0fa03ce8d3017)�����ĳ�����

![image-20201221231226076](JVM-notes.assets/image-20201221231226076.png)

- ����̸̸���JVM����⣿java8�������֮ǰ�ı仯���£�
- ʲô��OOM��ʲô��ջ���StackOverFlowError����ô������
- JVM�ĳ��õ��Ų�������Щ��
- �ڴ�������ץȡ����ô����Dump�ļ���֪����
- ̸̸JVM�У�������������ʶ��



## 1JVM��λ��

- java��������jvm���棬jre-jvm�� �ڲ���ϵͳ֮�ϣ��������Ӳ��ϵͳ��
- linux����jar,��������������ֱ�Ӱ�װjre�Ϳ����ˣ����ذ�װJDK

![image-20201217135857782](JVM-notes.assets/image-20201217135857782.png)

## 2 JVM����ϵ�ṹ

![���������ͼƬ����](https://img-blog.csdnimg.cn/20200817162604620.png��x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

- [��ϵ�ṹ](https://www.processon.com/view/5ea567b163768974669293f3)
- [jvm�ڴ�ģ��](https://www.processon.com/view/5c31d6e2e4b0fa03ce8d3017)�����ĳ�����
- jvm���ţ���Ҫ˵�������������͡��ѡ���99% �Ƕѣ���==����ջ���������ط���ջ�������������������������������һ��==
- �������ͼʹ������ڴ�Ϊ�����ڴ��1/4, ��jvm��ʼ���ڴ�Ϊ1/64��**-Xms1024m -Xmx1024m -XX:+PrintGCDetails**��



## 3 �������

- ���壺 ��ļ���ָ���ǽ����.class�ļ��еĶ��������ݶ��뵽�ڴ��У������������ʱ�������ķ������ڣ�Ȼ���ڶ�������һ�� java.lang.Class����������װ���ڷ������ڵ����ݽṹ
- ���ã��������ļ���������ջ�У�����ʵ���ڶ���

![image-20201217142545861](JVM-notes.assets/image-20201217142545861.png)





![image-20201217142729280](JVM-notes.assets/image-20201217142729280.png)





�������Դ������������

- �����������������Bootstrap��

- ��չ���������Ext

- Ӧ�ó����������ϵͳ�������SystemAppClass ���߽� Applicaton��

- CustomClassLoader���û��Զ������������

  `java`��д,�û��Զ�����������,�ɼ���ָ��·����`class`�ļ�

![img](JVM-notes.assets/eaf81a4c510fd9f950e68758c03f2f2e2834a422.jpeg)



## 4 ˫��ί�ɻ���

### Java����ػ��ƣ�

[Java����ػ��ƣ����������](https://baijiahao.baidu.com/s��id=1636309817155065432&wfr=spider&for=pc)

### Java˫��ί�ɻ��Ƽ����ã�

[���Թ٣�java˫��ί�ɻ��Ƽ�����](https://www.jianshu.com/p/1e4011617650)

1. ��ֹ�ظ�����ͬһ��`.class`��ͨ��ί��ȥ��������һ�ʣ����ع��ˣ��Ͳ����ټ���һ�顣
2. ��֤���ݰ�ȫ����֤����`.class`���ܱ��۸ġ�ͨ��ί�з�ʽ��==����ȥ�۸ĺ���`.class`==����ʹ�۸�Ҳ����ȥ���أ���ʹ����Ҳ������ͬһ��`.class`�����ˡ�



- ��ĳ�����������Ҫ����ĳ��`.class`�ļ�ʱ�������Ȱ��������ί�и������ϼ�����������ݹ��������������ϼ����������û�м��أ��Լ��Ż�ȥ��������ࡣ

<img src="JVM-notes.assets/7634245-7b7882e1f4ea5d7d.png" alt="img" style="zoom: 67%;" />



>note�� ����Ա����дjava.lang.String������˫��ί�ɻ��ƣ�ȷ����ȫ���أ����ⱨ��

![image-20201217150543823](JVM-notes.assets/image-20201217150543823.png)



```java
public class Student {
    @Override
    public String toString() {
        return "Student{}";
    }

    public static void main(String[] args) {
        Student student = new Student();
        System.out.println(student.getClass().getClassLoader().toString()); // AppClassLoader
    }

    /**
     * 1. ��������յ�����AppClassLoader  ---> ExtClassLoader��D:Environment\java\jre\lib\ext)  ---> Bootstrap
     * 2. ���������ί�и�����ȥ��ɣ�һֱ����ί�У�ֱ���������������Bootstrap)
     * 3. ��������� �Ƿ��ܹ����ص�ǰ�࣬�ܹ��ͼ��ؽ�����ʹ�õ�ǰ�࣬�����ܹ����ܳ��쳣��
     * 4. �ظ�����3.
     *
     * Class Not found: ��
     * null��
     */
}
```



��һ�����յ�����������������Ȳ��᳢���Լ�ȥ��������࣬���ǰ��������ί�ɸ�����ȥ��ɣ�ÿһ������������������ˣ����
���еļ�������Ӧ�ô��͵�������������У�ֻ�е���������������Լ��޷������������ʱ�������ļ���·����û���ҵ��������
��Class���� ����������Ż᳢���Լ�ȥ���ء�
����˫��ί�ɵ�һ���ô��Ǳ������λ�� rt.jar ���е��� java.lang.Object���������ĸ���������������࣬���ն���ί�и������������
���������м��أ������ͱ�֤��ʹ�ò�ͬ������������յõ��Ķ���ͬ��һ�� Object ����

![���������ͼƬ����](JVM-notes.assets/20201213224546527.png)
˫��ί�ɵĺô������Լ���д�������java.lang�����Լ�����ģ�����jar������ġ������ᱨ����Ϊ�����Լ���д����ᱻί�е�BootStrap,������������jar�������String����ؽ��ڴ棬���Լ��ز����Լ����ࡣ���԰��Լ�����д��ȥbin/ext��



## 5 ɳ�䰲ȫ����

- Java��ȫģ�ͺ���
- ɳ�䣺���Ƴ��������ʱ����
- ��Domain����
- ��java�����޶���������ض������з�Χ�ڣ��ϸ����ƴ���Ա���ϵͳ��Դ�ķ��ʣ�������ʩ��֤�Դ������Ч���룬��ֹ�Ա���ϵͳ���ƻ�



ava��ȫģ�͵ĺ��ľ���Javaɳ��(sandbox) , ��

ʲô��ɳ�䣿ɳ����һ�����Ƴ������еĻ�����ɳ����ƾ��ǽ�Java�����޶��������(JVM)�ض������з�Χ�У������ϸ����ƴ���Ա���ϵͳ��Դ���ʣ�ͨ�������Ĵ�ʩ����֤�Դ������Ч���룬��ֹ�Ա���ϵͳ����ƻ���

ɳ����Ҫ����ϵͳ��Դ���ʣ���ϵͳ��Դ����ʲô�� CPU���ڴ桢�ļ�ϵͳ�����硣��ͬ�����ɳ�����Щ��Դ���ʵ�����Ҳ���Բ�һ���� ���е�Java�������ж�����ָ��ɳ�䣬���Զ��ư�ȫ���ԡ�

��Java�н�ִ�г���ֳɱ��ش����Զ�̴������֣����ش���Ĭ����Ϊ�����εģ���Զ�̴����򱻿����ǲ����ŵġ��������ŵı��ش���,���Է���һ�б�����Դ�������ڷ����ŵ�Զ�̴��������ڵ�Javaʵ���У���ȫ������ɳ��Sandbox)���ơ�����ͼ��ʾJDK1.0��ȫģ�� ![���������ͼƬ����](JVM-notes.assets/20201213230825785.png)

ͼ JDK1.0��ȫģ��

������ϸ�İ�ȫ����Ҳ������Ĺ�����չ�����ϰ������統�û�ϣ��Զ�̴�����ʱ���ϵͳ���ļ�ʱ�򣬾��޷�ʵ�֡�����ں�����Java1.1�汾�У���԰�ȫ�������˸Ľ��������˰�ȫ���ԣ������û�ָ������Ա�����Դ�ķ���Ȩ�ޡ�![����ͼ��ʾJDK1.1��ȫģ�� ���������ͼƬ����](JVM-notes.assets/20201213230841367.png)

ͼ JDK1.1��ȫģ��

��Java1.2�汾�У��ٴθĽ��˰�ȫ���ƣ������˴���ǩ�������۱��ش������Զ�̴��룬���ᰴ���û��İ�ȫ�����趨��������������ص��������Ȩ�޲�ͬ�����пռ䣬��ʵ�ֲ��컯�Ĵ���ִ��Ȩ�޿���![������ͼ��ʾ ���������ͼƬ����](JVM-notes.assets/20201213230909996.png)

ͼ JDK1.2��ȫģ��

��ǰ���µİ�ȫ����ʵ�֣�����������(Domain)�ĸ�������������д�����ص���ͬ��ϵͳ���Ӧ����,ϵͳ�򲿷�ר�Ÿ�����ؼ���Դ���н�����������Ӧ���򲿷���ͨ��ϵͳ��Ĳ��ִ������Ը�����Ҫ����Դ���з��ʡ�������в�ͬ���ܱ�����(Protected Domain),��Ӧ��һ����Ȩ��(Permission)�������ڲ�ͬ���е����ļ��;����˵�ǰ���ȫ��Ȩ��
![ͼ JDK1.6��ȫģ��](JVM-notes.assets/20201213230952622.png)

���ɳ��Ļ������

- �ֽ���У����(bytecode verifier)��ȷ��Java���ļ���ѭJava���Թ淶���������԰���Java����ʵ���ڴ汣���������������е����ļ����ᾭ���ֽ���У�飬��������ࡣ 
- ���b����(class loader)��
  - ������װ������3�������Javaɳ�������� 
    -  ����ֹ�������ȥ��������Ĵ���;
    -  ���ػ��˱����ε����߽�; 
    -  ����������뱣����,ȷ���˴�����Խ�����Щ������ 
  - �����Ϊ��ͬ�����������������ṩ��ͬ�������ռ䣬�����ռ���һϵ��Ψһ��������ɣ� ÿһ����װ�ص��ཫ��һ�����֣���������ռ�����Java�����Ϊÿһ����װ����ά���ģ����ǻ���֮���������ɼ��� ��װ�������õĻ�����˫��ί��ģʽ�� 
    - �����ڲ�JVM�Դ����������ʼ����,������ͬ����ò������شӶ��޷�ʹ��;
    - �����ϸ�ͨ�����������˷�����,���������ͨ�����ô���Ҳ�޷����Ȩ�޷��ʵ��ڲ��࣬�ƻ��������Ȼ�޷���Ч��
- ��ȡ������(access controller)����ȡ���������Կ��ƺ���API�Բ���ϵͳ�Ĵ�ȡȨ�ޣ���������ƵĲ����趨,�������û�ָ����
- ��ȫ������(security manager)�� �Ǻ���API�Ͳ���ϵͳ֮�����Ҫ�ӿڡ�ʵ��Ȩ�޿��ƣ��ȴ�ȡ���������ȼ��ߡ�
- ��ȫ�����(security package)�� java.security�µ������չ���µ��࣬�����û�Ϊ�Լ���Ӧ�������µİ�ȫ���ԣ�����:  ��ȫ�ṩ�� \ ��ϢժҪ \ ����ǩ�� \ ���� \ ����



## 6 Native

- ���õײ�c��c++���Կ�
- native -> jni -> ���ط����ӿ� -> ���ط�����





- ���ط���ջ
- һ���õĲ��࣬Ӳ�������õĶ�



��⣺
![���������ͼƬ����](JVM-notes.assets/2020121323143094.png)
��ͼ���̼߳���ľ���java�����˵ġ����start()��������������һ�����󷽷��������Լ���дһ�����ǳ����࣬�������дһ�����󷽷��ᱨ���������native�ؼ��ֲ��ᱨ�������в��ˡ�
![���������ͼƬ����](JVM-notes.assets/20201213231527252.png)

�� native�����Ǵ���native�ؼ��ֵģ�˵��java�����÷�Χ�ﲻ���ˣ���ȥ���õײ�c���ԵĿ�! �� ����뱾�ط���ջ �� ���ñ��ط������ؽӿ� JNI (Java Native Interface) �� JNI����:����Java��ʹ�ã��ںϲ�ͬ�ı������ΪJava����!���: C��C++ �� Java������ʱ��C��C++���У���Ҫ���㣬����Ҫ�е���C��C++�ĳ��� �� �����ڴ�������ר�ſ�����һ��������: Native Method Stack���Ǽ�native���� �� ������ִ�е�ʱ�򣬼��ر��ط������еķ���ͨ��JNI �� ���磺Java����������ӡ��������ϵͳ�����ռ��ɣ�����ҵ��Ӧ�ñȽ��� �� private native void start0(); �� //���������ӿ�:Socket. . WebService~. .http~

Native Method Stack
�����ľ���������Native Method Stack�еǼ�native��������( Execution Engine )ִ������ִ�е�ʱ�����Native Libraies��[���ؿ�]

Native Interface���ؽӿ�
�����ؽӿڵ��������ںϲ�ͬ�ı������ΪJava���ã����ĳ������ں�C/C++����, Java�ڵ�����ʱ����C/C++���е�ʱ����Ҫ���㣬�����е���C��C++�ĳ������Ǿ����ڴ���ר�ſ����˿���������Ϊnative�Ĵ��룬���ľ�����������**Native Method Stack �еǼ�native����**,��( Execution Engine )ִ������ִ�е�ʱ�����Native Libraies�� ��Ŀǰ�÷���ʹ�õ�Խ��Խ���ˣ���������Ӳ���йص�Ӧ�ã�����ͨ��Java����������ӡ������Javaϵͳ���������豸������ҵ��Ӧ�����Ѿ��Ƚ��ټ�����Ϊ���ڵ��칹�����ͨ�źܷ���������ʹ��Socketͨ��,Ҳ����ʹ��Web Service



![image-20201217155525957](JVM-notes.assets/image-20201217155525957.png)

## 7 PC���������

- pc�Ĵ���
- ���������Program Counter Register
- ÿ���̶߳���һ��������������߳�˽�У�����һ��ָ�룬ָ�򷽷����еķ����ֽ��루�����洢ָ����һ��ָ��ĵ�ַ�� Ҳ������Ҫִ�е�ָ����룩
- �ǳ���С�Ŀռ� --���Ժ��Բ���

## 8 ������

- �����̹߳���

- ==��̬����������������Ϣ�����췽�����ӿڶ��壩������ʱ�ĳ�����Ҳ���ڷ������У�����ʵ���������ڶ��ڴ��У��ͷ������޹�==

  > static��final ��Class(��ģ��)������ʱ�ĳ�����

## 9 ջ

- ջ���Ƚ����������ȳ����ѣ��Ƚ��ȳ���������
- �߳̽�����ջ�ڴ��ͷ�

> sun��mainҲ���̣߳�һ���߳̽�����ջ�ͽ�����



- ���ܳ��������
- ջ�����ŵĶ�����8��������ͣ�ʵ���������������ã�Ox8888)
- ջ֡����֡��֡��ÿһ����ִ�еķ����������ջ֡

<img src="JVM-notes.assets/image-20201218085344144.png" alt="image-20201218085344144" style="zoom:67%;" />



- ջ������StackOverflowError

==����1������ʵ�����Ĺ��̣�ջ���ѣ���������ʵ����ϵ==

![image-20201218090219044](JVM-notes.assets/image-20201218090219044.png)



==����ʵ�����Ĺ��̣�new�Ĺ��̣�==

1. �ȶ�1����������ջ����
2. �ڶ�1������ʵ�������ã���������
3. ��ʵ��ָ��̬�����أ�����1������



### ����

1. ջ���������Щ��������ô��ģ�
2. ���������������ʲô������



## 10 ����JVM

- SUN ��˾ - HotSpot ��ʹ������Ҫ�о��ģ�
- BEA ��˾ JRocket������������JVM���ʺϾ��£���
- IBM ��˾ J9

## 11 ��

- һ��JVMֻ��һ�����ڴ�

- �������������������͵���ʵ����

- 3������

  - ������������԰��: ���еĶ���new��������԰ȥ�����г���
    - ����԰���ˣ�����GC����Щ�������ƶ����Ҵ���
    - �Ҵ������ˣ��������GC����ʣ�µģ��͵�����������
    - �ܵ���˵������������ռ����new�ģ�����1%��
  - ������-- ������ --�����������Ҵ�0�Ҵ�1����˳�����ģ��ɲ�����ɱ����
  - ==������==
    - ��������һ����פ�ڴ��������ڴ��JDK����Я����Class����InterfaceԪ���ݣ�==�洢����Java���е�һЩ����==
    - �汾��
      - jdk1.6֮ǰ�������ô�������������`������`
      - jdk1.7�����ô������Ҫ�����˻���ȥ���ô�������������`��`�� 
      - jdk1.8֮�������ô�����������`Ԫ�ռ�`
    - ��Щ������ܻ�������������һ���ӱ����ˣ�
      - �����򲻴����������գ�����Ҳ����� �����˴���������jar�� 
      - ������̬���ɵķ�����
      - Tomcat������̫��Ӧ��
    - �ر�������ͻ��ͷ�����ڴ�

  


![image-20201218093012237](JVM-notes.assets/image-20201218093012237.png)





### �ѵĽṹ��1.8�Ժ������������

![image-20201218100143315](JVM-notes.assets/image-20201218100143315.png)

Ԫ�ռ䣺==�߼��ϴ��ڣ������ϲ�����==

- PSYoungGen + ParOldGen  = 981.5�����ʶ����֣�Ԫ�ռ䣨Metaspace���������ϲ�û�з����ڴ档



- gc����������Ҫ���������������԰������������

  ```shell
  max:981.5M
  total:981.5M
  Heap
   PSYoungGen      total 305664K, used 15729K [0x00000000eab00000, 0x0000000100000000, 0x0000000100000000)
    eden space 262144K, 6% used [0x00000000eab00000,0x00000000eba5c420,0x00000000fab00000)
    from space 43520K, 0% used [0x00000000fd580000,0x00000000fd580000,0x0000000100000000)
    to   space 43520K, 0% used [0x00000000fab00000,0x00000000fab00000,0x00000000fd580000)
   ParOldGen       total 699392K, used 0K [0x00000000c0000000, 0x00000000eab00000, 0x00000000eab00000)
    object space 699392K, 0% used [0x00000000c0000000,0x00000000c0000000,0x00000000eab00000)
   Metaspace       used 2998K, capacity 4496K, committed 4864K, reserved 1056768K
    class space    used 322K, capacity 388K, committed 512K, reserved 1048576K
  
  ```

- �׳�OOM demo��ʾ

```java
package com.xiaofan;

import java.util.Random;

public class Main {

    public static void main(String[] args) {
        String a = "kuangshensayjava";
        while(true) {
            a += a + new Random().nextInt(999999999) + new Random().nextInt(999999999);
        }
    }
}
```

![image-20201218101213825](JVM-notes.assets/image-20201218101213825.png)



```java
D:\jdk1.8\bin\java.exe -Xms8m -Xmx8m -XX:+PrintGCDetails -javaagent:E:\idea_ultimate\IntelliJ_IDEA_2020_2\lib\idea_rt.jar=50684:E:\idea_ultimate\IntelliJ_IDEA_2020_2\bin -Dfile.encoding=UTF-8 -classpath D:\jdk1.8\jre\lib\charsets.jar;D:\jdk1.8\jre\lib\deploy.jar;D:\jdk1.8\jre\lib\ext\access-bridge-64.jar;D:\jdk1.8\jre\lib\ext\cldrdata.jar;D:\jdk1.8\jre\lib\ext\dnsns.jar;D:\jdk1.8\jre\lib\ext\jaccess.jar;D:\jdk1.8\jre\lib\ext\jfxrt.jar;D:\jdk1.8\jre\lib\ext\localedata.jar;D:\jdk1.8\jre\lib\ext\nashorn.jar;D:\jdk1.8\jre\lib\ext\sunec.jar;D:\jdk1.8\jre\lib\ext\sunjce_provider.jar;D:\jdk1.8\jre\lib\ext\sunmscapi.jar;D:\jdk1.8\jre\lib\ext\sunpkcs11.jar;D:\jdk1.8\jre\lib\ext\zipfs.jar;D:\jdk1.8\jre\lib\javaws.jar;D:\jdk1.8\jre\lib\jce.jar;D:\jdk1.8\jre\lib\jfr.jar;D:\jdk1.8\jre\lib\jfxswt.jar;D:\jdk1.8\jre\lib\jsse.jar;D:\jdk1.8\jre\lib\management-agent.jar;D:\jdk1.8\jre\lib\plugin.jar;D:\jdk1.8\jre\lib\resources.jar;D:\jdk1.8\jre\lib\rt.jar;E:\idea_ultimate\Project\Hello\out\production\Hello com.xiaofan.Main
[GC (Allocation Failure) [PSYoungGen: 1520K->504K(2048K)] 1520K->632K(7680K), 0.0008567 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 1973K->488K(2048K)] 2101K->1314K(7680K), 0.0006303 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 1578K->488K(2048K)] 2404K->1619K(7680K), 0.0004381 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 1576K->224K(2048K)] 3766K->2944K(7680K), 0.0006442 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 782K->224K(2048K)] 4562K->4004K(7680K), 0.0004239 secs] [Times: user=0.03 sys=0.02, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 224K->224K(2048K)] 4004K->4004K(7680K), 0.0004558 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[Full GC (Allocation Failure) [PSYoungGen: 224K->0K(2048K)] [ParOldGen: 3780K->2165K(5632K)] 4004K->2165K(7680K), [Metaspace: 2947K->2947K(1056768K)], 0.0064615 secs] [Times: user=0.00 sys=0.00, real=0.01 secs] 
[Full GC (Ergonomics) [PSYoungGen: 1134K->0K(2048K)] [ParOldGen: 5345K->2697K(5632K)] 6480K->2697K(7680K), [Metaspace: 2963K->2963K(1056768K)], 0.0057346 secs] [Times: user=0.00 sys=0.00, real=0.01 secs] 
[GC (Allocation Failure) [PSYoungGen: 39K->160K(2048K)] 4856K->4976K(7680K), 0.0003290 secs] [Times: user=0.02 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 160K->160K(2048K)] 4976K->4976K(7680K), 0.0002194 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[Full GC (Allocation Failure) [PSYoungGen: 160K->0K(2048K)] [ParOldGen: 4816K->3760K(5632K)] 4976K->3760K(7680K), [Metaspace: 2966K->2966K(1056768K)], 0.0020017 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[GC (Allocation Failure) [PSYoungGen: 0K->0K(2048K)] 3760K->3760K(7680K), 0.0002045 secs] [Times: user=0.00 sys=0.00, real=0.00 secs] 
[Full GC (Allocation Failure) [PSYoungGen: 0K->0K(2048K)] [ParOldGen: 3760K->3741K(5632K)] 3760K->3741K(7680K), [Metaspace: 2966K->2966K(1056768K)], 0.0064159 secs] [Times: user=0.00 sys=0.00, real=0.01 secs] 
Heap
 PSYoungGen      total 2048K, used 131K [0x00000000ffd80000, 0x0000000100000000, 0x0000000100000000)
  eden space 1536K, 8% used [0x00000000ffd80000,0x00000000ffda0c38,0x00000000fff00000)
  from space 512K, 0% used [0x00000000fff00000,0x00000000fff00000,0x00000000fff80000)
  to   space 512K, 0% used [0x00000000fff80000,0x00000000fff80000,0x0000000100000000)
 ParOldGen       total 5632K, used 3741K [0x00000000ff800000, 0x00000000ffd80000, 0x00000000ffd80000)
  object space 5632K, 66% used [0x00000000ff800000,0x00000000ffba7700,0x00000000ffd80000)
 Metaspace       used 3075K, capacity 4496K, committed 4864K, reserved 1056768K
  class space    used 332K, capacity 388K, committed 512K, reserved 1048576K
Exception in thread "main" java.lang.OutOfMemoryError: Java heap space
	at java.util.Arrays.copyOf(Arrays.java:3332)
	at java.lang.AbstractStringBuilder.ensureCapacityInternal(AbstractStringBuilder.java:124)
	at java.lang.AbstractStringBuilder.append(AbstractStringBuilder.java:674)
	at java.lang.StringBuilder.append(StringBuilder.java:208)
	at com.xiaofan.Main.main(Main.java:10)
```



```java
OOM:
    1. �������� ���ڴ棬�鿴���
    2. �����ڴ棬 ��һ����Щ�ط� �������⣨רҵ���ߣ�

�������
    -Xms ����Java��������ʱ�ĳ�ʼ�Ѵ�С-- ��ʼ���ڴ��С
    -Xmx ����java�����ܻ�õ����Ѵ�С-- ����ڴ��С
    -XX:+HeapDumpOnOutOfMemoryError ʹ�øĲ����������ڴ����ʱ�����������Ϣ
    -XX:+HeapDumpPath�� �������õ����ѵĴ��·��
    -XX:+PrintGCDetails ��ӡGC����������Ϣ
    -Xlog:gc*           �������
```





## 12 ���ڴ����

- ��OOMʱ���״ΰ�����������ڴ�ռ�鿴����������ڴ棬�鿴һ���ĸ��ط��������⣨JProfiler��
- JProfiler���ã�����DumpN�ڴ��ļ������ٶ�λ�ڴ�й©����ö��е����ݣ���ȡ��Ķ���
- ������������ò���
  - -Xms ����Java��������ʱ�ĳ�ʼ�Ѵ�С-- ��ʼ���ڴ��С
  - -Xmx ����java�����ܻ�õ����Ѵ�С-- ����ڴ��С
  - -XX:+HeapDumpOnOutOfMemoryError ʹ�øĲ����������ڴ����ʱ�����������Ϣ
  - -XX:+HeapDumpPath�� �������õ����ѵĴ��·��
  - -XX:+PrintGCDetails ��ӡGC����������Ϣ
  - ���� ----- -Xms1m -Xmx1m -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=d:/Test3.dump



�ڴ���շ������ߣ�JProfiler��MAT���߷���OOM��ԭ��

- ����Dump�ļ������ٶ�λ�ڴ�й¶
- ��ȡ���е�����
- ��ô�Ķ���

```xml
OOM:
    1. �������� ���ڴ棬�鿴���
    2. �����ڴ棬 ��һ����Щ�ط� �������⣨רҵ���ߣ�

�������
    -Xms ����Java��������ʱ�ĳ�ʼ�Ѵ�С-- ��ʼ���ڴ��С
    -Xmx ����java�����ܻ�õ����Ѵ�С-- ����ڴ��С
    -XX:+HeapDumpOnOutOfMemoryError ʹ�øĲ����������ڴ����ʱ�����������Ϣ
    -XX:+HeapDumpPath�� �������õ����ѵĴ��·��
    -XX:+PrintGCDetails ��ӡGC����������Ϣ
    -Xlog:gc*           �������
```



### Jprofiler

```java
/*
    -Xms ���ó�ʼ���ڴ��С
    -Xmx �����������ڴ�
    -XX:+HeapDumpOnOutOfMemoryError
    -XX:+PrintGCDetails

    -Xms1m -Xms2m -XX:+HeapDumpOnOutOfMemoryError
 */

public class OomForJprofiler {
    byte[] array = new byte[1024*1024];

    public static void main(String[] args) {
        ArrayList<OomForJprofiler> list = new ArrayList<>();
        int count = 0;

        try{
            while (true){
                list.add(new OomForJprofiler());
                count++;
            }
        }catch (Error e){
            System.out.println("Error " + count);
            e.printStackTrace();
        }
    }
}
```



![image-20201218160352490](JVM-notes.assets/image-20201218160352490.png)



Profiler������־�Ĳ��裺

1. ȥ�����ļ��������Ǹ����ļ���������
2. ���̣߳������Ǹ��߳�ʹ�õ����������

![image-20201218162026160](JVM-notes.assets/image-20201218162026160.png)

## 13 GC

- ��������Ϊ�Զ����ֶ�ֻ������

- GC�����ڶ�+������

- GC�󲿷����������
  - ��GC ----- ��ͨGC
  - ��GC ----- ȫ��GC
  
- ��Ҫ��Ӧ��

  - ��Ǹ����㷨 --- �������㷨       ----  CMS�ռ���
  - ����������ѹ�����㷨       ------ ������㷨

- GC�㷨����
  - 1 �����㷨 ---[GC�㷨-�����㷨](https://www.cnblogs.com/hujingnb/p/12642079.html)
    
    - ���㷨���ڴ�ƽ���ֳ������֣�Ȼ��ÿ��ֻʹ�����е�һ���֣����ⲿ���ڴ�����ʱ�򣬽��ڴ������д��Ķ����Ƶ���һ���ڴ��У�Ȼ��֮ǰ���ڴ���գ�ֻʹ���ⲿ���ڴ棬ѭ����ȥ
      - �Ҵ���01�� from...to...�� 0��1���಻�Ͻ���������gc���и����㷨
      
      <img src="JVM-notes.assets/image-20201218165100496.png" alt="image-20201218165100496" style="zoom: 67%;" />
      
      - ��һֱû�������뵽������
        - �ŵ㣺ʵ�ּ򵥣��������ڴ���Ƭ
        - ȱ�㣺�˷�һ����ڴ�ռ�
        
        <img src="JVM-notes.assets/image-20201218164654811.png" alt="image-20201218164654811" style="zoom:80%;" />
    
  - 2 �������㷨 -----ɨ����󣬶Ի��ŵĶ�����б�ǣ� ��û�б�ǵĶ���������
    
    - �ŵ㣺����Ҫ����ռ䣬���ڸ����㷨
    - ����ɨ�裬�˷�ʱ�䣬������ڴ���Ƭ
    - ==���ѹ���㷨== ----- ���Ż���ѹ������ֹ��Ƭ�Ĳ����� ������ ��һ���ƶ���Ķ��󣬶���һ���ƶ��ɱ�
    
    ![image-20201218165651004](JVM-notes.assets/image-20201218165651004.png)
    
  - 3 ������ѹ���㷨 ----- �ȱ����������ٽ���ѹ��������Ƭ����֮��

  - 4 ���ü����㷨 ------ ÿ������һ����������һ�㲻�ã���Ϊ�����������ģ��ù���εĲ�ɾ��0�εľ�ɾ���� ---���ó���+1,����ɾ��-1

  <img src="JVM-notes.assets/image-20201218163131434.png" alt="image-20201218163131434" style="zoom: 50%;" />
  
- �ܽ᣺
  - �ڴ�Ч�ʣ������㷨 > ������ >���ѹ����ʱ�临�Ӷȣ�
  - �ڴ�����ȣ������㷨=���ѹ��>��������û��ѹ����
  - �ڴ������ʣ� ���ѹ��=������ > �����㷨��to���ǿ��еģ�
  - �ִ��ռ��㷨��JVM���ţ��� û����õ��㷨��ֻ������ʵ�
    - ����� ----- ����ʵͣ������㷨
    - ����� ----- ����ʸߣ� ����������ѹ�����ʵ��



### GC������Ŀ��

![image-20201218163155910](JVM-notes.assets/image-20201218163155910.png)





## ==14 JMM��==

1. ʲô��JMM��Java Memory Model����д��

   ������ ����һ����Э�飬���ڶ������ݵĶ�д�������أ�����Java�ڴ�ģ�ͣ�Java Memory Model ,JMM������һ�ַ����ڴ�ģ�͹淶�ģ������˸���Ӳ���Ͳ���ϵͳ�ķ��ʲ���ģ���֤��Java�����ڸ���ƽ̨�¶��ڴ�ķ��ʶ��ܱ�֤Ч��һ�µĻ��Ƽ��淶

2. JMM��������ʲô�ġ����������͡���Ƶ

   - `volatile`�ؼ��ֻ��ָֹ�����ţ�����ɼ������⡣
   - `synchronized`�ؼ��ֱ�֤ͬһʱ��ֻ����һ���̲߳����������ָֹ���������⡣
   - ==�����ܽ᣺==JMM����˹����ڴ�ģ��ɼ��ԣ������ԣ�ԭ���ԣ������⣬���Գ���Ա�ṩ���� `volatile` `synchronized`�ȵȹؼ��ֵķ�ʽ�������ڻ���һ����Э�顣

   

3. JMM������𰸣�

   - �߳�֮�����ͨ�š�ͬ����java�������õ��ǹ����ڴ�ģ��



### �߳�֮���ͨ��

- �����ڴ�Ĳ���ģ����߳�֮�乲�����Ĺ���״̬
- ��Ϣ���ݵĲ���ģ����



### ����ڲ����µ�����

1���ڴ����ϡ�����ֹ������

2���ٽ�����synchronized����

2.5 Happens-Before��

����Ҫ��ǰһ��������ִ�еĽ�����Ժ�һ�������ɼ�����ǰһ��������˳�����ڵڶ�������֮ǰ



### **JMM�ڴ�ģ����������**

1��ԭ����

- AtomicInteger
- ʹ�� synchronized ����������֤������ԭ����

2���ɼ��ԣ�

- volatile����ǿ�ƽ��ñ����Լ��͵�ʱ����������״̬��ˢ�����档�����ܱ�֤�̰߳�ȫ��

  - �ɼ��ԡ���һ��volatile�����Ķ��������ܿ����������̣߳������volatile��������д�롣

    ԭ���ԣ������ⵥ��volatile�����Ķ�/д����ԭ���ԣ���������volatile++���ָ��ϲ���������ԭ���ԡ�

- synchronized����һ������ִ�� unlock ����֮ǰ������ѱ���ֵͬ�������ڴ档

- final���� final �ؼ������ε��ֶ��ڹ�������һ����ʼ����ɣ�����û�з��� this ���ݣ������߳�ͨ�� this ���÷��ʵ���ʼ����һ��Ķ��󣩣���ô�����߳̾��ܿ��� final �ֶε�ֵ��

==3�������ԣ���==

Դ���� -> �������Ż������� -> ָ��е����� -> �ڴ�ϵͳ������ ->����ִ�е�����

��������̲���Ӱ�쵽���̳߳����ִ�У�ȴ��Ӱ�쵽���̲߳���ִ�е���ȷ��

�������ڽ�������ʱ���뿼�����ݵ������ԣ����̻߳����߳̽���ִ�У����ڱ������Ż����ŵĴ��ڣ������߳���ʹ�õı����ܷ�֤һ�������޷�ȷ���ġ�



==���ӣ�==

�������˰�Java�ڴ�ģ��JMM˵����ˣ�https://www.jianshu.com/p/8420ade6ff76

JMM�͵ײ�ʵ��ԭ��https://www.jianshu.com/p/8a58d8335270



BAT���������⣬�������Java�ڴ�ģ��JMM��http://www.hellojava.com/a/77344.html





![���������ͼƬ����](https://img-blog.csdnimg.cn/20200818164234102.png��x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2ZhbmppYW5oYWk=,size_16,color_FFFFFF,t_70#pic_center)

JMM��Java Memory Model��Java�ڴ�ģ�ͣ�



- Java Memory Model: Java�ڴ�ģ�� -- ������ ����
- �������̹߳����ڴ�����ڴ�֮��ĳ����ϵ
  - �߳�֮��Ĺ�������洢�����ڴ��� ----MAIN MEMORY
  - ÿ���̶߳���һ��˽�еı����ڴ� ---- LOCAL MEMORY
- �벢�����



## 15 OOM�������ԭ��

- java.lang.OutOfMemoryError
- �ڴ�й©��memory leak�� ��ָ������һ��̬����Ķ��ڴ�����ĳ��ԭ�����δ�ͷţ����ϵͳ�ڴ���˷ѣ����³������м�������ϵͳ���������غ��
- �ڴ������out of memory����ָ���������ڴ�ʱ�� û���㹻���ڴ湩������ʹ�ã�˵�׾����ڴ治���ã���ʱ�ͻᱨ��OOM,����ν���ڴ����
- OOM�����ԭ��
  - java����� ---- ��Ȼ���Ǵ��ʵ������ģ��Ǿ����޴���ʵ������
  - �����ջ��� ----- �����ջ��������java����ִ�е��ڴ�ģ�ͣ� ÿ��������ִ�е�ʱ�򶼻ᴴ��һ��ջ֡���ڴ洢�ֲ�������������ջ����̬���ӡ��������ڵ���Ϣ�����ط���ջ������ջ�������ǣ������ջΪ���������java�������񣬶����ط���ջΪ������ṩnative���������ڵ��̵߳Ĳ����У�����������ջ̫֡�󣬻�������ջ�ռ�̫С����ռ�ռ��޷�����ʱ��������׳��Ķ���StackOverflowError��������õ�OutOfMemoryError�쳣���ڶ��߳�����£�����׳�OutOfMemoryError�쳣
  - ���ط���ջ�����
  - ������������ʱ��������� - java�Ѻͷ������� java������Ҫ��Ŷ���ʵ��������ȣ���������������Ϣ����̬�����ȵȣ�����ʱ����Ҳ�Ƿ�������һ���֣� �������������̹߳��������ֻ���׳�OutOfMemeryError��
  - �����ڴ�ֱ����� -- NIO�йأ�New input/Output��,������һ�ֻ���ͨ���뻺������I/O��ʽ������native������ֱ�ӷ�������ڴ棬 Ȼ��ͨ��һ���洢��java���еĶ�����Ϊ����ڴ��Ӧ�ý��в�������������һЩ����������������ܣ���Ϊ��������Java�Ѻ�Native�������ظ�������

	1. �ٶ�

 	2. ˼ά��ͼ





































