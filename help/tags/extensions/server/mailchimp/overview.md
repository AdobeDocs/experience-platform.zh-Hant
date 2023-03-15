---
title: Mailchimp擴充功能概觀
description: 使用事件轉送功能來觸發Mailchimp電子郵件。
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

# Mailchimp事件轉送擴充功能概觀

>[!NOTE]
>  
>Adobe Experience Platform Launch在Adobe Experience Platform中已重新命名為一套資料收集技術。 因此，所有產品文件中出現了幾項術語變更。 如需術語變更的彙整參考資料，請參閱以下[文件](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html)。

Mailchimp [事件轉送](../../../ui/event-forwarding/overview.md) 擴充功能會將事件傳送至Mailchimp行銷API，可針對Mailchimp行銷活動、歷程或交易觸發電子郵件。

本檔案說明如何使用「新增事件」動作來設定擴充功能和設定規則。

## 先決條件

本檔案假設您熟悉擴充功能運用的相關Mailchimp產品。 如需詳細資訊，請參閱Mailchimp說明檔案， [行銷活動](https://mailchimp.com/help/getting-started-with-campaigns/), [歷程](https://mailchimp.com/help/about-customer-journeys/)，和 [交易](https://mailchimp.com/help/transactional/).

使用此擴充功能需要Mailchimp帳戶。 您可以註冊帳戶 [此處](https://login.mailchimp.com/signup/). 在Mailchimp帳戶控制面板中，記下下列值以供本指南使用：

- 您的Mailchimp網域首碼
- 您的API金鑰
- 對象ID
- 預設的「寄件者」電子郵件地址

根據您的Mailchimp帳戶計畫，您可能對Mailchimp客戶歷程工具的存取權限有限。

>[!TIP]
>  
>如果您使用Mailchimp自動化，例如交易電子郵件或客戶歷程，步驟和畫面可能會與此處列出的稍微不同。 不過，使用此擴充功能仍需相同的資訊，如上所述。 請參閱 [Mailchimp幫助中心](https://mailchimp.com/help/) 以取得您特定帳戶和計畫中這些值的詳細資訊。

### 網域前置詞

登入Mailchimp並登入控制面板檢視後，瀏覽器的位址列應該會顯示類似 `https://us11.admin.mailchimp.com` 或 `us11.admin.mailchimp.com`. 在此範例中，首碼 `us11` 只是預留位置，而您的值將會不同。 記錄您的URL並加上首碼，以供稍後步驟使用。

### API金鑰

若要尋找您的帳戶的API金鑰，請在Mailchimp UI中選取您的設定檔圖示，然後選取 **設定檔**. 您應該會看到 `https://us11.admin.mailchimp.com/account/profile/` 但 **您的** 前置詞而非前置詞 `us11`.

選擇 **額外**，然後 **API金鑰**:

![額外功能表、API金鑰連結](../../../images/extensions/server/mailchimp/menu-API-keys.png)

在 **您的API金鑰**，您可以選擇現有索引鍵，或選取 **建立金鑰** 來建立新的。 您可以建立新索引鍵，以專門與此擴充功能搭配使用。 複製API金鑰並儲存以供稍後步驟使用。 如需詳細資訊，請參閱Mailchimp檔案，了解如何 [產生您的API金鑰](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### 對象ID和寄件者位址

選擇 **對象** 在左側導覽中，然後 **對象儀表板**. 接下來，選取您要與此擴充功能搭配使用的對象。 若要進一步了解，請參閱 [建立對象](https://mailchimp.com/help/create-audience/).

在建立並選取對象後，選取 **管理對象** 下拉式清單，選擇 **設定**. 此畫面會顯示您對象的各種設定。

在「設定」畫面底部，您應會看到 `Unique id for audience [audience name]` where `[audience name]` 是實際對象的名稱。 複製對象ID並儲存以供後續步驟使用。

選擇 **對象名稱和預設值** 並確認 **預設寄件者電子郵件地址** 對您的促銷活動有正確的值。 請注意，「對象ID」也會列在此頁面頂端，與您在最後一個步驟中下復的值相同。

## Mailchimp自動化

根據您的Mailchimp計畫，以及您是否使用交易式電子郵件、客戶歷程或其他Mailchimp自動化，您的特定歷程設定可能會有所不同。

>[!IMPORTANT]
>  
>您選擇在Mailchimp中觸發自動化或歷程的事件名稱，與您隨此擴充功能傳送的事件名稱相同。 請記下Mailchimp自動化中的事件名稱，並儲存以供稍後步驟使用。

## 安裝和設定

本節列出安裝和設定擴充功能的步驟。 若要安全地儲存Mailchimp API金鑰，您必須使用事件轉送 [秘密](../../../ui/event-forwarding/secrets.md).

### 建立機密和資料元素

在事件轉送屬性中， [建立 [!UICONTROL 代號] 秘密](../../../ui/event-forwarding/secrets.md#token) 呼叫 `Mailchimp API Key`.

下一個， [建立資料元素](../../../ui/managing-resources/data-elements.md#create-a-data-element) 使用 [!UICONTROL 核心] 擴充功能與 [!UICONTROL 機密] 要參考的資料元素類型 `Mailchimp API Key` 你剛建立的秘密。 輸入 `Mailchimp Token` 作為資料元素名稱。

### 安裝並設定 擴充功能

在相同的事件轉送屬性中，選取 **[!UICONTROL 擴充功能],** then **[!UICONTROL 目錄]** 顯示可安裝的擴充功能。 在此搜尋Mailchimp擴充功能，然後選取 **[!UICONTROL 安裝]**.

![安裝Mailchimp擴充功能](../../../images/extensions/server/mailchimp/install.png)

設定畫面隨即顯示。 在 **[!UICONTROL Mailchimp伺服器前置詞域名]**，輸入您先前從Mailchimp帳戶複製的網域，包括您的唯一網域首碼。

>[!IMPORTANT]
>
>不包括 `http://` 或 `https://` 在此欄位中。

![擴充功能組態](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

在 **[!UICONTROL Mailchimp代號]**，請選取資料元素圖示，然後選取 `Mailchimp Token` 您先前建立的資料元素。 選擇 **[!UICONTROL 儲存]** 以儲存變更。

擴充功能現在已安裝且已設定為可在您的屬性中使用。

## 資料收集

在 [規則](../../../ui/managing-resources/rules.md)，擴充功能會透過每個事件傳送數個資料值給Mailchimp。 對於一般實作，您可以設定 [Adobe Experience Platform Web SDK擴充功能](../../client/sdk/overview.md) 將資料傳送至 [!DNL Platform Edge Network] 供擴充功能在事件轉送屬性中使用。

此擴充功能所需的資料可從Web SDK以XDM資料或非XDM資料的形式傳送。 請參閱本檔案以深入了解 [傳送XDM資料](../../../../edge/fundamentals/tracking-events.md#sending-non-xdm-data).

例如，如果客戶購買或註冊您網站上的事件，您可以透過此擴充功能的Mailchimp傳送確認電子郵件。 一旦您將必要資訊從Web SDK傳送至邊緣網路，擴充功能就會使用Mailchimp觸發電子郵件。

![新增事件動作設定](../../../images/extensions/server/mailchimp/action-configurations.png)

### 資料元素

上一節的螢幕擷圖顯示資料，您可以隨著每個事件從此擴充功能傳送至Mailchimp。 在您設定Web SDK將此資料傳送至邊緣網路後，您可以在事件轉送屬性中建立資料元素，讓擴充功能可以存取這些值。

下表提供每個可能值的詳細資訊。

| 名稱 | 範例路徑 | 類型 | 說明 | 必填 | 限制 |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> 或<br /> `arc.event.data._tenant.emailId` | 字串 | 接收電子郵件的地址 | **是** | 必須存在於Mailchimp對象中 |
| `listId` | `arc.event.xdm._tenant.listId`<br /> 或<br /> `arc.event.data._tenant.listid` | 字串 | 對象ID | **是** | 必須符合現有的對象ID |
| `name` | `arc.event.xdm._tenant.name`<br /> 或<br /> `arc.event.data._tenant.name` | 字串 | 事件名稱 | **是** | 長度為2-30個字元 |
| `properties` | `arc.event.xdm._tenant.properties`<br /> 或<br /> `arc.event.data._tenant.properties` | 物件 | JSON格式的屬性選用清單，內含事件的詳細資訊 | 無 |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> 或<br /> `arc.event.data._tenant.isSyncing` | 布林值 | 使用建立的事件 `is_syncing` 設為 `true` **不會** 觸發自動 | 無 |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> 或 `arc.event.data._tenant.occuredAt` | 字串 | 事件發生時的ISO 8601時間戳記 | 無 |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>此 **範例路徑** 以上的值僅為範例。 欄位名稱和 [路徑](../../../ui/event-forwarding/overview.md#data-element-path) 根據您在上述步驟中命名和設定Web SDK的方式，這些資料元素中參考的內容可能會在您的屬性中有所不同。

在事件轉送屬性中，您可以為上述每個欄位建立資料元素。 建立後，即可參考 [!UICONTROL 新增事件] 此擴充功能的動作。

![新增事件動作設定](../../../images/extensions/server/mailchimp/action-configurations.png)

您現在可以使用此擴充功能和「新增事件」動作，為您的對象觸發Mailchimp電子郵件。

## 資料驗證

使用事件轉送擴充功能時， [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) 非常有用。 在「記錄檔」區段的「Edge記錄檔」下方，可以查看觸發後，事件轉送規則提出的請求。 下列螢幕擷取畫面顯示擴充功能對Mailchimp API提出的要求。

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

在Mailchimp控制面板中，在對象或對象成員的活動摘要檢視上，會提供該對象或對象成員的事件清單。 這應符合擴充功能所傳送的事件，並顯示任何已傳送的選用資料，以及其收到的電子郵件或行銷活動。 請參閱 [Mailchimp自動化說明指南](https://mailchimp.com/help/automation/) 以取得更多詳細資訊。
