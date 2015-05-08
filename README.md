# test
这是我的作业
该系统主要建立一个基于基本模式的图书馆登录系统,该系统类似二叉树，可以对跟系统的二个用户类型的使用实现:
1用户（User）登录
用户登录包含的是管理员和读者的登录信息，管理员和读者的信息内容都是调用用户类中的信息。
2读者（Reader）登录
读者登录包含的老师和学生的登录信息，登录时则是调用读者类中相关信息。
主要涉及六个类。
代码如下：
user类分为reader类和Manager类
reader类：
package books;

/**
 * 读者对象
 * @author cz
 *
 */
public class Reader extends User {

	public Reader(String userName) {
		super(userName);
	}
	
manager类:
package books;

public class Manager extends User{

	public Manager(String userName) {
		super(userName);
	}

	public String toString() {
		return "您好，尊敬的管理员: " + this.name+"你好";
	}
}

reader类又分为studet类和Teacher类。
studet类：package books;

public class Student extends Reader {
	
	public Student(String userName) {
		super(userName);
	}

	public String toString() {
		return "您好，尊敬的学生用户: " + this.name+"你好";
	}
}
Teacher类：
package books;

public class Teacher extends Reader {

	public Teacher(String userName) {
		super(userName);
	}
	
	public String toString() {
		return "您好，尊敬的老师用户: " + this.name+"你好";
	}
}
最后是一个测试类：
Test类：package books;

import java.io.BufferedReader;
import java.io.BufferedWriter;
import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class Test {
	
	static int count=0;
	static List<String> list = new ArrayList<String>();
	static BufferedReader br;
	
	
	public static void main(String[] args) {
		init();
		menu();

		System.out.println("请选择功能");
		//创建获取控制台信息的对象
		Scanner input = new Scanner(System.in);
		//从控制台中获取一个整数
		int select = input.nextInt();
		//对用户选择的功能进行识别
		switch (select) {
		case 0:
			userDenglu();break;
		case 1:
			System.out.println("抱歉，该功能还没有开发");break;
		case 2:
			System.out.println("抱歉，该功能还没有开发");break;
		case 3:
			System.exit(0);
			System.out.println("您已成功退出");
		}

	}

	public static void menu() {
		System.out.println("--------------------齐鲁工业大学图书管理系统-------------");
		System.out
				.println("|                         【0】用户登录                                     |");
		System.out
				.println("|                         【1】用户注册                                     |");
		System.out
				.println("|                         【2】信息查询                                     |");
		System.out
				.println("|                         【3】退出系统                                     |");
		System.out
				.println("----------------------------------------------------");
	}

	private static void init() {
		try {
			//创建一个文件缓冲流
			br = new BufferedReader(new FileReader(new File("E:/lvcaixia/book/src/userInfo")));
			String str = null;
			//如果文件不为空，就读入记录
			while ((str = br.readLine()) != null) {
				list.add(str);
			}
			br.close();
		} catch (Exception e) {
			e.printStackTrace();
		} 
	}

	public static boolean login(String name,String pw){
		boolean flag=false;
		for (int i = 0; i < list.size(); i++) {
			
			if(list.get(i).contains(name+" "+pw)){
				count=i;
				flag=true;
				break;
			}
		}
		return flag;
	}
	
	public static void userDenglu() {
		Scanner input = new Scanner(System.in);
		//提示用户输入用户名和密码
		System.out.print("请输入用户名：");
		String name=input.next();
		System.out.print("请输入密码");
		String password=input.next();
		//判断用户登录是否成功
		if (login(name, password)) {
			User s = null;
			//将对应记录存到str变量里
			String str=list.get(count);
			//对记录分割乘数组，确定身份,创建相应的子类赋给他们的父类
			if (str.split(" ")[2].equals("s")) {
				s=new Student(name);
			}else if(str.split(" ")[2].equals("t")){
				s=new Teacher(name);
			}else{
				s=new Manager(name);
			}
			System.out.println(s);
		} else {
			System.out.println("登录失败");
			userDenglu();
		}
	}

}

