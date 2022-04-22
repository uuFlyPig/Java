# **尚硅谷**-ja**va基础项目三总结**

## **一、项目概述**

##### **项目介绍：**    模拟实现一个基于文本界面的《开发团队调度软件》

**理论知识:**       此软件通过基础的java语法与面向对象编程的思想,包括的知识有:数组的灵活应用,数组                             的增删改查,面向对象的封装性,封装的对象和属性;面向对象的继承性,父类子类的继承,                                 方法的不断重写调用;面向对象的多态性,多个类实现同一个接口,实现软件功能的多样化,                        自定义异常,通过throws抛出异常,实现各种丰富的信息交互.

**需求说明：**     软件启动时，根据给定的数据创建公司部分成员列表（数组） 根据菜单提示，

​                        基于现有的公司成员，组建一个开发团队以开发一个新的项目 组建过程包括将成员插入 

​                        到团队中，或从团队中删除某成员，还可以列出团队中现有成员的列表 开发团队成员包

​                        括架构师、设计师和程序员                     



##### **需求图示：**

![img](F:\CodeNode/medley/resources/BJHAeZuf9_HJCxXb_zc.png)

------

![img](F:\CodeNode/medley/resources/BJHAeZuf9_BJ3nmWdz9.png)

------

![img](F:\CodeNode/medley/resources/BJHAeZuf9_H1_yEbOG9.png)

![img](F:\CodeNode/medley/resources/BJHAeZuf9_BkxfNZOM9.png)

![img](F:\CodeNode/medley/resources/BJHAeZuf9_SytMEZ_fc.png)

​	**小结：**

​				**通过文本界面的交互，用户可对软件进行操作，在原有团队的基础数据上，添加团队成员到					开发团队中去，同时可以展示开发团队的成员，但开发团队中最多有一名架构师等限制，最					终实现此文本交互软件。**

## 二、软件结构设计

##### 总体模块设计：以最常用的MVC模式（module， view，control）进行设计。

![img](F:\CodeNode/medley/resources/BJHAeZuf9_ry7SI-_fq.png)

​    

- uu_fly_pig.team.view 模块为主控模块，负责菜单的显示和处理用户操作。
- uu_fly_pig.team.servie 模块为实体对象（Employee及其子类等）的管理模块。其中类                                         NameistService用数组管理公司原有员工，类TeamService管理开发团队。
- uu_fly_pig.team.domain 模块提供Employee及其子类等JavaBean类所在的包。

##### 软件模块详细设计

uu_fly_pig.team.domain 模块：员工信息中包括名字，年龄等个人信息以及所使用的设备信息，此                                                       														包下创建一个父类Employee，程序员、设计师以及架构师继承父类，														同时创建设备接口Equipment，将各类设备PC、Print等实现接口。

![img](F:\CodeNode/medley/resources/BJHAeZuf9_BJJfqZ_zq.png)

- uu_fly_pig.team.service 模块：公司中，原有团队成员，创建Data类存储员工个人信息以及设备信 息，并创建Status类记录员工的													个人状态，记录是否加入开发团队中。此包下创建TeamException类，自定义异常，保证成功实现在													添加和删除开发团队时的各种异常情况处理，创建NameListService 将员工的信息实现在数组中，													并给出操作方法。类TeamService实 现对开发团队的添加、删除等操作。

![img](F:\CodeNode/medley/resources/BJHAeZuf9_rJZk2-uzq.png)

- uu_fly_pig.team.view 模块：此包下提供了TSUtility类，将控制台的交互功能封装，供TeamView类                                                 													调用实现软件界面的展示，实现最终的软件形势。

![img](F:\CodeNode/medley/resources/BJHAeZuf9_HkEOp-dGq.png)

## 三、各包下各类的详细实现（源码—文末）

### 1、uu_fly_pig.team.domain 模块：

- 类Employee : id（员工id）、name（员工姓名）、age（年龄）、salary（薪水）、构造方法							Employee（）、toString方法返回信息；



