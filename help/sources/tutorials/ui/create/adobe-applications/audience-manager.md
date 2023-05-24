---
keywords: Experience Platform；首頁；熱門主題；受眾管理器源連接器；Audience Manager；受眾管理器連接器
title: 在UI中建立Adobe Audience Manager源連接
description: 本教程將指導您完成建立源連接的步驟，以便Adobe Audience Manager使用用戶介面將消費者體驗事件資料引入平台。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 0%

---

# 在UI中建立Adobe Audience Manager源連接

本教程將指導您完成為Adobe Audience Manager建立源連接器的步驟，以便使用用戶介面將消費者體驗事件資料引入平台。

## 建立與Adobe Audience Manager的源連接

在平台UI中，選擇 **[!UICONTROL 源]** 從左側導航 [!UICONTROL 源] 工作區。 的 [!UICONTROL 目錄] 螢幕顯示可建立帳戶的各種源。

可以從螢幕左側的目錄中選擇相應的類別。 或者，您可以使用搜索欄找到要使用的特定源。

下 [!UICONTROL Adobe應用程式]選中 **[!UICONTROL Adobe Audience Manager]** ，然後選擇 **[!UICONTROL 設定]**。

![目錄](../../../../images/tutorials/create/aam/catalog.png)

### 選擇特徵和段

>[!NOTE]
>
>無法將區域資料從Audience Manager源接收到Experience Platform。 如果您有分析使用需要區域資料的案例，請使用 [分析源連接器](../adobe-applications/analytics.md)。

的 [!UICONTROL 選擇特徵和段] 步驟，提供互動式介面來瀏覽和選擇您的特徵、段和資料。

* 介面的左面板包含 [!UICONTROL 選擇特徵和段] 選項，以及所有可用段的分層目錄。
* 介面的右半部分允許您與選定的段交互，並通過要使用的特定資料進行選擇。

![添加資料](../../../../images/tutorials/create/aam/add-data.png)

要瀏覽可用段，請從 [!UICONTROL 所有段] 的子菜單。 選擇資料夾允許您遍歷資料夾的層次結構，並提供要篩選的段清單。

![段資料夾](../../../../images/tutorials/create/aam/segment-folder.png)

確定並選擇要使用的段後，右側將出現一個新面板，顯示選定項的清單。 您可以繼續訪問不同的資料夾，並為連接選擇不同的段。 選擇更多段將更新右側的面板。

![選擇資料](../../../../images/tutorials/create/aam/select-data.png)

或者，可以選取 **[!UICONTROL 選擇所有段]** 和 **[!UICONTROL 選擇所有特徵]** 框。 選擇所有段將將Audience Manager段帶到平台，而選擇所有特徵將啟用所有第一方特徵來自Audience Manager。

>[!WARNING]
>
>當您首次使用Audience Manager源將Audience Manager段發送到平台時，大量Audience Manager段的接收會直接影響您的總配置檔案計數。 這意味著選擇所有段可能會導致配置檔案計數超過許可證使用權限。 請查看 [許可證使用許可](../../../../../dashboards/guides/license-usage.md) 才能繼續。

完成後，選擇 **[!UICONTROL 下一個]**

![所有段](../../../../images/tutorials/create/aam/all-segments.png)

的 [!UICONTROL 審閱] 步驟，允許您在選定的特徵和段連接到平台之前查看它們。 詳細資訊按以下類別分組：

* **[!UICONTROL 連接]**:顯示源平台和連接的狀態。
* **[!UICONTROL 所選資料]**:顯示選定段和啟用的特徵數。

![審查](../../../../images/tutorials/create/aam/review.png)

查看資料流後，選擇 **[!UICONTROL 完成]** 並為建立資料流留出一些時間。

## 後續步驟

當Audience Manager資料流處於活動狀態時，傳入資料將自動被插入即時客戶配置檔案。 您現在可以使用此傳入資料並使用平台分段服務建立受眾段。 有關詳細資訊，請參閱以下文檔：

* [即時客戶概要資訊概述](../../../../../profile/home.md)
* [分段服務概述](../../../../../segmentation/home.md)
