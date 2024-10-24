---
keywords: Experience Platform；首頁；熱門主題；身分服務；身分服務；共用裝置；共用裝置
title: 共用裝置概述(Beta)
description: 共用裝置偵測可識別相同裝置的不同已驗證使用者，以便在身分圖表中更準確地呈現客戶資料
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 2a2e3fcc4c118925795951a459a2ed93dfd7f7d7
workflow-type: tm+mt
source-wordcount: '1353'
ht-degree: 0%

---

# 共用裝置偵測概觀(Beta)

>[!IMPORTANT]
>
>[!DNL Shared Device Detection]功能為測試版。 其功能和檔案可能會有所變更。

Adobe Experience Platform [!DNL Identity Service]可跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，協助您更清楚瞭解客戶及其行為。

[!DNL Shared Device]是指一個以上個人使用的裝置。 舉例來說，共用裝置包含平板電腦、圖書館電腦和資訊站。 透過[!DNL Shared Device Detection]功能，可防止同一裝置的不同使用者合併為單一身分，以更精確的方式呈現個人。

透過[!DNL Shared Device Detection]，您可以：

* 為相同裝置的不同使用者建立個別的身分圖表；
* 避免混合使用相同裝置的不同個人資料；
* 為您的客戶產生更簡潔且更精確的檢視。

>[!TIP]
>
>在啟用資料集的設定檔之前，必須先完成[!DNL Shared Device Detection]的設定，因為一旦在[!DNL Identity Service]中產生圖形，您就無法再修訂設定。

## 快速入門：[!DNL Shared Device Detection]

使用[!DNL Shared Device Detection]需要瞭解相關的各種Platform服務。 開始使用[!DNL Shared Device Detection]之前，請檢閱下列服務的檔案：

* [[!DNL Identity Service]](./home.md)：跨裝置和系統橋接身分，以更清楚瞭解個別客戶及其行為。
   * [身分圖表檢視器](./features/identity-graph-viewer.md)：將身分圖表檢視器視覺化並與之互動，以更加瞭解客戶身分如何拼接在一起，以及拼接方式為何。
   * [身分識別名稱空間](./features/namespaces.md)：檢視完整身分識別的元件，以及身分識別名稱空間如何讓您區分身分識別的內容和型別。

## 瞭解 [!DNL Shared Device Detection]

使用時，請務必瞭解下列術語
[!DNL Shared Device Detection]。 請參閱下表，以取得瞭解[!DNL Shared Device Detection]所必須的辭彙清單。

### 術語

| 辭彙 | 定義 |
| --- | --- |
| 共用裝置 | 共用裝置是指不止一個使用者使用的任何裝置。 舉例來說，共用裝置包含平板電腦、圖書館電腦和資訊站。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection]是指允許來自相同裝置不同使用者的資料彼此分離的組態設定。 |
| 共用的身分命名空間 | 共用身分名稱空間代表多個使用者可以使用的裝置。 共用身分名稱空間通常是ECID，但可以設定為其他裝置ID。 |
| 使用者身分命名空間 | 使用者身分名稱空間代表共用裝置的已驗證（已登入）使用者。 |
| 上次驗證的使用者 | 如果裝置正由多個帳戶登入，則上次驗證的使用者代表上次登入裝置的使用者。 |

{style="table-layout:auto"}

[!DNL Shared Device Detection]藉由建立兩個名稱空間來運作： **共用身分名稱空間**&#x200B;和&#x200B;**使用者身分名稱空間**。

* 共用身分名稱空間代表多個使用者可以使用的裝置。 Adobe建議客戶使用ECID作為共用裝置識別碼。
* 使用者身分名稱空間會對應至對應至使用者登入ID的身分名稱空間，這可以是使用者的CRMID、電子郵件地址、雜湊電子郵件或電話號碼。

共用裝置（例如平板電腦）具有單一&#x200B;**共用身分名稱空間**。 另一方面，共用裝置的每個使用者都有自己的指定&#x200B;**使用者身分名稱空間**，這些名稱空間會對應到其各自的登入ID。 例如，Kevin和Nora共用用於電子商務的平板電腦有自己的ECID `1234`，而Kevin有自己的使用者身分名稱空間對應到他的`kevin@email.com`帳戶，而Nora有自己的使用者身分名稱空間對應到她的`nora@email.com`帳戶。

[!DNL Shared Device Detection]可以連結共用的身分名稱空間(例如， ECID)搭配上次驗證的使用者身分名稱空間（登入ID）。

### 如何將身分資料傳送至身分圖表

請參考下列範例，協助您瞭解[!DNL Shared Device Detection]的運作方式：

>[!NOTE]
>
>在此圖表中，共用身分名稱空間已設定為ECID，而使用者身分名稱空間已設定為CRMID。

![圖表](./images/shared-device/diagram.png)

* Kevin和Nora分享平板電腦來造訪電子商務網站。 不過，他們都有自己的獨立帳戶，用於瀏覽和線上購物；
   * 做為共用裝置，平板電腦擁有對應的ECID，代表平板電腦的網頁瀏覽器Cookie ID；