- 类Programmer（继承父类Employee实现接口Equipment）：
  - memberId （用来记录成员加入开发团队后在团队中的ID ）
  - Status（是项目service包下自定义的类，声明三个对象属性，分别表示成员的状态。）
  - FREE-空闲
  - BUSY-已加入开发团队
  - VOCATION-正在休假
  - equipment（表示该成员领用的设备 ）
  - toString方法返回信息
  - getDescription（）重写接口方法返回程序员设备信息。



- 类Desiner（继承父类Programmer）：
  - bonus（表示奖金）
  - toString方法返回信息。



- 类Archite（继承父类Desiner）：
  - stock（表示股票）
  - toString方法返回信息



- 接口Equipment：创建一个抽象方法getDescription（）返回设备信息，供子类重写。



- 类Pc（实现接口Equipment）：
  - model（表示机器型号）
  - display（表示显示器的型号）
  - 构造方法。



- 类NoteBook（实现接口Equipment）：
  - model（表示机器型号）
  - price（表示价格）
  - 构造方法。



- 类Print（实现接口Equipment）：
  - name（表示机器名字）
  - type（表示打印机的类型）
  - 构造方法。

### 2、uu_fly_pig.team.service 模块：

- 类Data（存储团队员工信息，其中以数字编号区分代表）



- 类Status(记录员工状态的一个类,包含 FREE \ VOCATION \ BUSY三个状态)



- 类NameListService (负责将Data中的数据封装到Employee[]数组中，同时提供相关操作Employee[]的方法  )

  - employees(用来保存公司所有员工对象 )

  - 构造函数:初始化员工信息,将员工的基本信息通过二维数组存储.

  - createEquipment方法:获取指定index上的员工设备,传入指定index,返回所指定index上员工所使用的设备信息(返回值类型为Equipmen).

  - getAllEmpolyees:获取当前所有员工,返回Employee[]实例对象employees

  - getEmployee:获取指定ID的员工对象,输入员工id返回此员工的对象emploee[id].



- 类TeamService(关于开发团队成员的管理：添加、删除等)
  - counter为静态变量，用来为开发团队新增成员自动生成团队中的唯一ID，即memberId。（提示：应使用增1的方式）
  - MAX_MEMBER：表示开发团队最大成员数 team数组：用来保存当前团队中的各成员对象 
  - total：记录团队成员的实际人数
  - getTeam函数:(获取整个开发团队的成员对象数组)方法中,new一个新的数组,将开发团队的数组赋值到新的数组中,保证返回的开发团队成员对象数组没有多余空出的内存.
  - addMember函数:(将指定员工添加到团队中)通过判断团队成员数是否满,以及该成员是否开发人员等条件,满足就将该成员添加到团队中.
  - isExist:判断指定的员工是否已经存再现有的开发团队中.返回boolean类型值
  - removeMember方法:(从团队中删除成员)判断是否在成员团队中找到该成员,利用后一个覆盖前一个实现删除操作



- 类TeamException:(提供自定义异常类,给其他类操作,捕获异常)

###  

### 3、uu_fly_pig.team.view模块：

- TSUtility类:(项目中提供了TSUtility.java类，可用来方便地实现键盘访问。)
  - readMenuSelection方法:(该方法读取键盘，如果用户键入’1’-’4’中的任意字符，则方法返回。返回值为用户键入字符。)
  - readReturn方法:(该方法提示并等待，直到用户按回车键后返回。)
  - readInt方法:(该方法从键盘读取一个长度不超过2位的整数，并将其作为方法的返回值。)
  - readConfirmSelection方法:(从键盘读取‘Y’或’N’，并将其作为方法的返回值。)
  - readKeyBoard方法:(判断用户从键盘输入的字符是否超过长度限制,返回一个String提醒)




