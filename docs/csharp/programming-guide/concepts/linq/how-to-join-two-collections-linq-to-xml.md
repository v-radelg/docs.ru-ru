---
title: "Практическое руководство. Объединение двух коллекций (LINQ to XML) (C#) | Документы Майкрософт"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 7b817ede-911a-4cff-9dd3-639c3fc228c9
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 30e68bb1fef31d9ef8f4ea6ea5262ae9efe466a1
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-join-two-collections-linq-to-xml-c"></a>Практическое руководство. Объединение двух коллекций (LINQ to XML) (C#)
Элемент или атрибут в XML-документе может иногда относиться к другому элементу или атрибуту. Например, XML-документ [Пример XML-файла. Клиенты и заказы (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml-2.md) содержит список клиентов и список заказов. Каждый элемент `Customer` содержит атрибут `CustomerID`. Каждый элемент `Order` содержит элемент `CustomerID`. Элемент `CustomerID` для каждого заказа ссылается на атрибут `CustomerID`, присвоенный также и клиенту.  
  
 Раздел [Пример XSD-файла. Клиенты и заказы](../../../../csharp/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders1.md) содержит XSD, с помощью которого можно проверить этот документ. Здесь используются функции XSD `xs:key` и `xs:keyref` для установления того, что атрибут `CustomerID` элемента `Customer` является ключом, а также для установления связи между элементом `CustomerID` каждого из элементов `Order` и атрибутом `CustomerID` каждого из элементов `Customer`.  
  
 В [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] можно воспользоваться преимуществами таких связей элементов и атрибутов при помощи предложения `join`.  
  
 Обратите внимание, что, поскольку индекс недоступен, такое соединение будет сильно загружать среду.  
  
 Более подробные сведения о функции `join` см. в разделе [Операции соединения (C#)](../../../../csharp/programming-guide/concepts/linq/join-operations.md).  
  
## <a name="example"></a>Пример  
 В следующем примере выполняется соединение элементов `Customer` с элементами `Order` и создается новый XML-документ, который включает элемент `CompanyName` в заказы.  
  
 Перед выполнением запроса в примере выполняется проверка соответствия документа схеме [Пример XSD-файла. Клиенты и заказы](../../../../csharp/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders1.md). Это позволяет обеспечить бесперебойную работу предложения соединения.  
  
 В этом запросе сначала выполняется получение всех элементов `Customer`, а затем присоединение их к элементам `Order`. Он отбирает только заказы от клиентов со значением `CustomerID` больше «K». После этого выполняется проецирование нового элемента `Order`, который содержит сведения о клиентах внутри каждого заказа.  
  
 В этом примере используется следующий XML-документ: [Пример XML-файла. Клиенты и заказы (LINQ to XML)](../../../../csharp/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml-2.md).  
  
 В этом примере используется следующая XSD-схема: [Пример XSD-файла. Клиенты и заказы](../../../../csharp/programming-guide/concepts/linq/sample-xsd-file-customers-and-orders1.md).  
  
 Обратите внимание, что такое соединение не будет работать оптимально. Соединение осуществляется путем линейного поиска. Не используются хэш-таблицы и индексы, которые могли бы помочь оптимизировать производительность.  
  
```csharp  
XmlSchemaSet schemas = new XmlSchemaSet();  
schemas.Add("", "CustomersOrders.xsd");  
  
Console.Write("Attempting to validate, ");  
XDocument custOrdDoc = XDocument.Load("CustomersOrders.xml");  
  
bool errors = false;  
custOrdDoc.Validate(schemas, (o, e) =>  
                     {  
                         Console.WriteLine("{0}", e.Message);  
                         errors = true;  
                     });  
Console.WriteLine("custOrdDoc {0}", errors ? "did not validate" : "validated");  
  
if (!errors)  
{  
    // Join customers and orders, and create a new XML document with  
    // a different shape.  
  
    // The new document contains orders only for customers with a  
    // CustomerID > 'K'  
    XElement custOrd = custOrdDoc.Element("Root");  
    XElement newCustOrd = new XElement("Root",  
        from c in custOrd.Element("Customers").Elements("Customer")  
        join o in custOrd.Element("Orders").Elements("Order")  
                   on (string)c.Attribute("CustomerID") equals  
                      (string)o.Element("CustomerID")  
        where ((string)c.Attribute("CustomerID")).CompareTo("K") > 0  
        select new XElement("Order",  
            new XElement("CustomerID", (string)c.Attribute("CustomerID")),  
            new XElement("CompanyName", (string)c.Element("CompanyName")),  
            new XElement("ContactName", (string)c.Element("ContactName")),  
            new XElement("EmployeeID", (string)o.Element("EmployeeID")),  
            new XElement("OrderDate", (DateTime)o.Element("OrderDate"))  
        )  
    );  
    Console.WriteLine(newCustOrd);  
}  
```  
  
 Этот код выводит следующие результаты:  
  
```  
Attempting to validate, custOrdDoc validated  
<Root>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-03-21T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LAZYK</CustomerID>  
    <CompanyName>Lazy K Kountry Store</CompanyName>  
    <ContactName>John Steel</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-05-22T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>1</EmployeeID>  
    <OrderDate>1997-06-25T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>8</EmployeeID>  
    <OrderDate>1997-10-27T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>6</EmployeeID>  
    <OrderDate>1997-11-10T00:00:00</OrderDate>  
  </Order>  
  <Order>  
    <CustomerID>LETSS</CustomerID>  
    <CompanyName>Let's Stop N Shop</CompanyName>  
    <ContactName>Jaime Yorres</ContactName>  
    <EmployeeID>4</EmployeeID>  
    <OrderDate>1998-02-12T00:00:00</OrderDate>  
  </Order>  
</Root>  
```  
  
## <a name="see-also"></a>См. также  
 [Дополнительные способы создания запросов (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/advanced-query-techniques-linq-to-xml.md)
