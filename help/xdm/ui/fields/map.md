---
title: 在UI中定義對應欄位
description: 瞭解如何在Experience Platform使用者介面中定義對應欄位。
exl-id: 657428a2-f184-4d7c-b657-4fc60d77d5c6
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---

# 在使用者介面中定義對應欄位

Adobe Experience Platform可讓您完全自訂自訂Experience Data Model (XDM)類別、結構描述欄位群組和資料型別的結構。

您也可以在結構描述編輯器中定義對應欄位，以模型化和動態資料結構，或儲存索引鍵值配對的集合。

在Experience Platform使用者介面(UI)中定義新欄位時，請使用&#x200B;**[!UICONTROL 型別]**&#x200B;下拉式清單，然後從清單中選取&#x200B;**[!UICONTROL 地圖]**。

![包含反白顯示的[型別]下拉式清單和[對應]值的結構描述編輯器。](../../images/ui/fields/special/map.png)

出現[!UICONTROL 對應值型別]屬性。 [!UICONTROL 對應]資料型別需要此值。 對應的可用值為[!UICONTROL 字串]和[!UICONTROL 整數]。 從可用選項的下拉式清單中選取值。

![反白顯示[!UICONTROL 對應值型別]下拉式清單的結構描述編輯器。](../../images/ui/fields/special/map-value-type.png)

設定好子欄位後，您必須將其指派給欄位群組。 使用&#x200B;**[!UICONTROL 欄位群組]**&#x200B;下拉式功能表或搜尋欄位，然後選取&#x200B;**[!UICONTROL 套用]**。 您可以使用相同的程式繼續將欄位新增至物件，或選取[儲存]以確認您的設定。****

![正在套用的欄位群組選擇和設定的錄製。](../../images/ui/fields/special/assign-to-field-group.gif)

## 使用限制 {#restrictions}

XDM對於此資料型別的使用有下列限制：

* 對應型別必須屬於型別`object`。
* 對應型別不得有已定義的屬性（換言之，它們會定義「空白」物件）。
* 對應型別必須包含`additionalProperties.type`欄位，描述可能放置在對應中的值： `string`或`integer`。
* 多實體分段只能根據對應索引鍵而不是值來定義。
* 帳戶對象不支援地圖。

請確定您只在絕對必要時才使用對應型別欄位，因為這些欄位具有下列效能缺陷：

* 來自[Adobe Experience Platform查詢服務](../../../query-service/home.md)的回應時間，1億筆記錄會從3秒降低到10秒。
* 地圖必須少於16個索引鍵，否則可能會進一步降低。

>[!NOTE]
>
>Experience Platform UI在擷取對應型別欄位索引鍵的方式上有所限制。 雖然物件型別欄位可以展開，但地圖會顯示為單一欄位。 透過Schema Registry API建立的非字串或整數資料型別的對應欄位會顯示為&quot;[!UICONTROL 複雜]&quot;資料型別。

## 後續步驟

閱讀本檔案後，您現在可以在Experience Platform UI中定義對應欄位。 請記住，您只能使用類別和欄位群組來將欄位新增到結構描述。 若要進一步瞭解如何在UI中管理這些資源，請參閱建立和編輯[類別](../resources/classes.md)和[欄位群組](../resources/field-groups.md)的指南。

如需[!UICONTROL 結構描述]工作區功能的詳細資訊，請參閱[[!UICONTROL 結構描述]工作區概觀](../overview.md)。
