---
keywords: 事件轉送擴充功能；mixpanel;mixpanel事件轉送擴充功能
title: Mixpanel追蹤事件API事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Adobe Experience Edge網路事件傳送至Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
source-git-commit: 1c417744518a7ac7cfb9c65d6af8219dcbc70d46
workflow-type: tm+mt
source-wordcount: '953'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件轉送擴充功能

[[!DNL Mixpanel]](https://www.mixpanel.com) 是產品分析工具，可讓您擷取使用者與數位產品互動的相關資料。 您可以透過簡單的互動式報表來分析產品資料，只需按幾下即可查詢並視覺化資料。 [!DNL Mixpanel] 旨在讓每個人都能即時分析使用者資料，以識別趨勢、了解使用者行為，並決定您的產品，進而提高團隊的效率。

[!DNL Mixpanel] 採用以事件為基礎、以使用者為中心的模型，將每個互動連結至單一使用者。 此 [!DNL Mixpanel] 資料模型是以使用者、事件和屬性的概念為基礎所建置。

>[!NOTE]
>
>請參閱 [!DNL Mixpanel] 檔案 [身分管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management) 了解 [!DNL Mixpanel] 合併事件以建立身份群集。 此外，建議您檢閱 [不重複ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-) 了解如何在事件資料中識別使用者。

## 使用案例

如果您想要使用來自邊緣網路的資料，應使用此擴充功能。 [!DNL Mixpanel] 以運用其產品分析功能。

例如，假設零售組織有多頻道存在（網站和行動裝置）。 組織會從其平台擷取交易式或對話式輸入作為事件資料，並載入至 [!DNL Mixpanel] 使用事件轉送擴充功能。

分析團隊便可運用 [!DNL Mixpanel's] 可處理資料集並衍生業務深入分析的功能，可用來產生圖形、控制面板或其他視覺化，以通知業務利害關係人。

如需特定使用案例的詳細資訊，請參閱 [!DNL Mixpanel]，請參閱下列檔案：

* [新增至 [!DNL Mixpanel]](https://help.mixpanel.com/hc/en-us/sections/360008533532-New-to-Mixpanel)
* [什麼是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12次必試 [!DNL Mixpanel] 功能](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel] 必要條件 {#prerequisites-mixpanel}

您必須具備有效 [!DNL Mixpanel] 帳戶，以便使用此擴充功能。 前往 [[!DNL Mixpanel] 註冊頁面](https://mixpanel.com/register/) 註冊並建立帳戶（如果尚未註冊）。

確保 [[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices) 已為您的專案啟用設定。 導覽至 **[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]** 並切換設定。

### 了解 [!DNL Mixpanel]

在 [!DNL Mixpanel]，則身分叢集包含 `distinct_id` 連線至個別使用者的值。 [!DNL Mixpanel] 處理每個使用者的身分叢集，解析單一canonical `distinct_id` 從每個要用於報告的叢集。 您也可以包含自己的識別碼(稱為本機 `distinct_id`)，適用於在使用者識別事件之前發生的匿名事件。

[!DNL Mixpanel] 透過兩種方法解析身分叢集：

* **識別** : [!DNL Mixpanel] 將您選擇的標識符連接到匿名 `distinct_id`. 若您的網站具有 [!DNL Mixpanel] 啟用SDK後，Platform將使用 `distinct_id` 指派給目前登入的使用者。
* **別名**: [!DNL Mixpanel] 組合了兩個非匿名 `distinct id`若符合其他合併條件，則會一起。

>[!NOTE]
>
>請參閱 [!DNL Mixpanel] 文檔 [身分管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification) 以取得這些方法的詳細資訊。
>
>確認您已啟用 [[!DNL Mixpanel] 身分合併功能](#prerequisites-mixpanel) 以確保正確解析身份群集。

### 收集所需配置詳細資訊 {#configuration-details}

將Experience Platform連結至 [!DNL Mixpanel] 您必須具備下列輸入：

| 鍵類型 | 說明 | 範例 |
| --- | --- | --- |
| 專案代號 | 與您的 [!DNL Mixpanel] 帳戶。 請參閱 [!DNL Mixpanel] 檔案 [找到專案代號](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-) 以取得指引。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安裝並設定 [!DNL Mixpanel] 擴充功能 {#install}

若要安裝擴充功能， [建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties) 或選擇要編輯的現有屬性。

選擇 **[!UICONTROL 擴充功能]** 的下一頁。 在 **[!UICONTROL 目錄]** 索引標籤，選取 **[!UICONTROL 安裝]** 在 [!DNL Mixpanel] 擴充功能。

![安裝 [!DNL Mixpanel] 擴充功能。](../../../images/extensions/server/mixpanel/install-extension.png)

## 建立 [!DNL Send Event] 規則

開始在事件轉送屬性中建立新規則。 在 **[!UICONTROL 動作]**，新增動作並將擴充功能設為 **[!UICONTROL Mixpanel]**. 接下來，將動作類型設為 **[!UICONTROL 追蹤事件]** 若要將Adobe Experience Edge Network事件傳送至 [!DNL Mixpanel].

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 專案代號] | 此欄位應對應至與您的 [!DNL Mixpanel] 帳戶。 | 是 |
| [!UICONTROL 事件類型] | 事件名稱。 | 是 |
| [!UICONTROL 事件時間] | 事件時間。 |  |
| [!UICONTROL Mixpanel不重複ID] | 執行事件的用戶的唯一標識符。 |  |
| [!UICONTROL 插入ID] | 事件的唯一識別碼，用於重複資料刪除。 |  |
| [!UICONTROL 事件屬性] | 包含事件自訂屬性的JSON物件。 從提供原始JSON或使用簡化的鍵值輸入集進行選取。 |  |

>[!NOTE]
>
>如需 [!DNL Mixpanel] 事件，請參閱 [官方檔案](https://developer.mixpanel.com/reference/import-events#event).

![新增事件轉送規則動作設定。](../../../images/extensions/server/mixpanel/track-event-action.png)

一旦 [!UICONTROL 追蹤事件] 動作會新增至規則中，您可以設定規則的條件，使其只針對特定事件引發，或將條件區段保留為空白，讓規則為所有事件引發。

>[!IMPORTANT]
>
>若您的網站使用 [!DNL Mixpanel] SDK，您可以繼續 [在 [!DNL Mixpanel]](#validate). 如果您未使用 [!DNL Mixpanel] SDK，您必須 [建立個別身分追蹤規則](#create-an-identity-tracking-rule) 確保有適當的 `distinct_id` 值傳送至 [!DNL Mixpanel] 當發生使用者識別事件時。

## 在內驗證資料 [!DNL Mixpanel] {#validate}

如果您的實作成功且已收集事件，您會在 [[!DNL Mixpanel] 主控台](https://help.mixpanel.com/hc/en-us/articles/4402837164948).

檢查 [!DNL Mixpanel] 已合併填入電子郵件值的貼文登入事件，與使用 **[!UICONTROL 傳送事件]**. 如果實作正確， [!DNL Mixpanel] 會將它們與單一 [使用者設定檔](https://help.mixpanel.com/hc/en-us/articles/115004501966).

## 後續步驟

本指南說明如何將轉換事件傳送至 [!DNL Mixpanel] 使用事件轉送。 此事件轉送擴充功能會利用 [!DNL Mixpanel] SDK和JavaScript API。 有關這些基礎技術的詳細資訊，請參閱官方檔案：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

如需Experience Platform中事件轉送功能的詳細資訊，請參閱 [事件轉送概觀](../../../ui/event-forwarding/overview.md).