- TeamView类:(mian方法主程序,实现显示页面和功能调用)
  - NameListService listSvc = new NameListService();
  - TeamService teamSvc = new TeamService();(实例化对象,供后续调用)
  - enterMainMenu函数(团队调度软件的菜单页面)
  - listAllEmployees函数(显示所有员工信息,利用制表符展示)
  - getTeam方法:(获取开发团队中成员信息,如果还没添加输出开发团队暂没有成员)
  - addMember方法:(添加开发团队成员,view页面交互添加成员)
  - deleteMember方法:(删除开发团队成员,view页面交互删除成员)
  - main方法:(程序的入口,实例化TeamView类,调用enterMainMenu方法)

## 四、成果展示

![img](F:\CodeNode/medley/resources/BJHAeZuf9_ry8qTNgmc.png)

![img](F:\CodeNode/medley/resources/BJHAeZuf9_H1RsTVxXq.png)

![img](F:\CodeNode/medley/resources/BJHAeZuf9_rkCkR4g7q.png)

# 五、项目源码

### 1、uu_fly_pig.team.domain 模块：

- 类Employee : 



```java
package uu_fly_pig.team.domain;

public class Employee {
	private int id;
	private String name;
	private int age;
	private double salary;

	public Employee(int id, String name, int age, double salary) {
		super();
		this.id = id;
		this.name = name;
		this.age = age;
		this.salary = salary;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public double getSalary() {
		return salary;
	}

	public void setSalary(double salary) {
		this.salary = salary;
	}

	public Employee() {
		super();
	}
	
	public String getDetails() {
		return id + "\t" + name + "\t" + age + "\t" + salary;
	}
	
	
	@Override
	public String toString() {
		
		return getDetails();
	}
}
```

- 类Programmer（继承父类Employee实现接口Equipment）：



```java
package uu_fly_pig.team.domain;

import uu_fly_pig.team.service.Status;

public class Programmer extends Employee implements Equipment{

	
	private int memberId;
	
	private Status status = Status.FREE;
	
	private Equipment equipment;

	public Programmer(int id, String name, int age, double salary,Equipment equipment) {
		super(id, name, age, salary);
		this.equipment = equipment;
	}

	public int getMemberId() {
		return memberId;
	}

	public void setMemberId(int memberId) {
		this.memberId = memberId;
	}

	public Status getStatus() {
		return status;
	}

	public void setStatus(Status status) {
		this.status = status;
	}

	public Equipment getEquipment() {
		return equipment;
	}

	public Programmer() {
		super();
	}

	public void setEquipment(Equipment equipment) {
		this.equipment = equipment;
	}

	public  void getFree() {

	}

	@Override
	public String getDescription() {
		return status + "\t" + equipment;
	}
	@Override
	public String toString() {
		
		return super.toString() + "\t程序员\t" + status + "\t\t\t" + equipment.getDescription();
	}
	public String getBaseDetailsForTeam() {
		return memberId + "/" + getId() + "\t" + getName() + "\t" + getAge() + "\t" + getAge() + "\t" + getSalary();
	}

	public String getDetailsForTeam() {
		return getBaseDetailsForTeam() + "\t程序员";
	}
}

```

- 类Desiner（继承父类Programmer）：



```java
package uu_fly_pig.team.domain;

public class Designer extends Programmer {
	private double bonus;

	public Designer(int id, String name, int age, double salary, Equipment equipment, double bonus) {
		super(id, name, age, salary, equipment);
		this.bonus = bonus;

	}

	public Designer() {
		super();
	}

	public double getBonus() {
		return bonus;
	}

	public void setBouns(double bouns) {
		this.bonus = bonus;
	}

	public String getDescription() {
		return super.getDescription() + "\t" + bonus;
	}
	
	
	@Override
	public String toString() {
		
		return getDetails() + "\t设计师\t" + getStatus() + "\t" + bonus + "\t\t" + getEquipment().getDescription();
	}

	public String getDetailsForTeam() {
		return getBaseDetailsForTeam() + "\t设计师" + bonus;
	}
}

```

- 类Archite（继承父类Desiner）：



