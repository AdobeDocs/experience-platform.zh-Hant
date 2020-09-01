---
keywords: Experience Platform;home;popular topics;sandbox developer guide
solution: Experience Platform
title: 沙盒API開發人員指南
topic: developer guide
description: 此開發人員指南提供步驟，協助您使用沙盒API來管理Experience Platform中的沙盒，並包含執行各種作業的範例API呼叫。
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# 沙盒API開發人員指南

Adobe Experience Platform中的沙盒可提供獨立的開發環境，讓您測試功能、執行實驗並建立自訂組態，而不會影響您的生產環境。

此開發人員指南提供步驟，協助您使用沙盒API來管理Experience Platform中的沙盒，並包含執行各種作業的範例API呼叫。

## 沙盒API快速入門

若要管理IMS組織的沙盒，您必須擁有沙盒管理權限。 沒有存取權限的使用者只能使用端點來列 [出目前使用者的作用中沙盒](./list-active-sandboxes.md)。 如需如何 [指派「體驗平台」沙箱權限的詳細資訊](../../access-control/home.md) ，請參閱存取控制概觀。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中使用之慣例的詳細資訊，請參閱「Experience Platform疑難排解指 [南」中有關如何讀取範例API呼叫的章節](../../landing/troubleshooting.md#how-do-i-format-an-api-request) 。

### 收集必要標題的值

本指南要求您完成驗證教 [學課程](../../tutorials/authentication.md) ，才能成功呼叫平台API。 完成驗證教學課程後，所有Experience Platform API呼叫中每個必要標題的值都會顯示在下方：

* 授權：生產者 `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

除了驗證標題外，所有請求都需要一個標題，該標題會指定執行下列操作的沙盒名稱：

* x-sandbox-name: `{SANDBOX_NAME}`

所有包含裝載（POST、PUT和PATCH）的請求都需要額外的標題：

* 內容類型：application/json

## 後續步驟

現在您已收集到必要的認證，您可以繼續閱讀其餘的開發人員指南。 每個區段都提供其端點的重要資訊，並示範執行CRUD作業的範例API呼叫。 每個呼叫都包含一般 **API格式**、顯示必要標題 **和正確格式化負載的範例請求，以及成功呼叫** 的範例回應 **** 。