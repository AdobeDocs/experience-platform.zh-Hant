---
keywords: Experience Platform；首頁；熱門主題；Oracle服務雲端；oracle服務雲端
title: 在UI中建立Oracle服務雲端來源連線
description: 了解如何使用Adobe Experience Platform UI建立Oracle服務雲端來源連線。
exl-id: e5869c09-b61e-4d23-a594-5a07769da3c4
source-git-commit: 1695b7d638feb648d5cd7af07879f3ed13f938eb
workflow-type: tm+mt
source-wordcount: '480'
ht-degree: 1%

---

# 在UI中建立Oracle服務雲端來源連線

本教學課程提供使用Adobe Experience Platform使用者介面建立Oracle服務雲端來源連線的步驟。

## 快速入門

本教學課程需要妥善了解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效的Oracle服務雲源連接，則可以略過本檔案的其餘部分，並繼續進行上的教學課程 [配置資料流](../../dataflow/customer-success.md)

### 收集所需憑據

若要存取您的Oracle服務雲端帳戶，請依 [!DNL Platform]，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| Host | 您的Oracle服務雲例項的主機URL。 |
| 使用者名稱 | 您的Oracle服務雲端使用者帳戶的使用者名稱。 |
| 密碼 | 您的Oracle服務雲端帳戶的密碼。 |

如需驗證Oracle服務雲端帳戶的詳細資訊，請參閱 [[!DNL Oracle] 驗證指南](https://docs.oracle.com/en/cloud/saas/b2c-service/20c/cxska/OKCS_Authenticate_and_Authorize.html).

## 連線您的Oracle服務雲端帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示可用來建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋列找到您要使用的特定來源。

在 [!UICONTROL 客戶成功] 類別，選擇 **[!UICONTROL Oracle服務雲]** 然後選取 **[!UICONTROL 新增資料]**.

![突出顯示Oracle服務雲源的源目錄。](../../../../images/tutorials/create/oracle-service-cloud/catalog.png)

此 **[!UICONTROL 連線至Oracle服務雲端]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取您要連線的Oracle服務雲端帳戶，然後選取 **[!UICONTROL 下一個]** 繼續。

![現有帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的Oracle服務雲端憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![具有的佔位符值的新帳戶介面。](../../../../images/tutorials/create/oracle-service-cloud/new.png)

## 後續步驟

依照本教學課程，您已建立與Oracle服務雲端帳戶的連線。 您現在可以繼續下一個教學課程，以及 [設定資料流，將客戶成功資料匯入平台](../../dataflow/crm.md).
