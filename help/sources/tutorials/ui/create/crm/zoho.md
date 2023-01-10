---
keywords: Experience Platform；首頁；熱門主題；Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: 在UI中建立Zoho CRM來源連線
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立Zoho CRM來源連線。
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# 建立 [!DNL Zoho CRM] UI中的源連接

Adobe Experience Platform中的來源連接器可讓您排程內嵌外部來源的CRM資料。 本教學課程提供建立 [!DNL Zoho CRM] 源連接器使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已有有效 [!DNL Zoho CRM] 帳戶，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/crm.md).

### 收集所需憑據

為了連接 [!DNL Zoho CRM] 若要使用Platform，您必須提供下列連線屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 端點 | 的端點 [!DNL Zoho CRM] 伺服器。 |
| 帳戶URL | 帳戶URL可用來產生您的存取權和重新整理Token。 URL必須是網域專屬的。 |
| 用戶端ID | 與您的 [!DNL Zoho CRM] 使用者帳戶。 |
| 用戶端密碼 | 與您的 [!DNL Zoho CRM] 使用者帳戶。 |
| 存取權杖 | 存取權杖可授權您對 [!DNL Zoho CRM] 帳戶。 |
| 重新整理Token | 重新整理Token是用來在您的存取Token過期後產生新存取Token的Token。 |

如需這些認證的詳細資訊，請參閱 [[!DNL Zoho CRM] 驗證](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## 連接您的 [!DNL Zoho CRM] 帳戶

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Zoho CRM] 帳戶 [!DNL Platform].

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽列存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL CRM] 類別，選擇 **[!UICONTROL Zoho CRM]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/zoho/catalog.png)

此 **[!UICONTROL 連接Zoho CRM帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Zoho CRM] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/zoho/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明，以及 [!DNL Zoho CRM] 憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

>[!TIP]
>
>您的帳戶URL網域必須與適當的網域位置對應。 以下是各種網域及其對應的帳戶URL:<ul><li>美國：https://accounts.zoho.com</li><li>澳大利亞：https://accounts.zoho.com.au</li><li>歐洲：https://accounts.zoho.eu</li><li>印度：https://accounts.zoho.in</li><li>中國：https://accounts.zoho.com.cn</li></ul>

![new](../../../../images/tutorials/create/zoho/new.png)

## 後續步驟

依照本教學課程，您已建立與 [!DNL Zoho CRM] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料導入Platform](../../dataflow/crm.md).
