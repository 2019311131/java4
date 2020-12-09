# 实验目的
 掌握字符串String及其方法的使用
 掌握文件的读取/写入方法
 掌握异常处理结构

#  实验内容
 在某课上,学生要提交实验结果，该结果存储在一个文本文件A中。
 文件A包括两部分内容：
 一是学生的基本信息；
 二是学生处理后的作业信息，该作业的业务逻辑内容是：利用已学的字符串处理知识编程完成《长恨歌》古诗的整理对齐工作，写出功能方法，实现如下功能：
 1.每7个汉字加入一个标点符号，奇数时加“，”，偶数时加“。”；
 2.允许提供输入参数，统计古诗中某个字或词出现的次数；
 3.输入的文本来源于文本文件B读取，把处理好的结果写入到文本文件A；
 4.考虑操作中可能出现的异常，在程序中设计异常处理程序。
 输入：汉皇重色思倾国御宇多年求不得······<未完，待续>
 输出：
 汉皇重色思倾国，御宇多年求不得。
 杨家有女初长成，养在深闺人未识。
 天生丽质难自弃，一朝选在君王侧。
 ······
 
 
#   实验要求
1.设计学生类（可利用之前的）；
2. 采用交互式方式实例化某学生；
3. 设计程序完成上述的业务逻辑处理，并且把“古诗处理后的输出”结果存储到学生基本信息所在的文本文件A中。

#  实验过程
 1.创建一个封装类：即学生类Student，
定义学生的基本属性name、sex、age，
利用super设置有参和无参的构造方法，
设置set()、get()方法以及toString()方法；
 2.创建一个统计古诗中某个汉字出现的次数的类time（即从字符串中提取子字符串，需要用到正则表达式）
创建BufferedReader对象读取文本文件A；
初始化StringBuffer对象；
创建一个空字符串；
利用while方法，写入readLine()方法判断每一行的内容有没有被读取到；
再用append()方法将实例化的StringBuffer对象和字符串拼接在一起；
声明要统计的汉字；
利用正则表达式中的两个类：Pattern和Matcher的相关方法以及find()方法统计所求汉字出现的次数。
 3.创建测试类Test，
用Scanner相关方法实现运行时交互式输入，即实例化学生；
利用文件字符的输入输出流写出读取和写入的文件；
利用FileReader方法将读取的文件设为只读文件；
定义一个char型数组；
利用Writer流的子类FileWriter创建指向目的地的输出流和Reader流的子类FileReader创建源的输入流；
（输出流的目的是提供一个通往目的地的通道，输入流的目的是提供一个读取源中数据的通道）
利用write方法把学生类的基本信息写入到缓冲区；
利用for循环和if判断方法添加“，”和“。”；
利用flush()方法将当前缓冲区的内容写入到目的地；
最后利用close()方法关闭所有打开的流。
1.类中的异常处理，根据具体情况而定

#  核心代码
package java4;

import java.io.*;
import java.util.Scanner;
public class java4 {
	    public static void main(String args[]) {
	        @SuppressWarnings("resource")
			Scanner input = new Scanner(System.in);
	        @SuppressWarnings("unused")
			int w;
	        StringBuffer str2 = null;
	        @SuppressWarnings("unused")
			Handle xms = new Handle();
	        StringBuffer str1 = Handle.Read();
	        @SuppressWarnings("unused")
			Homework one = new Homework();
	        str2 = Homework.HW(str1);
	        Handle.Write(str2);

	        System.out.println("请输入要查询的字符：");
	        String z = input.next();
	        w = Handle.getCharMaps(z,str1);

	        System.out.println("******************学生信息*********************");
	        Student xm = new Student();
	        xm.setName("张三");
	        xm.setAge(18);
	        xm.setNumber(2019999999);
	        xm.setSex("男");
	        System.out.println("学生姓名:" + xm.getName());
	        System.out.println("学生年龄:" + xm.getAge());
	        System.out.println("学生编号:" + xm.getNumber());
	        System.out.println("学生性别:" + xm.getSex());

	        System.out.println("作业处理完成");
	        System.out.println(z + "出现的次数为："+ z + "次");
	    }
	}


	class Student{
	    public Student(){

	    }
	    public Student(String name,int age,int number,String sex){
	        this.name = name;
	        this.age = age;
	        this.number = number;
	        this.sex = sex;
	    }

	    private String name;
	    private int age;
	    private int number;
	    private String sex;

	    public String getName() {
	        return name;
	    }
	    public int getAge() {
	        return age;
	    }
	    public String getSex() {
	        return sex;
	    }
	    public int getNumber() {
	        return number;
	    }
	    public void setName(String name) {
	        this.name = name;
	    }
	    public void setAge(int age) {
	        this.age = age;
	    }
	    public void setNumber(int number) {
	        this.number = number;
	    }
	    public void setSex(String sex) {
	        this.sex = sex;
	    }

	}

	class Homework{
	    public static StringBuffer HW(StringBuffer str1){
	        StringBuffer str2 = new StringBuffer(str1);
	        int j=0;int z;
	        for(int i = 7;i < str2.length()-45;i= i+7){
	            z = i +j;
	            if(i%2 == 0){
	                str2.insert(z,"。\n");
	                j = j+2;
	            }
	            else{
	                str2.insert(z,"，");
	                j= j+1;
	            }
	        }
	        System.out.println(str2);
	        return str2;
	    }

	}

	class Handle{
	    public static StringBuffer Read(){
	        String str1 = "";
	        StringBuffer str2 = new StringBuffer(str1);
	        try {
	            File file = new File("C:/Users/Desktop/许力元/B.txt");
	            FileReader fr = new FileReader(file);
	            BufferedReader bReader = new BufferedReader(fr);
	            while ((str1 =bReader.readLine()) != null) {
	                str2.append(str1);
	            }
	            fr.close();


	        } catch (IOException e) {
	            e.printStackTrace();
	        }
	        return  str2;
	    }

	    public static void Write(StringBuffer s){
	        try{
	            BufferedWriter bw = new BufferedWriter(new FileWriter("C:/Users/Desktop/许力元/A.txt"));
	            bw.write(s.toString());
	            bw.close();
	        }catch (IOException e){
	        }
	    }

	    public static int getCharMaps(String z,StringBuffer s) {
	        boolean p;
	        int w = 0;
	        String a = s.toString();
	        char[] b = a.toCharArray();
	        for (int i = 0; i < a.length(); i++) {
	            String x = String.valueOf(b[i]);
	            p = z.equals(x);
	            if(p == true){
	                w = w + 1;
	            }

	        }
	        return w;
	    }
	}
# 实验结果
研究生一 姓名张三 年龄:18 编号:2019310999999 性别:男 每年学费：4500 每月工资：1000.0 每年纳税为：480.0 




#  实验感悟
在此次JAVA实验中遇到了许许多多的困难，上次进行的实验测试，有些步骤已经忘记。
通过请教同学以及观看b站视频一步一步的摸索了出来，在编写程序上也遇到了很大的阻力，不过在我和同学的共同努力下一起完成了它。
接下来就是注册github账号以及上交内容，本来以为主体做完，这个应该不难了，没想到，这个想法是及其天真的，首先遇到的困难是保存的问题，
网站提示搜索自己的文件，却怎么也搜不到，最后找到了JAVA的路径复制粘贴找到了地方，总之JAVA此次实验对我来说是个很大的挑战，通过此次JAVA实验，我又跟进了一步，这就是我的全部感悟。
