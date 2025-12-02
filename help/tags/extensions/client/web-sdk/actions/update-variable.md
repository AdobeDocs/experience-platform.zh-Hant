---
title: 更新變數
description: 修改變數資料元素的內容。
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# 更新變數

**[!UICONTROL Update variable]**&#x200B;動作可讓您對[變數資料元素](../data-element-types.md#variable)進行部分或漸進式變更。 您可以使用此動作來建立物件，以便稍後在[[!UICONTROL Send event]](send-event.md)動作中參照。 填入資料元素並將它們指派給XDM物件內的屬性，符合大部分的使用案例；此動作提供更大的彈性，可讓您根據規則條件，有條件地將屬性設定為不同的資料元素。

使用此動作之前，您必須先建立變數資料元素。 選取要修改的變數資料元素後，編輯器隨即顯示，允許您為此動作設定任何需要的欄位。

![動作設定介面中更新變數動作的熒幕擷圖](../assets/update-variable.png)

編輯器中使用的XDM結構描述符合在變數資料元素中選取的結構描述。 您可以展開物件並選取想要的屬性，來設定物件的一或多個屬性。 例如，在下方的熒幕擷圖中，`producedBy`屬性設定為資料元素`%Produced by data element%`。

![顯示更新屬性的動作設定介面熒幕擷圖](../assets/update-variable-set-property.png)

如果您選取的變數資料元素使用資料物件，而不是XDM物件，則可用欄位取決於設定資料元素時選取的產品。 例如，如果您建立包含Adobe Analytics的資料物件欄位，那麼在此UI中選取變數資料元素將提供您能填寫Adobe Analytics專屬的欄位。

![動作組態介面的熒幕擷圖，顯示以資料物件為基礎的變數資料元素](../assets/variable-data-element-data.png)
