---
solution: Experience Platform
title: 導覽至使用案例教戰手冊
description: 瞭解如何在教戰手冊的收藏館中導覽，並開始使用勵志沙箱。
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: 54b3d2ef22f7afb47fa8c9430c5c1645c94c837d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# 導覽至使用案例教戰手冊

所有Adobe Experience Platform客戶都可免費取得使用案例教戰手冊。 若要在Experience Platform UI中存取豐富的用例教戰手冊，請選取 **[!UICONTROL 教戰手冊]** 從左側導覽。

![使用案例Playbook庫。](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![直接存取左側導覽列中的使用案例教戰手冊。](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

選取任一Playbook前往詳細資訊頁面，然後選取 **[!UICONTROL 前往勵志沙箱]**. 確認強制回應視窗隨即出現。 選取 **確認** 前往勵志沙箱，探索並實驗不同的使用案例。

如果您沒有建立沙箱的許可權，請聯絡您的管理員以尋求建立勵志沙箱的協助。

>[!TIP]
>
>勵志沙箱是Adobe Experience Platform中的開發沙箱，您可以在其中建立、測試及實驗不同的使用案例，然後才在即時生產環境中實作。

![前往勵志沙箱。](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

如果您尚未設定任何勵志沙箱，請選取「 」 **[!UICONTROL 建立勵志沙箱]**. 強制回應視窗隨即顯示。 輸入 **名稱** 和 **標題** 在必填欄位方塊中，然後選取 **建立**. 建立啟發性的沙箱後，請確保 [定義許可權](/help/access-control/home.md) 切換作業選項回使用案例教戰手冊詳細資料頁面以建立執行個體之前。

![建立鼓舞人心的沙箱。](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![輸入名稱和標題以建立勵志沙箱。](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

如果您從啟發性的沙箱外部選取使用案例行動手冊，將無法建立例項。 在詳細資訊頁面上，選取 **前往勵志沙箱** 前往現有的勵志沙箱，然後選取 **[!UICONTROL 建立例項]**.

如果您沒有建立沙箱的許可權，請聯絡您的管理員以尋求建立勵志沙箱的協助。

![沒有建立沙箱的許可權。](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

如果您已達到已分配給您的沙箱數量限制，會出現一則訊息，要求您聯絡組織管理員以增加限制，或停用或移除一些使用中的沙箱。 在調整沙箱限制或減少使用中沙箱的數量後，您可以繼續建立啟發性的沙箱。

![已達到沙箱限制。](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

請注意，當您建立啟發性的沙箱時，不會自動設定電子郵件、推播和簡訊通知的頻道介面。 請連絡您的IT管理員以手動進行設定，否則執行個體建立可能會失敗。

![設定頻道預設集。](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## 在Journey Optimizer中設定沙箱和管道表面 {#configure-channel-surfaces}

如果您的組織獲得授權 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant)，而您正在尋求使用專為Journey Optimizer設計的教戰手冊，您需要在沙箱中設定頻道預設集，以定義訊息所需的技術引數。 [了解如何在 Adob&#x200B;&#x200B;e Journey Optimizer 中設定管道表面](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=zh-Hant)。

若要在Journey Optimizer中建立教戰手冊的例項，您需要設定電子郵件、推播和簡訊通知的頻道介面。

### 電子郵件頻道介面

前往 `Channels` 在Journey Optimizer介面中。 設定行銷電子郵件和異動訊息的個別子網域和IP集區（如果尚未設定）。 這些最佳實務可確保異動訊息（例如訂單確認電子郵件）傳遞至您的客戶。 輸入名稱、電子郵件地址和其他設定。 選取 **提交** ，以建立行銷管道表面。 請閱讀以下檔案： [如何設定電子郵件頻道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### 簡訊頻道介面

若要建立SMS頻道介面，請先建立SMS API認證，然後選取偏好的廠商（例如Sinch）。 為SMS頻道表面命名（例如SMS Marketing），選取設定，然後輸入傳送者號碼。 選取 **提交** 位於頁面右上角，儲存SMS頻道介面。 請閱讀以下檔案： [如何設定簡訊頻道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms).

此外，也為包含訂單確認等異動訊息的行動手冊設定頻道。

### 推播頻道介面

確認已從Experience Platform或資料收集介面設定應用程式介面。 這就是應用程式表面在資料收集環境中的樣子。

## 後續步驟 {#next-steps}

閱讀本檔案後，您應會知道如何設定啟發靈感的沙箱，並熟悉存取Platform內使用案例教戰手冊的不同方式。 接下來，請閱讀如何 [選擇](/help/use-case-playbooks/playbooks/choose.md) 正確的行動手冊。
