---
title: 管理資料集有效期
description: 瞭解如何在Adobe Experience Platform UI中排程資料集有效期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 7931c8fe4a1ca5d255a80e7e6b0deb976d53c3de
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 20%

---

# 管理資料集有效期 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="刪除不要的或過期的客戶記錄和資料集"
>abstract="<h2>說明</h2><p>要管理與合規性無關的 Experience Platform 資料的生命週期，您可以刪除消費者記錄並排程資料集的到期日。若要建立或管理資料主體要求，請參閱「執行資料主體隱私權要求」使用案例區塊。</p>"

此 [[!UICONTROL 資料生命週期] 工作區](./overview.md) Adobe Experience Platform UI中，可讓您為資料集排程有效期。 當資料集到達其到期日時，資料湖、身分服務和即時客戶設定檔會開始個別程式，從各自的服務中移除資料集的內容。 從所有三項服務中刪除資料後，到期日即會標示為完成。

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更任何可能會將資料擷取至該資料集的資料流程，讓您的下游工作流程不會受到負面影響。

本文介紹如何在Platform UI中排程及管理資料集有效期。

>[!NOTE]
>
>資料集到期目前不會從Adobe Experience Platform Edge Network刪除資料。 不過，資料集設為過期後，資料不可能保留在Edge Network內。 這是因為資料集到期的14天服務授權合約與14天資料存在於Edge Network中的期間重合，之後才捨棄資料。

## 排程資料集到期日 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=zh-Hant">資料生命週期</a>，然後選取<b>建立要求</b>。</li><li>如果您要刪除記錄：</li>   <li>選取<b>記錄</b>。</li>   <li>選擇要從中刪除記錄的特定資料集，或選擇從所有資料集中刪除記錄的選項。</li>   <li>提供要刪除其記錄之消費者的身分。選取<b>新增身分</b>一次提供一個身分，或選取<b>選擇檔案</b>改上傳身分的 JSON 檔案。</li>   <li>如果需要，選取 <b>範本</b> 以查看 JSON 檔案的預期格式。</li><li>如果您想要 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=zh-Hant#schedule-dataset-expiration">排程資料集的到期日</a>，請參閱文件以取得指示。</li></ul>"

若要建立請求，請選取 **[!UICONTROL 建立請求]** 從工作區的主要頁面。

>[!IMPORTANT]
>
您最多可以有20個同時排程的資料集有效期。 這表示您可以同時排程刪除20個資料集。 這些過期的設定時間或年份沒有限制。 例如，如果您有20個排程的資料集有效期，而其中一個資料集將於明天刪除，則在刪除該資料集之前，您無法設定任何其他有效期。

![此 [!UICONTROL 資料生命週期] 工作區，使用 [!UICONTROL 建立請求] 反白顯示。](../images/ui/ttl/create-request-button.png)

此時會出現請求建立工作流程。 在 [!UICONTROL 請求的動作] 區段，選取 **[!UICONTROL 刪除資料集]** 更新資料集到期排程的控制項。

![使用的請求建立工作流程 [!UICONTROL 刪除資料集] 選項會醒目提示。](../images/ui/ttl/dataset-selected.png)

### 選取日期和資料集 {#select-date-and-dataset}

在 **[!UICONTROL 請求的動作]** 區段，選取要刪除資料集的日期。 您可以手動輸入日期(格式為 `mm/dd/yyyy`)或選取行事曆圖示(![行事曆圖示。](../images/ui/ttl/calendar-icon.png))以從對話方塊選取日期。

![包含為資料集選取並反白之到期日的行事曆對話方塊。](../images/ui/ttl/select-date.png)

下一個，在 **[!UICONTROL 資料集詳細資訊]**，選取資料庫圖示(![資料庫圖示。](../images/ui/ttl/database-icon.png))以開啟資料集選取對話方塊。 從清單中選擇要套用有效期的資料集，然後選取「 」 **[!UICONTROL 完成]**.

![此 [!UICONTROL 選取資料集] 對話方塊，其中已選取資料集並 [!UICONTROL 完成] 反白顯示。](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
只會顯示屬於目前沙箱的資料集。

### 提交請求 {#submit-request}

此 [!UICONTROL 資料集詳細資訊] 區段會填入，以包含所選資料集的主要身分和結構描述。 在 **[!UICONTROL 請求設定]**，輸入要求的名稱和說明（選用），然後按一下 **[!UICONTROL 提交]**.

![具有的已完成資料集到期要求 [!UICONTROL 請求設定] 和 [!UICONTROL 提交] 按鈕反白顯示。](../images/ui/ttl/submit.png)

A [!UICONTROL 確認請求] 對話方塊隨即顯示。 系統會要求您確認資料集名稱以及要刪除資料集的日期。 選取 **[!UICONTROL 提交]** 以繼續。

提交請求後，即會建立工單，並顯示在 [!UICONTROL 資料生命週期] 工作區。 從這裡，您可以在工單處理請求時監視工單的狀態。

>[!NOTE]
>
請參閱的概觀區段： [時間軸和透明度](../home.md#dataset-expiration-transparency) 以取得資料集過期執行後如何處理的詳細資訊。

## 編輯或取消資料集有效期 {#edit-or-cancel}

若要編輯或取消資料集有效期，請選取「 」 **[!UICONTROL 資料集]** ，並從清單中選取資料集有效期。

在資料集到期日的詳細資訊頁面上，右側邊欄會顯示用於編輯或取消已排程刪除的控制項。

## 後續步驟

本檔案說明如何在Experience Platform UI中排程資料集有效期。 有關如何在UI中執行其他資料最小化任務的資訊，請參閱 [資料生命週期UI總覽](./overview.md).

若要瞭解如何使用資料衛生API排程資料集有效期，請參閱 [資料集到期端點指南](../api/dataset-expiration.md).
