---
title: 在UI中建立Google雲儲存源連接
description: 瞭解如何使用GoogleUI建立Adobe Experience Platform雲儲存源連接。
exl-id: 3258ccd7-757c-4c4a-b7bb-0e8c9de3b50a
source-git-commit: 7181cb92dd44d8005fe1054020ffeb36c309b42e
workflow-type: tm+mt
source-wordcount: '613'
ht-degree: 1%

---

# 建立 [!DNL Google Cloud Storage] UI中的源連接

本教程提供建立 [!DNL Google Cloud Storage] 源連接使用Adobe Experience PlatformUI。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化框架。
   * [架構組合的基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本構建基塊，包括架構組成中的關鍵原則和最佳做法。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自定義架構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):基於來自多個源的聚合資料提供統一、即時的用戶配置檔案。

如果您已經有 [!DNL Google Cloud Storage] 連接，您可以跳過本文檔的其餘部分並繼續學習有關 [配置資料流](../../dataflow/batch/cloud-storage.md)。

### 支援的檔案格式

[!DNL Experience Platform] 支援從外部儲存接收的以下檔案格式：

* 分隔符分隔的值(DSV):任何單字元值都可用作DSV格式資料檔案的分隔符。
* JavaScript對象符號(JSON):JSON格式的資料檔案必須符合XDM。
* Apache Parke:拼花格式化資料檔案必須符合XDM。

### 收集所需憑據

為了訪問 [!DNL Google Cloud Storage] 資料，必須提供以下值：

| 憑據 | 說明 |
| ---------- | ----------- |
| 訪問密鑰ID | 61個字元的字母數字字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。 |
| 秘密訪問密鑰 | 一個40個字元、基64編碼的字串，用於驗證 [!DNL Google Cloud Storage] 帳戶到平台。 |
| 貯體名稱 | 您的名稱 [!DNL Google Cloud Storage] 桶。 如果要提供對雲儲存中特定子資料夾的訪問權限，則必須指定儲存段名稱。 |
| 檔案夾路徑 | 要提供訪問權限的資料夾的路徑。 |

有關這些值的詳細資訊，請參見 [Google雲儲存HMAC密鑰](https://cloud.google.com/storage/docs/authentication/hmackeys#overview) 的子菜單。 有關如何生成您自己的訪問密鑰ID和密鑰訪問密鑰的步驟，請參閱 [[!DNL Google Cloud Storage] 概述](../../../../connectors/cloud-storage/google-cloud-storage.md)。

收集了所需的憑據後，您可以按照以下步驟連結 [!DNL Google Cloud Storage] 帳戶到平台。

## 連接 [!DNL Google Cloud Storage] 帳戶

在平台UI中，選擇 **[!UICONTROL 源]** 從左導航欄訪問 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索選項找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 **[!UICONTROL Google雲儲存]** ，然後選擇 **[!UICONTROL 添加資料]**。

![顯示源目錄頁的平台UI螢幕。](../../../../images/tutorials/create/google-cloud-storage/catalog.png)

的 **[!UICONTROL 連接到Google雲儲存]** 的子菜單。 在此頁上，您可以使用新憑據或現有憑據。

### 現有帳戶

要連接現有帳戶，請選擇 [!DNL Google Cloud Storage] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![平台UI螢幕顯示Google雲儲存源的現有帳戶頁](../../../../images/tutorials/create/google-cloud-storage/existing.png)

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**。 在顯示的輸入表單上，提供名稱、可選說明和 [!DNL Google Cloud Storage] 憑據。 在此步驟中，您還可以通過定義子資料夾路徑的名稱來指定帳戶將有權訪問的子資料夾。

完成後，選擇 **[!UICONTROL 連接到源]** 然後再給新連接建立一段時間。

![平台UI螢幕顯示Google雲儲存源的新帳戶頁。](../../../../images/tutorials/create/google-cloud-storage/new.png)


## 後續步驟

按照本教程，您已建立到 [!DNL Google Cloud Storage] 帳戶。 現在，您可以繼續下一個教程， [配置資料流，將雲儲存中的資料引入平台](../../dataflow/batch/cloud-storage.md)。
