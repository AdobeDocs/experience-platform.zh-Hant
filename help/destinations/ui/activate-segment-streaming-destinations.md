---
keywords: 激活段流目標；激活段流目標；激活資料
title: 將受眾資料激活到流段導出目標
type: Tutorial
description: 瞭解如何通過將段映射到段流式傳輸目標來激活您在Adobe Experience Platform擁有的觀眾資料。
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 546758c419670746cf55de35cbb33131d4457cb9
workflow-type: tm+mt
source-wordcount: '972'
ht-degree: 8%

---

# 將受眾資料激活到流段導出目標

>[!IMPORTANT]
> 
> * 激活資料並啟用 [映射步驟](#mapping) 工作流中，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。
> * 在不通過 [映射步驟](#mapping) 工作流中，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活段而不映射]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。
> 
> 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

## 總覽 {#overview}

本文介紹在Adobe Experience Platform段流目的地激活觀眾資料所需的工作流。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的目標，並配置要使用的目標。

## 選擇目標 {#select-destination}

1. 轉到 **[!UICONTROL 連接>目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。

   ![目標目錄頁籤](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 選擇 **[!UICONTROL 激活段]** 在與要激活段的目標相對應的卡上，如下圖所示。

   ![激活按鈕](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. 選擇要用於激活段的目標連接，然後選擇 **[!UICONTROL 下一個]**。

   ![選擇目標](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. 移至下一節 [選擇段](#select-segments)。

## 選擇段 {#select-segments}

使用段名稱左側的複選框選擇要激活到目標的段，然後選擇 **[!UICONTROL 下一個]**。

![選擇段](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## 映射屬性和標識 {#mapping}

>[!IMPORTANT]
>
>此步驟僅適用於某些段流目標。 如果目標沒有 **[!UICONTROL 映射]** 步驟，跳至 [計畫段導出](#scheduling)。

某些段流目標要求您選擇源屬性或標識命名空間以映射為目標標識。

1. 在 **[!UICONTROL 映射]** ，選擇 **[!UICONTROL 添加新映射]**。

   ![添加新映射](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. 選擇右側的箭頭 **[!UICONTROL 源欄位]** 的子菜單。

   ![選擇源欄位](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. 在 **[!UICONTROL 選擇源欄位]** 頁，使用 **[!UICONTROL 選擇屬性]** 或 **[!UICONTROL 選擇標識命名空間]** 選項，在兩類可用源欄位之間切換。 從可用 [!DNL XDM] 配置檔案屬性和標識命名空間，選擇要映射到目標的屬性，然後選擇 **[!UICONTROL 選擇]**。

   ![「選擇源欄位」頁](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. 選擇右側的按鈕 **[!UICONTROL 目標欄位]** 的子菜單。

   ![選擇目標欄位](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. 在 **[!UICONTROL 選擇目標欄位]** 頁，選擇要將源欄位映射到的目標標識命名空間，然後選擇 **[!UICONTROL 選擇]**。

   ![「選擇目標欄位」頁](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. 要添加更多映射，請重複步驟1至5。

### 套用轉換  {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="套用轉換 "
>abstract="使用未雜湊的來源欄位時勾選此選項，讓 Adobe Experience Platform 在啟動時自動將它們雜湊。"

將未散列的源屬性映射到目標預期散列的目標屬性時(例如： `email_lc_sha256` 或 `phone_sha256`)，檢查 **應用轉換** 選項，使Adobe Experience Platform在激活時自動散列源屬性。

![標識映射](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## 計畫段導出 {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="結束日期"
>abstract="無法使用新增區段排程的結束日期。"

預設情況下， [!UICONTROL 段計畫] 頁只顯示在當前激活流中選擇的新選定段。

![新段](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

要查看激活到目標的所有段，請使用篩選選項並禁用 **[!UICONTROL 僅顯示新段]** 的子菜單。

![所有段](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. 在 **[!UICONTROL 段計畫]** 頁，選擇每個段，然後使用 **[!UICONTROL 開始日期]** 和 **[!UICONTROL 結束日期]** 選擇器，用於配置將資料發送到目標的時間間隔。

   ![段計畫](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * 某些目標要求您選擇 **[!UICONTROL 受眾來源]** 使用日曆選擇器下方的下拉菜單，為每個段。 如果目標未包括此選擇器，請跳過此步驟。

      ![對應 ID](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * 某些目標要求您手動映射 [!DNL Platform] 與目標目標中的對應方分段。 為此，請選擇每個段，然後在 **[!UICONTROL 映射ID]** 的子菜單。 如果目標未包括此欄位，請跳過此步驟。

      ![對應 ID](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * 某些目標要求您輸入 **[!UICONTROL 應用ID]** 激活 [!DNL IDFA] 或 [!DNL GAID] 段。 如果目標未包括此欄位，請跳過此步驟。

      ![應用程式 ID](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. 選擇 **[!UICONTROL 下一個]** 轉到 [!UICONTROL 審閱] 的子菜單。

## 請檢閱 {#review}

在 **[!UICONTROL 審閱]** 的子菜單。 選擇 **[!UICONTROL 取消]** 分解流， **[!UICONTROL 後退]** 修改設定，或 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

![審閱步驟中的選擇摘要。](/help/destinations/assets/ui/activate-segment-streaming-destinations/review.png)

### 同意政策評估 {#consent-policy-evaluation}

如果您的組織購買了 **Adobe Healthcare Shield** 或 **Adobe Privacy &amp; Security Shield**，請選取&#x200B;**[!UICONTROL 檢視適用的同意原則]**，以查看套用了哪些同意原則以及由於這些原則啟動中包含了多少個設定檔。閱讀 [同意政策評估](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) 的子菜單。

### 資料使用策略檢查 {#data-usage-policy-checks}

在 **[!UICONTROL 審閱]** 步驟，Experience Platform還檢查是否存在任何資料使用策略違規。 下面顯示的示例違反了策略。 在解決違規之前，無法完成段激活工作流。 有關如何解決策略違規的資訊，請閱讀 [資料使用策略違規](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) 資料治理文檔部分。

![資料策略違規](../assets/common/data-policy-violation.png)

### 篩選區段 {#filter-segments}

此外，在此步驟中，還可以使用頁面上的可用篩選器來僅顯示其計畫或映射已作為此工作流的一部分進行更新的段。 還可以切換要查看的表列。

![顯示審閱步驟中可用段篩選器的螢幕錄制。](/help/destinations/assets/ui/activate-segment-streaming-destinations/filter-segments-review-step.gif)

如果您對所選內容感到滿意，但未檢測到任何違反策略的情況，請選擇 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

## 驗證段激活 {#verify}

檢查 [目標監控文檔](../../dataflows/ui/monitor-destinations.md) 有關如何監視資料流到目標的詳細資訊。

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
