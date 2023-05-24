---
title: 郵箱擴展概述
description: 使用事件轉發來觸發Mailchimp電子郵件。
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bfbad3c11df64526627e4ce2d766b527df678bca
workflow-type: tm+mt
source-wordcount: '1303'
ht-degree: 5%

---

# Mailchimp事件轉發擴展概述

>[!NOTE]
>  
>Adobe Experience Platform Launch已被改名為Adobe Experience Platform的一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

《郵編》 [事件轉發](../../../ui/event-forwarding/overview.md) 擴展將事件發送到Mailchimp Marketing API，該API可觸發Mailchimp營銷活動、旅程或交易的電子郵件。

本文檔介紹如何使用「添加事件」操作設定擴展和配置規則。

## 先決條件

本文檔假定您熟悉擴展使用的相關Mailchimp產品。 有關詳細資訊，請參閱Mailchimp幫助文檔， [活動](https://mailchimp.com/help/getting-started-with-campaigns/)。 [乘](https://mailchimp.com/help/about-customer-journeys/), [交易](https://mailchimp.com/help/transactional/)。

需要Mailchimp帳戶才能使用此擴展。 您可以註冊帳戶 [這裡](https://login.mailchimp.com/signup/)。 在Mailchimp帳戶控制板中，記下以下值以供本指南使用：

- 您的Mailchimp域前置詞
- 您的API密鑰
- 受眾ID
- 預設「發件人」電子郵件地址

根據您的Mailchimp帳戶計畫，您對Mailchimp客戶行程工具的訪問可能有限。

>[!TIP]
>  
>如果您使用的是Mailchimp自動化，如事務性電子郵件或客戶旅程，則步驟和螢幕可能與此處列出的步驟和螢幕稍有不同。 但是，您仍需要相同的資訊才能使用此擴展，如上所述。 查看 [Mailchimp幫助中心](https://mailchimp.com/help/) 有關您特定帳戶和計畫的這些值的詳細資訊。

### 域前置詞

登錄到Mailchimp並登錄到「儀表板」視圖後，瀏覽器的地址欄應顯示類似 `https://us11.admin.mailchimp.com` 或者 `us11.admin.mailchimp.com`。 在此示例中，前置詞 `us11` 只是一個佔位符，您的值將不同。 用前置詞記錄URL，以便稍後執行步驟。

### API密鑰

要查找帳戶的API密鑰，請在Mailchimp UI中選擇您的配置檔案表徵圖，然後選擇 **配置檔案**。 您應看到類似 `https://us11.admin.mailchimp.com/account/profile/` 但 **你** 前置詞 `us11`。

選擇 **額外**，則 **API密鑰**:

![額外菜單、API密鑰連結](../../../images/extensions/server/mailchimp/menu-API-keys.png)

下 **您的API密鑰**，可以選擇現有鍵或 **建立密鑰** 的雙曲餘切值。 您可以建立一個新密鑰，以專門用於此擴展。 複製API密鑰並保存以備稍後的步驟。 有關詳細資訊，請參閱Mailchimp文檔，瞭解如何 [生成API密鑰](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key)。

### 受眾ID和發件人地址

選擇 **觀眾** 的 **受眾儀表板**。 接下來，選擇要與此擴展一起使用的受眾。 要瞭解更多資訊，請參閱上的Mailchimp文檔 [建立受眾](https://mailchimp.com/help/create-audience/)。

建立並選擇受眾後，選擇 **管理受眾** 下拉清單 **設定**。 此螢幕顯示觀眾的各種設定。

在「設定」螢幕的底部，您應看到 `Unique id for audience [audience name]` 何處 `[audience name]` 是你實際聽眾的名字。 複製「受眾ID」並保存以備稍後的步驟。

選擇 **受眾名稱和預設值** 並確認 **預設發件人電子郵件地址** 對您的市場活動具有正確的價值。 請注意，「受眾ID」也列在此頁頂部，與您在上一步驟中複製的值相同。

## 郵件自動化

根據您的Mailchimp計畫以及您是否使用事務性電子郵件、客戶行程還是其他Mailchimp自動化，您的特定行程設定可能會有所不同。

>[!IMPORTANT]
>  
>您選擇在Mailchimp中觸發自動化或行程的事件名稱與您必須使用此擴展發送的事件名稱相同。 在Mailchimp自動化中記錄事件名稱，並保存它以備稍後的步驟。

## 安裝和設定

本節列出安裝和配置擴展的步驟。 要安全地保存Mailchimp API密鑰，必須使用事件轉發 [秘密](../../../ui/event-forwarding/secrets.md)。

### 建立機密和資料元素

在事件轉發屬性中， [建立 [!UICONTROL 令牌] 秘密](../../../ui/event-forwarding/secrets.md#token) 調用 `Mailchimp API Key`。

下一個， [建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 擴展和 [!UICONTROL 秘密] 引用的資料元素類型 `Mailchimp API Key` 你剛剛創造的秘密。 輸入 `Mailchimp Token` 作為資料元素名稱。

### 安裝並設定 擴充功能

在同一事件轉發屬性中，選擇 **[!UICONTROL 擴展]。** 然後 **[!UICONTROL 目錄]** 顯示可用於安裝的擴展。 在此處搜索Mailchimp擴展並選擇 **[!UICONTROL 安裝]**。

![安裝Mailchimp擴展](../../../images/extensions/server/mailchimp/install.png)

出現配置螢幕。 下 **[!UICONTROL 郵箱伺服器前置詞域名]**，輸入您以前從Mailchimp帳戶複製的域，包括您唯一的域前置詞。

>[!IMPORTANT]
>
>不包括 `http://` 或 `https://` 的子菜單。

![擴充功能組態](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

下 **[!UICONTROL 郵件令牌]**，選擇資料元素表徵圖，然後選擇 `Mailchimp Token` 建立的資料元素。 選擇 **[!UICONTROL 保存]** 的子菜單。

現在，擴展已安裝並配置為在屬性中使用。

## 資料收集

在 [規則](../../../ui/managing-resources/rules.md)，每個事件中都有多個資料值被擴展發送到Mailchimp。 對於典型的實施，您可以配置 [Adobe Experience PlatformWeb SDK擴展](../../client/sdk/overview.md) 將資料發送到 [!DNL Platform Edge Network] 以供擴展在事件轉發屬性中使用。

此擴展所需的資料可以從Web SDK以XDM資料或非XDM資料的形式發送。 請參閱文檔以瞭解有關 [發送XDM資料](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data)。

例如，如果客戶在您的站點上購買或註冊某個事件，您可以通過帶有此擴展的Mailchimp發送確認電子郵件。 一旦您將所需資訊從Web SDK發送到邊緣網路，擴展將使用Mailchimp觸發電子郵件。

![添加事件操作配置](../../../images/extensions/server/mailchimp/action-configurations.png)

### 資料元素

上一節的螢幕快照顯示您可以隨每個事件從此擴展發送到Mailchimp的資料。 配置Web SDK將此資料發送到邊緣網路後，可以在事件轉發屬性中建立資料元素，以便擴展可以訪問這些值。

下表提供了每個可能值的更多詳細資訊。

| 名稱 | 示例路徑 | 類型 | 說明 | 必填 | 限制 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> 或<br /> `arc.event.data._tenant.emailId` | 字串 | 接收電子郵件的地址 | **是** | 必須存在於郵件群體中 |
| `listId` | `arc.event.xdm._tenant.listId`<br /> 或<br /> `arc.event.data._tenant.listid` | 字串 | 受眾ID | **是** | 必須與現有受眾ID匹配 |
| `name` | `arc.event.xdm._tenant.name`<br /> 或<br /> `arc.event.data._tenant.name` | 字串 | 事件名稱 | **是** | 長度為2-30個字元 |
| `properties` | `arc.event.xdm._tenant.properties`<br /> 或<br /> `arc.event.data._tenant.properties` | 物件 | JSON格式的可選屬性清單，其中包含有關事件的詳細資訊 | 無 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> 或<br /> `arc.event.data._tenant.isSyncing` | 布林值 | 建立的事件 `is_syncing` 設定為 `true` **不會** 觸發自動 | 無 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> 或 `arc.event.data._tenant.occuredAt` | 字串 | 事件發生時的ISO 8601時間戳 | 無 |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>的 **示例路徑** 以上值僅是示例。 欄位名和 [路徑](../../../ui/event-forwarding/overview.md#data-element-path) 這些資料元素中引用的Web SDK在屬性中可能不同，具體取決於您在上述步驟中命名和配置Web SDK的方式。

在事件轉發屬性中，可以為上述每個欄位建立資料元素。 建立後，可以引用 [!UICONTROL 添加事件] 此擴展的操作。

![添加事件操作配置](../../../images/extensions/server/mailchimp/action-configurations.png)

現在，您可以使用此擴展和「添加事件」操作來為您的受眾觸發電子郵件。

## 資料驗證

使用事件轉發擴展時， [Adobe Experience Platform調試器](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 非常有用。 在「日誌」部分的「邊緣日誌」下，您可以看到事件轉發規則在觸發後發出的請求。 以下螢幕截圖顯示擴展向Mailchimp API發出的請求。

![Adobe Experience Platform調試器](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

在「郵箱」面板中，在「受眾」或「受眾成員」的「活動源」視圖中，將提供該受眾或受眾成員的事件清單。 這應與擴展發送的事件相匹配，並顯示所發送的任何可選資料以及它們收到的電子郵件或市場活動。 查看 [Mailchimp Automation幫助指南](https://mailchimp.com/help/automation/) 的子菜單。
