---
keywords: 事件轉送擴充功能；mixpanel；mixpanel事件轉送擴充功能
title: Mixpanel追蹤事件API事件轉送擴充功能
description: 此Adobe Experience Platform事件轉送擴充功能會將Edge Network事件傳送至Mixpanel。
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 21e2e0fa-4949-4be4-859f-d449d21d8f41
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '892'
ht-degree: 1%

---

# [!DNL Mixpanel Track Events] API事件轉送擴充功能

[[!DNL Mixpanel]](https://www.mixpanel.com)是產品分析工具，可讓您擷取使用者與數位產品互動的相關資料。 您可以使用簡單的互動式報表來分析產品資料，只要按幾下滑鼠，就能查詢資料並以視覺效果呈現。 [!DNL Mixpanel]的設計目的是讓團隊更有效率，讓每個人都能即時分析使用者資料，以找出趨勢、瞭解使用者行為，以及針對您的產品做出決策。

[!DNL Mixpanel]採用以事件為基礎、以使用者為中心的模型，將每個互動都連結到單一使用者。 [!DNL Mixpanel]資料模型是以使用者、事件和屬性的概念為基礎所建置。

>[!NOTE]
>
>請參閱有關[識別管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management)的[!DNL Mixpanel]檔案，瞭解[!DNL Mixpanel]如何合併事件以建立識別叢集。 也建議您檢閱[個不同ID](https://help.mixpanel.com/hc/en-us/articles/115004509426-Distinct-ID-Creation-JavaScript-iOS-Android-)的檔案，以瞭解如何使用它們來識別事件資料中的使用者。

## 使用案例

如果您想要使用[!DNL Mixpanel]中Edge Network的資料以利用其產品分析功能，應使用此擴充功能。

例如，假設某個零售組織擁有多頻道實體（網站和行動裝置）。 組織從其平台擷取交易式或對話式輸入作為事件資料，並使用事件轉送擴充功能將其載入到[!DNL Mixpanel]。

然後，分析團隊可以利用[!DNL Mixpanel's]功能處理資料集並取得業務深入分析，其可用於產生圖表、儀表板或其他視覺效果，以告知業務利害關係人。

如需[!DNL Mixpanel]特定使用案例的詳細資訊，請參閱下列檔案：

* [新到 [!DNL Mixpanel]](https://docs.mixpanel.com/docs)
* [什麼是 [!DNL Mixpanel]？](https://developer.mixpanel.com/docs)
* [12必須試用 [!DNL Mixpanel] 功能](https://mixpanel.com/blog/12-things-you-probably-didnt-know-you-could-do-with-mixpanel/)

## [!DNL Mixpanel]必要條件 {#prerequisites-mixpanel}

您必須擁有有效的[!DNL Mixpanel]帳戶才能使用此擴充功能。 移至[[!DNL Mixpanel] 註冊頁面](https://mixpanel.com/register/)進行註冊並建立帳戶（如果尚未建立帳戶）。

確定您的專案已啟用[[!DNL Identity Merge]](https://help.mixpanel.com/hc/en-us/articles/9648680824852-ID-Merge-Implementation-Best-Practices)設定。 導覽至「**[!DNL Settings]** > **[!DNL Project Setting]** > **[!DNL Identity Merge]**」並切換設定。

### 瞭解[!DNL Mixpanel]中的身分叢集

在[!DNL Mixpanel]中，識別叢集包含連線到個別使用者的`distinct_id`值集合。 [!DNL Mixpanel]會處理每個使用者的身分叢集，從每個叢集中解析要用於報告中的單一規範`distinct_id`。 您也可以針對在使用者識別事件之前發生的匿名事件，加入您自己的識別碼（稱為本機`distinct_id`）。

[!DNL Mixpanel]透過兩種方法解析身分叢集：

* **識別碼** ： [!DNL Mixpanel]會將您選擇的識別碼連線至匿名`distinct_id`。 如果您的網站已啟用[!DNL Mixpanel] SDK，Platform將會使用指派給目前登入之使用者的`distinct_id`。
* **別名**：如果符合其他合併條件，[!DNL Mixpanel]會將兩個非匿名`distinct id`合併在一起。

>[!NOTE]
>
>如需這些方法的詳細資訊，請參閱[識別管理](https://help.mixpanel.com/hc/en-us/articles/360041039771-Getting-Started-with-Identity-Management#user-identification)上的[!DNL Mixpanel]檔案。
>
>確認您已啟用[[!DNL Mixpanel] 識別合併功能](#prerequisites-mixpanel)，以確保識別叢集已正確解析。

### 收集必要的設定詳細資料 {#configuration-details}

若要將Experience Platform連線到[!DNL Mixpanel]，您必須有下列輸入：

| 金鑰型別 | 說明 | 範例 |
| --- | --- | --- |
| 專案權杖 | 與您的[!DNL Mixpanel]帳戶相關聯的專案權杖。 請參閱有關[尋找您的專案權杖](https://help.mixpanel.com/hc/en-us/articles/115004502806-Find-Project-Token-)的[!DNL Mixpanel]檔案以取得指引。 | `25470xxxxxxxxxxxxxxxxxxx1289` |

## 安裝並設定[!DNL Mixpanel]擴充功能 {#install}

若要安裝擴充功能，[請建立事件轉送屬性](../../../ui/event-forwarding/overview.md#properties)，或選擇現有的屬性來編輯。

在左側導覽中選取&#x200B;**[!UICONTROL 擴充功能]**。 在&#x200B;**[!UICONTROL 目錄]**&#x200B;標籤中，選取[!DNL Mixpanel]擴充功能的卡片上的&#x200B;**[!UICONTROL 安裝]**。

![正在安裝[!DNL Mixpanel]擴充功能。](../../../images/extensions/server/mixpanel/install-extension.png)

## 建立[!DNL Send Event]規則

開始在您的事件轉送屬性中建立新規則。 在&#x200B;**[!UICONTROL 動作]**&#x200B;底下，新增動作並將擴充功能設為&#x200B;**[!UICONTROL Mixpanel]**。 接著，將動作型別設定為&#x200B;**[!UICONTROL 追蹤事件]**&#x200B;以傳送Edge Network事件給[!DNL Mixpanel]。

| 輸入 | 說明 | 必填 |
| --- | --- | --- |
| [!UICONTROL 專案權杖] | 此欄位應該對應到與您[!DNL Mixpanel]帳戶關聯的專案權杖。 | 是 |
| [!UICONTROL 事件類型] | 事件名稱。 | 是 |
| [!UICONTROL 事件時間] | 事件時間。 | |
| [!UICONTROL Mixpanel相異識別碼] | 執行事件之使用者的唯一識別碼。 | |
| [!UICONTROL 插入ID] | 事件的唯一識別碼，用於重複資料刪除。 | |
| [!UICONTROL 事件屬性] | 包含事件自訂屬性的JSON物件。 從提供原始JSON或使用簡化的鍵值輸入集進行選取。 | |

>[!NOTE]
>
>如需[!DNL Mixpanel]事件之標準欄位的詳細資訊，請參閱[正式檔案](https://developer.mixpanel.com/reference/import-events#event)。

![新增事件轉送規則動作設定。](../../../images/extensions/server/mixpanel/track-event-action.png)

將[!UICONTROL 追蹤事件]動作新增至規則後，您可以設定規則的條件，使其只對特定事件引發，或者將條件區段保留空白以使規則對所有事件引發。

>[!IMPORTANT]
>
>如果您的網站正在使用[!DNL Mixpanel] SDK，您可以繼續下一步驟： [在 [!DNL Mixpanel]](#validate)內驗證您的資料。 如果您沒有使用[!DNL Mixpanel] SDK，您必須[建立個別的身分追蹤規則](#create-an-identity-tracking-rule)，以確保在使用者識別事件發生時，適當的事件和`distinct_id`值會傳送至[!DNL Mixpanel]。

## 驗證[!DNL Mixpanel]中的資料 {#validate}

如果實作成功且已收集事件，您將會在[[!DNL Mixpanel] 主控台](https://help.mixpanel.com/hc/en-us/articles/4402837164948)中看到事件。

檢查[!DNL Mixpanel]是否已合併填入電子郵件值的張貼登入事件與使用&#x200B;**[!UICONTROL 傳送事件]**&#x200B;時建立的事件。 如果實作正確，[!DNL Mixpanel]會將它們與單一[使用者設定檔](https://help.mixpanel.com/hc/en-us/articles/115004501966)建立關聯。

## 後續步驟

本指南說明如何使用事件轉送將轉換事件傳送至[!DNL Mixpanel]。 此事件轉送擴充功能採用[!DNL Mixpanel] SDK和JavaScript API。 如需這些基礎技術的詳細資訊，請參閱正式檔案：

* [[!DNL Mixpanel] SDK](https://developer.mixpanel.com/docs/nodejs)
* [[!DNL Mixpanel] JavaScript API](https://developer.mixpanel.com/docs/javascript-full-api-reference#mixpanelidentify)

如需Experience Platform中事件轉送功能的詳細資訊，請參閱[事件轉送概觀](../../../ui/event-forwarding/overview.md)。
