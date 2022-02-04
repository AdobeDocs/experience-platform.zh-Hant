---
keywords: Experience Platform；首頁；熱門主題；資料登錄區；資料登錄區
solution: Experience Platform
title: 使用UI將資料登錄區連接到平台
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用平台用戶介面建立資料著陸區源連接器。
exl-id: 653c9958-5d89-4b0c-af3d-a3e74aa47a08
source-git-commit: b007cdf92811b453df5b5d005456a05cd845b769
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# 連接 [!DNL Data Landing Zone] 到使用UI的平台

[!DNL Data Landing Zone] 是基於雲的資料儲存設施，用於預配有Adobe Experience Platform的臨時檔案儲存。 資料將自動從 [!DNL Data Landing Zone] 七天後。

本教程提供建立 [!DNL Data Landing Zone] 源連接。

## 快速入門

本教程需要對Adobe Experience Platform的以下部分進行有效的理解：

* [源](../../../../home.md):Experience Platform允許從各種源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Experience Platform提供虛擬沙箱，將單個平台實例分區為獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

## 從 [!DNL Data Landing Zone] 到平台

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

在 [!UICONTROL 雲儲存] 類別，選擇 [!DNL Data Landing Zone] ，然後選擇 **[!UICONTROL 添加資料]**。

![目錄](../../../../images/tutorials/create/dlz/catalog.png)

的 [!UICONTROL 添加資料] 步驟，提供一個介面來選擇和預覽要帶到平台的資料。

![添加資料](../../../../images/tutorials/create/dlz/add-data.png)

有關如何為雲儲存源建立資料流的詳細、分步指南，請參見上的教程 [建立雲儲存資料流以將資料帶到平台](../../dataflow/batch/cloud-storage.md)。

## 檢索並刷新 [!DNL Data Landing Zone] 憑據

[!DNL Data Landing Zone] 是隨您的Adobe Experience Platform源許可證提供的開箱即用源。 [!DNL Data Landing Zone] 使用基於SAS URI和SAS令牌的身份驗證。 您可以從 [!UICONTROL 源目錄] 的子菜單。

在 [!UICONTROL 源目錄]，也請參見Wiki頁。 [!UICONTROL 雲儲存] 類別，選取橢圓(**...**) **[!UICONTROL 資料登錄區]** 卡。 從顯示的下拉菜單中，選擇 **[!UICONTROL 查看憑據]**。

![選項](../../../../images/tutorials/create/dlz/options.png)

出現跨距，顯示您的容器名稱、SAS令牌、儲存帳戶名和SAS URI。

選擇 **[!UICONTROL 刷新憑據]** 並允許幾秒鐘內處理更新的憑據。

>[!TIP]
>
>您 [!DNL Data Landing Zone] 憑據設定為在90天後自動過期，您必須使用新憑據重新連接到 [!DNL Data Landing Zone] 到期後。 平台中的資料流不受憑據過期的影響，您仍然可以使用新的憑據繼續使用新的和現有的資料流。

![查看憑據](../../../../images/tutorials/create/dlz/credentials.png)

## 後續步驟

按照本教程，您已訪問了 [!DNL Data Landing Zone] 並學會檢索和刷新您的憑據。 現在，您可以繼續下一個教程， [建立資料流，將資料從雲儲存帶到平台](../../dataflow/batch/cloud-storage.md)。
