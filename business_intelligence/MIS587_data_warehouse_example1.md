# MIS 587 Guide to Data Warehouse Creation using SSIS Package


(For more materials and examples, go to [shared link](https://drive.google.com/drive/folders/1Qr5WbOvNK3JHDyUwpoiNvETpJd482ZKB?usp=sharing))

[TOC]

### Overview:

In this exercise, we are going to build a data warehouse for the given data sample. We will be using SQL Server Integration Services tool to build a data warehouse. By the end of this exercise you should be able to design a data warehouse schema, implement the design using SSIS tool and perform analysis/ reporting using SSAS/ SSRS.

### Problem Statement: 

A physical warehouse near Tucson has inventory belonging to various categories which is shipped to many countries around the world by three shippers. A data warehouse needs to be built to maintain a single source of truth relating to the information about the goods shipped. They want to use this data to make business decisions.

### Solution:

* Analyze the data sample

* Design appropriate schema for data warehouse

* Build Data warehouse

* Design dashboards and reports to help Inventory/ Superstore make their business decisions (Out of Scope of this Lab session)

### Pre-requisite: 

Install SQL Server Express, SQL Server Management studio, SQL Server Data Tools, Visual Studio community   following the [Installation tutorial](https://github.com/liuhoward/teaching/blob/master/business_intelligence/Datawarehouse_Installation.md)





### Description step by step:

We will extract tables from [Northwind database](https://github.com/liuhoward/teaching/blob/master/business_intelligence/Northwind-Sample-Database-Diagram.pdf), import data into `Northwind_DW` database and build star schema.

1. Open Microsoft SQL server Management Studio.

![image-20210203101724743](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/image-20210203101724743.png)

2. Build Northwind database as data source:

click `New Query`, copy SQL code from the [link](https://raw.githubusercontent.com/liuhoward/teaching/master/business_intelligence/instnwnd.sql.txt), paste the code into query editor, click `Execute`, you will find a database `Northwind` in left sidebar. This contains Inventory source tables with data. Relevant attributes for each entity are present in the tables.

![2](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/2.PNG)                                

3. Build a database named `Northwind_DW` with empty tables for the `Northwind` Data warehouse using [sql code](https://raw.githubusercontent.com/liuhoward/teaching/master/business_intelligence/Northwind_DW_init.sql.txt) like previous step. Refresh database list, you will find a new database `Northwind_DW`.

![3](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/3.PNG)



Next, Microsoft Visual Studio will be used to load the data to the Northwind_DW data warehouse from the Northwind database, after doing certain transformations.

4. Open Microsoft Visual Studio. Choose `File-> New->Project`

![image-20210203103314861](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/image-20210203103314861.png)

![image-20210203103452589](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/image-20210203103452589.png)

5.  A window `New Project` pops up. Scroll down to the bottom and Choose `Integration Services Project`

![image-20210203121026959](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/image-20210203121026959.png)

![image-20210203103707271](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/image-20210203103707271.png)



6. You should get a blank screen as below:

![image-20210203104134864](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/image-20210203104134864.png)



Using Microsoft Visual Studio, Microsoft SQL server is accessed for the data integration of the Northwind Data warehouse.

7. From left sidebar, Drag and drop `Data Flow task` onto the workspace. Rename it as `Order Dimension`
![7](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/7.PNG)

8. Double Click on the `Order Dimension` data flow. You should see a page like below open.

![8](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/8.PNG)

9.  On the left-hand bar, Drag `OLE DB Source` from `Other Sources`  onto the workspace and drag `OLE DB Destinations` under `Other Destinations` onto the workspace. Join both using the blue arrow.

![9](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/9.PNG)

10. Double Click on the `OLE DB Source`. 

![1580890146985](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1580890146985.png)

11. Click `New` Button to create a new connection manager. This creates a new connection to a database installed on Microsoft SQL server.

![1580890186745](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1580890186745.png)

12. In the field `Server Name`, Type in the name of the Microsoft SQL Server installed on your computer. In SQL Sever Management Studio, the name to choose is shown by right click on your server name, choose `Properties`.

![Screenshot1](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/Screenshot1.png)

![10](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/10.PNG)

13. Next, under Select or enter a database name, choose `Northwind` Database. Click OK.

![11](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/11.PNG)

14. Now choose `Orders` table under `Name of the table or view`. Click OK.

![1580890791647](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1580890791647.png)


15.  In the Data Flow workspace, double click on the `OLE DB destination` and Create a connection manager to the Northwind_DW Database. Repeat Steps 11-13 to create a new connection manager similar to what was done for the Northwind database.

![1582066668981](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582066668981.png)


16. After the new connection manager has been set up, Choose `Dim Orders`. This is a dimension created to hold basic qualitative attributes about orders. Click `Mappings` (you has to click it once or errors would not disappear), then Choose OK. `Errors` of `OLE DB Source` and `OLE DB Destination` disappear. (`Keep identity`: [link1](https://docs.microsoft.com/en-us/sql/relational-databases/import-export/keep-identity-values-when-bulk-importing-data-sql-server?view=sql-server-ver15#keep_identity), [link2](http://bageshkumarbagi-msbi.blogspot.com/2019/09/keep-identity-option-in-oledb.html))

![1582066842117](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582066842117.png)

![1582066956388](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582066956388.png)


17. Repeat this procedure for `Supplier Dimension`, `Category Dimension`, `Shipper Dimension`, `Product Dimension`, `Employee Dimension`. Then join them as shown below:

![1582067614443](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582067614443.png)


18. The Inventory Fact table is loaded from the Inventory `order details` table. We already create an empty Fact table in `Northwind_DW`, foreign key placeholders are created, which will be populated later.

    Similarly, drag `Data Flow Task`, rename it as `Fact Table`, double click, Like before:

![1582067872939](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582067872939.png)

Drag the DB source from the left pane, select `Order Details` from Northwind database.

![1582068027442](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582068027442.png)

19. Next choose the Lookup task from the left pane under `common` and drag it into the workspace. Rename the lookup as `Time Lookup`. Join with `OLE DB source` using blue line.

![1582068242165](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582068242165.png)

20.  Click on the lookup icon. Click `Connection`, Choose the `Northwind_DW` connection manager. Choose `Use results of a SQL query`. And paste the query below.

```sql
Select do.OrderID, dt.[Time skey] 
from Dim_Time dt, [Dim Orders] do 
where do.OrderDate= dt.Date;
```

![1582071385129](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582071385129.png)

21. In the `columns` section of the editor, link `OrderID` (drag OrderID from left table to right table). Choose `Time Skey`. Click OK. 

 ![1582071450161](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582071450161.png)


22. Choose another lookup and drag it onto the workspace, rename it as `Order Lookup`. Connect time lookup blue to the order lookup, choose `lookup match output`

![1582069241560](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582069241560.png)

Double click on `Order Lookup` to open the editor. Choose `Northwind_DW` connection manager. Choose `Dim Orders` dimension. 

![1582069358609](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582069358609.png)

In `Columns` section of editor, link `OrderID`, choose `Order Skey`.

![1582086595545](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582086595545.png)

23. Choose another lookup and drag it onto the workspace, rename it as `Product Lookup`. Connect `Order Lookup` to `Product Lookup`. Double click on it to open the editor. Choose `Northwind_DW` connection manager. Choose `Dim Products` dimension. 

![1582069670763](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582069670763.png)

![1582086661830](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582086661830.png)



24. Similar to `Time Lookup`, use sql codes below to create lookups for employee, category, supplier, shipper.

`Employee Lookup`

```sql
Select do.OrderID, de.[Employee skey]
from [Dim Employees] de, [Dim Orders] do
where do.EmployeeID= de.EmployeeID;
```

![1582070077155](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070077155.png)

![1582070112779](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070112779.png)



`Category Lookup`

```sql
select dc.[Category Skey],dp.ProductID 
from [Dim Products] dp, [Dim Categories] dc
where dp.CategoryID=dc.CategoryID;
```

![1582070373940](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070373940.png)

![1582070407098](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070407098.png)

`Supplier Lookup`

```sql
select ds.[Supplier Skey],dp.ProductID 
from [Dim Products] dp, [Dim Suppliers] ds 
where dp.SupplierID=ds.SupplierID;
```

![1582070497760](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070497760.png)

![1582070517335](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070517335.png)

`Shipper Lookup`

```sql
Select do.OrderID, ds.[Shipper skey]
from [Dim Shippers] ds, [Dim Orders] do
where do.ShipVia= ds.ShipperID;
```

![1582070579650](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070579650.png)

![1582070606898](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070606898.png)

  So we have lookups for fact table:

![1582070661351](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070661351.png)

25. Drag `OLE DB destination`, double click, choose `Fact Order Details` from Northwind_DW: 

![1582072231804](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072231804.png)

![1582070833817](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582070833817.png)

The Foreign keys in the inventory fact table are populated from the dimension tables by matching the primary keys from their respective dimension tables.

![1582071812175](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582071812175.png)

![1582072231804](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072231804.png)

   

26. Truncate the data warehouse database tables:

Click the `Control Flow` tab. Drag `Execute SQL Task` task onto the design surface of the Data Flow tab. connect `Execute SQL task` to `Order Dimension`

![1582072972058](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072972058.png)

Right-click the task component and when click Edit. 

In General tab, Configure your SQL Connection to Northwind_DW

![1582072482373](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072482373.png)

 

Add the attached SQL query to truncate all tables next to `SQLStatement`. Click OKs.

```sql
TRUNCATE TABLE [Dim Categories];
TRUNCATE TABLE [Dim Employees];
TRUNCATE TABLE [Dim Orders];
TRUNCATE TABLE [Dim Products];
TRUNCATE TABLE [Dim Shippers];
TRUNCATE TABLE [Dim Suppliers];
TRUNCATE TABLE [Fact Order Details];
```

![1582072592908](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072592908.png)

![1582072642703](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072642703.png)

 

27. Go to control flow and click `start`. You should get a page like below:

![1582072839772](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582072839772.png)   

(you can stop it by clicking red square button)

![1582073179868](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582073179868.png)  

28. Go to Microsoft SQL server. The tables in the Northwind_DW database must have values now.

![Screenshot2](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/Screenshot2.png)

![1582073629870](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582073629870.png)



Done!

----------------------------------

## Screenshots for submission

**Note:** Put these screenshots in MS word and save it as pdf for submission. 

1. Results of successful execution in Visual Studio in Step 27 like the following (areas labeled in yellow must be included in your screenshot): 
![1582073888490](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582073888490.png)



2. Top rows of `Fact table` in `Northwind_DW` in step 28 (areas labeled in yellow must be included in your screenshot):

![1582073678934](https://github.com/liuhoward/teaching/raw/master/business_intelligence/dw_assets/1582073678934.png)