---
id: 376
title: Working with the Object Data Source
date: 2006-11-25T13:33:32+00:00
author: Hibri Marzook
layout: post
guid: http://www.hibri.net/2006/11/25/WorkingWithTheObjectDataSource.aspx
permalink: /2006/11/25/working-with-the-object-data-source/
categories:
  - .Net Data
  - .Net Web
---
[The Object Data Source (ODS)](http://msdn2.microsoft.com/en-us/library/9a4kyhcx.aspx) helps you expose your business objects, to provide data to databound controls&nbsp;such as&nbsp;the GridView, DetailsView and many other data bound controls.

Compared to the other data sources like the DataTable and DataSet, the ODS does require some work to achieve the same functionality. The main advantage of the ODS is that it allows you to maintain your layers, without polluting your presentation layer with data code.

To start off,&nbsp; drag and drop the ODS control to a web form. Set the TypeName property to the business object you want to work with. For example, if we have a&nbsp;BO named Employees in the TimeTracker namespace, this will be&nbsp;TimeTracker.Employee.

**Selecting**  
&nbsp;A common scenario is to display the a list of records. Say we want to display the list of all employees in a GridView. To retrieve the records, the Employee object needs a GetEmployees static method that will retrieve&nbsp; all the employees from the DB.&nbsp; Set the [SelectMethod](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.selectmethod.aspx) property of the ODS to GetEmployees. Now bind the ODS to the GridView just like any other data source.

At runtime the ODS uses reflection to find the GetEmployees method and invokes it.

**Paging and filtering**

Filtering Employee objects is as easy as adding a new method to your Employee object. If we want to select Employees by department, the Employee object should have a static&nbsp;method 

GetEmployees(string department)

In the properties window of the ODS, add the department parameter to the [SelectParameters](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.selectparameters.aspx) collection. You can set a default value to it, and this is where things get real easy. You can bind the parameter to a control on your web form ( like a DropDownList)&nbsp;, a Session variable and even a query string parameter.&nbsp; Adding&nbsp; filtering functionality is simple as that. You can do the same programmatically by adding Parameters to the SelectParameters collection. Be sure to clear the collection before you add a parameter( or check if the parameter exists).

Paging is where working with the ODS gets a bit complicated. To enable paging ( in conjunction with the GridView) set the EnablePaging property to true. The Employee object too, needs to have methods to support paging. 

When paging is enabled, the ODS calls the GetEmployee method with&nbsp;two extra parameters. by default the parameters are **startRowIndex** and **maximumRows**. These can be changed by setting the [StartRowIndexParameterName](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.startrowindexparametername.aspx) and [MaximumRowsParameterName](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.maximumrowsparametername.aspx) properties.

Now we need a GetEmployees method with the signature like  
GetEmployees(int startRowIndex,int maxiumRows)  
To support filtering it will have to be GetEmployees(string department ,int startRowIndex,int maxiumRows)

The maximumRows parameter, will have the value of how many rows to display per page. This will have the value of the PageSize property of the GridView. The startRowIndex will contain the the index of the current page. This can be the starting row index of the current page of records. See [here for more on how to pass these on to an SQL query](http://weblogs.asp.net/scottgu/archive/2006/01/07/434787.aspx). 

In addition to this the ODS needs another method that is set by the [SelectCountMethod](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.selectcountmethod.aspx) property. This is invoked to find out the total number of rows available. So we need another static method in our Employee object. GetEmployeesCount() .If the total number of rows is 100, and you have a page size of 20. The GetEmployees count method should return 100, so that the ODS can tell the GridView, how many pager links to display. I usually return this as an out parameter from the stored procedure that retrieves the paged results.

**Inserting, Editing and Deleting** 

Inserting, editing and deleting is pretty easy. All you will again is to have the appropriate static methods in the Employee object.  
AddEmployee(Employee e)  
UpdateEmployee(Employee e)  
DeleteEmployee(Emplyee e).

Set the [InsertMethod](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.insertmethod.aspx) , [UpdateMethod](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.updatemethod.aspx) and [DeleteMethod](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.deletemethod.aspx) properties accordingly. All these method can be configured with parameters like the SelectMethod. However, setting the [DataObjectTypeName](http://msdn2.microsoft.com/en-us/library/system.web.ui.webcontrols.objectdatasource.dataobjecttypename.aspx) property to the Employee object will reduce a lot of the hassle by passing Employee objects to the Add,Update and DeleteMethods.