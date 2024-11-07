---
keywords: Experience Platform；首頁；熱門主題；Oracle服務雲端；oracle服務雲端
title: 在UI中建立Oracle Service Cloud Source連線
description: 瞭解如何使用Adobe Experience Platform UI建立Oracle Service Cloud來源連線。
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: a32d0d7ed7d18454099d2b55b3f6809cfbcd9b62
workflow-type: tm+mt
source-wordcount: '479'
ht-degree: 2%

---

# 在UI中建立Oracle服務雲端來源連線

>[!IMPORTANT]
>
>[!DNL Oracle Service Cloud]來源將於2025年5月底淘汰。

本教學課程提供使用Adobe Experience Platform使用者介面建立Oracle Service Cloud來源連線的步驟。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)：Experience Platform用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的Oracle服務雲端來源連線，可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/customer-success.md)的教學課程

### 收集必要的認證

若要在[!DNL Platform]上存取您的Oracle服務雲端帳戶，您必須提供下列值：

| 認證 | 說明 |
| ---------- | ----------- |
| Host | oracle服務雲端例項的主機URL。 |
| 使用者名稱 | 您的Oracle服務雲端使用者帳戶使用者名稱。 |
| 密碼 | 您的Oracle Service Cloud帳戶密碼。 |

如需驗證您的Oracle服務雲端帳戶的詳細資訊，請參閱驗證](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html)的[[!DNL Oracle] 指南。

## 連線您的Oracle服務雲端帳戶

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示可用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL 客戶成功]類別下，選取&#x200B;**[!UICONTROL Oracle服務雲端]**，然後選取&#x200B;**[!UICONTROL 新增資料]**。

![已反白顯示Oracle服務雲端來源的來源目錄。](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

**[!UICONTROL 連線至Oracle服務雲端]**&#x200B;頁面隨即顯示。 您可以在此頁面使用新的證明資料或現有的證明資料。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Oracle服務雲端帳戶，然後選取[下一步] **[!UICONTROL 以繼續。]**

![現有的帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### 新帳戶

如果您正在使用新認證，請選取&#x200B;**[!UICONTROL 新帳戶]**。 在出現的輸入表單上，提供名稱、可選說明和您的Oracle Service Cloud憑證。 完成時，請選取&#x200B;**[!UICONTROL 連線到來源]**，然後等待一段時間以建立新連線。

![新帳戶介面具有。](../../../../images/tutorials/create/oracle-service-cloud/new.png)的預留位置值

## 後續步驟

依照本教學課程中的指示，您已建立與Oracle Service Cloud帳戶的連線。 您現在可以繼續進行下一個教學課程，並[設定資料流，將客戶成功資料帶入Platform](../../dataflow/crm.md)。
