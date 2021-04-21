---
keywords: Experience Platform;home；熱門主題；Microsoft Dynamics;microsoft dynamics;Dynamics;Dynamics
solution: Experience Platform
title: 在UI中建立Microsoft Dynamics Source連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Adobe Experience PlatformUI建立Microsoft Dynamics來源連線。
exl-id: 1a7a66de-dc57-4a72-8fdd-5fd80175db69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 1%

---

# 在UI中建立[!DNL Microsoft Dynamics]源連接

本教學課程提供使用Adobe Experience PlatformUI建立[!DNL Microsoft Dynamics]（下稱&quot;[!DNL Dynamics]&quot;）源連接的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):Experience Platform組織客戶體驗資料的標準化架構。
   * [架構構成基礎](../../../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構編輯器教程](../../../../../xdm/tutorials/create-schema-ui.md):瞭解如何使用架構編輯器UI建立自訂架構。
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，提供統一、即時的消費者個人檔案。

如果您已經擁有有效的[!DNL Dynamics]帳戶，則可跳過本文檔的其餘部分，並繼續有關為CRM源](../../dataflow/crm.md)配置資料流的教程。[

### 收集必要的認證

| 憑證 | 說明 |
| ---------- | ----------- |
| `serviceUri` | [!DNL Dynamics]實例的服務URL。 |
| `username` | [!DNL Dynamics]使用者帳戶的使用者名稱。 |
| `password` | [!DNL Dynamics]帳戶的密碼。 |
| `servicePrincipalId` | [!DNL Dynamics]帳戶的用戶端ID。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| `servicePrincipalKey` | 服務主機密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |

有關開始使用的詳細資訊，請參閱[this [!DNL Dynamics] document](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth)。

## 連接您的[!DNL Dynamics]帳戶

收集完所需憑證後，您可依照下列步驟將[!DNL Dynamics]帳戶連結至平台。

登入[Adobe Experience Platform](https://platform.adobe.com)，然後從左側導覽列選擇&#x200B;**[!UICONTROL Sources]**&#x200B;以存取[!UICONTROL Sources]工作區。 **[!UICONTROL Catalog]**&#x200B;畫面會顯示各種來源，您可以用來建立帳戶。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在&#x200B;**[!UICONTROL CRM]**&#x200B;類別下，選擇&#x200B;**[!UICONTROL Microsoft Dynamics]**。 如果這是您第一次使用此連接器，請選擇&#x200B;**[!UICONTROL Configure]**。 否則，請選擇&#x200B;**[!UICONTROL Add data]**&#x200B;以建立新的[!DNL Dynamics]連接器。

![目錄](../../../../images/tutorials/create/ms-dynamics/catalog.png)

此時將顯示&#x200B;**[!UICONTROL Connect to Dynamics]**&#x200B;頁。 在此頁上，您可以使用新認證或現有認證。

### 新帳戶

如果使用新憑據，請選擇&#x200B;**[!UICONTROL New account]**。 在顯示的輸入表單上，提供新[!DNL Dynamics]帳戶的名稱和選用說明。

[!DNL Dynamics]連接器為您提供不同的訪問驗證類型。 在[!UICONTROL Account authentication]下，選擇&#x200B;**[!UICONTROL Basic authentication]**&#x200B;以使用基於密碼的憑據。

完成後，選擇&#x200B;**[!UICONTROL Connect to source]**，然後允許一些時間建立新帳戶。

![基本認證](../../../../images/tutorials/create/ms-dynamics/basic-auth.png)

或者，您也可以選擇&#x200B;**[!UICONTROL Service-principal and key authentication]**，並使用[!UICONTROL Service principal ID]和[!UICONTROL Service principal key]的組合來連接[!DNL Dynamics]帳戶。

>[!IMPORTANT]
>
> [!DNL Dynamics]中的基本驗證可能會被雙因素驗證所阻止，而平台目前不支援雙因素驗證。 在這種情況下，建議使用基於密鑰的身份驗證來建立使用[!DNL Dynamics]的源連接器。

![密鑰認證](../../../../images/tutorials/create/ms-dynamics/key-based-auth.png)

| 憑證 | 說明 |
| ---------- | ----------- |
| [!UICONTROL Service principal ID] | [!DNL Dynamics]帳戶的用戶端ID。 使用服務主體和基於密鑰的身份驗證時需要此ID。 |
| [!UICONTROL Service principal key] | 服務主機密鑰。 使用服務主體和基於密鑰的身份驗證時需要此憑據。 |

### 現有帳戶

若要連接現有帳戶，請選擇您要連接的[!DNL Dynamics]帳戶，然後選擇右上角的&#x200B;**[!UICONTROL Next]**&#x200B;以繼續。

![現有](../../../../images/tutorials/create/ms-dynamics/existing.png)

## 後續步驟

在本教學課程之後，您已建立與[!DNL Dynamics]帳戶的連線。 您現在可以繼續下一個教程，並[配置資料流以將資料導入Platform](../../dataflow/crm.md)。
