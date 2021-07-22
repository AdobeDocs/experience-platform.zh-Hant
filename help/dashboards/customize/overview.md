---
keywords: Experience Platform；使用者介面；UI；控制面板；設定檔；區段；目的地
title: 控制面板自訂概述
description: 進一步了解您可以如何自訂Adobe Experience Platform控制面板中顯示的資料。
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# 控制面板自訂概觀

Adobe Experience Platform中可用的設定檔、區段和目的地控制面板，可透過多種不同方式加以自訂。 本指南提供可用自訂項目的概觀，其中包含逐步指示的連結，引導您逐步了解如何個人化控制面板中顯示的介面工具集，以及這些介面工具集的大小、形狀和位置。

>[!NOTE]
>
>無法自訂[!UICONTROL 授權使用]控制面板中顯示的介面工具集。 若要深入了解此唯一控制面板，請參閱[授權使用控制面板檔案](../guides/license-usage.md)。

## 修改控制面板

從設定檔、區段或目的地控制面板選取&#x200B;**[!UICONTROL 修改控制面板]**&#x200B;可讓您調整控制面板中目前可見的介面工具集的大小、順序和位置。 有關如何修改儀表板中小部件外觀的資訊，請參閱[修改儀表板指南](modify.md)。

## 介面工具集程式庫

Experience Platform內的介面工具集程式庫可讓您檢視組織可用的所有[standard](#standard-widgets)和[custom](#custom-widgets)介面工具集。 從控制面板（例如，設定檔控制面板），您可以選取&#x200B;**[!UICONTROL 修改控制面板]**&#x200B;以顯示&#x200B;**[!UICONTROL Widget library]**&#x200B;按鈕。

![](../images/customization/modify-dashboard.png)

選擇&#x200B;**[!UICONTROL Widget庫]**&#x200B;以開啟Widget庫並查看所有可用的標準度量或開始建立自定義Widget。

![](../images/customization/widget-library-button.png)

### 標準介面工具集 {#standard-widgets}

標準介面工具集是指Adobe提供的介面工具集，以便在控制面板中使用。 這些小工具集是唯讀的，您的組織無法編輯。

在介面工具集庫內，**[!UICONTROL Standard]**&#x200B;標籤包含Adobe提供的所有可用標準介面工具集。 您可以使用任何這些標準量度來更新控制面板。 若要進一步了解如何將標準介面工具集新增至控制面板，請參閱[使用控制面板](standard-widgets.md)中的標準介面工具集的指南。

### 自訂小工具 {#custom-widgets}

自訂小工具是指由組織成員建立和共用的小工具。 這些Widget是透過Widget資料庫的&#x200B;**[!UICONTROL Custom]**&#x200B;標籤建立的，並且需要您的組織透過使用[結構](#edit-schema)來指定可用的量度

有關建立自己的小工具的完整步驟，請參閱控制面板的[自訂小工具指南](custom-widgets.md)。

![](../images/customization/widget-library.png)

#### 編輯方案 {#edit-schema}

若要為控制面板建立[自訂Widget](#custom-widgets)，您必須先識別Widget所依據的即時客戶設定檔屬性。

有關編輯組織架構以建立自定義儀表板小部件的逐步說明，請訪問[編輯儀表板架構](edit-schema.md)的指南。

## 後續步驟

閱讀本檔案後，您就可以開始自訂Experience Platform控制面板，方法是修改現有小工具的大小、形狀和順序、新增Adobe提供的標準小工具，或建立自訂小工具並與組織共用。
