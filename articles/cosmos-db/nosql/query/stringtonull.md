---
title: StringToNull in Azure Cosmos DB query language
description: Learn about SQL system function StringToNull in Azure Cosmos DB.
author: ginamr
ms.service: cosmos-db
ms.subservice: nosql
ms.topic: conceptual
ms.date: 03/03/2020
ms.author: girobins
ms.custom: query-reference, ignite-2022
---
# StringToNull (Azure Cosmos DB)
[!INCLUDE[NoSQL](../../includes/appliesto-nosql.md)]

 Returns expression translated to null. If expression can't be translated, returns undefined.  
  
## Syntax
  
```sql
StringToNull(<str_expr>)  
```  
  
## Arguments
  
*str_expr*  
   Is a string expression to be parsed as a null expression.
  
## Return types
  
  Returns a null expression or undefined.  
  
## Examples
  
  The following example shows how `StringToNull` behaves across different types. 

The following are examples with valid input.

 Whitespace is allowed only before or after "null".

```sql
SELECT 
    StringToNull("null") AS n1, 
    StringToNull("  null ") AS n2,
    IS_NULL(StringToNull("null   ")) AS n3
```  
  
 Here's the result set.  
  
```json
[{"n1": null, "n2": null, "n3": true}]
```  

The following are examples with invalid input.

Null is case sensitive and must be written with all lowercase characters such as `null`.

```sql
SELECT    
    StringToNull("NULL"),
    StringToNull("Null")
```  
  
 Here's the result set.  
  
```json
[{}]
```  

The expression passed will be parsed as a null expression; these inputs don't evaluate to type null and thus return undefined.

```sql
SELECT    
    StringToNull("true"), 
    StringToNull(false), 
    StringToNull(undefined),
    StringToNull(NaN) 
```  
  
 Here's the result set.  
  
```json
[{}]
```  

## Remarks

This system function won't utilize the index.

## Next steps

- [System functions Azure Cosmos DB](system-functions.yml)
- [Introduction to Azure Cosmos DB](../../introduction.md)
