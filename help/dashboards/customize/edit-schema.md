---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用
title: 編輯結構以建立自訂控制面板小工具
description: 本指南提供選取屬性和設定組織結構以建立Adobe Experience Platform控制面板自訂Widget的逐步指示。
exl-id: a744eb24-5ba7-4971-9183-3f891e807863
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 編輯架構以建立自訂小工具

若要建立Adobe Experience Platform控制面板的自訂Widget，您必須先識別Widget所依據的即時客戶設定檔屬性。

本指南提供編輯組織結構的逐步指示，方法是選取屬性以建立自訂控制面板小工具。

在選取屬性並設定結構後，您可以繼續進行 [建立控制面板的自訂小工具](custom-widgets.md).

>[!NOTE]
>
>必須授予使用者「管理標準控制面板」權限，才能編輯結構。 有關授予控制面板存取權限的步驟，請參閱 [控制面板權限指南](../permissions.md).

## 介面工具集程式庫 {#widget-library}

本指南需要存取 [!UICONTROL 介面工具集程式庫] Experience Platform。 若要進一步了解Widget程式庫，以及如何在UI中存取，請先閱讀 [介面工具集程式庫概述](widget-library.md).

## 編輯方案

在介面工具集程式庫內， **[!UICONTROL 自訂]** 索引標籤可讓您建立介面工具集並與組織中的其他使用者共用，以自訂控制面板的外觀。

在建立自定義小部件之前，必須選擇「即時客戶配置檔案」屬性以確保資料包含在每日快照中。

>[!IMPORTANT]
>
>您的組織最多可選取20個屬性。

如果您的組織尚未選取任何設定檔屬性，請從選取 **[!UICONTROL 設定]** 在螢幕中央。

![醒目提示「配置」時，介面工具集庫工作區的「自訂」標籤。](../images/customization/configure-schema.png)

至少已建立一個自定義屬性時，請選擇 **[!UICONTROL 編輯結構]** 查看所選屬性並添加更多屬性。

![介面工具集庫工作區的「自訂」標籤會反白顯示「編輯」結構。](../images/customization/edit-schema.png)

## 選取屬性

若要在 **[!UICONTROL 選擇聯合架構欄位]** 對話框，導航到聯合架構中的屬性（或使用搜索），並選中該屬性旁的複選框。 選取核取方塊也會將屬性新增至 **[!UICONTROL 所選屬性]** 清單。

>[!NOTE]
>
>為了讓屬性可見以供選取，它必須是下列其中一項：字串、日期、日期時間、布林值、短、長、整數或位元組。 地圖和雙重資料類型不受支援，且呈現灰色，因此無法選取。

選擇要添加的屬性後，請選擇 **[!UICONTROL 儲存]** 以保存屬性並返回「自定義小工具」頁簽。

>[!WARNING]
>重新整理資料後，新選取的屬性將可在下次每日快照後使用。

![用於選擇具有屬性的架構屬性並突出顯示「保存」的對話框。](../images/customization/select-attribute.png)

## 後續步驟

閱讀本指南後，您可以導覽至介面工具集資料庫，並選取「即時客戶設定檔屬性」來設定您的結構。 選取設定檔屬性後，您就可以開始 [建立控制面板的自訂小工具](custom-widgets.md).
