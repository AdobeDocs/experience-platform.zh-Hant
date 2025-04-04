---
title: 使用UI連線AWS Redshift至Experience Platform
description: 瞭解如何使用來源UI將AWS Redshift帳戶連結至Experience Platform。
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 4faf3200-673b-4a20-8f94-d049e800444b
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '719'
ht-degree: 2%

---

# 使用UI連線[!DNL AWS Redshift]至Experience Platform

>[!IMPORTANT]
>
>[!DNL AWS Redshift]來源可在來源目錄中提供給已購買Real-Time Customer Data Platform Ultimate的使用者。

請閱讀本指南，瞭解如何使用UI中的來源工作區將您的[!DNL AWS Redshift]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

- [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： Experience Platform用來組織客戶體驗資料的標準化架構。
   - [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   - [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
- [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已經有有效的[!DNL AWS Redshift]連線，您可以略過本檔案的其餘部分，並繼續進行有關[設定資料流](../../dataflow/databases.md)的教學課程。

## 瀏覽來源目錄

在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取[!UICONTROL 來源]工作區。 您可以從熒幕左側的目錄中選取適當的類別。 或者，您可以使用搜尋選項來尋找您要使用的特定來源。

在&#x200B;*[!UICONTROL 資料庫]*&#x200B;類別下選取&#x200B;**[!DNL AWS Redshift]**，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 一旦驗證帳戶存在，此選項就會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取AWS Redshift來源卡的來源目錄。](../../../../images/tutorials/create/redshift/catalog.png)

## 使用現有帳戶 {#existing}

接下來，您將進入來源工作流程的驗證步驟。 在這裡，您可以使用現有帳戶或建立新帳戶。

若要使用現有的帳戶，請從帳戶目錄中選取[!DNL AWS Redshift]帳戶，然後選取[下一步]**[!UICONTROL 以繼續。]**

![在此列出來源工作流程中現有的帳號。](../../../../images/tutorials/create/redshift/existing.png)

## 建立新帳戶 {#create}

如果您沒有現有的帳戶，則必須提供與您來源對應的必要驗證認證，以建立新的帳戶。

若要建立新帳戶，請選取&#x200B;**[!UICONTROL 新帳戶]**，然後提供名稱並選擇性地為您的帳戶新增說明。

### 在Azure上連線到Experience Platform {#azure}

若要將您的[!DNL AWS Redshift]帳戶連線到Azure上的Experience Platform，請在輸入表單中提供您的驗證認證，然後選取&#x200B;**（[!UICONTROL 連線到來源]）**。

![新帳戶介面，可將AWS Redshift連線至Azure上的Experience Platform。](../../../../images/tutorials/create/redshift/new.png)

| 認證 | 說明 |
| --- | --- |
| 伺服器 | [!DNL AWS Redshift]執行個體的伺服器名稱。 |
| 連接埠 | [!DNL AWS Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| 使用者名稱 | 您要授與存取權的帳戶使用者名稱。 |
| 密碼 | 與使用者帳戶對應的密碼。 |
| 資料庫 | 要從中擷取資料的[!DNL AWS Redshift]資料庫。 |

如需開始使用的詳細資訊，請參閱[此 [!DNL AWS Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)。

### 在AWS上連線至Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在AWS Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

若要建立新的[!DNL AWS Redshift]帳戶並連線至AWS上的Experience Platform，請確定您位於VA6沙箱，提供驗證所需的認證，然後選取&#x200B;**[!UICONTROL 連線至來源]**。

![新帳戶介面，可將AWS Redshift連線至AWS上的Experience Platform。](../../../../images/tutorials/create/redshift/aws-auth.png)

| 認證 | 說明 |
| --- | --- |
| 伺服器 | [!DNL AWS Redshift]執行個體的伺服器名稱。 |
| 連接埠 | [!DNL AWS Redshift]伺服器用來監聽使用者端連線的TCP連線埠。 |
| 使用者名稱 | 您要授與存取權的帳戶使用者名稱。 |
| 密碼 | 與使用者帳戶對應的密碼。 |
| 資料庫 | 要從中擷取資料的[!DNL AWS Redshift]資料庫。 |
| 結構描述 | 與您的[!DNL AWS Redshift]資料庫關聯的結構描述名稱。 您必須確保您要授與資料庫存取權的使用者也擁有此綱要的存取權。 |

如需開始使用的詳細資訊，請參閱[此 [!DNL AWS Redshift] 檔案](https://docs.aws.amazon.com/redshift/latest/gsg/new-user-serverless.html)。

## 後續步驟

依照本教學課程中的指示，您已建立[!DNL AWS Redshift]資料庫與Experience Platform之間的連線。 您現在可以繼續進行下一個教學課程，並[建立資料流，以將資料從您的資料庫擷取到Experience Platform](../../dataflow/databases.md)。