---
keywords: Experience Platform；首頁；熱門主題；沙盒疑難排解
solution: Experience Platform
title: 沙盒疑難排解指南
topic-legacy: troubleshooting guide
description: 本檔案提供有關Adobe Experience Platform沙盒的常見問題解答。
exl-id: 6a496509-a4e9-4e76-829b-32d67ccfcce6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 沙盒疑難排解指南

本檔案提供有關Adobe Experience Platform沙盒的常見問題解答。 有關其他平台服務的問題和故障排除，請參閱[Experience Platform故障排除指南](../landing/troubleshooting.md)。

沙盒將單一平台實例分割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。 如需詳細資訊，請參閱[沙盒概述](home.md)。

## 什麼是沙盒？

沙盒是單一Experience Platform實例中的虛擬分區。 每個沙盒都會維護其獨立的平台資源庫（包括結構描述、資料集、設定檔等）。 在沙盒中執行的所有內容和動作都僅限於該沙盒，不會影響任何其他沙盒。 如需詳細資訊，請參閱[沙盒概述](home.md)。

## 有哪些沙盒類型，有哪些不同？

Experience Platform中有兩種沙盒類型：

* 製作沙盒
* 非生產沙盒

Experience Platform提供單一生產沙盒，無法刪除或重設。 單一平台例項只能有一個生產沙盒。

相反地，沙盒管理員可針對單一平台例項建立多個非生產沙盒。 非生產沙盒可讓您測試功能、執行實驗並建立自訂組態，而不會影響生產沙盒。 此外，非生產沙盒具有重設功能，可從沙盒移除所有客戶建立的資源。 非生產沙盒無法轉換為生產沙盒。 預設的Experience Platform授權會授與您五個沙盒（一個製作與四個非製作）。 您可新增10個非生產沙盒，最多可新增75個沙盒。 如需詳細資訊，請連絡您的IMS組織管理員或Adobe銷售代表。

如需詳細資訊，請參閱[沙盒概述](./home.md)。

## 我可以從多個沙盒存取資源嗎？

沙盒是單一平台例項的隔離分區，每個沙盒會維護其獨立的資源庫。 存在於一個沙盒中的資源無法從任何其他沙盒存取，而不論沙盒類型（生產或非生產）。

## 我能有多少個製作沙盒？

Experience Platform僅支援每個IMS組織一個生產沙盒，現成提供。 雖然生產沙盒可以重新命名，但無法刪除或重設。 具有「沙盒管理」權限的使用者只能建立、重設和刪除非生產沙盒。

## 我能買多少個非生產沙盒？

Experience Platform目前允許在單一IMS組織內最多15個非生產沙盒啟用。

## 我剛建立了沙盒。 我要如何為使用此沙盒的使用者設定權限？

Adobe Admin Console會透過產品設定檔，將使用者連結至沙盒和權限。 建立新沙盒後，導覽至您要授與存取之產品描述檔的&#x200B;**權限**&#x200B;標籤，然後按一下&#x200B;**沙盒**。 從這裡，您可以以與其他權限相同的方式新增或移除新沙盒的存取權。

如果您想要為特定沙盒的使用者新增獨特權限，您可能需要建立新的產品設定檔，並套用適當的沙盒和權限，並指派這些使用者至該設定檔。

如需有關管理Admin Console中沙盒和權限的詳細資訊，請參閱[存取控制使用指南](../access-control/ui/overview.md)。
