---
title: java的文件和时间操作
date: 2018-09-25 22:37:09
tags:
---
## File 类
### 构造函数有：  
	传入相对路径（一个参数）  
	传入绝对路径（一个参数）  
	File类指定为当前文件的父级，当前文件的名称（两个参数）  

## 文件删除读写改名

	File file = new File("hello.txt");//对于工程而言用相对路径，创建在根目录下。也可以用绝对路径指定文件夹  
	//File file = new File("bin/hello.txt");工程文件夹下的bin文件夹的hello.txt文件  
	//File file = new File("../hello.txt");工程文件夹的上一级文件中新建hello.txt文件  
	if(file.exists()){  
		System.out.printlen(file.isFile());//判断文件是文件  
		System.out.println(file.isDirectory());//判断文件是文件夹  
		File nameto = new File("new name .txt");  
		file.renameTo(nameto);//将file的名字改为nameti的名字  
		File nameto1 = new File("src/new name.txt");  
		file.renameTo(nameto1);//将文件移动到src目录下  
		file.delete();//删除文件  
	}else{  
		System.out.println("文件不存在");  
		try{  
			file.createNewFile();  
			System  
		}catch(IOException e){//抛出异常  
			e.printStackTrace();  
			System.out.println("文件无法创建");  
		}  
	}  


### 测试样例，用于文件的读取
新建一个test.txt文件，内容随意。

	File file = new File("text.txt");
	if(file.exitst()){
		try{
			FileInputStream fis = new FileInputStream(file);//属于字节流
			InputStreamReader isr = new InputStreamReader(fis. "UTF-8");//属于字符流，在字节转换为字符的时候，需要指定编码，否则可能会出现乱码。
			BufferedReader br = new BufferedReader(isr);//带有缓冲区的reader
			String line;//用于存放临时数据
			while ((line = br.readLine()) != null){
				System.out.println(line);//输出读取的一行
			}
			关闭输入流，先打开的后关闭，后打开的先关闭。
			br.close();
			isr.close();
			fis.close();
		}catch (FileNotFoundException e){
			该异常对应于 FileInputStream
		}catch (UnsupportedEncodingException e){
			该异常对应于 InputStreamReader
		}catch (IOException e){
			该异常对应于 ***.close()
		}
	}


### 测试样例，用于写入文件
	
	File newfile = new File("newtest.txt");
	try{
		FileOutPutStream fos = new FileOutputStream(newfile);
		OutPutStreamWriter osw = new OutPutStream(fos, "UTF-8");
		BufferedWriter bw = new BufferedWriter(osw);
		bw.write("你要写入的内容");
		。。。。。。。
		bw.close();
		osw.close();
		fos.close();
		//同样，先打开的后关闭，后打开的先关闭。
	}


## 文件夹操作

	File类可以表示文件或者文件夹，但是两者之间的是有区别的
	File folder = new File("my new folder");
	// folder.createNewFile()  使用该方法创建的是一个文件，只是文件没有后缀罢了
	folder.mkdir();//创建一个文件夹，返回值是一个bool类型，true为创建成功，false为失败
	//如果 已经存在 名为 “my new folder”的文件夹，则创建失败。也就是说不能出现同名的文件或者文件夹
`如果使用mkdir()，那么创建的文件夹必须是物理上存在的文件夹，也就是说，如果创建“one/two/test”这样的文件夹，但是 不存在one文件夹，那么是不会自动补全路径的。这时候我们就需要用 mkdirs()，也就是 file.mkdirs()这个语句。`

	//文件夹给名字的方法跟文件改名字的方法类似
	File folder = new File("my new folder");
	File newfolder = new File("new folder");
	folder.renameTo(newfolder);//返回的是一个bool类型的值，可以通过if判断是否修改成功
	//用这种方式修改文件夹的名字
	forlder.delete();//删除文件夹，但是只能删除空文件夹

`在windows中，千万注意移动文件夹不要跨盘移动，否则失败。因为Windows的文件系统是森林格式，而Linux和Mac系统是数状的`


## 一些判断获取语句
	
	File file = new File("test.txt");
	//判断文件是否存在
		file.exists();
	//读取文件名称
		file.getName();
	//读取文件相对路径
		file.getPath();
	//读取文件的绝对路径
		file.getAbsolutePath();
	//读取文件父级路径
		file.getParent();
	//读取文件大小（字节）
		file.length();
	//判断文件是否被隐藏（Linux和unix中，文件以 " . "开头代表隐藏）
		file.isHidden();
	//判断文件是否可读
		file.canRead();
	//判断文件是否可写
		file.canWrite();
	//判断文件是否为文件夹
		file.isDirectory();
	//当程序退出时将文件删除
		file.deleteOnExit();


## 设置文件属性：
	
	File file = new File("test.file");
	//设置为可写
		file.setWritable(true);//传入 true 则设置文件可写，否则设置为不可写
	//设置为可读
		file.setReadable(true);//与上述相同。
	//设置为只读
		file.setReadOnly();


## 遍历文件夹

	public static void printfFiles(File dir){
	{
		if( dir.isDirectory() ){
			File next[] = dir.listFiles();
			for( int i = 0; i<next.length; i++){
				if( next[i].ifFile() ){//输出文件的名字
					System.out.println(next[i].name);
				}else{//递归的输出文件的名字
					printfFiles(next[i]);
				}
			}
		}
	}


## 时间操作

Date表示时间，日期。但是更新jdk之后就不推荐使用了。  
官方解释是 使用Date类`不利于国际化`。所以jdk1.1版本后推荐使用Calendar类。使用DateFormat类进行时间日期的格式化。Long类型表示时间类型。String类型表示时间日期类的显示。 

	Date.getTime();//获取Date对象的时间  
	Date.setTime(long time);//设置Date的时间  

	Calendar rightnow = Calendar.getInstance();//获取当前时间  
	long now = System.currentTimeMillis();//获得系统的当前时间，但是这个时间只有机器能读懂

	Date d1 = new Date(now);// 获取人能够读懂的时间  
	Calendar c1 = Calendar .getInstance();  
	System.out.print(c1.getTime().toString());//获得人能够读懂的时间  

`String -> 时间  && 时间 -> String  `

	SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");//指定日期的格式  
	sdf.format(date);//将Date类型转换为指定格式的String类型，返回的是一个String类型  
	sdf.parse("2015-06-01");//将String转换为Date类型，返回的是一个Date类型  
	//SimpleDateFormat("yyyy-MM-dd hh:mm:ss"); 时间格式为 年月日  时分秒  

