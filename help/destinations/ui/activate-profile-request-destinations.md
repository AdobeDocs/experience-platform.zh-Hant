---
keywords: 激活配置檔案請求目標；激活資料；配置檔案請求目標
title: 將受眾資料激活到配置檔案請求目標
type: Tutorial
description: 瞭解如何通過將段映射到配置檔案請求目標來激活您在Adobe Experience Platform擁有的受眾資料。
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: cda4591021c5b0a0bd6f43765d72b5867ec59aea
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# 將受眾資料激活到配置檔案請求目標

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

## 總覽 {#overview}

本文介紹在Adobe Experience Platform配置檔案請求目標中激活受眾資料所需的工作流。 當與 [邊緣分割](../../segmentation/ui/edge-segmentation.md)，這些目標在Web屬性上啟用同頁和下頁個性化使用案例。 閱讀有關 [啟用同頁和下頁個性化用例](/help/destinations/ui/configure-personalization-destinations.md)。

配置檔案請求目標的示例包括 [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) 和 [自定義個性化](../../destinations/catalog/personalization/custom-personalization.md) 連接。

## 先決條件 {#prerequisites}

要將資料激活到目標，必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的個性化目標，並配置要使用的目標。

### 段合併策略 {#merge-policy}

當前，配置檔案請求目標僅支援激活使用 [活動邊緣合併策略](../../segmentation/ui/segment-builder.md#merge-policies) 設定為預設值。

## 選擇目標 {#select-destination}

1. 轉到 **[!UICONTROL 連接>目標]**，然後選擇 **[!UICONTROL 目錄]** 頁籤。

   ![目標目錄頁籤](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. 選擇 **[!UICONTROL 激活段]** 在與要激活段的個性化目標對應的卡上，如下圖所示。

   ![激活按鈕](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. 選擇要用於激活段的目標連接，然後選擇 **[!UICONTROL 下一個]**。

   ![選擇目標](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. 移至下一節 [選擇段](#select-segments)。

## 選擇段 {#select-segments}

使用段名稱左側的複選框選擇要激活到目標的段，然後選擇 **[!UICONTROL 下一個]**。

![選擇段](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Beta)地圖屬性 {#map-attributes}

>[!IMPORTANT]
>
>映射步驟，它允許對 [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) 和 [通用個性化目標](/help/destinations/catalog/personalization/custom-personalization.md)，當前處於測試版，您的組織可能尚未訪問它。 本文檔可能會更改。

選擇要為用戶啟用個性化用例的屬性。 這意味著，如果屬性值更改或將屬性添加到配置檔案，則該配置檔案將成為段的成員並將激活到個性化目標。

添加屬性是可選的，您仍然可以繼續執行下一步並啟用同頁和下一頁個性化，而無需選擇屬性。 如果在此步驟中未添加任何屬性，則仍會根據截面梁的段成員資格和身份映射資格進行個性化設定。

![顯示選定屬性的映射步驟的影像](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### 選擇源屬性 {#select-source-attributes}

要添加源屬性，請選擇 **[!UICONTROL 添加新欄位]** 控制項 **[!UICONTROL 源欄位]** 列和搜索，或導航到所需的XDM屬性欄位，如下所示。

![顯示如何在映射步驟中選擇目標屬性的螢幕錄制](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### 選擇目標屬性 {#select-target-attributes}

>[!NOTE]
>
>某些目標要求您只選擇源屬性，而其他目標則要求源屬性和目標屬性。
>
>當前， [Adobe TargetV2](../catalog/personalization/adobe-target-connection.md) 目標僅需要源屬性，而 [具有屬性的自定義個性化](../catalog/personalization/custom-personalization.md) 需要源屬性和目標屬性。

要添加目標屬性，請選擇 **[!UICONTROL 添加新欄位]** 控制項 **[!UICONTROL 目標欄位]** 列和鍵入要將源屬性映射到的自定義屬性名稱。

![顯示如何在映射步驟中選擇XDM屬性的螢幕錄制](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## 計畫段導出 {#scheduling}

預設情況下， [!UICONTROL 段計畫] 頁只顯示在當前激活流中選擇的新選定段。

![新段](../assets/ui/activate-profile-request-destinations/new-segments.png)

要查看激活到目標的所有段，請使用篩選選項並禁用 **[!UICONTROL 僅顯示新段]** 的子菜單。

![所有段](../assets/ui/activate-profile-request-destinations/all-segments.png)

在 **[!UICONTROL 段計畫]** 頁，選擇每個段，然後使用 **[!UICONTROL 開始日期]** 和 **[!UICONTROL 結束日期]** 選擇器，用於配置將資料發送到目標的時間間隔。

![段計畫](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

選擇 **[!UICONTROL 下一個]** 轉到 [!UICONTROL 審閱] 的子菜單。

## 審閱 {#review}

在 **[!UICONTROL 審閱]** 的子菜單。 選擇 **[!UICONTROL 取消]** 分解流， **[!UICONTROL 後退]** 修改設定，或 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

>[!IMPORTANT]
>
>在此步驟中，Adobe Experience Platform檢查資料使用策略違規。 下面顯示的示例違反了策略。 在解決違規之前，無法完成段激活工作流。 有關如何解決策略違規的資訊，請參見 [策略執行](../../rtcdp/privacy/data-governance-overview.md#enforcement) 資料治理文檔部分。

![資料策略違規](../assets/common/data-policy-violation.png)

如果未檢測到任何策略違規，請選擇 **[!UICONTROL 完成]** 確認選擇並開始向目標發送資料。

![審閱](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->