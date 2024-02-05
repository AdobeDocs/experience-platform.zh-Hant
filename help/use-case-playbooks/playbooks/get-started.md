---
solution: Experience Platform
title: 快速入門
description: 了解如何開始使用「使用案例教戰手冊」功能。
role: Admin
exl-id: 1c39792e-49fe-4c5f-9796-fa29f60b7461
source-git-commit: 785e32b27372cef9d23761f648bcbaa431448ce7
workflow-type: tm+mt
source-wordcount: '943'
ht-degree: 14%

---


# 快速入門

瞭解如何針對使用案例行動手冊設定帳戶，這些行動手冊是專為Real-time Customer Data Platform和Adobe Journey Optimizer而設計。 三個主要設定步驟為：

* 建立沙箱
* 設定使用者許可權
* 設定電子郵件、推播和簡訊通知的Journey Optimizer頻道介面(如果您打算使用Journey Optimizer教戰手冊)

## 設定使用案例教戰手冊 — 影片逐步解說 {#video}

觀看此影片，瞭解在Journey Optimizer中建立沙箱、設定許可權及設定電子郵件、推播和簡訊通知的頻道介面所需的步驟。

>[!VIDEO](https://video.tv.adobe.com/v/3426987?learn=on)

## 建立開發沙箱 {#create-development-sandbox}

使用案例教戰手冊使用特殊型別的開發沙箱。 若要開始使用並存取[[!UICONTROL 使用案例教戰手冊]](/help/use-case-playbooks/playbooks/overview.md)功能，[可建立新的開發沙箱](/help/sandboxes/ui/user-guide.md#create) (確保您沒有選取生產沙箱) 並使用尾碼包含 `-ucp` 或 `-UCP` 的名稱 (非標題)，如下所示。

>[!IMPORTANT]
>
>當您建立新的開發沙箱時，請確定名稱包含 `-ucp` 或 `-UCP` 在尾碼中。


![建立使用案例教戰手冊的開發沙箱](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

您現在應該會看到 [!UICONTROL 教戰手冊] 在左側邊欄中的 [!UICONTROL 使用案例教戰手冊].

![建立沙箱後，UI 中的使用案例教戰手冊。](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

如果您沒有如上面所顯示的在左側邊欄中看到[!UICONTROL 教戰手冊]，可使用此連結 `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` 直接瀏覽至該處。在連結中，`<YOUR_ORG>` 是您的組織名稱，而 `<YOUR_SANDBOX_NAME>` 則是您建立的開發沙箱的名稱。

## 授予您的團隊所需的存取權限 {#grant-access-permissions}

開始使用 [!UICONTROL 使用案例教戰手冊]，您的行銷團隊成員需要正確的許可權，才能檢視已建立的教戰手冊清單，或自行建立教戰手冊。

**必要許可權**

若要新增必要許可權，請在許可權UI中，將新的使用案例行動手冊沙箱納入 [您已設定的角色](/help/access-control/abac/ui/permissions.md#managing-sandboxes-for-role)，包括用於其他開發沙箱的沙箱。

![角色的Playbook沙箱已設定](/help/use-case-playbooks/assets/playbooks/get-started/permissions-to-existing-roles.png)

**設定教戰手冊的角色：**

或者，您也可以考慮透過新增角色 [必要的許可權](/help/access-control/home.md#sandboxes-and-permissions).

[設定新角色](/help/access-control/abac/ui/permissions.md) 提供必要的許可權，以執行基本的Playbook工作。 建立角色並將新沙箱新增到其中，如下所示。

![建立角色並將其新增到沙箱](/help/use-case-playbooks/assets/playbooks/get-started/create-new-role.png)

**Playbook執行個體的許可權**

在使用案例教戰手冊中，您將建立各種資產，例如結構描述、受眾、目的地、歷程。 您和其他使用者需要正確的許可權才能建立這些物件。

**結構描述的許可權**

若要建立和管理方案，請使用資料模型許可權； **[!UICONTROL 管理結構描述]**， **[!UICONTROL 檢視結構描述]**， **[!UICONTROL 管理關係]**， **[!UICONTROL 管理身分中繼資料]**

**目的地的許可權**

若要建立和管理目的地，請使用目的地許可權； **[!UICONTROL 管理]**， **[!UICONTROL 目的地]**， **[!UICONTROL 檢視目的地]**， **[!UICONTROL 啟用目的地]**， **[!UICONTROL 啟用區段而不進行對應]**， **[!UICONTROL 管理和啟用資料集目的地]**， **[!UICONTROL 目的地製作]**.

**歷程的許可權**

若要建立和管理歷程，請使用歷程許可權； **[!UICONTROL 管理歷程]**， **[!UICONTROL 檢視歷程]**， **[!UICONTROL 檢視歷程報表]**， **[!UICONTROL 管理歷程]**， **[!UICONTROL 活動]**， **[!UICONTROL 資料來源與動作]**， **[!UICONTROL 檢視歷程]**， **[!UICONTROL 活動]**， **[!UICONTROL 資料來源與動作、發佈歷程]**.

下圖顯示使用者檢視、建立和管理教戰手冊的建議許可權快照，以及教戰手冊產生的資產。

![建立教戰手冊所有例項所需的所有許可權專案的快照](/help/use-case-playbooks/assets/playbooks/get-started/permission-snapshot.png)

**將使用者新增至角色**

一旦您 [已建立新角色](/help/access-control/abac/ui/permissions.md#managing-users-for-role) 如上所述，請將您自己新增為報表套裝的使用者。 如果您為另一組具有僅限檢視存取權的使用者建立具有有限存取權的角色，請僅包含與這些許可權關聯的必要檢視專案。

## 在Journey Optimizer中設定沙箱和管道表面 {#configure-channel-surfaces}

如果您的組織獲得授權 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html)，而您正在尋求使用專為Journey Optimizer設計的教戰手冊，您需要在沙箱中設定頻道預設集，以定義訊息所需的技術引數。 [了解如何在 Adob&#x200B;&#x200B;e Journey Optimizer 中設定管道表面](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=zh-Hant)。

若要在Journey Optimizer中建立教戰手冊的例項，您需要設定電子郵件、推播和簡訊通知的頻道介面。

### 電子郵件頻道介面

前往 `Channels` 在Journey Optimizer介面中。 設定行銷電子郵件和異動訊息的個別子網域和IP集區（如果尚未設定）。 這些最佳實務可確保異動訊息（例如訂單確認電子郵件）傳遞至您的客戶。 輸入名稱、電子郵件地址和其他設定。 選取 **提交** ，以建立行銷管道表面。 請閱讀以下檔案： [如何設定電子郵件頻道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/email/configure-email/email-settings.html).

### 簡訊頻道介面

若要建立SMS頻道介面，請先建立SMS API認證，然後選取偏好的廠商（例如Sinch）。 為SMS頻道表面命名（例如SMS Marketing），選取設定，然後輸入傳送者號碼。 選取 **提交** 位於頁面右上角，儲存SMS頻道介面。 請閱讀以下檔案： [如何設定簡訊頻道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=zh-Hant#message-preset-sms).

此外，也為包含訂單確認等異動訊息的行動手冊設定頻道。

### 推播頻道介面

確認已從Experience Platform或資料收集介面設定應用程式介面。 這就是應用程式表面在資料收集環境中的樣子。

<!-- ![App surfaces in Data collections](/help/use-case-playbooks/assets/playbooks/get-started/.png) -->

接著，選取您在應用程式表面設定中檢視的頻道、平台和應用程式。 選取 **提交** 以建立推播通道表面。

請閱讀以下檔案： [如何設定推播頻道介面](https://experienceleague.adobe.com/docs/journey-optimizer/using/push/push-config/push-configuration.html).

## 後續步驟 {#next-steps}

現在您已依照本檔案中的所有步驟進行，您應該已使用左側導覽中提供的使用案例教戰手冊來建立開發沙箱。 您現在也知道如何授予團隊成員檢視和管理教戰手冊以及產生資產所需的許可權。 接下來，請閱讀如何 [探索正確的行動手冊](/help/use-case-playbooks/playbooks/discover.md) 為您，然後 [從中建立執行個體](/help/use-case-playbooks/playbooks/create-share-reuse.md).