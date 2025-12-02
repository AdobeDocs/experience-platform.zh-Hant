---
title: 設定同意
description: 設定訪客的所需同意。
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# 設定同意

**[!UICONTROL Set consent]**&#x200B;動作會判斷標籤擴充功能是否應該傳送資料（選擇加入）、捨棄資料（選擇退出）或使用[預設同意](../configure/consent.md) （同意不明）。 當使用者允許或拒絕您的網站同意時，您可以使用此動作將其偏好設定與標籤擴充功能同步。 此動作的JavaScript程式庫同等專案是[`setConsent`](/help/collection/js/commands/setconsent.md)命令。

1. 使用您的Adobe ID憑證登入[experience.adobe.com](https://experience.adobe.com)。
1. 導覽至&#x200B;**[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**。
1. 選取所需的標籤屬性。
1. 導覽至&#x200B;**[!UICONTROL Rules]**，然後選取所需的規則。
1. 在[!UICONTROL Actions]下，選取現有動作或建立動作。
1. 將[!UICONTROL Extension]下拉式欄位設為&#x200B;**[!UICONTROL Adobe Experience Platform Web SDK]**，然後將[!UICONTROL Action type]設為&#x200B;**[!UICONTROL Set consent]**。

標籤擴充功能支援下列標準：

* **[Adobe standard](/help/landing/governance-privacy-security/consent/adobe/overview.md)**：同時支援1.0和2.0標準。
* **[IAB透明與同意架構](/help/landing/governance-privacy-security/consent/iab/overview.md)**：若您使用此標準，若您的實作已正確設定，訪客的即時客戶設定檔會以同意資訊更新：
   1. XDM個別設定檔結構描述包含[IAB TCF 2.0同意欄位群組](/help/xdm/field-groups/profile/iab.md)。
   1. 體驗事件結構描述包含[IAB TCF 2.0同意欄位群組](/help/xdm/field-groups/event/iab.md)。

Adobe建議您個別儲存任何同意對話方塊偏好設定，例如儲存在資料元素中。 標籤擴充功能無法提供擷取同意的方式。 若要確保使用者偏好設定與標籤擴充功能保持同步，您可以在每次載入頁面時執行此操作。

## 可用欄位

此動作型別支援下列組態選項：

* **[!UICONTROL Instance]**：動作套用的SDK執行個體。 如果您的實作使用單一SDK例項，此下拉式功能表會停用。
* **[!UICONTROL Identity map]**：資料元素，可控制ECID的產生方式以及同意資訊繫結至哪些ID。
* **[!UICONTROL Consent information]**：決定您要填寫表單，或提供包含同意資訊的資料元素。
* **[!UICONTROL Standard]**：您要使用的同意標準。 可用的選項包括&#39;[!UICONTROL Adobe]&#39;和&#39;[!UICONTROL IAB TCF]&#39;。
* **[!UICONTROL Version]**：您要使用的同意標準版本。
* **[!UICONTROL Datastream configuration overrides]**：這個命令支援資料流設定覆寫，讓您能夠控制哪些應用程式和服務接收這個資料。 當您在個別命令和標籤延伸組態設定中設定資料流組態覆寫時，個別命令優先。 如需詳細資訊，請參閱[資料流組態覆寫](../configure/configuration-overrides.md)。

## 建立更新同意資訊的規則

使用此動作的理想時機是當客戶的同意偏好設定已變更時。 您可以建立標籤規則來監聽此變更。

1. 在標籤屬性中，導覽至&#x200B;**[!UICONTROL Rules]**&#x200B;並選取&#x200B;**[!UICONTROL Add rule]**。
1. 為規則指定所需的名稱，然後選取`+`旁的&#39;**[!UICONTROL Events]**&#39;圖示。
1. 在左側設定下列屬性：
   * **[!UICONTROL Extension]**：[!UICONTROL Core]
   * **[!UICONTROL EVent type]**：[!UICONTROL Custom code]
1. 開啟右側的編輯器，並使用下列程式碼作為範本：

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. 選擇「**[!UICONTROL Keep changes]**」。

上述自訂程式碼區塊有兩個作用：

* 同意偏好設定變更時觸發規則。
* 設定兩個資料元素： **IAB TCF同意字串**&#x200B;和&#x200B;**IAB TCF同意GDPR**。

設定&#39;[!UICONTROL Set Consent]&#39;動作時，這些資料元素很有用：

1. 選取`+`旁的&#39;**[!UICONTROL Actions]**&#39;圖示。
1. 在左側設定下列屬性：
   * **[!UICONTROL Extension]**：[!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**：[!UICONTROL Set consent]
1. 在右側設定下列屬性：
   * **[!UICONTROL Standard]**：[!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**：[!UICONTROL 2.0]
   * **[!UICONTROL Value]**：`%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**： [!UICONTROL Provide a data element]，值為`%IAB TCF Consent GDPR%`

![IAB設定同意動作](../assets/iab-action.png)

>[!NOTE]
>
>您無法使用資料元素選擇器來選擇這些資料元素，因為它們是透過自訂程式碼建立的。 您必須輸入有百分比符號的資料元素名稱。