```java
package uu_fly_pig.team.domain;

public class Architect extends Designer {
	private int stock;

	public Architect(int id, String name, int age, double salary, Equipment equipment, double bouns, int stock) {
		super(id, name, age, salary, equipment, bouns);
		this.stock = stock;
	}

	public int getStock() {
		return stock;
	}

	public void setStock(int stock) {
		this.stock = stock;
	}

	public Architect() {
		super();
	}

	public String getDescription() {
		return super.getDescription();
	}

	
	public String toString() {
		
		return getDetails() + "\t架构师\t" + getStatus() + "\t" + getBonus() + "\t" + stock +"\t" +  getEquipment().getDescription();
	}
	
	public String getDetailsForTeam() {
		return getBaseDetailsForTeam() + "\t架构师" + getBonus() + "\t" + getStock();
	}
}

```

- 接口Equipment：



```java
package uu_fly_pig.team.domain;

public interface Equipment {
	
	String getDescription();
	
}

```

- 类Pc（实现接口Equipment）：



```java
package uu_fly_pig.team.domain;

public class PC implements Equipment {
	private String model; // 机器型号
	private String display; // 显示器名称

	public PC() {
		super();
	}

	public String getModel() {
		return model;
	}

	public PC(String model, String display) {
		super();
		this.model = model;
		this.display = display;
	}

	public void setModel(String model) {
		this.model = model;
	}

	public String getDisplay() {
		return display;
	}

	public void setDisplay(String display) {
		this.display = display;
	}

	@Override
	public String getDescription() {
		return model + "(" + display + ")";
	}

}

```

- 类NoteBook（实现接口Equipment）：



```java
package uu_fly_pig.team.domain;

public class NoteBook implements Equipment {
	private String model;// 机器型号
	private double price;// 价格

	@Override
	public String getDescription() {
		return model + "(" + price + ")";
	}

	public NoteBook() {
		super();
	}

	public String getModel() {
		return model;
	}

	public void setModel(String model) {
		this.model = model;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}

	public NoteBook(String model, double price) {
		super();
		this.model = model;
		this.price = price;
	}

}

```

- 类Print（实现接口Equipment）：



```java
package uu_fly_pig.team.domain;

public class Printer implements Equipment {
	private String name;// 机器型号
	private String type;// 机器类型

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getType() {
		return type;
	}

	public void setType(String type) {
		this.type = type;
	}

	public Printer(String name, String type) {
		super();
		this.name = name;
		this.type = type;
	}

	public Printer() {
		super();
	}

	@Override
	public String getDescription() {
		return name + "(" + type + ")";
	}

}

```

### 2、uu_fly_pig.team.service 模块：

- 类Data



```java
package uu_fly_pig.team.service;


public class Data {
    public static final int EMPLOYEE = 10;
    public static final int PROGRAMMER = 11;
    public static final int DESIGNER = 12;
    public static final int ARCHITECT = 13;

    public static final int PC = 21;
    public static final int NOTEBOOK = 22;
    public static final int PRINTER = 23;

    //Employee  :  10, id, name, age, salary
    //Programmer:  11, id, name, age, salary
    //Designer  :  12, id, name, age, salary, bonus
    //Architect :  13, id, name, age, salary, bonus, stock
    public static final String[][] EMPLOYEES = {
        {"10", "1", "马云", "22", "3000"},
        {"13", "2", "马化腾", "32", "18000", "15000", "2000"},
        {"11", "3", "李彦宏", "23", "7000"},
        {"11", "4", "刘强东", "24", "7300"},
        {"12", "5", "雷军", "28", "10000", "5000"},
        {"11", "6", "任志强", "22", "6800"},
        {"12", "7", "柳传志", "29", "10800","5200"},
        {"13", "8", "杨元庆", "30", "19800", "15000", "2500"},
        {"12", "9", "史玉柱", "26", "9800", "5500"},
        {"11", "10", "丁磊", "21", "6600"},
        {"11", "11", "张朝阳", "25", "7100"},
        {"12", "12", "杨致远", "27", "9600", "4800"}
    };
    
    //如下的EQUIPMENTS数组与上面的EMPLOYEES数组元素一一对应
    //PC      :21, model, display
    //NoteBook:22, model, price
    //Printer :23, name, type 
    public static final String[][] EQUIPMENTS = {
        {},
        {"22", "联想T4", "6000"},
        {"21", "戴尔", "NEC17寸"},
        {"21", "戴尔", "三星 17寸"},
        {"23", "佳能 2900", "激光"},
        {"21", "华硕", "三星 17寸"},
        {"21", "华硕", "三星 17寸"},
        {"23", "爱普生20K", "针式"},
        {"22", "惠普m6", "5800"},
        {"21", "戴尔", "NEC 17寸"},
        {"21", "华硕","三星 17寸"},
        {"22", "惠普m6", "5800"}
    };
}

```

