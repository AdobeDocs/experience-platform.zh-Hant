---
title: （測試版）使用Experience PlatformUI，隨選將檔案匯出至批次目的地
type: Tutorial
description: 了解如何使用Experience PlatformUI將隨選檔案匯出至批次目的地。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 29962e07aa50c97b6098f4c892facf48508d28cf
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# （測試版）使用Experience PlatformUI，隨選將檔案匯出至批次目的地

>[!IMPORTANT]
>
>此 **[!UICONTROL 立即匯出檔案]** Adobe Experience Platform中的選項目前為測試版。 檔案和功能可能會有所變更。
>請連絡您的Adobe代表以取得此功能的存取權。

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**, **[!UICONTROL 啟動目的地]**, **[!UICONTROL 檢視設定檔]**，和 **[!UICONTROL 檢視區段]** [存取控制權限](/help/access-control/home.md#permissions). 閱讀 [存取控制概觀](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得所需的權限。

## **[!UICONTROL 立即匯出檔案]** 概述 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即匯出檔案"
>abstract="選取此控制項，除了任何先前排程的匯出外，還可傳送完整檔案匯出。 檔案匯出會立即觸發，並從Experience Platform細分執行中擷取最新結果。"

本文說明如何使用Experience PlatformUI，依需求將檔案匯出至批次目的地，例如 [雲端儲存](/help/destinations/catalog/cloud-storage/overview.md) 和 [電子郵件行銷](/help/destinations/catalog/email-marketing/overview.md) 目的地。

此 **[!UICONTROL 立即匯出檔案]** 控制項可讓您匯出完整檔案，而不會中斷先前排程區段的目前匯出排程。 此匯出除了先前排程的匯出外，也不會變更區段的匯出頻率。 檔案匯出會立即觸發，並從Experience Platform細分執行中擷取最新結果。

您也可以為此目的使用Experience PlatformAPI。 閱讀如何 [透過臨機啟動API隨選啟動對象區段，以批次目的地](/help/destinations/api/ad-hoc-activation-api.md).

## 先決條件 {#prerequisites}

若要隨需將檔案匯出至批次目的地，您必須成功 [連接到目的地](./connect-destination.md). 如果尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

## 如何按需導出檔案 {#how-to-export-files-on-demand}

1. 前往 **[!UICONTROL 連線>目的地]**，請選取 **[!UICONTROL 瀏覽]** 標籤和篩選符號，顯示與所需批次目的地的現有連線。

   ![影像突出顯示如何訪問瀏覽頁簽並篩選現有資料流。](../assets/ui/activate-on-demand/browse-tab.png)

2. 選擇所需的目標連接以檢查到目標的現有資料流。

   ![影像突出顯示已過濾的資料流。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 選取 **[!UICONTROL 啟動資料]** 標籤，然後選取您要隨需匯出檔案的區段，並選取 **[!UICONTROL 立即匯出檔案]** 控制項，以觸發一次性匯出，該匯出會將檔案傳送至批次目的地。

   >[!IMPORTANT]
   >
   >UI目前不支援依需求大量選取多個區段以匯出檔案。 使用 [臨機啟動API](/help/destinations/api/ad-hoc-activation-api.md) 為此。

   ![突出顯示「立即導出檔案」按鈕的影像。](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. 選擇 **[!UICONTROL 是]** 確認並觸發檔案匯出。

   ![顯示「立即導出檔案」確認對話框的影像。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 畫面會顯示確認訊息，告知您檔案匯出已開始。

   ![顯示成功臨機啟動確認的影像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您也可以切換至 **[!UICONTROL 資料流運行]** 頁簽，確認檔案匯出已開始。

## 考量事項 {#considerations}

使用 **[!UICONTROL 立即匯出檔案]** 控制：

* **[!UICONTROL 立即匯出檔案]** 僅適用於批處理激活資料流中的調度與當前日期重疊的段。 這包括具有沒有結束日期之排程的區段(匯出頻率為 **[!UICONTROL 一次]**)，或結束日期尚未通過的位置。
* 將段添加到現有資料流時，請至少等待15分鐘，直到使用 **[!UICONTROL 立即匯出檔案]** 控制。
* 如果您變更了區段的合併原則，或您建立了使用新合併原則的區段，請等待24小時，直到使用 **[!UICONTROL 立即匯出檔案]** 控制。

## UI錯誤訊息 {#ui-error-messages}

使用 **[!UICONTROL 立即匯出檔案]** 控制，您可能會遇到下列任何錯誤訊息。 請檢閱表格，了解在顯示時如何處理。

| 錯誤訊息 | 解決方法 |
|---------|----------|
| 已針對區段執行 `segment ID` 訂購 `dataflow ID` 使用執行id `flow run ID` | 此錯誤訊息指出某個區段目前正在進行臨機啟動流程。 等待作業完成，然後再次觸發啟動作業。 |
| 區段 `<segment name>` 不屬於此資料流或超出計畫範圍！ | 此錯誤消息表示您選擇要激活的段未映射到資料流，或者為段設定的激活計畫已過期或尚未啟動。 檢查該段是否確實映射到資料流，並確認段激活時間表與當前日期重疊。 |

## 相關資訊 {#related-information}

* [使用Experience PlatformAPI，隨選啟用受眾區段以批次目的地](/help/destinations/api/ad-hoc-activation-api.md)
* [啟用受眾資料以批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md)
