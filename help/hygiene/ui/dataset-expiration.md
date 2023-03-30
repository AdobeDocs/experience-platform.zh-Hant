---
title: 管理資料集有效期
description: 了解如何在Adobe Experience Platform UI中排程資料集的有效期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: a1628df7d0eefc795d1eaeefce842a65c7133322
workflow-type: tm+mt
source-wordcount: '736'
ht-degree: 0%

---

# 管理資料集過期時間 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="刪除不想要或過期的客戶記錄和資料集"
>abstract="<h2>說明</h2><p>若要管理與法規遵循性無關的Experience Platform資料生命週期，您可以刪除消費者記錄並排程資料集的到期日。 若要建立或管理資料主體請求，請參閱「執行資料主體隱私請求」使用案例區塊。</p>"

>[!IMPORTANT]
>
>Adobe Experience Platform中的資料衛生功能目前僅適用於已購買的組織 **Adobe醫療保健盾** 或 **Adobe隱私與安全防護**. 這些功能預計於近期內正式發行。 如需近期上市的詳細資訊，請洽詢您的Adobe服務代表。 不過，您可以立即 [透過刪除資料集 [!UICONTROL 資料集] UI](../../catalog/datasets/user-guide.md#delete).

此 [[!UICONTROL 資料衛生] 工作區](./overview.md) 在Adobe Experience Platform UI中，可讓您排程資料集的到期日。 當資料集到期日時，資料湖、身分服務和即時客戶設定檔會開始個別的程式，從各自的服務中移除資料集的內容。 從這三項服務中刪除資料後，過期時間就會標示為完成。

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更可能會將資料內嵌至該資料集的任何資料流，以免對下游工作流程造成負面影響。

本檔案說明如何在Platform UI中排程和管理資料集有效期。

## 排程資料集的有效期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="說明"
>abstract="<ul><li>選擇 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html">資料衛生</a> 在左側導覽器中，然後選取 <b>建立請求</b>.</li><li>如果要刪除記錄：</li>   <li>選擇 <b>記錄</b>.</li>   <li>選取要從中刪除記錄的特定資料集，或選擇從所有資料集中刪除記錄的選項。</li>   <li>提供要刪除其記錄的消費者的身分。 選擇 <b>新增身分</b> 一次提供一個身分，或選取 <b>選擇檔案</b> 上傳身分識別的JSON檔案。</li>   <li>如有需要，請選取 <b>範本</b> 檢視預期的JSON檔案格式。</li><li>如需相關指示，請參閱本檔案 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html#schedule-dataset-expiration">排程資料集的到期日</a>.</li></ul>"

若要建立新請求，請選取 **[!UICONTROL 建立請求]** 從工作區的主要頁面。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/ttl/create-request-button.png)

請求建立對話方塊隨即顯示。 在 **[!UICONTROL 請求的操作]** 部分，選擇 **[!UICONTROL 刪除資料集]** 更新資料集過期排程的可用控制項。

![顯示 [!UICONTROL 建立請求] 按鈕](../images/ui/ttl/dataset-selected.png)

### 選取日期和資料集

請求建立對話方塊隨即顯示。 在 **[!UICONTROL 請求的操作]** 區段，選取您要刪除資料集的日期。 您可以手動輸入日期（格式） `mm/dd/yyyy`)或選取日曆圖示(![日曆圖示的影像](../images/ui/ttl/calendar-icon.png))，從對話方塊選取日期。

![顯示資料集所設定到期日的影像](../images/ui/ttl/select-date.png)

下一個，下 **[!UICONTROL 資料集詳細資料]**，請選取資料庫圖示(![資料庫表徵圖的影像](../images/ui/ttl/database-icon.png))開啟資料集選取對話方塊。 從清單中選擇要套用到期日的資料集，然後選取 **[!UICONTROL 完成]**.

![顯示所選資料集的影像](../images/ui/ttl/select-dataset.png)

>[!NOTE]
只會顯示屬於目前沙箱的資料集。

### 提交請求

此 [!UICONTROL 資料集詳細資料] 區段會填入，以包含所選資料集的主要身分和結構。 在 **[!UICONTROL 請求設定]**，輸入請求的名稱和可選說明，後跟 **[!UICONTROL 提交]**.

![顯示 [!UICONTROL 提交] 按鈕](../images/ui/ttl/submit.png)

系統會要求您確認資料集的刪除日期。 選擇 **[!UICONTROL 提交]** 繼續。

提交請求後，會建立工作單，並顯示在 [!UICONTROL 資料衛生] 工作區。 在此處，您可以在工作單處理請求時監控其狀態。

>[!NOTE]
請參閱以下的概觀區段： [時間表和透明度](../home.md#dataset-expiration-transparency) 如需執行資料集過期時的處理方式詳細資訊。

## 編輯或取消資料集的過期時間

若要編輯或取消資料集的過期時間，請選取 **[!UICONTROL 資料集]** 在工作區的主要頁面上，並從清單中選取資料集過期時間。

在資料集過期的詳細資訊頁面上，右側邊欄會顯示編輯或取消排程刪除的控制項。

## 後續步驟

本檔案說明如何在Experience PlatformUI中排程資料集到期日。 有關如何在UI中執行其他資料衛生任務的資訊，請參閱 [資料衛生UI概述](./overview.md).

若要了解如何使用資料衛生API排程資料集到期日，請參閱 [資料集過期端點指南](../api/dataset-expiration.md).