- 类Status:



```java
package uu_fly_pig.team.service;

public class Status {
	private final String NAME;

	private Status(String name) {
		this.NAME = name;
	}

	public static final Status FREE = new Status("FREE");
	public static final Status VOCATION = new Status("VOCATION");
	public static final Status BUSY = new Status("BUSY");

	public String getNAME() {
		return NAME;
	}

	@Override
	public String toString() {
		return NAME;
	}
}

```

- 类NameListService 



```java
package uu_fly_pig.team.service;

import uu_fly_pig.team.domain.Architect;
import uu_fly_pig.team.domain.Designer;
import uu_fly_pig.team.domain.Employee;
import uu_fly_pig.team.domain.Equipment;
import uu_fly_pig.team.domain.NoteBook;
import uu_fly_pig.team.domain.PC;
import uu_fly_pig.team.domain.Printer;
import uu_fly_pig.team.domain.Programmer;

import static uu_fly_pig.team.service.Data.*;
/**
 * @Description 负责将Data中的数据封装到Employee[]数组中，同时提供相关操作Employee[]的方法。
 * @author lp
 * @vison
 * @date2022年3月21日
 */
public class NameListService {
	private Employee[] employees;

	//给employees及数组元素进行初始化
	public NameListService() {
//		根据项目提供的Data类构建相应大小的employees数组
//		再根据Data类中的数据构建不同的对象，包括Employee、Programmer、Designer和Architect对象，以及相关联的Equipment子类的对象
//		将对象存于数组中
		employees = new Employee[EMPLOYEES.length];
		
		for(int i = 0;i< employees.length;i++) {
			int type = Integer.parseInt(EMPLOYEES[i][0]);
			
			//获取Employee个的基本信息的
			int id = Integer.parseInt(EMPLOYEES[i][1]);
			String name = EMPLOYEES[i][2];
			int age = Integer.parseInt(EMPLOYEES[i][3]);
			double salary = Double.parseDouble(EMPLOYEES[i][4]);
			
			Equipment equipment;
			double bouns;
			int stock;
			
			switch(type) {
			case EMPLOYEE:
				employees[i] = new Employee(id, name, age, salary);
				break;
			case PROGRAMMER:
				equipment = createEquipment(i);
				
				employees[i] = new Programmer(id, name, age, salary, equipment);
				break;
			case DESIGNER:
				equipment = createEquipment(i);
				bouns = Double.parseDouble(EMPLOYEES[i][5]);
				employees[i] = new Designer(id, name, age, salary, equipment, bouns);
				break;
			case ARCHITECT:
				equipment = createEquipment(i);
				bouns = Double.parseDouble(EMPLOYEES[i][5]);
				stock = Integer.parseInt(EMPLOYEES[i][6]);
				employees[i] = new Architect(id, name, age, salary, equipment, salary, stock);
				break;
			}
		
		}
		
	}
	
	/**
	 * 获取指定index上的员工设备。
	 * @param i
	 * @return
	 */
	private Equipment createEquipment(int index) {
		int type = Integer.parseInt(EQUIPMENTS[index][0]);
		String model = EQUIPMENTS[index][1];
		
		switch(type) {
		case PC://21
			String display = EQUIPMENTS[index][2];
			return new PC(EQUIPMENTS[index][1], EQUIPMENTS[index][2]);
	
		case NOTEBOOK:
			//22
			double price = Double.parseDouble(EQUIPMENTS[index][2]);
			return new NoteBook(model, price);
			
		case PRINTER:
			//23
			String name = EQUIPMENTS[index][1];
			String type_p = EQUIPMENTS[index][2];
			return new Printer(name, type_p);
		}
		
		return null;
	}
	/**
	 * 获取当前所有员工。
	 * @return
	 */
	public Employee[] getAllEmployees() {
		return employees;
	}
	
	/**
	 * 获取指定ID的员工对象。
	 * @param id
	 * @return
	 * @throws TeamException
	 */
	public Employee getEmployee(int id) throws TeamException{
		
		for(int i = 0; i<employees.length;i++) {
			if(employees[i].getId() == id) {
				return employees[i];
			}
		}
		throw new TeamException("找不到指定员工！");
	}
}

```

