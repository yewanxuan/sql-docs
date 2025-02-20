---
title: "Windows Application Log | Microsoft Docs"
description: Learn how to view event messages in the application log that are generated by report server applications that run on the local system.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.technology: report-server


ms.topic: conceptual
helpviewer_keywords: 
  - "Windows application logs [Reporting Services]"
  - "logs [Reporting Services], Windows application logs"
  - "application logs [Reporting Services]"
ms.assetid: 742fd00e-aa6c-4c8a-b58f-c03c489b1699
author: maggiesMSFT
ms.author: maggies
---
# Windows Application Log
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] writes event messages to the Windows application log. You can use the message information written to the application log to find out about events that are generated by the report server applications running on the local system.  
  
## Viewing Report Server Events  
 You can use the Event Viewer to view the log file and to filter the messages it contains. For more information about event messages, see [Errors and Events Reference &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md). For more information about Windows application log or Event Viewer, see the Windows product documentation.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] provides three event sources:  
  
-   Report Server (Report Server Windows service)  
  
-   Report Manager  
  
-   Scheduling and Delivery Processor  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] does not provide a way to turn off application event logging for a report server or control which events are logged. The schema that describes report server event logging is fixed. You cannot extend the schema to support custom events.  
  
 The following table describes the event types that the report server writes to the application event log.  
  
|Event type|Description|  
|----------------|-----------------|  
|Information|An event that describes a successful operation (for example, when the report server services starts).|  
|Warning|An event that indicates a potential problem (for example, low disk space).|  
|Error|An event that describes a significant problem (for example, the service did not start).|  
|Success Audit|A security event that describes a successful logon.|  
|Failure Audit|An event that is logged when a logon attempt fails.|  
  
## See Also  
 [Reporting Services Log Files and Sources](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
 [Errors and Events Reference &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
