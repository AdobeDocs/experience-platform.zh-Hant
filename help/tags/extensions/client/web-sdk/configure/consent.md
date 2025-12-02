---
title: 同意組態設定
description: 設定標籤擴充功能的預設同意和隱私權設定。
source-git-commit: 46e5d007b27eaa67c9ee49e35a711424de383d68
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---

# 同意組態設定

**[!UICONTROL Consent]**&#x200B;區段可讓您選取在未提供其他明確同意偏好設定時所假設的預設同意層級。 預設同意層級未儲存到使用者設定檔。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Extensions]**，然後選取&#x200B;**[!UICONTROL Configure]**&#x200B;卡片上的[!UICONTROL Adobe Experience Platform Web SDK]。
1. 向下捲動至&#x200B;**[!UICONTROL Consent]**&#x200B;區段。

![此影像顯示標籤UI中Web SDK標籤擴充功能的隱私設定](../assets/web-sdk-ext-privacy.png)

此區段包含單一選項按鈕集，可決定預設的同意層級：

* **[!UICONTROL In]**：收集在使用者提供同意偏好設定之前發生的事件。
* **[!UICONTROL Out]**：丟棄在使用者提供同意偏好設定之前發生的事件。
* **[!UICONTROL Pending]**：在使用者提供同意偏好設定之前發生的佇列事件。 取得同意時，會傳送已加入佇列的事件至Adobe。 拒絕同意時，會捨棄已加入佇列的事件。
* **[!UICONTROL Provide a data element]**：選取可決定上述其中一個組態設定的資料元素。 有效值包括字串`"in"`、`"out"`或`"pending"`。

如果您的組織需要明確的使用者同意才能收集資料，Adobe建議將預設同意設定為&#x200B;**[!UICONTROL Out]**&#x200B;或&#x200B;**[!UICONTROL Pending]**。
