---
title: 套用回應
description: 根據Edge Network的回應執行動作。
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 0%

---

# 套用回應

**[!UICONTROL Apply response]**&#x200B;動作型別可讓您根據Edge Network的回應執行各種動作。 此動作型別通常用於混合部署，其中伺服器會對Edge Network發出初始呼叫，然後此動作型別會從該呼叫取得回應，並在瀏覽器中初始化Web SDK。 使用此動作型別可減少混合個人化使用案例的使用者端載入時間。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Apply response]**。

![顯示[套用回應]動作型別的Experience Platform使用者介面影像。](../assets/apply-response.png)

## 使用案例

* **資料收集與個人化之間的手動分割**：您可以在轉譯器決定設為[時觸發](send-event.md)傳送事件`false`動作，然後讓「傳送事件完成」規則擷取Promise。 此規則中的第一個動作可以是「套用回應」。 此工作流程可讓您延遲DOM操作，直到組織自己的程式碼完成其他工作為止。
* **從Web SDK外部接收的Edge回應**：如果您使用其他資料庫與Edge Network通訊，可以允許Web SDK仍使用此動作處理來自Edge Network的回應。

## 可用欄位

此動作型別支援下列組態選項：

* **[!UICONTROL Instance]**：動作套用的SDK執行個體。 如果您的實作使用單一SDK例項，此下拉式功能表會停用。
* **[!UICONTROL Response headers]**：選取傳回物件的資料元素，該物件包含從Edge Network伺服器呼叫傳回的標頭索引鍵和值。
* **[!UICONTROL Response body]**：選取資料元素，此資料元素會傳回包含Edge Network回應所提供JSON裝載的物件。
* **[!UICONTROL Render visual personalization decisions]**：啟用此選項以自動轉譯Edge Network提供的個人化內容，並預先隱藏內容以防止閃爍。