- 类TeamService



```java
package uu_fly_pig.team.service;

import uu_fly_pig.team.domain.Architect;
import uu_fly_pig.team.domain.Designer;
import uu_fly_pig.team.domain.Employee;
import uu_fly_pig.team.domain.Programmer;

/**
 * @Description 关于开发团队成员的管理：添加、删除等
 * @author lp
 * @vison
 * @date2022年3月22日
 */
public class TeamService {
	private int counter = 1;	//开发团队中的成员ID
	private final int MAX_MEMBER = 5;	//表示开发团队最大成员数
	private Programmer[] team = new Programmer[MAX_MEMBER];	//保存当前团队中的各成员数
	private int total;	//记录团队成员的实际人数。
	
	public TeamService() {
		super();
	}
	/**
	 * 
	 * 获取整个开发团队的成员对象数组
	 * @return
	 */
	public Programmer[] getTeam() {
		Programmer[] team_ = new Programmer[total];
		for(int i = 0;i < total; i++) {
			team_[i] = team[i];
		}
		return team_;
	}
	/**
	 * 将指定员工添加到团队中
	 * @param e
	 * @throws TeamException
	 */
	public void addMember(Employee e) throws TeamException{
//		成员已满，无法添加
		if(total >= MAX_MEMBER) {
			throw new TeamException("团队已满！");
		}
//		该成员不是开发人员，无法添加
		if(!(e instanceof Programmer)) {
			throw new TeamException("该成员不是开发人员，无法添加");
		}
//		该员工已在本开发团队中
		if(isExist(e)) {
			throw new TeamException("该员工已在本开发团队中");
		}
//		该员工已是某团队成员 
		
//		该员正在休假，无法添加
		
		Programmer p = (Programmer)e; //一定不会出现错误，强转成功
//		if(p.getStatus().getNAME().equals("BUSY")) {
		if("BUSY".equals(p.getStatus().getNAME())) {
			throw new TeamException("该员工已是某团队成员 ");
		}else if("VOCATION".equals(p.getStatus().getNAME())) {
			throw new TeamException("该员正在休假，无法添加");
		}
//		团队中至多只能有一名架构师
//		团队中至多只能有两名设计师
//		团队中至多只能有三名程序员

		//获取team已有成员中架构师、设计师、程序员的人数
		int numofArch = 0,numofDes = 0,numofPro = 0;
		for(int i = 0;i<total;i++) {
			if(team[i] instanceof Architect) {
				numofArch++;
			}else if(team[i] instanceof Designer) {
				numofDes++;
			}else if(team[i] instanceof Programmer) {
				numofPro++;
			}
		}
		
		if(p instanceof Architect) {
			if(numofArch >= 1) {
				throw new TeamException("团队中至多只能有一名架构师");
			}
		}else if(p instanceof Designer) {
			if(numofDes >=2) {
				throw new TeamException("团队中至多只能有两名设计师");
			}
		}else if(p instanceof Programmer) {
			if(numofPro >=3) {
				throw new TeamException("团队中至多只能有三名程序员");
			}
		}
		
		//将e添加到现有team中
		team[total++] = p;
		//p的属性复制
		p.setStatus(Status.BUSY);
		p.setMemberId(counter++);
		
		
	}
	
	/**
	 * 判断指定的员工是否已经存在于现有的开发团队中
	 * @param e
	 * @return
	 */
	private boolean isExist(Employee e) {
		for(int i = 0;i < total;i++) {
			if(team[i].getId() == e.getId()) {
				return true;
			}
		}
		
		return false;
	}
	/**
	 * 从团队中删除成员
	 * @param memberId
	 * @throws TeamException 
	 */
	public void removeMember(int memberId) throws TeamException {
		int i=0;
		for(;i<total;i++) {
			if(team[i].getMemberId() == memberId) {
				team[i].setStatus(Status.FREE);
				break;
			}
		}
		
		//未找到指定Memberid的情况
		if(i == total) {
			throw new TeamException("找不到指定memberId的员工，删除失败");
		}
		
		
		//后面一个元素覆盖前一个，实现删除操作
		for(int j = i+1;j<total;j++) {
			team[j-1] = team[j];
		}
		team[--total] = null;
		
		
	}
}

```

