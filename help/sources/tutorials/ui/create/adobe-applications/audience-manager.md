---
keywords: Experience Platform；首頁；熱門主題；Audience Manager源連接器；Audience Manager;Audience Manager連接器
solution: Experience Platform
title: 在UI中建立Adobe Audience Manager來源連線
topic-legacy: overview
type: Tutorial
description: 本教學課程會逐步帶您建立來源連接器，供Adobe Audience Manager使用，以使用使用者介面將消費者體驗事件資料匯入平台。
exl-id: 90c4a719-aaad-4687-afd8-7a1c0c56f744
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---

# 在UI中建立Adobe Audience Manager來源連線

本教學課程會逐步帶您建立來源連接器，供Adobe Audience Manager使用，以使用使用者介面將消費者體驗事件資料匯入平台。

## 建立與Adobe Audience Manager的來源連線

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 [!UICONTROL Catalog]畫面會顯示各種來源，您可以用來建立帳戶。

在[!UICONTROL Adobe applications]類別下，選擇&#x200B;**[!UICONTROL Adobe Audience Manager]**，然後選擇&#x200B;**[!UICONTROL Configure]**。

![目錄](../../../../images/tutorials/create/aam/catalog.png)

出現[!UICONTROL Select traits and segments]步驟，提供您互動式介面來探索並選取您的特徵、區段和資料。

* 介面的左側面板包含[!UICONTROL Select traits and segments]選項，以及可供您使用的所有區段的階層式目錄。
* 介面的右半部分可讓您與選取的區段互動，並挑選您要使用的特定資料。

![添加資料](../../../../images/tutorials/create/aam/add-data.png)

若要導覽可用區段，請從[!UICONTROL All Segments]面板選取您要存取的資料夾。 選取資料夾可讓您遍歷資料夾的階層，並提供要篩選的區段清單。

![segment-folder](../../../../images/tutorials/create/aam/segment-folder.png)

在您識別並選取要使用的區段後，右側會出現新面板，顯示您選取的項目清單。 您可以繼續存取不同的資料夾，並為連線選取不同的區段。 選取更多區段會更新右側的面板。

![select-data](../../../../images/tutorials/create/aam/select-data.png)

或者，您也可以選擇&#x200B;**[!UICONTROL Select all segments]**&#x200B;和&#x200B;**[!UICONTROL Select all traits]**&#x200B;框。 選取所有區段會將Audience Manager區段帶入「平台」，而選取所有特徵會啟用Audience Manager的所有第一方特徵。

完成後，選擇&#x200B;**[!UICONTROL Next]**

![所有區段](../../../../images/tutorials/create/aam/all-segments.png)

出現[!UICONTROL Review]步驟，讓您在選取的特性和區段連線至平台之前先加以檢閱。 詳細資訊會分組在下列類別中：

* **[!UICONTROL Connection]**:顯示源平台和連接狀態。
* **[!UICONTROL Selected data]**:顯示選取的區段和啟用的特徵數。

![審查](../../../../images/tutorials/create/aam/review.png)

複查資料流後，請選擇&#x200B;**[!UICONTROL Finish]**&#x200B;並為建立資料流留出一些時間。

## 後續步驟

當Audience Manager資料流處於活動狀態時，傳入的資料會自動被吸收到即時客戶配置檔案中。 您現在可以利用此傳入資料，並使用「平台區隔服務」來建立觀眾區隔。 如需詳細資訊，請參閱下列檔案：

* [即時客戶個人檔案總覽](../../../../../profile/home.md)
* [區段服務概觀](../../../../../segmentation/home.md)
