---
title: 在UI中建立Google雲端儲存來源連線
description: 了解如何使用Google UI建立Adobe Experience Platform雲端儲存空間來源連線。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] UI中的源連接

本教學課程提供建立 [!DNL Google Cloud Storage] 來源連線。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Google Cloud Storage] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/batch/cloud-storage.md).

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存器擷取的下列檔案格式：

* 分隔字元分隔值(DSV):任何單字元值都可用作DSV格式化資料檔案的分隔符。
* JavaScript物件標籤法(JSON):JSON格式化資料檔案必須符合XDM標準。
* 阿帕奇拼花：必須符合XDM規範，才能使用鑲木格式化資料檔案。

### 收集所需憑據

若要存取 [!DNL Google Cloud Storage] 資料，您必須提供下列值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 訪問密鑰ID | 61個字元的英數字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 |
| 秘密訪問密鑰 | 40個字元的base-64編碼字串，用於驗證您的 [!DNL Google Cloud Storage] 帳戶至Platform。 |
| 貯體名稱 | 您的 [!DNL Google Cloud Storage] 桶。 如果您想要提供雲端儲存空間中特定子資料夾的存取權，則必須指定貯體名稱。 |
| 資料夾路徑 | 要提供訪問權限的資料夾的路徑。 |

如需這些值的詳細資訊，請參閱 [Google雲端儲存HMAC金鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 指南。 有關如何生成您自己的訪問密鑰ID和秘密訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md).

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Google Cloud Storage] 帳戶至Platform。

## 連接您的 [!DNL Google Cloud Storage] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 雲端儲存空間] 類別，選擇 **[!UICONTROL Google雲端儲存空間]** 然後選取 **[!UICONTROL 新增資料]**.

![顯示來源目錄頁面的平台UI畫面。](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

此 **[!UICONTROL 連線至Google雲端儲存空間]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要連線現有帳戶，請選取 [!DNL Google Cloud Storage] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![Platform UI畫面顯示Google雲端儲存空間來源的現有帳戶頁面](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、選用說明和您的 [!DNL Google Cloud Storage] 憑證。 在此步驟中，您也可以定義子資料夾的路徑名稱，以指定您的帳戶將可存取的子資料夾。

完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![Platform UI畫面顯示Google雲端儲存空間來源的新帳戶頁面。](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 後續步驟

依照本教學課程，您已建立與 [!DNL Google Cloud Storage] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料從雲儲存帶入平台](../../dataflow/batch/cloud-storage.md).
