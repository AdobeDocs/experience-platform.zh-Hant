---
title: (Beta)使用Experience PlatformUI按需導出檔案到批處理目標
type: Tutorial
description: 瞭解如何使用Experience PlatformUI將按需檔案導出到批處理目標。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 874c590e83712a45e75308239fb71db04614bd1e
workflow-type: tm+mt
source-wordcount: '745'
ht-degree: 0%

---

# (Beta)使用Experience PlatformUI按需導出檔案到批處理目標

>[!IMPORTANT]
>
>的 **[!UICONTROL 立即導出檔案]** 選項當前處於Beta中。 文檔和功能可能會更改。
>請與Adobe代表聯繫以訪問此功能。

>[!IMPORTANT]
> 
>要激活資料，您需要 **[!UICONTROL 管理目標]**。 **[!UICONTROL 激活目標]**。 **[!UICONTROL 查看配置檔案]**, **[!UICONTROL 查看段]** [訪問控制權限](/help/access-control/home.md#permissions)。 閱讀 [訪問控制概述](/help/access-control/ui/overview.md) 或聯繫您的產品管理員以獲取所需權限。

## **[!UICONTROL 立即導出檔案]** 概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即導出檔案"
>abstract="選擇此控制項，除以前計畫的導出外，還提供完整檔案導出。 檔案導出會立即觸發，它會從Experience Platform分段運行中獲取最新結果。"

本文介紹如何使用Experience PlatformUI將檔案按需導出到批處理目標，如 [雲儲存](/help/destinations/catalog/cloud-storage/overview.md) 和 [電子郵件營銷](/help/destinations/catalog/email-marketing/overview.md) 目標。

的 **[!UICONTROL 立即導出檔案]** control允許您導出完整檔案，而不中斷先前計畫的段的當前導出計畫。 此導出除了以前計畫的導出外，不會更改段的導出頻率。 檔案導出會立即觸發，它會從Experience Platform分段運行中獲取最新結果。

您也可以為此目的使用Experience PlatformAPI。 閱讀如何 [通過即席激活API按需激活受眾段以批處理目標](/help/destinations/api/ad-hoc-activation-api.md)。

## 先決條件 {#prerequisites}

要按需將檔案導出到批處理目標，必須已成功 [連接到目標](./connect-destination.md)。 如果尚未執行此操作，請轉至 [目標目錄](../catalog/overview.md)，瀏覽支援的目標，並配置要使用的目標。

## 如何按需導出檔案 {#how-to-export-files-on-demand}

1. 轉到 **[!UICONTROL 連接>目標]**，選擇 **[!UICONTROL 瀏覽]** 頁籤和篩選器符號，以顯示到所需批處理目標的現有連接。

   ![突出顯示如何進入瀏覽頁籤和篩選現有資料流的影像。](../assets/ui/activate-on-demand/browse-tab.png)

2. 選擇所需的目標連接以檢查到目標的現有資料流。

   ![突出顯示已過濾的資料流的影像。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 選擇 **[!UICONTROL 激活資料]** 頁籤，然後選擇要按需導出檔案的段，然後選擇 **[!UICONTROL 立即導出檔案]** 控制項，以觸發將檔案傳送到批處理目標的一次性導出。

   >[!IMPORTANT]
   >
   >當前UI不支援選擇多個段以按需批量導出檔案。 使用 [點對點激活API](/help/destinations/api/ad-hoc-activation-api.md) 為了這個目的。

   ![突出顯示「立即導出檔案」按鈕的影像。](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. 選擇 **[!UICONTROL 是]** 確認並觸發檔案導出。

   ![顯示「立即導出檔案」確認對話框的影像。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 將顯示一條確認消息，讓您知道檔案導出已啟動。

   ![顯示確認成功即席激活的影像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您還可以切換到 **[!UICONTROL 資料流運行]** 頁籤，確認檔案導出已啟動。

## 考量事項 {#considerations}

使用 **[!UICONTROL 立即導出檔案]** 控制項：

* **[!UICONTROL 立即導出檔案]** 僅適用於批處理激活資料流中的調度與當前日期重疊的段。 這包括具有沒有結束日期的計畫的段(導出頻率為 **[!UICONTROL 一次]**)，或結束日期尚未通過的地方。
* 將段添加到現有資料流時，請至少等待15分鐘，直到使用 **[!UICONTROL 立即導出檔案]** 控制項。
* 如果更改了段的合併策略，或者建立了使用新合併策略的段，則等待24小時，直到 **[!UICONTROL 立即導出檔案]** 控制項。

## UI錯誤消息 {#ui-error-messages}

使用 **[!UICONTROL 立即導出檔案]** control，您可能會遇到下面列出的任何錯誤消息。 查看表，瞭解當它們確實出現時如何解決它們。

| 錯誤訊息 | 解析度 |
|---------|----------|
| 已運行段 `segment ID` 訂單 `dataflow ID` 運行id `flow run ID` | 此錯誤消息表示當前正在為段執行點對點激活流。 等待作業完成，然後再次觸發激活作業。 |
| 段 `<segment name>` 不是此資料流的一部分或超出計畫範圍！ | 此錯誤消息表示選定要激活的段未映射到資料流，或者為段設定的激活計畫已過期或尚未啟動。 檢查段是否確實映射到資料流，並驗證段激活計畫是否與當前日期重疊。 |

## 相關資訊 {#related-information}

* [使用Experience PlatformAPI按需激活受眾段以批處理目標](/help/destinations/api/ad-hoc-activation-api.md)
* [將受眾資料激活到批配置檔案導出目標](/help/destinations/ui/activate-batch-profile-destinations.md)
