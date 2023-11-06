---
title: （測試版）使用Experience PlatformUI隨選將檔案匯出至批次目的地
type: Tutorial
description: 瞭解如何使用Experience PlatformUI隨選將檔案匯出至批次目的地。
exl-id: 0cbe5089-b73d-4584-8451-2fc34d47c357
source-git-commit: 165793619437f403045b9301ca6fa5389d55db31
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 8%

---

# （測試版）使用Experience PlatformUI隨選將檔案匯出至批次目的地

>[!IMPORTANT]
>
>此 **[!UICONTROL 立即匯出檔案]** Adobe Experience Platform中的選專案前是Beta版。 檔案和功能可能會有所變更。
>請聯絡您的Adobe代表以取得此功能的存取權。

>[!IMPORTANT]
> 
>若要啟用資料，您需要 **[!UICONTROL 管理目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 檢視設定檔]**、和 **[!UICONTROL 檢視區段]** [存取控制許可權](/help/access-control/home.md#permissions). 閱讀 [存取控制總覽](/help/access-control/ui/overview.md) 或聯絡您的產品管理員以取得必要許可權。

## **[!UICONTROL 立即匯出檔案]**&#x200B;概觀 {#overview}

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_activatenow"
>title="立即匯出檔案"
>abstract="選取此控制項可在任何先前排程的匯出外實現完整的檔案匯出。檔案匯出會即刻觸發，並從 Experience Platform 分段執行中獲取最新結果。"

本文會說明如何使用Experience Platform UI，隨選將檔案匯出至批次目的地，例如 [雲端儲存空間](/help/destinations/catalog/cloud-storage/overview.md) 和 [電子郵件行銷](/help/destinations/catalog/email-marketing/overview.md) 目的地。

此 **[!UICONTROL 立即匯出檔案]** 控制可讓您匯出完整的檔案，而不會中斷先前排程對象的目前匯出排程。 除了先前排程的匯出外，也會進行此匯出，不會變更對象的匯出頻率。 檔案匯出會即刻觸發，並從 Experience Platform 分段執行中獲取最新結果。

您也可以將Experience Platform API用於此目的。 閱讀如何 [透過臨時啟用API依需求啟用批次目的地的受眾](/help/destinations/api/ad-hoc-activation-api.md).

## 先決條件 {#prerequisites}

若要隨選將檔案匯出至批次目的地，您必須已成功完成 [已連線至目的地](./connect-destination.md). 如果您尚未這麼做，請前往 [目的地目錄](../catalog/overview.md)，瀏覽支援的目的地，並設定您要使用的目的地。

## 如何隨選匯出檔案 {#how-to-export-files-on-demand}

1. 前往 **[!UICONTROL 連線>目的地]**，選取 **[!UICONTROL 瀏覽]** 標籤和篩選符號來顯示與您想要的批次目的地的現有連線。

   ![反白顯示如何前往瀏覽標籤並篩選現有資料流程的影像。](../assets/ui/activate-on-demand/browse-tab.png)

2. 選取您需要的目的地連線，以檢查到目的地的現有資料流。

   ![影像反白顯示篩選的資料流。](../assets/ui/activate-on-demand/filtered-dataflow.png)

3. 選取 **[!UICONTROL 啟用資料]** 標籤並選取您要隨選匯出檔案的對象，然後選取 **[!UICONTROL 立即匯出檔案]** 控制以觸發一次性匯出，將檔案傳送到批次目的地。

   >[!IMPORTANT]
   >
   >UI目前不支援選取多個對象來大量隨選匯出檔案。 使用 [臨機啟動API](/help/destinations/api/ad-hoc-activation-api.md) 用於此目的。

   ![反白顯示「立即匯出檔案」按鈕的影像。](../assets/ui/activate-on-demand/activate-segment-on-demand.png)

4. 選取 **[!UICONTROL 是]** 以確認並觸發檔案匯出。

   ![此影像顯示立即匯出檔案確認對話方塊。](../assets/ui/activate-on-demand/confirm-activation.png)

5. 系統會顯示確認訊息，告知您已開始匯出檔案。

   ![顯示成功隨機啟動確認的影像。](../assets/ui/activate-on-demand/ad-hoc-success.png)

6. 您也可以切換至 **[!UICONTROL 資料流執行]** 標籤以確認檔案匯出已啟動。

## 考量事項 {#considerations}

使用時，請牢記以下注意事項 **[!UICONTROL 立即匯出檔案]** 控制：

* **[!UICONTROL 立即匯出檔案]** 僅適用於批次啟用資料流中的排程與目前日期重疊的對象。 這包含其排程沒有結束日期(匯出頻率 **[!UICONTROL 一次]**)，或尚未超過結束日期時。
* 將對象新增至現有資料流時，請等候至少15分鐘，直到使用 **[!UICONTROL 立即匯出檔案]** 控制。
* 如果您變更對象的合併原則，或如果您建立使用新合併原則的對象，請等待24小時，直到使用 **[!UICONTROL 立即匯出檔案]** 控制。

## UI錯誤訊息 {#ui-error-messages}

使用時 **[!UICONTROL 立即匯出檔案]** 控制，您可能會遇到下列任何錯誤訊息。 請檢閱表格以瞭解如何在它們出現時解決它們。

| 錯誤訊息 | 解決方法 |
|---------|----------|
| 已針對對象執行中 `segment ID` 訂購 `dataflow ID` 具有執行id `flow run ID` | 此錯誤訊息表示對象目前正在進行臨機啟動流程。 再次觸發啟動工作前，請等候工作完成。 |
| 受眾 `<segment name>` 不是此資料流的一部分或超出排程範圍！ | 此錯誤訊息指出您選取要啟用的對象未對應至資料流，或是為對象設定的啟用排程已過期或尚未開始。 檢查對象是否確實對應至資料流，並確認對象啟用排程與目前日期重疊。 |

## 相關資訊 {#related-information}

* [使用Experience PlatformAPI依需求啟用批次目的地的對象](/help/destinations/api/ad-hoc-activation-api.md)
* [啟用對象資料至批次設定檔匯出目的地](/help/destinations/ui/activate-batch-profile-destinations.md)
