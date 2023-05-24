---
title: 管理資料集過期
description: 瞭解如何在Adobe Experience PlatformUI中安排資料集過期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 22%

---

# 管理資料集過期 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="刪除不要的或過期的客戶記錄和資料集"
>abstract="<h2>說明</h2><p>要管理與合規性無關的 Experience Platform 資料的生命週期，您可以刪除消費者記錄並排程資料集的到期日。若要建立或管理資料主體要求，請參閱「執行資料主體隱私權要求」使用案例區塊。</p>"

>[!IMPORTANT]
>
>Adobe Experience Platform的資料衛生功能目前僅適用於已購買資料的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**。 這些功能將在不久的將來發佈。 有關他們即將上市的更多資訊，請與您的Adobe服務代表聯繫。 但是，你可以馬上 [刪除資料集 [!UICONTROL 資料集] UI](../../catalog/datasets/user-guide.md#delete)。

的 [[!UICONTROL 資料衛生] 工作區](./overview.md) 在Adobe Experience PlatformUI中，可以為資料集安排到期時間。 當資料集到達其到期日期時，資料湖、身份服務和即時客戶配置檔案將開始單獨的進程，以從各自的服務中刪除資料集的內容。 從所有三個服務中刪除資料後，過期將標籤為完成。

>[!WARNING]
>
>如果資料集設定為過期，則必須手動更改可能正在將資料插入該資料集的任何資料流，以便下游工作流不會受到負面影響。

本文檔介紹如何在平台UI中安排和管理資料集過期。

## 計畫資料集過期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">資料檢疫</a>，然後選取<b>建立要求</b>。</li><li>如果您要刪除記錄：</li>   <li>選取<b>記錄</b>。</li>   <li>選擇要從中刪除記錄的特定資料集，或選擇從所有資料集中刪除記錄的選項。</li>   <li>提供要刪除其記錄之消費者的身分。選取<b>新增身分</b>一次提供一個身分，或選取<b>選擇檔案</b>改上傳身分的 JSON 檔案。</li>   <li>如果需要，選取<b>範本</b>以查看 JSON 檔案的預期格式。</li><li>如果您想要<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">排程資料集的到期日</a>，請參閱文件以取得指示。</li></ul>"

要建立新請求，請選擇 **[!UICONTROL 建立請求]** 的下界。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/ttl/create-request-button.png)

此時將出現請求建立對話框。 在 **[!UICONTROL 請求的操作]** 選擇 **[!UICONTROL 刪除資料集]** 更新資料集到期計畫的可用控制項。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/ttl/dataset-selected.png)

### 選擇日期和資料集

此時將出現請求建立對話框。 在 **[!UICONTROL 請求的操作]** 部分，選擇希望資料集刪除的日期。 您可以手動輸入日期(格式為 `mm/dd/yyyy`)或選擇日曆表徵圖(![日曆表徵圖的影像](../images/ui/ttl/calendar-icon.png))以從對話框中選擇日期。

![顯示為資料集設定的到期日期的影像](../images/ui/ttl/select-date.png)

下一個，下 **[!UICONTROL 資料集詳細資訊]**，選擇資料庫表徵圖(![資料庫表徵圖的影像](../images/ui/ttl/database-icon.png))開啟資料集選擇對話框。 從清單中選擇要應用到期日的資料集，然後選擇 **[!UICONTROL 完成]**。

![顯示正在選擇的資料集的影像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
僅顯示屬於當前沙箱的資料集。

### 提交請求

的 [!UICONTROL 資料集詳細資訊] 部分填充以包括所選資料集的主標識和模式。 下 **[!UICONTROL 請求設定]**，輸入請求的名稱和可選說明，然後 **[!UICONTROL 提交]**。

![顯示 [!UICONTROL 提交] 按鈕](../images/ui/ttl/submit.png)

系統會要求您確認資料集的刪除日期。 選擇 **[!UICONTROL 提交]** 繼續。

提交請求後，將建立工作單，並在 [!UICONTROL 資料衛生] 工作區。 在此處，您可以監視工作單處理請求時的狀態。

>[!NOTE]
請參閱上的概述部分 [時間表和透明度](../home.md#dataset-expiration-transparency) 有關執行資料集過期後如何處理的詳細資訊。

## 編輯或取消資料集過期

要編輯或取消資料集過期，請選擇 **[!UICONTROL 資料集]** 在工作區的首頁上，並從清單中選擇資料集過期。

在資料集到期的詳細資訊頁面上，右欄顯示了編輯或取消計畫刪除的控制項。

## 後續步驟

本文檔介紹了如何在Experience PlatformUI中安排資料集過期。 有關如何在UI中執行其他資料衛生任務的資訊，請參閱 [資料衛生UI概述](./overview.md)。

要瞭解如何使用資料衛生API安排資料集過期，請參閱 [資料集到期終結點指南](../api/dataset-expiration.md)。
