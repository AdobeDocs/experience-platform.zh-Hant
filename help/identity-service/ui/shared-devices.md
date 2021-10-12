---
keywords: Experience Platform；首頁；熱門主題；身分服務；身分服務；共用裝置；共用裝置
solution: Experience Platform
title: 共用裝置概述（測試版）
topic-legacy: tutorial
description: 「共用裝置偵測」可識別相同裝置的不同已驗證使用者，讓客戶資料在身分圖表中的呈現更準確
hide: true
hidefromtoc: true
source-git-commit: 1cdab6ce71c748ae174700ce50f50b143e46b40f
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 0%

---

# 共用裝置偵測概述（測試版）

>[!IMPORTANT]
>
>[!DNL Shared Device Detection]功能為測試版。 其功能和檔案可能會有所變更。

Adobe Experience Platform [!DNL Identity Service]可協助您跨裝置和系統橋接身分，以便即時提供具影響力的個人數位體驗，進而更全面了解客戶及其行為。

[!DNL Shared Device] 是指多個個人使用的裝置。共用裝置的範例包括平板電腦、程式庫電腦和資訊站。 透過[!DNL Shared Device Detection]功能，可防止將同一裝置的不同使用者合併為單一身分，以更精確地呈現個人。

使用[!DNL Shared Device Detection]，您可以：

* 為同一設備的不同用戶建立單獨的標識圖；
* 防止使用同一設備的不同個體的資料混合；
* 生成更清晰、更準確的客戶視圖。

>[!TIP]
>
>[!DNL Shared Device Detection]的設定必須在啟用資料集的設定檔之前完成，因為一旦在[!DNL Identity Service]中產生圖表，您便無法再修訂設定。

## 快速入門

使用[!DNL Shared Device Detection]需要了解所涉的各種平台服務。 Before beginning to work with [!DNL Shared Device Detection], please review the documentation for the following services:

* [[!DNL Identity Service]](../home.md):跨裝置和系統橋接身分，以更全面了解個別客戶及其行為。
   * [身分圖表檢視器](./identity-graph-viewer.md):以視覺化方式與身分圖表檢視器互動，以便更清楚了解客戶身分識別的匯整方式，以及匯整方式。
   * [身分識別命名空間](../namespaces.md):請參閱完全限定身分的元件，以及身分識別命名空間如何讓您區分身分識別的內容和類型。

### 術語

下表列出了了解[!DNL Shared Device Detection]所必需的術語：

| 詞彙 | 定義 |
| --- | --- |
| 共用裝置 | 共用裝置是指由多個個人使用的任何裝置。 共用裝置的範例包括平板電腦、程式庫電腦和資訊站。 |
| [!DNL Shared Device Detection] | [!DNL Shared Device Detection] 指的是一種配置設定，允許來自同一設備的不同用戶的資料彼此分離。 |
| [!UICONTROL 共用身分命名空間] | [!UICONTROL 共用身份命名空間]用於表示由多個不同用戶共用的單個設備。 |
| [!UICONTROL 使用者身分命名空間] | [!UICONTROL 使用者身分命名空間]代表已驗證或登入的共用裝置使用者。 |

## 共用裝置UI

在Platform UI中，從左側導覽中選取&#x200B;**[!UICONTROL 身分]**，然後選取&#x200B;**[!UICONTROL 身分設定]**。

![identity-dashboard](../images/shared-device/identity-dashboard.png)

此時將顯示「[!UICONTROL 共用設備設定]」頁，該頁為您提供了配置資料共用設備設定的介面。 共用裝置設定預設為停用。

啟用後，共用設備設定允許來自同一設備的不同用戶的資料彼此分離。 This configuration setting allows for a cleaner and more accurate representation of identity graphs, where user identities of the same device are not combined together.

選擇&#x200B;**[!UICONTROL 啟用]**&#x200B;以開始修改共用設備設定。

![enable-shared-device](../images/shared-device/enable-shared-device.png)

此時將顯示「共用身份命名空間]」和「[!UICONTROL 用戶身份命名空間]」配置選項，允許您修改要使用的身份命名空間。[!UICONTROL 

![set-namespaces](../images/shared-device/set-namespaces.png)

[!UICONTROL 共用身] 分命名空間代表多個不同使用者使用的單一裝置。此命名空間一律會設為&#x200B;**[!UICONTROL ECID]**，因為所有Platform使用者都使用&#x200B;**[!UICONTROL ECID]**&#x200B;作為網頁瀏覽器識別碼。

![shared-identity-namespace](../images/shared-device/shared-identity-namespace.png)

[!UICONTROL 使用者身分命名空間]可讓您識別相同裝置的不同使用者，並防止資料合併至相同的身分圖表。

![user-identity-namespace](../images/shared-device/user-identity-namespace.png)

選擇&#x200B;**[!UICONTROL 用戶身份命名空間]**&#x200B;搜索欄，然後輸入身份命名空間或從下拉菜單中選擇身份命名空間。

>[!TIP]
>
>[!UICONTROL 使用者身分識別命名空間]應對應至與一般使用者登入ID對應的身分識別命名空間。 選項包括客戶ID、電子郵件和雜湊電子郵件。

![電子郵件](../images/shared-device/emails.png)

配置[!UICONTROL 共用設備設定]後，選擇&#x200B;**[!UICONTROL 保存]**。

![儲存](../images/shared-device/save.png)

出現彈出窗口，提示您確認您的選擇。 選擇&#x200B;**[!UICONTROL Yes]**&#x200B;以完成配置設定。

![confirm](../images/shared-device/confirm.png)
