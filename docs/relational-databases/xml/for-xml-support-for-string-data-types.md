---
title: "FOR XML Support for String Data Types | Microsoft Docs"
description: Learn how string data types are handled when XML is generated by the FOR XML clause in a SQL query.
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: sql
ms.prod_service: "database-engine"
ms.reviewer: ""
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords: 
  - "strings [SQL Server], XML"
ms.assetid: bf069da8-de1e-44d2-a1fb-ade383076ac1
author: MikeRayMSFT
ms.author: mikeray
---
# FOR XML Support for String Data Types
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  The XML generated by the FOR XML white space characters in the data is entitized.  
  
 The following example creates a sample table **T** and inserts sample data that includes the line feed, carriage return, and tab characters. The SELECT statement retrieves the data from the table.  
  
```  
CREATE TABLE T  
(  
  c1 int identity primary key,  
  c2 varchar(100)  
);  
go  
  
INSERT T (c2) VALUES ('Special character 0xD for carriage return ' + convert(varchar(10), 0xD) + ' after carriage return');  
INSERT T (c2) VALUES ('Special character 0x9 for tab ' + convert(varchar(10), 0x9) + ' after tab' );  
INSERT T (c2) VALUES ('Special character 0xA for line feed ' + convert(varchar(10), 0xA) + ' after line feed');  
go  
SELECT *   
FROM T  
FOR XML AUTO;  
go  
```  
  
 This is the result:  
  
```  
 <T c1="1" c2="Special character 0xD for carriage return   
 after carriage return" />  
 <T c1="2" c2="Special character 0x9 for tab     after tab" />  
 <T c1="3" c2="Special character 0xA for line feed   
after line feed" />  
```  
  
 Note the following from the previous query:  
  
-   The carriage return in the first row is entitized as &#xD.  
  
-   The tab character in the second row is entitized as &#x09.  
  
-   The line feed character in the third row is entitized as &#xA.  
  
## See Also  
 [FOR XML Support for Various SQL Server Data Types](../../relational-databases/xml/for-xml-support-for-various-sql-server-data-types.md)  
  
  
