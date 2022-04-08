---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；查詢編輯器；查詢編輯器；查詢編輯器；查詢編輯器；
solution: Experience Platform
title: 查詢服務UI指南
topic-legacy: guide
description: Adobe Experience Platform查詢服務提供一個用戶介面，可用於編寫和執行查詢、查看以前執行的查詢以及訪問IMS組織內用戶保存的查詢。
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: a887c502213e96d6af90af0859da78c2984f89a7
workflow-type: tm+mt
source-wordcount: '662'
ht-degree: 2%

---

# [!DNL Query Service] UI指南

Adobe Experience Platform [!DNL Query Service] 提供一個用戶介面，可用於編寫和執行查詢、查看以前執行的查詢以及訪問由IMS組織內的用戶保存的查詢。 在中訪問UI [Adobe Experience Platform](https://platform.adobe.com)選中 **[!UICONTROL 查詢]** 的子菜單。

## [!DNL Query Editor]

的 [!DNL Query Editor] 使您無需使用外部客戶端即可編寫和執行查詢。 選擇 **[!UICONTROL 建立查詢]** 開啟 [!DNL Query Editor] 並建立新查詢。 您還可以訪問 [!DNL Query Editor] 從 **[!UICONTROL 日誌]** 或 **[!UICONTROL 瀏覽]** 頁籤。 選擇以前執行或保存的查詢將開啟 [!DNL Query Editor] 顯示所選查詢的SQL。

![突出顯示了「建立查詢」的「查詢」操控板。](../images/ui/overview/overview.png)

[!DNL Query Editor] 提供了編輯空間，您可以在其中開始鍵入查詢。 鍵入時，編輯器會自動完成表內的SQL保留字、表和欄位名。 完成查詢後，選擇 **播放** 按鈕。 的 **[!UICONTROL 控制台]** 下方的 [!DNL Query Service] 正在執行，指示何時返回查詢。 的 **[!UICONTROL 結果]** 頁籤，顯示查詢結果。 查看 [查詢編輯器指南](./user-guide.md) 的子菜單。 [!DNL Query Editor]。

![在 [!DNL Query Editor]。](../images/ui/overview/query-editor.png)

## 瀏覽 {#browse}

的 **[!UICONTROL 瀏覽]** 頁籤顯示組織中的用戶保存的查詢。 將這些內容視為查詢項目非常有用，因為此處保存的查詢可能仍在構建中。 顯示在 **[!UICONTROL 瀏覽]** 頁籤還顯示為運行查詢 **[!UICONTROL 日誌]** 頁籤 [!DNL Query Service]。

![在「查詢」面板的「瀏覽」頁籤的視圖中放大顯示多個已保存的查詢。](../images/ui/overview/browse.png)

| 欄目 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 用戶建立的查詢名稱。 可以在名稱上選擇以在 [!DNL Query Editor]。 也可以使用搜索欄搜索查詢的名稱。 搜索區分大小寫。 |
| **[!UICONTROL SQL]** | SQL查詢的前幾個字元。 懸停在代碼上方顯示完整查詢。 |
| **[!UICONTROL 修改者]** | 上次修改查詢的用戶。 組織中有權訪問 [!DNL Query Service] 可以修改查詢。 |
| **[!UICONTROL 上次修改日期]** | 瀏覽器時區中上次修改查詢的日期和時間。 |

## 記錄檔

的 **[!UICONTROL 日誌]** 頁籤提供以前已執行的查詢清單。 預設情況下，日誌會以逆序順序列出查詢。

![在「查詢」面板的「日誌」頁籤的視圖中縮放，該頁籤顯示按時間倒序排列的查詢清單。](../images/ui/overview/log.png)

| 欄目 | 說明 |
| --- | --- |
| **[!UICONTROL 名稱]** | 查詢名稱，由SQL查詢的前幾個字元組成。 選擇名稱將開啟 [!DNL Query Editor]，允許您編輯查詢。 可以使用搜索欄搜索查詢的名稱。 搜索區分大小寫。 |
| **[!UICONTROL 建立者]** | 建立查詢的人員的姓名。 |
| **[!UICONTROL 用戶端]** | 用於查詢的客戶端。 |
| **[!UICONTROL 資料集]** | 查詢使用的輸入資料集。 選擇要轉到輸入資料集詳細資訊螢幕的資料集。 |
| **[!UICONTROL 狀態]** | 查詢的當前狀態。 |
| **[!UICONTROL 上次運行]** | 上次運行查詢時。 通過選擇此列上的箭頭，可以按升序或降序對清單進行排序。 |
| **[!UICONTROL 運行時間]** | 運行查詢所花費的時間。 |

## 憑據

的 **[!UICONTROL 憑據]** 頁籤同時顯示過期和未過期的憑據。 有關如何使用這些憑據與外部客戶端連接的詳細資訊，請閱讀 [憑據指南](../clients/overview.md)。

![突出顯示了「憑據」頁籤的「查詢」儀表板。](../images/ui/overview/credentials.png)

## 後續步驟

現在你已經熟悉了 [!DNL Query Service] 用戶介面 [!DNL Platform]，您可以 [!DNL Query Editor] 開始建立您自己的查詢項目以與組織中的其他用戶共用。 有關在中創作和運行查詢的詳細資訊 [!DNL Query Editor]，請參見 [[!DNL Query Editor] 使用手冊](./user-guide.md)。