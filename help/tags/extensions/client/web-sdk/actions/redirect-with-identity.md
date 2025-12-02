---
title: 使用身分重新導向
description: 允許在貴組織的網域間共用訪客識別碼。
source-git-commit: db7e6df1b1a0eb19518d9c6ccd6e6bb9131d5a3e
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 1%

---

# 使用身分重新導向

**[!UICONTROL Redirect with identity]**&#x200B;動作型別可讓您將目前頁面的訪客識別碼分享到貴組織擁有的其他網域。 此變數專門設計為搭配點選事件和值比較條件使用。 它的功能類似於JavaScript資料庫中的[`appendIdentityToUrl`](/help/collection/js/commands/appendidentitytourl.md)命令。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Redirect with identity]**。

## 使用案例

* **跨網域識別個人**：如果訪客從某個網域點選到您組織擁有的另一個網域，您可以使用此動作，這樣他們仍會被視為同一個人。 如果您的報表結合來自多個網域的資料，避免訪客流量膨脹，此識別方法特別實用。
* **識別從行動應用程式到網頁應用程式的個人**：如果訪客進入您的行動應用程式，且他們按一下您網頁應用程式的連結，您就可以使用此動作，讓網頁SDK確認自己是同一個人。 此工作流程可為報告和個人化提供一致的體驗。

## 可用欄位

* **[!UICONTROL Instance]**：動作套用的SDK執行個體。 如果您的實作使用單一SDK例項，此下拉式功能表會停用。
* **[!UICONTROL Datastream configuration overrides]**：這個命令支援資料流設定覆寫，讓您能夠控制哪些應用程式和服務接收這個資料。 當您在個別命令和標籤延伸組態設定中設定資料流組態覆寫時，個別命令優先。 如需詳細資訊，請參閱[資料流組態覆寫](../configure/configuration-overrides.md)。

## 規則範例

這個命令通常會與特定規則搭配使用，此規則會監聽點按次數並檢查所需的網域。

+++規則事件條件

當具有`href`屬性的錨點標籤被點按時觸發。

* **[!UICONTROL Extension]**：核心
* **[!UICONTROL Event type]**：按一下
* **[!UICONTROL When the user clicks on]**：特定元素
* **[!UICONTROL Elements matching the CSS selector]**：`a[href]`

![規則事件](../assets/id-sharing-event-configuration.png)

+++

+++規則條件

僅在所需的網域上觸發。

* **[!UICONTROL Logic type]**：一般
* **[!UICONTROL Extension]**：核心
* **[!UICONTROL Condition Type]**：值比較
* **[!UICONTROL Left Operand]**：`%this.hostname%`
* **[!UICONTROL Operator]**：符合Regex
* **[!UICONTROL Right Operand]**：符合所需網域的規則運算式。 例如, `adobe.com$|behance.com$`

![規則條件](../assets/id-sharing-condition-configuration.png)

+++

+++規則動作

將身分識別附加至URL。

* **[!UICONTROL Extension]**： Adobe Experience Platform Web SDK
* **[!UICONTROL Action Type]**：使用身分重新導向

![規則動作](../assets/id-sharing-action-configuration.png)

+++
