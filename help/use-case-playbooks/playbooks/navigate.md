---
solution: Experience Platform
title: 導覽至使用案例教戰手冊
description: 瞭解如何在教戰手冊的收藏館中導覽，並開始使用勵志沙箱。
role: User
exl-id: 1f5dae75-1136-4be3-9132-01d36a4066ca
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 2%

---

# 導覽至使用案例教戰手冊

所有Adobe Experience Platform客戶都可免費取得使用案例教戰手冊。 若要在Experience Platform UI中存取豐富的使用案例教戰手冊，請從左側導覽中選取&#x200B;**[!UICONTROL 教戰手冊]**。

![使用案例Playbook庫。](/help/use-case-playbooks/assets/playbooks/discover/playbooks-gallery.png)

![直接存取左側導覽列中的使用案例教戰手冊。](/help/use-case-playbooks/assets/playbooks/discover/left-nav-playbooks.png)

選取任何行動手冊以移至詳細資訊頁面，然後選取&#x200B;**[!UICONTROL 移至勵志沙箱]**。 確認強制回應視窗隨即出現。 選取&#x200B;**確認**&#x200B;以移至啟發性的沙箱，您可以在此探索並實驗不同的使用案例。

如果您沒有建立沙箱的許可權，請聯絡您的管理員以尋求建立勵志沙箱的協助。

>[!TIP]
>
>勵志沙箱是Adobe Experience Platform中的開發沙箱，您可以在其中建立、測試及實驗不同的使用案例，然後才在即時生產環境中實作。

![移至勵志沙箱。](/help/use-case-playbooks/assets/playbooks/discover/inspirational-sandbox.png)

如果您尚未設定任何勵志沙箱，請選取&#x200B;**[!UICONTROL 建立勵志沙箱]**。 強制回應視窗隨即顯示。 在必填欄位方塊中輸入&#x200B;**名稱**&#x200B;和&#x200B;**標題**，然後選取&#x200B;**建立**。 建立啟發性的沙箱後，在導覽回使用案例教戰手冊詳細資訊頁面以建立執行個體之前，請確定[定義許可權](/help/access-control/home.md)。

![建立勵志沙箱。](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox.png)

![輸入名稱和標題以建立勵志沙箱。](/help/use-case-playbooks/assets/playbooks/discover/create-inspirational-sandbox-modal.png)

如果您從啟發性的沙箱外部選取使用案例行動手冊，將無法建立例項。 在詳細資訊頁面上，選取&#x200B;**移至勵志沙箱**&#x200B;以移至現有的勵志沙箱，然後選取&#x200B;**[!UICONTROL 建立執行個體]**。

如果您沒有建立沙箱的許可權，請聯絡您的管理員以尋求建立勵志沙箱的協助。

![沒有建立沙箱的許可權。](/help/use-case-playbooks/assets/playbooks/discover/no-permissions-to-create-sandbox.png)

如果您已達到已分配給您的沙箱數量限制，會出現一則訊息，要求您聯絡組織管理員以增加限制，或停用或移除一些使用中的沙箱。 在調整沙箱限制或減少使用中沙箱的數量後，您可以繼續建立啟發性的沙箱。

已達到![沙箱限制。](/help/use-case-playbooks/assets/playbooks/discover/sandbox-limit-reached.png)

請注意，當您建立啟發性的沙箱時，不會自動設定電子郵件、推播和簡訊通知的頻道介面。 請連絡您的IT管理員以手動進行設定，否則執行個體建立可能會失敗。

![設定頻道預設集。](/help/use-case-playbooks/assets/playbooks/discover/configure-channel-presets.png)

## 在Journey Optimizer中設定沙箱和管道表面 {#configure-channel-surfaces}

如果您的組織已獲得[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant)的授權，而您想要使用專為Journey Optimizer設計的教戰手冊，則需要在沙箱中設定頻道預設集，以定義訊息所需的技術引數。 [了解如何在 Adob&#x200B;&#x200B;e Journey Optimizer 中設定管道表面](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=zh-Hant)。

若要在Journey Optimizer中建立教戰手冊的例項，您需要設定電子郵件、推播和簡訊通知的頻道介面。

### 電子郵件頻道介面

前往Journey Optimizer介面中的`Channels`。 設定行銷電子郵件和異動訊息的個別子網域和IP集區（如果尚未設定）。 這些最佳實務可確保異動訊息（例如訂單確認電子郵件）傳遞至您的客戶。 輸入名稱、電子郵件地址和其他設定。 選取頁面右上方的&#x200B;**提交**，以建立行銷管道表面。 閱讀有關[如何設定電子郵件通道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html)的檔案。

### 簡訊頻道介面

若要建立SMS頻道介面，請先建立SMS API認證，然後選取偏好的廠商（例如Sinch）。 為SMS頻道表面命名（例如SMS Marketing），選取設定，然後輸入傳送者號碼。 選取頁面右上方的&#x200B;**提交**&#x200B;以儲存SMS頻道介面。 閱讀有關[如何設定SMS頻道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms)的檔案。

此外，也為包含訂單確認等異動訊息的行動手冊設定頻道。

### 推播頻道介面

確認頻道設定是從Experience Platform或資料收集介面設定。 這是管道設定在資料收集環境中的樣子。

## 後續步驟 {#next-steps}

閱讀本檔案後，您應會知道如何設定啟發靈感的沙箱，並熟悉Experience Platform中存取使用案例教戰手冊的不同方式。 接下來，閱讀如何[選擇](/help/use-case-playbooks/playbooks/choose.md)正確的行動手冊。
