---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；oracle；
title: (Beta)使用Platform UI建立OracleResponsys來源連線
description: 瞭解如何使用Platform UI連線Adobe Experience Platform至OracleResponsys。
hide: true
hidefromtoc: true
exl-id: 9ec5e1c2-3d9e-4729-be81-89a85d5ea782
source-git-commit: e37c00863249e677f1645266859bf40fe6451827
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 2%

---

# (Beta)使用平台UI建立[!DNL Oracle Responsys]來源連線

>[!NOTE]
>
>[!DNL Oracle Responsys]來源是測試版。 如需使用Beta標籤聯結器的詳細資訊，請參閱[來源概觀](../../../../home.md#terms-and-conditions)。

本教學課程提供您使用Adobe Experience Platform使用者介面建立[[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md)來源連線的步驟。

## 快速入門

本指南需要深入瞭解下列Platform元件：

* [來源](../../../../home.md)： Platform允許從各種來源擷取資料，同時讓您能夠使用Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Platform提供可將單一Platform執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

如果您已在Platform上擁有已驗證的[!DNL Oracle Responsys]帳戶，則您可以略過本檔案的其餘部分，並繼續進行有關[建立資料流以將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md)的教學課程。

### 收集必要的認證

為了將[!DNL Oracle Responsys]連線到Platform，您必須提供下列驗證屬性的值：

| 認證 | 說明 |
| --- | --- |
| 端點 | [!DNL Oracle Responsys]執行個體的REST驗證端點URL。 |
| 用戶端 ID | [!DNL Oracle Responsys]執行個體的使用者端識別碼。 |
| 用戶端密碼 | [!DNL Oracle Responsys]執行個體的使用者端密碼。 |

如需[!DNL Oracle Responsys]的驗證認證詳細資訊，請參閱驗證](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm)的[[!DNL Oracle Responsys] 指南。

收集必要的認證後，您可以依照下列步驟將[!DNL Oracle Responsys]帳戶連結至Platform。

## 連線您的[!DNL Oracle Responsys]帳戶

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在[!UICONTROL 行銷自動化]類別下，選取&#x200B;**[!UICONTROL OracleResponsys]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![反白顯示Oracle為Responsys來源的Adobe Experience Platform來源目錄。](../../../../images/tutorials/create/oracle-responsys/catalog.png)

**[!UICONTROL 連線OracleResponsys帳戶]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要使用現有帳戶，請選取您要用來建立新資料流的[!DNL Oracle Responsys]帳戶，然後選取[下一步] ]**以繼續。**[!UICONTROL 

![OracleResponsys的現有帳戶驗證畫面。](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 新帳戶

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後為您的[!DNL Oracle Responsys]認證提供名稱、選擇性說明和適當的值。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![OracleResponsys的新帳戶驗證畫面。](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 後續步驟

依照本教學課程，您已驗證並建立[!DNL Oracle Responsys]帳戶與平台之間的來源連線。 您現在可以繼續進行下一個教學課程，並[建立資料流以將行銷自動化資料帶到Platform](../../dataflow/marketing-automation.md)。
