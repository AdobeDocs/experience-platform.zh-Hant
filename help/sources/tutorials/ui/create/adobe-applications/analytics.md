---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 在UI中建立Adobe Analytics來源連接器
topic: overview
translation-type: tm+mt
source-git-commit: ac1e5dbe435d9e85e8ce3ad90c60dd31ba9248ff

---


# 在UI中建立Adobe Analytics來源連接器

本教學課程提供在UI中建立Adobe Analytics來源連接器以將消費者資料匯入Adobe Experience Platform的步驟。

## 使用Adobe Analytics建立來源連線

登入 <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> ，然後從左側導覽列選 **取Sources** ，以存取來源工作區。 「目 *錄* 」螢幕顯示可用的源，以建立綁定內連接，每個源顯示與其關聯的現有連接數。 選取 **Adobe Analytics的選項** ，然後按一下「 **檢視來源** 」，查看所有已建立的系結連線。

![](../../../../images/tutorials/create/analytics/AA-sources_catalog.png)

「來 *源* 」活動畫面會列出所有先前已建立的Adobe Analytics連線，您可以按一下「選取資料」來建 **立新連線**。

>[!NOTE] 可以建立多個源的綁定內連接以引入不同的資料。

![](/help/sources/images/tutorials/create/analytics/AA-source_activity.png)

從可用報表套裝清單中，選取您要匯入「平台」的報表套裝，然後按一下「下 **一步**」。

>[!NOTE] 每個Analytics來源連線只能選取一個報表套裝。 此外，只有一個報表套裝只能存在於一個沙盒中。

![](../../../../images/tutorials/create/analytics/AA-select_data.png)

此時 *會出現* 「檢閱」步驟，讓您在建立新的Analytics內嵌連線之前，先加以檢閱。 連接的詳細資訊按類別分組，包括：

* *來源詳細資訊*:顯示來源連線和所選報表套裝的類型。
* *目標詳細資訊*:建立其他來源連接器時，此容器會顯示來源資料所吸收的資料集，包括資料集所遵守的架構。 分析資料會自動對應並收錄至即時客戶個人檔案。

![](../../../../images/tutorials/create/analytics/AA-review.png)

## 後續步驟

建立連線後，會自動建立目標模式和資料集以包含傳入的資料。 此外，還會進行資料回填，並且會收集長達13個月的歷史資料。 當初始擷取完成時，Analytics資料並供下游平台服務（例如即時客戶個人檔案和細分服務）使用。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../../profile/home.md)
* [區段服務概觀](../../../../../segmentation/home.md)
* [資料科學工作區概觀](../../../../../data-science-workspace/home.md)
* [查詢服務概述](../../../../../query-service/home.md)

