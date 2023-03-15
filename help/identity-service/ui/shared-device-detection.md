---
keywords: Experience Platform；首頁；熱門主題；身分服務；身分服務；共用裝置；共用裝置
title: 共用裝置概述（測試版）
description: 「共用裝置偵測」可識別相同裝置的不同已驗證使用者，讓客戶資料在身分圖表中的呈現更準確
hide: true
hidefromtoc: true
exl-id: 36318163-ba07-4209-b1be-dc193ab7ba41
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# 共用裝置偵測概述（測試版）

>[!IMPORTANT]
>
>此 [!DNL Shared Device Detection] 功能已測試。 其功能和檔案可能會有所變更。

Adobe Experience Platform [!DNL Identity Service] 可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。

[!DNL Shared Device] 是指多個個人使用的裝置。 共用裝置的範例包括平板電腦、程式庫電腦和資訊站。 透過 [!DNL Shared Device Detection] 功能，可防止將同一裝置的不同使用者合併為單一身分，以更精確地呈現個人。

使用 [!DNL Shared Device Detection] 您可以：

* 為同一設備的不同用戶建立單獨的標識圖；
* 防止使用同一設備的不同個體的資料混合；
* 生成更清晰、更準確的客戶視圖。

>[!TIP]
>
>配置 [!DNL Shared Device Detection] 必須在啟用資料集的設定檔之前完成，因為一旦在中產生圖表，您就無法再修訂設定 [!DNL Identity Service].

## 開始使用 [!DNL Shared Device Detection]

使用 [!DNL Shared Device Detection] 需要了解所涉的各種Platform服務。 開始使用之前 [!DNL Shared Device Detection]，請查閱以下服務的檔案：

