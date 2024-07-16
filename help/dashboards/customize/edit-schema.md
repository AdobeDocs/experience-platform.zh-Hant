---
keywords: Experience Platform；使用者介面；UI；儀表板；儀表板；設定檔；區段；目的地；授權使用情況
title: 編輯結構描述以建立自訂儀表板Widget
description: 本指南提供選取屬性和設定組織結構以建立Adobe Experience Platform儀表板之自訂Widget的逐步指示。
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '499'
ht-degree: 1%

---

# 編輯結構描述以建立自訂Widget

若要建立Adobe Experience Platform儀表板的自訂Widget，您必須先識別Widget所根據的即時客戶設定檔屬性。

本指南透過選取屬性以建立自訂儀表板Widget，提供編輯組織架構的逐步指示。

選取屬性並設定結構描述後，您可以繼續進行[為您的儀表板建立自訂Widget](custom-widgets.md)的步驟。

>[!NOTE]
>
>必須授與使用者「管理標準儀表板」許可權，才能編輯結構。 如需授與儀表板存取許可權的詳細步驟，請參閱[儀表板許可權指南](../permissions.md)。

## 介面工具資料庫 {#widget-library}

本指南需要存取Experience Platform中的[!UICONTROL Widget資料庫]。 若要進一步瞭解Widget程式庫，以及如何在UI中存取它，請先閱讀[Widget程式庫概觀](widget-library.md)。

## 編輯方案

在Widget資料庫中，**[!UICONTROL 自訂]**&#x200B;標籤可讓您建立Widget並與您組織中的其他使用者共用，以自訂儀表板的外觀。

在建立自訂Widget之前，您必須選取「即時客戶設定檔」屬性，以確保資料包含在每日快照中。

>[!IMPORTANT]
>
>您的組織最多可以選取20個屬性。

如果您的組織尚未選取任何設定檔屬性，請在畫面中央選取「**[!UICONTROL 設定]**」。

![醒目提示「設定」之Widget程式庫工作區的「自訂」索引標籤。](../images/customization/configure-schema.png)

建立至少一個自訂屬性後，請選取&#x200B;**[!UICONTROL 編輯結構描述]**&#x200B;以檢視選取的屬性並新增更多屬性。

![反白顯示[編輯]結構描述之Widget程式庫工作區的[自訂]索引標籤。](../images/customization/edit-schema.png)

## 選取屬性

若要在&#x200B;**[!UICONTROL 選取聯合結構描述欄位]**&#x200B;對話方塊中選取屬性，請導覽至聯合結構描述中的屬性（或使用搜尋），並選取屬性旁的核取方塊。 選取核取方塊也會將屬性新增至對話方塊右側的&#x200B;**[!UICONTROL 選取的屬性]**&#x200B;清單。

>[!NOTE]
>
>若要讓屬性在選取時可見，它必須是下列其中一項： String、Date、Date-Time、Boolean、Short、Long、Integer或Byte。 Map和Double資料型別不受支援，且會呈現灰色，因此無法選取。

選擇您要新增的屬性後，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存您的屬性並返回自訂Widget標籤。

>[!WARNING]
>當資料重新整理時，新選取的屬性可在下一個每日快照後使用。

![選取結構描述屬性的對話方塊中反白顯示屬性和「儲存」。](../images/customization/select-attribute.png)

## 後續步驟

閱讀本指南後，您可以導覽至Widget程式庫，並選取「即時客戶個人檔案」屬性以設定您的結構。 選取設定檔屬性後，您就可以開始[為您的儀表板](custom-widgets.md)建立自訂Widget。
