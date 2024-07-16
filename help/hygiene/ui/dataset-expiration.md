---
title: 自動化資料集有效期
description: 瞭解如何在Adobe Experience Platform UI中排程資料集有效期。
exl-id: 97db55e3-b5d6-40fd-94f0-2463fe041671
source-git-commit: 2aba88ac657e73a12be14d2c3a67dd5714513c97
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 18%

---

# 自動化資料集到期 {#dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_description"
>title="刪除不要的或過期的客戶記錄和資料集"
>abstract="<h2>說明</h2><p>要管理與合規性無關的 Experience Platform 資料的生命週期，您可以刪除消費者記錄並排程資料集的到期日。若要建立或管理資料主體要求，請參閱「執行資料主體隱私權要求」使用案例區塊。</p>"

Adobe Experience Platform UI中的[[!UICONTROL 資料生命週期]工作區](./overview.md)可讓您排程資料集的到期日。 當資料集到達其到期日時，資料湖、身分服務和即時客戶設定檔會開始個別程式，從各自的服務中移除資料集的內容。 從所有三項服務中刪除資料後，到期日即會標示為完成。

>[!WARNING]
>
>如果資料集設為過期，您必須手動變更任何可能會將資料擷取至該資料集的資料流程，讓您的下游工作流程不會受到負面影響。

本文介紹如何在Platform UI中排程及自動化資料集有效期。

>[!NOTE]
>
>資料集到期目前不會從Adobe Experience PlatformEdge Network中刪除資料。 不過，資料集設為過期後，資料不可能保留在Edge Network內。 這是因為資料集到期的15天服務授權合約與Edge Network中存在資料的14天期間重疊，之後才捨棄資料。

進階資料生命週期管理支援透過[資料集到期端點](../api/dataset-expiration.md)進行資料集刪除，以及透過[工單端點](../api/workorder.md)使用主要身分的ID刪除（資料列層級資料）。 您也可以透過Platform UI管理資料集到期日和[記錄刪除](./record-delete.md)。 如需詳細資訊，請參閱連結的檔案。

>[!NOTE]
>
>資料生命週期不支援批次刪除。

## 排程資料集到期 {#schedule-dataset-expiration}

>[!CONTEXTUALHELP]
>id="platform_privacyConsole_scheduleDatasetExpiration_instructions"
>title="說明"
>abstract="<ul><li>在左側導覽中選取<a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/overview.html?lang=zh-Hant">資料生命週期</a>，然後選取<b>建立要求</b>。</li><li>如果您要刪除記錄：</li>   <li>選取<b>記錄</b>。</li>   <li>選擇要從中刪除記錄的特定資料集，或選擇從所有資料集中刪除記錄的選項。</li>   <li>提供要刪除其記錄之消費者的身分。選取<b>新增身分</b>一次提供一個身分，或選取<b>選擇檔案</b>改上傳身分的 JSON 檔案。</li>   <li>如果需要，選取 <b>範本</b> 以查看 JSON 檔案的預期格式。</li><li>如果您想要 <a href="https://experienceleague.adobe.com/docs/experience-platform/hygiene/ui/dataset-expiration.html?lang=zh-Hant#schedule-dataset-expiration">排程資料集的到期日</a>，請參閱文件以取得指示。</li></ul>"

若要建立請求，請選取工作區首頁面中的&#x200B;**[!UICONTROL 建立請求]**。

>[!IMPORTANT]
>
>Real-Time CDP、Adobe Journey Optimizer和Customer Journey Analytics使用者有20個擱置中的排程資料集到期工作單。 Healthcare Shield和Privacy and Security Shield使用者有50個擱置中的排程資料集到期工作單。 這表示您可以同時排程刪除20或50個資料集。<br>例如，如果您有20個排程的資料集有效期，而一個資料集將於明天刪除，則在刪除該資料集之前，您無法設定任何其他有效期。

![強調顯示[!UICONTROL 建立請求]的[!UICONTROL 資料生命週期]工作區。](../images/ui/ttl/create-request-button.png)

此時會出現請求建立工作流程。 在[!UICONTROL 要求的動作]區段下，選取&#x200B;**[!UICONTROL 刪除資料集]**&#x200B;以更新資料集到期排程的控制項。

![要求建立工作流程中反白了[!UICONTROL 刪除資料集]選項。](../images/ui/ttl/dataset-selected.png)

### 選取日期和資料集 {#select-date-and-dataset}

在&#x200B;**[!UICONTROL 要求的動作]**&#x200B;區段下，選取要刪除資料集的日期。 您可以手動輸入日期（格式為`mm/dd/yyyy`）或選取行事曆圖示(![行事曆圖示。](../images/ui/ttl/calendar-icon.png))以從對話方塊中選取日期。

![已針對資料集選取並反白到期日的行事曆對話方塊。](../images/ui/ttl/select-date.png)

接下來，在&#x200B;**[!UICONTROL 資料集詳細資料]**&#x200B;下，選取資料庫圖示(![資料庫圖示。](../images/ui/ttl/database-icon.png))以開啟資料集選取對話方塊。 從清單中選擇要套用到期日的資料集，然後選取&#x200B;**[!UICONTROL 完成]**。

![已選取資料集並醒目提示[!UICONTROL 完成]的[!UICONTROL 選取資料集]對話方塊。](../images/ui/ttl/select-dataset.png)

>[!NOTE]
>
>只會顯示屬於目前沙箱的資料集。

### 提交請求 {#submit-request}

[!UICONTROL 資料集詳細資料]區段會填入，以包含所選資料集的主要身分和結構描述。 在&#x200B;**[!UICONTROL 要求設定]**&#x200B;下，輸入要求的名稱和選擇性描述，然後是&#x200B;**[!UICONTROL 提交]**。

![已完成的資料集到期要求，其中[!UICONTROL 要求設定]和[!UICONTROL 提交]按鈕已強調顯示。](../images/ui/ttl/submit.png)

[!UICONTROL Confirm要求]對話方塊隨即顯示。 系統會要求您確認資料集名稱以及要刪除資料集的日期。 選取&#x200B;**[!UICONTROL 提交]**&#x200B;以繼續。

提交請求後，工作單即建立並顯示在[!UICONTROL 資料生命週期]工作區的主要標籤上。 從這裡，您可以在工單處理請求時監視工單的狀態。

>[!NOTE]
>
>請參閱[時間軸和透明度](../home.md#dataset-expiration-transparency)的概觀區段，以取得資料集到期在執行後如何處理這些到期的詳細資訊。

## 編輯或取消資料集有效期 {#edit-or-cancel}

若要編輯或取消資料集有效期，請選取工作區首頁面上的&#x200B;**[!UICONTROL 資料集]**，然後從清單中選取資料集有效期。

在資料集到期日的詳細資訊頁面上，右側邊欄會顯示用於編輯或取消已排程刪除的控制項。

## 後續步驟

本檔案說明如何在Experience Platform UI中排程資料集有效期。 有關如何在UI中執行其他資料最小化工作的資訊，請參閱[資料生命週期UI概觀](./overview.md)。

若要瞭解如何使用資料衛生API排程資料集有效期，請參閱[資料集有效期端點指南](../api/dataset-expiration.md)。