- 类TeamException:



```java
package uu_fly_pig.team.service;

public class TeamException extends Exception{

	// 提供序列号
	static final long serialVersionUID = -3387994455482020L;

//		提供重载构造器
	public TeamException() {
			
		}

	public TeamException(String msg) {
			super(msg);
		}

}

```

###  

### 3、uu_fly_pig.team.view模块：

- TSUtility类:(项目中提供了TSUtility.java类，可用来方便地实现键盘访问。)



```java
package uu_fly_pig.team.view;

import java.util.*;
/**
 * 
 * @Description 项目中提供了TSUtility.java类，可用来方便地实现键盘访问。
 * 
 * @version 
 * @date 2019年2月12日上午12:02:58
 *
 */
public class TSUtility {
    private static Scanner scanner = new Scanner(System.in);
    /**
     * 
     * @Description 该方法读取键盘，如果用户键入’1’-’4’中的任意字符，则方法返回。返回值为用户键入字符。
     * 

     * @return
     */
	public static char readMenuSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false);
            c = str.charAt(0);
            if (c != '1' && c != '2' &&
                c != '3' && c != '4') {
                System.out.print("选择错误，请重新输入：");
            } else break;
        }
        return c;
    }
	/**
	 * 
	 * @Description 该方法提示并等待，直到用户按回车键后返回。


	 */
    public static void readReturn() {
        System.out.print("按回车键继续...");
        readKeyBoard(100, true);
    }
    /**
     * 
     * @Description 该方法从键盘读取一个长度不超过2位的整数，并将其作为方法的返回值。

     */
    public static int readInt() {
        int n;
        for (; ; ) {
            String str = readKeyBoard(2, false);
            try {
                n = Integer.parseInt(str);
                break;
            } catch (NumberFormatException e) {
                System.out.print("数字输入错误，请重新输入：");
            }
        }
        return n;
    }
    /**
     * 
     * @Description 从键盘读取‘Y’或’N’，并将其作为方法的返回值。

     * @return
     */
    public static char readConfirmSelection() {
        char c;
        for (; ; ) {
            String str = readKeyBoard(1, false).toUpperCase();
            c = str.charAt(0);
            if (c == 'Y' || c == 'N') {
                break;
            } else {
                System.out.print("选择错误，请重新输入：");
            }
        }
        return c;
    }

    private static String readKeyBoard(int limit, boolean blankReturn) {
        String line = "";

        while (scanner.hasNextLine()) {
            line = scanner.nextLine();
            if (line.length() == 0) {
                if (blankReturn) return line;
                else continue;
            }

            if (line.length() < 1 || line.length() > limit) {
                System.out.print("输入长度（不大于" + limit + "）错误，请重新输入：");
                continue;
            }
            break;
        }

        return line;
    }
}


```

