---
title: Entity Framework Code First - Delete a LocalDb instance
permalink: 2014/03/06/entity-framework-code-first-delete-a-localdb-instance/
layout: post
tags:
  - .NET
comments: true
---

<p>When working with the Entity Framework Code First I will often get the error below: </p> <blockquote> <p>An exception of type “System.Data.SqlClient.SqlException’ occurred in EntityFramework.dll but was not handled by in user code’</p> <p>Additional information: Cannot drop database [database name] because it is currently in use.</p></blockquote> <p>To force a delete of the database, follow the steps below. </p> <p><a href="./images/error_6-03-2014-11-04-30-am.jpg"><img title="error_6-03-2014 11-04-30 AM" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;" border="0" alt="error_6-03-2014 11-04-30 AM" src="./images/error_6-03-2014-11-04-30-am.jpg" width="244" height="237"></a></p> <p>Figure: This exception is common after you have opened a LocalDb database in Visual Studio.</p> 
<p> </p> 

<h2><font style="font-weight:normal;">Open Library Package Manager and Stop the LocalDb instance</font></h2> 

<p>a: Select Tools | Library Package manager | Package Manager Console<br></p> 
<p>b: Execute the following two statements<br></p> <p>                  sqllocaldb stop v11.0<br></p> <p>                  sqllocaldb delete v11.0<br></p>

<p><a href="./images/error_6-03-2014-11-05-59-am.jpg"><img title="error_6-03-2014 11-05-59 AM" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;" border="0" alt="error_6-03-2014 11-05-59 AM" src="./images/error_6-03-2014-11-05-59-am.jpg" width="244" height="135"></a><br></p> 
<p>Figure: The steps above will stop and delete the LocalDb instance.</p> <p> </p> 

<h2><font style="font-weight:normal;">Delete the database file from the database</font></h2> 
<p><a href="./images/image.png"><img title="image" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;margin:0;border-left:0;display:inline;padding-right:0;" border="0" alt="image" src="./images/image.png" width="244" height="49"></a></p> <p>Figure: Open the Solution Explorer and choose Show All Files</p> <p><a href="./images/error_6-03-2014-11-05-07-am.jpg"><img title="error_6-03-2014 11-05-07 AM" style="border-top:0;border-right:0;background-image:none;border-bottom:0;padding-top:0;padding-left:0;border-left:0;display:inline;padding-right:0;" border="0" alt="error_6-03-2014 11-05-07 AM" src="./images/error_6-03-2014-11-05-07-am.jpg" width="244" height="88"></a></p> <p>Figure: Delete the mdf from the App_Data folder</p>