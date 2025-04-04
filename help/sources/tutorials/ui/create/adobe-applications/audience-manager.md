---
keywords: Experience Platform；首頁；熱門主題；Audience Manager來源聯結器；Audience Manager；audience Manager聯結器
title: 在使用者介面中建立Adobe Audience Manager Source連線
description: 本教學課程將逐步帶您瞭解如何建立Adobe Audience Manager的來源連線，以便使用使用者介面將消費者體驗事件資料匯入Experience Platform。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '590'
ht-degree: 1%

---

# 在UI中建立Adobe Audience Manager來源連線

本教學課程將逐步帶您瞭解如何建立Adobe Audience Manager的來源聯結器，以便使用使用者介面將消費者體驗事件資料匯入Experience Platform。

## 建立與Adobe Audience Manager的來源連線

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 [!UICONTROL 目錄]畫面會顯示您可以用來建立帳戶的各種來源。

您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋列來尋找您要使用的特定來源。

在[!UICONTROL Adobe應用程式]下，選取&#x200B;**[!UICONTROL Adobe Audience Manager]**，然後選取&#x200B;**[!UICONTROL 設定]**。

![目錄](../../../../images/tutorials/create/aam/catalog.png)

### 選取特徵和區段

>[!NOTE]
>
>您無法從Audience Manager來源將地區資料擷取至Experience Platform。 如果您有需要地區資料的Analytics使用案例，請使用[Analytics來源聯結器](../adobe-applications/analytics.md)。

[!UICONTROL 選取特徵和區段]步驟隨即顯示，為您提供互動式介面，讓您探索和選取特徵、區段和資料。

* 介面的左側面板包含[!UICONTROL 選取特徵和區段]選項，以及所有可用區段的階層式目錄。
* 介面的右半部分可讓您與選取的區段互動，並挑選您要使用的特定資料。

![新增資料](../../../../images/tutorials/create/aam/add-data.png)

若要導覽可用區段，請從「[!UICONTROL 所有區段]」面板選取您要存取的資料夾。 選取資料夾可讓您周游資料夾的階層，並提供您要篩選的區段清單。

![區段資料夾](../../../../images/tutorials/create/aam/segment-folder.png)

當您識別並選取要使用的區段後，右側會出現一個新面板，顯示您選取的專案清單。 您可以繼續存取不同的資料夾，並為您的連線選取不同的區段。 選取更多區段會更新右側的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，您可以選取「**[!UICONTROL 選取所有區段]**」和「**[!UICONTROL 選取所有特徵]**」方塊。 選取所有區段會將Audience Manager區段引進Experience Platform，而選取所有特徵則會從Audience Manager啟用所有第一方特徵。

>[!WARNING]
>
>當您使用Audience Manager來源首次將Audience Manager區段傳送至Experience Platform時，大量的Audience Manager區段母體的擷取會直接影響您的總設定檔計數。 這表示選取所有區段可能會導致設定檔計數超過您的授權使用權益。 請先檢閱您的[授權使用量](../../../../../dashboards/guides/license-usage.md)，然後再繼續。

完成後，請選取&#x200B;**[!UICONTROL 下一步]**

![所有區段](../../../../images/tutorials/create/aam/all-segments.png)

[!UICONTROL 檢閱]步驟隨即顯示，可讓您在選取的特徵和區段連線至Experience Platform之前，先檢閱這些特徵和區段。 詳細資料會分組到以下類別中：

* **[!UICONTROL 連線]**：顯示來源平台和連線的狀態。
* **[!UICONTROL 選取的資料]**：顯示選取的區段數和啟用的特徵數。

![檢閱](../../../../images/tutorials/create/aam/review.png)

檢閱您的資料流後，請選取&#x200B;**[!UICONTROL 完成]**，並等待一些時間來建立資料流。

## 後續步驟

當Audience Manager資料流作用中時，傳入的資料會自動擷取到即時客戶個人檔案中。 您現在可以利用這些傳入資料，並使用Experience Platform Segmentation Service建立對象區段。 如需更多詳細資訊，請參閱下列檔案：

* [即時客戶輪廓概觀](../../../../../profile/home.md)
* [Segmentation Service概述](../../../../../segmentation/home.md)