- TeamView类:



```java
/**
 * 
 */
package uu_fly_pig.team.view;

import uu_fly_pig.team.domain.Employee;
import uu_fly_pig.team.domain.Programmer;
import uu_fly_pig.team.service.NameListService;
import uu_fly_pig.team.service.Status;
import uu_fly_pig.team.service.TeamException;
import uu_fly_pig.team.service.TeamService;

/**
 * @Description
 * @author lp
 * @vison
 * @date2022年3月22日
 */
public class TeamView {
	private NameListService listSvc = new NameListService();
	private TeamService teamSvc = new TeamService();

	public void enterMainMenu() {

		boolean loopFlag = true;
		char menu = 0;

		while (loopFlag) {
			if (menu != '1') {
				listAllEmployees();
			}

			System.out.print("1-团队列表  2-添加团队成员  3-删除团队成员 4-退出   请选择(1-4)：");

			menu = TSUtility.readMenuSelection();
			switch (menu) {
			case '1':
				getTeam();
				break;
			case '2':
				addMember();
				break;
			case '3':
				deleteMember();
				break;
			case '4':
				System.out.print("确认是否退出(Y/N)：");
				char isExit = TSUtility.readConfirmSelection();
				if (isExit == 'Y') {
					loopFlag = false;
				}
				break;
			}
		}
	}

	/**
	 * 显示所有的员工信息
	 */
	private void listAllEmployees() {
		System.out.println("-------------------------------开发团队调度软件--------------------------------\n");

		Employee[] employees = listSvc.getAllEmployees();
		if (employees == null || employees.length == 0) {
			System.out.println("公司没有任何员工信息");
			System.out.println("--------------------------------------------------------------");
		} else {
			System.out.println("ID\t姓名\t年龄\t工资\t职位\t状态\t奖金\t股票\t领用设备");
			// for(Employee emp: employees){
//					System.out.println(emp);
			for (int i = 0; i < employees.length; i++) {
				System.out.println(employees[i]);
			}
			System.out.println("--------------------------------------------------------------");
		}

	}

	// 获取团队成员列表
	private void getTeam() {

		System.out.println("--------------------团队成员列表---------------------");

		Programmer[] team = teamSvc.getTeam();

		if (team.length == 0) {
			System.out.println("开发团队目前没有成员！");
		} else {
			System.out.println("TDI/ID\t姓名\t年龄\t工资\t职位\t奖金\t股票");
			for (int i = 0; i < team.length; i++) {
				System.out.println(team[i].getDetailsForTeam());
			}
		}

		System.out.println("-----------------------------------------------------");
	}

	// 添加成员
	private void addMember() {
		System.out.println("---------------------添加成员---------------------");
		System.out.print("请输入要添加的员工ID：");
		int id = TSUtility.readInt();

		try {
			Employee emp = listSvc.getEmployee(id);
			teamSvc.addMember(emp);
			System.out.println("添加成功");
			// 按回车键继续...
			TSUtility.readReturn();
		} catch (TeamException e) {
			System.out.println("添加失败。失败的原因：" + e.getMessage());
		}

	}

	// 删除成员
	private void deleteMember() {
		System.out.println("---------------------删除成员---------------------");
		System.out.print("请输入要删除员工的TID：");
		int memberId = TSUtility.readInt();
		System.out.print("确认是否删除(Y/N)：");
		char isDelete = TSUtility.readConfirmSelection();
		if (isDelete == 'N') {
			return;
		}

		if (isDelete == 'Y') {
			try {
				teamSvc.removeMember(memberId);
				System.out.println("删除成功");

			} catch (TeamException e) {
				System.out.println("删除失败，失败原因：" + e.getMessage());
			}
			// 按回车键继续...
			TSUtility.readReturn();
		}

	}

	public static void main(String[] args) {
		TeamView view = new TeamView();
		view.enterMainMenu();

	}
}

```