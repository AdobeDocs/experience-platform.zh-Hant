---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務UI指南
description: Adobe Experience Platform查詢服務提供一個用戶介面，可用於編寫和執行查詢、查看以前執行的查詢以及訪問組織內用戶保存的查詢。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1133'
ht-degree: 2%

---

# [!DNL Query Service] UI指南

Adobe Experience Platform [!DNL Query Service] 提供一個用戶介面，可用於編寫和執行查詢、查看以前執行的查詢以及訪問組織內用戶保存的查詢。 在中訪問UI [Adobe Experience Platform](https://platform.adobe.com)選中 **[!UICONTROL 查詢]** 的子菜單。

## [!DNL Query Editor]

的 [!DNL Query Editor] 使您無需使用外部客戶端即可編寫和執行查詢。 選擇 **[!UICONTROL 建立查詢]** 開啟 [!DNL Query Editor] 並建立新查詢。 您還可以訪問 [!DNL Query Editor] 從 **[!UICONTROL 日誌]** 或 **[!UICONTROL 模板]** 頁籤。 選擇以前執行或保存的查詢將開啟 [!DNL Query Editor] 顯示所選查詢的SQL。

![突出顯示了「建立查詢」的「查詢」操控板。](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供了編輯空間，您可以在其中開始鍵入查詢。 鍵入時，編輯器會自動完成表內的SQL保留字、表和欄位名。 完成查詢後，選擇 **播放** 按鈕。 的 **[!UICONTROL 控制台]** 下方的 [!DNL Query Service] 正在執行，指示何時返回查詢。 的 **[!UICONTROL 結果]** 頁籤，顯示查詢結果。 查看 [查詢編輯器指南](./user-guide.md) 的子菜單。 [!DNL Query Editor]。

![在 [!DNL Query Editor]。](../images/ui/overview/query-editor.png)

## 計畫查詢 {#scheduled-queries}

已保存為模板的查詢可以計畫在常規節奏上運行。 在計畫查詢時，您可以選擇運行頻率、開始和結束日期、計畫查詢運行的周的某一天，以及要將查詢導出到的資料集。 查詢計畫是使用查詢編輯器設定的。

要瞭解如何通過UI計畫查詢，請參閱 [計畫查詢指南](./user-guide.md#scheduled-queries)。 要瞭解如何使用API添加計畫，請閱讀 [計畫查詢終結點指南](../api/scheduled-queries.md)。

在計畫查詢後，該查詢將出現在 [!UICONTROL 計畫查詢] 頁籤。 通過從清單中選擇計畫查詢，可以找到有關查詢、運行、建立者和計時的完整詳細資訊。

![「查詢」工作區中的「已調度查詢」頁籤突出顯示並顯示查詢計畫的行。](../images/ui/overview/scheduled-queries.png)

| 欄 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 名稱欄位是SQL查詢的模板名稱或前幾個字元。 通過UI使用查詢編輯器建立的任何查詢都會在開始時命名。 如果查詢是通過API建立的，則查詢的名稱是用於建立查詢的初始SQL的代碼段。 |
| **[!UICONTROL 範本]** | 查詢的模板名稱。 選擇要導航到查詢編輯器的模板名稱。 查詢模板將顯示在查詢編輯器中，以方便您。 如果沒有模板名稱，行將標籤為連字元，並且無法重定向到查詢編輯器來查看查詢。 |
| **[!UICONTROL SQL]** | SQL查詢的片段。 |
| **[!UICONTROL 運行頻率]** | 這是將查詢設定為運行的節奏。 可用值包括 `Run once` 和 `Scheduled`。 可根據查詢的運行頻率過濾查詢。 |
| **[!UICONTROL 建立者]** | 建立查詢的用戶的名稱。 |
| **[!UICONTROL 已建立]** | 以UTC格式建立查詢時的時間戳。 |
| **[!UICONTROL 上次運行時間戳]** | 運行查詢時的最新時間戳。 此列突出顯示查詢是否已根據其當前計畫執行。 |
| **[!UICONTROL 上次運行狀態]** | 最近執行查詢的狀態。 三個狀態值是： `successful` `failed` 或 `in progress`。 |

有關如何執行以下操作的詳細資訊，請參閱文檔 [通過查詢服務用戶介面監視查詢](./monitor-queries.md)。

## 範本 {#browse}

的 **[!UICONTROL 模板]** 頁籤顯示組織中的用戶保存的查詢。 將這些內容視為查詢項目非常有用，因為此處保存的查詢可能仍在構建中。 顯示在 **[!UICONTROL 模板]** 頁籤還顯示為運行查詢 **[!UICONTROL 日誌]** 頁籤 [!DNL Query Service]。

![在「查詢」面板的「模板」頁籤的視圖中放大顯示多個已保存的查詢。](../images/ui/overview/templates.png)

| 欄 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 名稱欄位是用戶建立的查詢名稱或SQL查詢的前幾個字元。 通過UI使用查詢編輯器建立的任何查詢都會在開始時命名。 如果查詢是通過API建立的，則查詢的名稱是用於建立查詢的初始SQL的代碼段。 您可以選擇查詢名稱以在 [!DNL Query Editor]。 您還可以使用搜索欄來搜索 [!UICONTROL 名稱] 的子菜單。 搜索區分大小寫。 |
| **[!UICONTROL SQL]** | SQL查詢的前幾個字元。 懸停在代碼上方顯示完整查詢。 |
| **[!UICONTROL 修改者]** | 上次修改查詢的用戶。 組織中有權訪問 [!DNL Query Service] 可以修改查詢。 |
| **[!UICONTROL 上次修改日期]** | 瀏覽器時區中上次修改查詢的日期和時間。 |

查看 [查詢模板](./query-templates.md) 文檔，瞭解有關平台UI中模板的詳細資訊。

## 記錄檔 {#log}

的 **[!UICONTROL 日誌]** 頁籤提供以前已執行的查詢清單。 預設情況下，日誌會以逆序順序列出查詢。

![在「查詢」面板的「日誌」頁籤的視圖中縮放，該頁籤顯示按時間倒序排列的查詢清單。](../images/ui/overview/log.png)

| 欄 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 查詢名稱，由SQL查詢的前幾個字元組成。 選擇模板名稱以開啟 [!UICONTROL 查詢日誌詳細資訊] 查看該運行。 可以使用搜索欄搜索查詢的名稱。 搜索區分大小寫。 |
| **[!UICONTROL 開始時間]** | 執行查詢的時間。 |
| **[!UICONTROL 完成時間]** | 查詢運行完成的時間。 |
| **[!UICONTROL 狀態]** | 查詢的當前狀態。 |
| **[!UICONTROL 資料集]** | 查詢使用的輸入資料集。 選擇要轉到輸入資料集詳細資訊螢幕的資料集。 |
| **[!UICONTROL 用戶端]** | 用於查詢的客戶端。 |
| **[!UICONTROL 建立者]** | 建立查詢的人員的姓名。 |

>!![Note]
選擇鉛筆表徵圖(![鉛筆表徵圖。](../images/ui/overview/edit-icon.png))，導航到 [!DNL Query Editor]。 為便於編輯，已預填充查詢。

查看 [查詢日誌文檔](./query-logs.md) 的子菜單。

## 憑據

的 **[!UICONTROL 憑據]** 頁籤同時顯示過期和未過期的憑據。 有關如何使用這些憑據與外部客戶端連接的詳細資訊，請閱讀 [憑據指南](../clients/overview.md)。

![突出顯示了「憑據」頁籤的「查詢」儀表板。](../images/ui/overview/credentials.png)

## 後續步驟

現在你已經熟悉了 [!DNL Query Service] 用戶介面 [!DNL Platform]，您可以 [!DNL Query Editor] 開始建立您自己的查詢項目以與組織中的其他用戶共用。 有關在中創作和運行查詢的詳細資訊 [!DNL Query Editor]，請參見 [[!DNL Query Editor] 使用手冊](./user-guide.md)。
