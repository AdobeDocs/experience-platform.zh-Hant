---
keywords: 事件轉發擴展；mixpanel;mixpanel事件轉發擴展
title: 混合面板跟蹤事件API事件轉發擴展
description: 此Adobe Experience Platform事件轉發擴展將Adobe體驗邊緣網路事件發送到Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件轉發擴展

[[!DNL Mixpanel]](https://www.mixpanel.com) 是一種產品分析工具，允許您捕獲有關用戶如何與數字產品交互的資料。 您可以使用簡單的互動式報告來分析產品資料，這樣您只需按一下幾下即可查詢和可視化資料。 [!DNL Mixpanel] 旨在通過讓每個人都能夠即時分析用戶資料來識別趨勢、瞭解用戶行為並就您的產品做出決策，提高團隊的效率。

[!DNL Mixpanel] 採用基於事件的以用戶為中心的模型，將每個交互連接到單個用戶。 的 [!DNL Mixpanel] 資料模型建立在用戶、事件和屬性的概念上。

>[!NOTE]
>
>請參閱 [!DNL Mixpanel] 文檔 [身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) 瞭解如何 [!DNL Mixpanel] 合併事件以建立標識群集。 還建議您在 [不同ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) 瞭解如何使用它們來識別事件資料中的用戶。

## 使用案例

如果要使用中的邊緣網路中的資料，應使用此擴展 [!DNL Mixpanel] 利用其產品分析功能。

例如，請考慮具有多渠道業務（網站和移動）的零售組織。 該組織將事務性或會話性輸入作為事件資料從其平台中捕獲，並將其載入到 [!DNL Mixpanel] 使用事件轉發擴展。

然後，分析團隊可以利用 [!DNL Mixpanel's] 用於處理資料集和獲取業務洞察力的功能，這些洞察力可用於生成圖形、儀表板或其他可視化內容，以通知業務相關方。

有關特定於 [!DNL Mixpanel]，請參閱以下文檔：

* [新到 [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [什麼是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12次必試 [!DNL Mixpanel] 特徵](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] 先決條件 {#prerequisites-mixpanel}

您必須具有 [!DNL Mixpanel] 帳戶以使用此分機。 轉到 [[!DNL Mixpanel] 註冊頁](https://mixpanel.com/register/) 註冊並建立帳戶。

確保 [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 已為項目啟用設定。 導航到 **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** 切換設定。

### 瞭解中的標識群集 [!DNL Mixpanel]

在 [!DNL Mixpanel]，標識群集包含 `distinct_id` 連接到單個用戶的值。 [!DNL Mixpanel] 處理每個用戶的標識群集，解析單個規範 `distinct_id` 從每個要在報告中使用的群集。 您還可以包括您自己的標識符（稱為本地標識符） `distinct_id`)，用於在用戶標識事件之前發生的匿名事件。

[!DNL Mixpanel] 通過兩種方法解析身份群集：

* **識別** : [!DNL Mixpanel] 將所選標識符連接到匿名 `distinct_id`。 如果您的網站 [!DNL Mixpanel] 啟用SDK，平台將使用 `distinct_id` 分配給當前登錄的用戶。
* **別名**: [!DNL Mixpanel] 合併兩個非匿名 `distinct id`如果滿足附加合併條件，則合併。

>[!NOTE]
>
>請參閱 [!DNL Mixpanel] 文檔 [身份管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) 的子菜單。
>
>確認已啟用 [[!DNL Mixpanel] 身份合併特徵](#prerequisites-mixpanel) 確保正確解析身份群集。

### 收集所需的配置詳細資訊 {#configuration-details}

為了將Experience Platform連接到 [!DNL Mixpanel] 必須具有以下輸入：

| 鍵類型 | 說明 | 範例 |
| --- | --- | --- |
| 項目標籤 | 與您的 [!DNL Mixpanel] 帳戶。 請參閱 [!DNL Mixpanel] 文檔 [查找項目標籤](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) 的上界。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安裝和配置 [!DNL Mixpanel] 擴展 {#install}

要安裝擴展， [建立事件轉發屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

選擇 **[!UICONTROL 擴展]** 的子菜單。 在 **[!UICONTROL 目錄]** 頁籤 **[!UICONTROL 安裝]** 卡上 [!DNL Mixpanel] 擴展。

![安裝 [!DNL Mixpanel] 擴展。](../../../images/extensions/server/mixpanel/install-extension.png)

## 建立 [!DNL Send Event] 規則

開始在事件轉發屬性中建立新規則。 下 **[!UICONTROL 操作]**，添加新操作並將擴展設定為 **[!UICONTROL 混合面板]**。 下一步，將操作類型設定為 **[!UICONTROL 跟蹤事件]** 將Adobe Experience Edge Network事件發送到 [!DNL Mixpanel]。

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 項目標籤] | 此欄位應映射到與您的 [!DNL Mixpanel] 帳戶。 | 是 |
| [!UICONTROL 事件類型] | 事件名稱。 | 是 |
| [!UICONTROL 事件時間] | 事件時間。 |  |
| [!UICONTROL 混合面板不同ID] | 執行事件的用戶的唯一標識符。 |  |
| [!UICONTROL 插入ID] | 事件的唯一標識符，用於重複資料消除。 |  |
| [!UICONTROL 事件屬性] | 包含事件的自定義屬性的JSON對象。 從提供原始JSON或使用一組簡化的鍵值輸入中進行選擇。 |  |

>[!NOTE]
>
>有關的標準欄位的詳細資訊 [!DNL Mixpanel] 事件，請參閱 [正式檔案](https://developer.mixpanel.com/reference/import-events#event)。

![添加事件轉發規則操作配置。](../../../images/extensions/server/mixpanel/track-event-action.png)

一旦 [!UICONTROL 跟蹤事件] 操作將添加到規則中，您可以配置規則的條件，以便僅針對某些事件觸發該規則，或者將條件部分留空，以使規則針對所有事件觸發。

>[!IMPORTANT]
>
>如果您的網站使用 [!DNL Mixpanel] SDK，您可以繼續 [驗證資料 [!DNL Mixpanel]](#validate)。 如果不使用 [!DNL Mixpanel] SDK，必須 [建立單獨的身份跟蹤規則](#create-an-identity-tracking-rule) 確保有關事件及 `distinct_id` 值發送到 [!DNL Mixpanel] 用戶標識事件時。

## 驗證資料 [!DNL Mixpanel] {#validate}

如果實施成功並收集了事件，您將看到 [[!DNL Mixpanel] 控制台](https://help.mixpanel.com/hc/en-us/articles/4402837164948)。

檢查 [!DNL Mixpanel] 已合併用電子郵件值填充的帖子登錄事件和使用 **[!UICONTROL 發送事件]**。 如果實施正確， [!DNL Mixpanel] 將把他們和 [用戶配置檔案](https://help.mixpanel.com/hc/en-us/articles/115004501966)。

## 後續步驟

本指南介紹如何將轉換事件發送到 [!DNL Mixpanel] 使用事件轉發。 此事件轉發擴展利用 [!DNL Mixpanel] SDK和JavaScript API。 有關這些基礎技術的詳細資訊，請參閱正式文檔：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

有關Experience Platform中事件轉發功能的詳細資訊，請參閱 [事件轉發概述](../../../ui/event-forwarding/overview.md)。
