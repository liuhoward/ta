# MIS 587 Guide to Data Warehouse SSIS Installation



Please follow below steps to setup and install below software, make sure your hard drive has at least 20GB free space: 

(For MAC users, ask IT to install Windows 10 and perform below steps or borrow a windows laptop from UA library)


[TOC]

### 1. Visual Studio Community
Download Visual Studio Community 2019  from https://visualstudio.microsoft.com/vs/older-downloads/. Install the visual studio:

scroll down to select `Data storage and processing`, on your right side, select `SQL Server Data Tools` (If you already installed Visual Studio 2019, please refer this [link](https://blog.pragmaticworks.com/visual-studio-2019-bi-design-tool-extensions) to install the `SQL Server Data Tools`).

![image-20201224150827471](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224150827471.png)

![image-20201224151407958](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224151407958.png)

![image-20201224151629376](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224151629376.png)

![image-20201224153340398](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224153340398.png)




### 2. SQL Server Express
Download SQL Server Express 2019 from https://www.microsoft.com/en-us/sql-server/sql-server-downloads

Click on `Customize`. Follow the instructions to set up SQL Server. Make a note of Server Instance Name. Choose authentication as Windows Authentication 

![image-20201224154020869](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224154020869.png)

![image-20201224154119995](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224154119995.png)

![image-20201224154920149](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224154920149.png)

 

Click “New SQL Server stand-alone installation or add features …”

![image-20201224155107105](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224155107105.png)

![image-20201224164640780](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224164640780.png)



If have Windows Firewall warning, You can turn off firewall in control panel or enable the required ports following the link  

![image-20201224164946540](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224164946540.png)

![image-20201224165435335](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224165435335.png)

![image-20201224165608197](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224165608197.png)

![image-20201224165718958](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224165718958.png)

![image-20201224165751601](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224165751601.png)

**Remember the `Specify SQL Server administrators`**

![image-20201224165842330](D:\Downloads\teaching\business_intelligence\Datawarehouse_Installation.assets\image-20201224165842330.png)











![img](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/clip_image025.png)

 

**Attention:** if you encounter errors, you may check the service `windows modules installer` is running following the **[6. Note](#6. Note)** part in the end of this tutorial.

### 3.  SQL Server Management studio
Download SQL Server Management studio (latest version) from https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms

Click on `Download SQL Server Management Studio (SSMS)`

Execute the installation files 


![img](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/clip_image027.png)



 

### 4. After SQL Server Data Tools has been installed, open Visual Studio. 

After opening Visual Studio 2019, choose `File -> New -> Project`, from left sidebar, you should be able to find Installed -> Business Intelligence -> Integration Services, and create new project.

![img](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/clip_image031.png)

 

### 5. Open Microsoft SQL server Management Studio. 
Choose server type as Database Engine, Appropriate server name and authentication as Windows Authentication. Click Connect. You should get an object explorer window. On drilling down, you can see various folders, one of which is databases.

![img](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/clip_image033.png)

 

![img](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/clip_image035.png)

 

 

### 6. NOTE

1. For MAC users, ask IT to install Windows or borrow a Windows laptop from UA library and perform above steps 
3. If you are not able to find the instance name/ Server name to connect to database engine. Follow below steps: 

Navigate to: 

Start->All Program->Microsoft SQL Server-> Configuration Tools-> SQL Server Configuration Manager->SQL Server services 

Verify the name of server instance. Check the state of Server instance. It should be in running state

4. If you encounter error when you install SQL Server Express, please check the service `Windows module installer` is running as following:

* press `win + r`, input 'services.msc'

 ![1](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/1.PNG)

* find the service `Windows module installer` and double click

  ![2](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/2.PNG)

* make sure the `service status` is `running` or else click `start`.

  ![3](https://github.com/liuhoward/teaching/raw/master/business_intelligence/install_assets/3.PNG)

5. You can use the following or any other such video as a guide to install

https://www.youtube.com/watch?v=UcsItGq3mmM
