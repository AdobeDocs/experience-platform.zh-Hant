---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用
title: 編輯結構以建立自訂控制面板小工具
description: '本指南提供選取屬性和設定組織結構以建立Adobe Experience Platform控制面板自訂Widget的逐步指示。 '
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# 編輯架構以建立自訂小工具

若要建立Adobe Experience Platform控制面板的自訂Widget，您必須先識別Widget所依據的即時客戶設定檔屬性。

本指南提供編輯組織結構的逐步指示，方法是選取屬性以建立自訂控制面板小工具。

選取屬性並設定結構後，您可以繼續進行[為控制面板](custom-widgets.md)建立自訂Widget的步驟。

>[!NOTE]
>
>必須授予使用者「管理標準控制面板」權限，才能編輯結構。 有關授予控制面板存取權限的步驟，請參閱[控制面板權限指南](../permissions.md)。

## 介面工具集程式庫 {#widget-library}

本指南需要存取Experience Platform內的[!UICONTROL Widget程式庫]。 若要進一步了解Widget程式庫，以及如何在UI中存取，請先閱讀[Widget程式庫概述](widget-library.md)開始。

## 編輯方案

在介面工具集程式庫中， **[!UICONTROL Custom]**&#x200B;標籤可讓您建立介面工具集，並與組織中的其他使用者共用介面工具集，以便自訂控制面板的外觀。

在建立自定義小部件之前，必須選擇「即時客戶配置檔案」屬性以確保資料包含在每日快照中。

>[!IMPORTANT]
>
>您的組織最多可選取20個屬性。

如果您的組織尚未選取任何設定檔屬性，請從介面工具集程式庫右上角的選取&#x200B;**[!UICONTROL 編輯結構]**&#x200B;開始。

至少已建立一個自定義屬性時，選擇&#x200B;**[!UICONTROL 編輯架構]**&#x200B;以查看所選屬性並添加更多屬性。

![](../images/customization/edit-schema.png)

## 選取屬性

要在&#x200B;**[!UICONTROL 選擇聯合架構欄位]**&#x200B;對話框中選擇屬性，請導航到聯合架構中的屬性（或使用搜索），然後選擇該屬性旁的複選框。 選中該複選框還會將該屬性添加到對話框右側的&#x200B;**[!UICONTROL 選定屬性]**&#x200B;清單中。

>[!NOTE]
>
>為了讓屬性可見以供選取，它必須是下列其中一項：字串、日期、日期時間、布林值、短、長、整數或位元組。 地圖和雙重資料類型不受支援，且呈現灰色，因此無法選取。

選擇要添加的屬性後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存屬性並返回自定義小工具頁簽。

>[!WARNING]
>重新整理資料後，新選取的屬性將可在下次每日快照後使用。

![](../images/customization/select-attribute.png)

## 後續步驟

閱讀本指南後，您可以導覽至介面工具集資料庫，並選取「即時客戶設定檔屬性」來設定您的結構。 選取設定檔屬性後，您就可以開始[建立控制面板的自訂小工具](custom-widgets.md)。