* 假設Kevin使用平板電腦並&#x200B;**登入**&#x200B;電子商務帳戶來瀏覽耳機，這表示Kevin的CRMID （**使用者身分名稱空間**）現在與平板電腦的ECID （**共用身分名稱空間**）連結。 平板電腦的瀏覽資料現在已與Kevin的身分圖表整合。
   * 如果Kevin **登出**，而Nora使用平板電腦，並&#x200B;**登入**&#x200B;自己的帳戶並購買相機，則她的CRMID現在已連結到平板電腦的ECID。 因此，平板電腦的瀏覽資料現在已與Nora的身分圖表合併。
   * 如果Nora **未登出**，而Kevin使用平板電腦，但&#x200B;**未登入**，則平板電腦的瀏覽資料仍會與Nora合併，因為她仍為已驗證的使用者，且她的CRMID仍與平板電腦的ECID連結。
   * 如果Nora **確實登出**，而Kevin使用平板電腦，但&#x200B;**沒有登入**，則平板電腦的瀏覽資料仍會與Nora的身分圖表合併，因為作為&#x200B;**上次驗證的使用者**，她的CRMID仍會與平板電腦的ECID連結。
   * 如果Kevin **再次登入**，他的CRMID現在會連結到平板電腦的ECID，因為他現在是最後驗證的使用者，而且平板電腦的瀏覽資料現在已合併到他的身分圖表中。

### [!DNL Profile Service]如何合併[!DNL Shared Device Detection]已啟用的設定檔片段

[!DNL Profile Service]記下設定檔片段和合併的設定檔。 每個個別客戶設定檔都由多個設定檔片段組成，這些片段已合併以構成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，則您的組織將會有多個與該單一客戶相關的設定檔片段出現在多個資料集中。 這些片段在擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。

啟用[!DNL Shared Device Detection]時，[!DNL Profile]會根據體驗事件是否已驗證或未驗證，定義設定檔片段的主要身分

**已驗證的體驗事件**&#x200B;是使用者登入裝置時完成的動作。 對於已驗證的體驗事件，主要身分是&#x200B;**使用者身分名稱空間** （登入識別碼）。 **未驗證的體驗事件**&#x200B;是未登入裝置的使用者所完成的動作。 對於未驗證的體驗事件，主要身分是&#x200B;**共用身分名稱空間** (ECID)。

如需詳細資訊，請參閱[[!DNL Real-Time Customer Profile] 總覽](../profile/home.md)。

## 共用裝置UI

在Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 身分]**，然後選取&#x200B;**[!UICONTROL 身分設定]**。

![身分識別儀表板](./images/shared-device/identity-dashboard.png)

「[!UICONTROL 共用裝置設定]」頁面會出現，提供您介面來設定資料的共用裝置設定。 共用裝置設定預設為停用。

啟用時，共用裝置設定可讓來自相同裝置不同使用者的資料互相分離。 此組態設定可讓身分圖表呈現得更清楚、更準確，因為相同裝置的使用者身分不會合併在一起。

選取&#x200B;**[!UICONTROL 啟用]**&#x200B;以開始修改您的共用裝置設定。

![啟用 — 共用裝置](./images/shared-device/enable-shared-device.png)

[!UICONTROL 共用身分名稱空間]和[!UICONTROL 使用者身分名稱空間]組態選項出現，可讓您修改要使用的身分名稱空間。

![設定名稱空間](./images/shared-device/set-namespaces.png)

[!UICONTROL 共用身分名稱空間]代表多個不同使用者使用的單一裝置。 此名稱空間一律設為&#x200B;**[!UICONTROL ECID]**，因為所有Platform使用者都會使用&#x200B;**[!UICONTROL ECID]**&#x200B;做為網頁瀏覽器識別碼。

![共用身分名稱空間](./images/shared-device/shared-identity-namespace.png)

[!UICONTROL 使用者身分識別名稱空間]可讓您識別相同裝置的不同使用者，並防止資料合併到相同的身分圖表中。

![使用者身分識別名稱空間](./images/shared-device/user-identity-namespace.png)

選取&#x200B;**[!UICONTROL 使用者身分名稱空間]**&#x200B;搜尋列，然後輸入身分名稱空間或從下拉式功能表選取身分名稱空間。

>[!TIP]
>
>[!UICONTROL 使用者身分識別名稱空間]應該對應到對應到一般使用者登入識別碼的身分識別名稱空間。 選項包括客戶ID、電子郵件和雜湊電子郵件。

![電子郵件](./images/shared-device/emails.png)

設定[!UICONTROL 共用裝置設定]後，請選取&#x200B;**[!UICONTROL 儲存]**。

![儲存](./images/shared-device/save.png)

會出現一個快顯視窗，提示您確認您的選取。 選取&#x200B;**[!UICONTROL 是]**&#x200B;以完成組態設定。

![確認](./images/shared-device/confirm.png)
