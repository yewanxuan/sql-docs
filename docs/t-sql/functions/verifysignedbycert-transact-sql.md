---
title: "VERIFYSIGNEDBYCERT (Transact-SQL)"
description: "VERIFYSIGNEDBYCERT (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.reviewer: ""
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
ms.custom: ""
f1_keywords:
  - "VERIFYSIGNEDBYCERT"
  - "VERIFYSIGNEDBYCERT_TSQL"
helpviewer_keywords:
  - "digitally signed data for changes [SQL Server]"
  - "verifying digitally signed data for changes"
  - "testing digitally signed data for changes"
  - "checking digitally signed data for changes"
  - "VERIFYSIGNEDBYCERT"
  - "signatures [SQL Server]"
  - "digital signatures [SQL Server]"
dev_langs:
  - "TSQL"
---
# VERIFYSIGNEDBYCERT (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Tests whether digitally signed data has been changed since it was signed.  
  
 ![Topic link icon](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
VerifySignedByCert( Cert_ID , signed_data , signature )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *Cert_ID*  
 Is the ID of a certificate in the database. *Cert_ID* is **int**.  
  
 *signed_data*  
 Is a variable of type **nvarchar**, **char**, **varchar**, or **nchar** that contains data that has been signed with a certificate.  
  
 *signature*  
 Is the signature that was attached to the signed data. *signature* is **varbinary**.  
  
## Return Types  
 **int**  
  
 Returns 1 when signed data is unchanged; otherwise 0.  
  
## Remarks  
 **VerifySignedBycert** decrypts the signature of the data by using the public key of the specified certificate, and compares the decrypted value to a newly computed MD5 hash of the data. If the values match, the signature is confirmed to be valid.  
  
## Permissions  
 Requires VIEW DEFINITION permission on the certificate.  
  
## Examples  
  
### A. Verifying that signed data has not been tampered with  
 The following example tests whether the information in `Signed_Data` has been changed since it was signed with the certificate called `Shipping04`. The signature is stored in `DataSignature`. The certificate, `Shipping04`, is passed to `Cert_ID`, which returns the ID of the certificate in the database. If `VerifySignedByCert` returns 1, the signature is correct. If `VerifySignedByCert` returns 0, the data in `Signed_Data` is not the data that was used to generate `DataSignature`. In this case, either `Signed_Data` has been changed since it was signed or `Signed_Data` was signed with a different certificate.  
  
```sql
SELECT Data, VerifySignedByCert( Cert_Id( 'Shipping04' ),  
    Signed_Data, DataSignature ) AS IsSignatureValid  
FROM [AdventureWorks2012].[SignedData04]   
WHERE Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
### B. Returning only records that have a valid signature  
 This query returns only records that have not been changed since they were signed using certificate `Shipping04`.  
  
```sql
SELECT Data FROM [AdventureWorks2012].[SignedData04]   
WHERE VerifySignedByCert( Cert_Id( 'Shipping04' ), Data,   
    DataSignature ) = 1   
AND Description = N'data signed by certificate ''Shipping04''';  
GO  
```  
  
## See Also  
 [CERT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/cert-id-transact-sql.md)   
 [SIGNBYCERT &#40;Transact-SQL&#41;](../../t-sql/functions/signbycert-transact-sql.md)   
 [CREATE CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/create-certificate-transact-sql.md)   
 [ALTER CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-certificate-transact-sql.md)   
 [DROP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-certificate-transact-sql.md)   
 [BACKUP CERTIFICATE &#40;Transact-SQL&#41;](../../t-sql/statements/backup-certificate-transact-sql.md)   
 [Encryption Hierarchy](../../relational-databases/security/encryption/encryption-hierarchy.md)  
  
  
