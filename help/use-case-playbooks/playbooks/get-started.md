---
solution: Experience Platform
title: 快速入門
description: 瞭解如何開始使用使用使用案例教戰手冊功能。
badgeBeta: label="Beta" type="Informative"
source-git-commit: 297dc9d6252d401f805fa5ebb5cf5111910286cf
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 8%

---


# (Beta)開始使用

>[!AVAILABILITY]
>
>此功能目前為測試版，並未開放所有使用者使用。 文件和功能可能會有所變更。

## 建立開發沙箱 {#create-development-sandbox}

若要開始使用並存取 [[!UICONTROL 使用案例教戰手冊]](/help/use-case-playbooks/playbooks/overview.md) 功能， [建立新的開發沙箱](/help/sandboxes/ui/user-guide.md#create) （請確定您沒有選取生產沙箱），其名稱（而非標題）包含 `-ucp` 或 `-UCP` 尾碼中的，如下所示。

![建立使用案例行動手冊的開發沙箱](/help/use-case-playbooks/assets/playbooks/get-started/create-sandbox-ucp.png)

您現在應該看到 [!UICONTROL 教戰手冊] 在左側邊欄中的 [!UICONTROL 使用案例教戰手冊] 或低於 [!UICONTROL 行銷人員遊樂場].

![建立沙箱後UI中的使用案例教戰手冊。](/help/use-case-playbooks/assets/playbooks/get-started/ucp-sandbox-in-ui.png)

如果您沒有看見 [!UICONTROL 教戰手冊] 在左側邊欄中（如上所示），使用此連結 `https://experience.adobe.com/#/@<YOUR_ORG>/sname:<YOUR_SANDBOX_NAME>/platform/mexp/templates` 直接導覽至該處。 在連結中， `<YOUR_ORG>` 是貴組織的名稱，並 `<YOUR_SANDBOX_NAME>` 是您建立的開發沙箱名稱。

### Adobe Journey Optimizer使用者的沙箱設定 {#sandbox-configuration-journey-optimizer}

如果貴組織獲得授權 [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=zh-Hant)，您需要在沙箱中設定管道預設集，這些預設集會定義訊息所需的技術引數。 [瞭解如何在Adobe Journey Optimizer中設定管道表面](https://experienceleague.adobe.com/docs/journey-optimizer/using/configuration/channel-surfaces.html?lang=zh-Hant).

## 授予您的團隊必要的存取許可權 {#grant-access-permissions}

開始使用 [!UICONTROL 使用案例教戰手冊]時，行銷營運團隊的成員需要正確的許可權。 您可以依照下列方式授與您的團隊許可權：

* 只想瀏覽教戰手冊的行銷營運團隊成員可以取得 **讀取** 許可權。
* 想要從教戰手冊建立執行個體的行銷營運團隊成員可以取得 **讀取和寫入** 許可權。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何開始使用 [!UICONTROL 使用案例教戰手冊]. 接下來，閱讀如何 [探索正確的行動手冊](/help/use-case-playbooks/playbooks/discover.md) 為您，然後 [從中建立執行個體](/help/use-case-playbooks/playbooks/create-share-reuse.md).