* [[!DNL Identity Service]](../home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
   * [身分圖表檢視器](./identity-graph-viewer.md):以視覺化方式與身分圖表檢視器互動，以便更清楚了解客戶身分識別的匯整方式，以及匯整方式。
   * [身分識別命名空間](../namespaces.md):請參閱完全限定身分的元件，以及身分識別命名空間如何讓您區分身分識別的內容和類型。

## 瞭解 [!DNL Shared Device Detection]

使用時，請務必了解下列術語
[!DNL Shared Device Detection]. 請參閱下表，以取得了解之必要術語的清單 [!DNL Shared Device Detection].

### 術語

| 詞彙 | 定義 |
| --- | --- |
| 共用裝置 | 共用裝置是指由多個個人使用的任何裝置。 共用裝置的範例包括平板電腦、程式庫電腦和資訊站。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 指的是一種配置設定，允許來自同一設備的不同用戶的資料彼此分離。 |
| 共用身分命名空間 | 「共用身分命名空間」代表可供多名使用者使用的裝置。 「共用身分識別命名空間」通常是ECID，但可設為其他裝置ID。 |
| 使用者身分命名空間 | 使用者身分命名空間代表已驗證（登入）的共用裝置使用者。 |
| 上次驗證的使用者 | 如果裝置是由多個帳戶登入，則上次驗證的使用者代表上次登入裝置的使用者。 |

{style="table-layout:auto"}

[!DNL Shared Device Detection] 可建立兩個命名空間來運作。the **共用身分命名空間** 和 **使用者身分命名空間**.

* 「共用身分命名空間」代表可供多名使用者使用的裝置。 Adobe建議客戶使用ECID做為共用裝置識別碼。
* 「使用者身分識別命名空間」對應至與使用者登入ID對應的身分識別命名空間，這可以是使用者的CRM ID、電子郵件地址、雜湊電子郵件或電話號碼。

共用裝置（如平板電腦）只有 **共用身分命名空間**. 另一方面，共用裝置的每個使用者都有自己的指定 **使用者身分命名空間** 與其個別登入ID對應。 例如，Kevin和Nora分享給電子商務使用的平板電腦，其ECID為 `1234`，而Kevin有自己的使用者身分命名空間已對應至其 `kevin@email.com` 帳戶和Nora有對應至她的使用者身分識別命名空間 `nora@email.com` 帳戶。

[!DNL Shared Device Detection] 可連結共用身分命名空間(例如， ECID)和上次驗證的使用者使用者身分命名空間（登入ID）。

### 如何將身分資料傳送至身分圖表

請參考下列範例，協助您了解如何 [!DNL Shared Device Detection] 工作：

>[!NOTE]
>
>此圖表中，共用身分命名空間已設為ECID，而使用者身分命名空間已設為CRM ID。

![圖表](../images/shared-device/diagram.png)

* 凱文和諾拉共用平板電腦訪問電子商務網站。 不過，他們都有自己獨立的賬戶，每個人都用這些賬戶來瀏覽和線上購物；
   * 平板電腦是共用裝置，其ECID代表平板電腦的網頁瀏覽器Cookie ID;
* 假設Kevin使用平板電腦和 **登入** 他的電子商務帳戶瀏覽耳機，這表示Kevin的CRM ID(**使用者身分命名空間**)現在已與平板電腦的ECID(**共用身分命名空間**)。 平板電腦的瀏覽資料現已與Kevin的身分圖表整合。
   * 如果凱文 **註銷** 諾拉用的是 **登入** 連結至自己的帳戶並購買相機，之後系統會將其CRM ID連結至平板電腦的ECID。 因此，平板電腦的瀏覽資料現在已與Nora的身分圖表整合。
   * 如果諾拉 **未登出** 凱文用的是平板電腦，但 **未登入**，則平板電腦的瀏覽資料仍會與Nora整合，因為她仍是已驗證的使用者，且其CRM ID仍會連結至平板電腦的ECID。
   * 如果諾拉 **註銷** 凱文用的是平板電腦，但 **未登入**，則平板電腦的瀏覽資料仍會與Nora的身分圖表整合，因為 **上次驗證的使用者**，則其CRM ID仍會與平板電腦的ECID連結。
   * 如果凱文 **登入** 同樣地，他的CRM ID現在會連結至平板電腦的ECID，因為他現在是最後一個已驗證的使用者，而平板電腦的瀏覽資料現在已與其身分圖表整合。

### 如何 [!DNL Profile Service] 合併設定檔片段 [!DNL Shared Device Detection] 已啟用

[!DNL Profile Service] 記下設定檔片段和已合併的設定檔。 每個個別客戶設定檔都由多個已合併的設定檔片段組成，以形成該客戶的單一檢視。 例如，如果客戶跨多個管道與您的品牌互動，您的組織會在多個資料集中顯示與該單一客戶相關的多個設定檔片段。 將這些片段擷取至Platform時，會合併在一起，以便為該客戶建立單一設定檔。

當 [!DNL Shared Device Detection] 啟用， [!DNL Profile] 會根據體驗事件是已驗證還是未驗證來定義設定檔片段的主要身分

安 **驗證體驗事件** 是使用者登入裝置時完成的動作。 若為已驗證的體驗事件，主要身分為 **使用者身分命名空間** （登入ID）。 安 **未驗證的體驗事件** 是未登入裝置的使用者完成的動作。 若為未驗證的體驗事件，主要身分為 **共用身分命名空間** (ECID)。

如需詳細資訊，請參閱  [[!DNL Real-Time Customer Profile] 概述](../../profile/home.md).

## 共用裝置UI

在平台UI中，選取 **[!UICONTROL 身分]** 從左側導覽中，然後選取 **[!UICONTROL 身分設定]**.

![identity-dashboard](../images/shared-device/identity-dashboard.png)

此 [!UICONTROL 共用裝置設定] 頁面，提供您為資料配置共用設備設定的介面。 共用裝置設定預設為停用。

啟用後，共用設備設定允許來自同一設備的不同用戶的資料彼此分離。 此配置設定允許更簡潔和更精確地表示身份圖，其中不將同一設備的用戶身份組合在一起。

選擇 **[!UICONTROL 啟用]** 以開始修改共用設備設定。

![enable-shared-device](../images/shared-device/enable-shared-device.png)

此 [!UICONTROL 共用身分命名空間] 和 [!UICONTROL 使用者身分命名空間] 設定選項隨即顯示，可讓您修改要使用的身分識別命名空間。

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL 共用身分命名空間] 代表多個不同使用者使用的單一裝置。 此命名空間一律設為 **[!UICONTROL ECID]** 因為所有Platform使用者都使用 **[!UICONTROL ECID]** 作為網頁瀏覽器識別碼。

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

此 [!UICONTROL 使用者身分命名空間] 可讓您識別相同裝置的不同使用者，並防止資料合併至相同的身分圖表。

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

選取 **[!UICONTROL 使用者身分命名空間]** 搜尋列，然後輸入身分命名空間，或從下拉式選單中選取身分命名空間。

>[!TIP]
>
>此 [!UICONTROL 使用者身分命名空間] 應對應至與使用者登入ID對應的身分命名空間。 選項包括客戶ID、電子郵件和雜湊電子郵件。

![電子郵件](../images/shared-device/emails.png)

在您設定 [!UICONTROL 共用裝置設定]，選取 **[!UICONTROL 儲存]**.

![儲存](../images/shared-device/save.png)

出現彈出窗口，提示您確認您的選擇。 選擇 **[!UICONTROL 是]** 完成配置設定。

![confirm](../images/shared-device/confirm.png)
