---
title: 透過UI將您的Salesforce Marketing Cloud帳戶連線至Experience Platform
description: 瞭解如何透過UI將您的Salesforce Marketing Cloud帳戶連結至Experience Platform。
exl-id: 1d9bde60-31e0-489c-9c1c-b6471e0ea554
source-git-commit: 0c6a51d06e57eb6de063a350bd4b17022555a0b4
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 0%

---

# 透過UI將您的[!DNL Salesforce Marketing Cloud]帳戶連線至Experience Platform

>[!WARNING]
>
>[!DNL Salesforce Marketing Cloud]來源將於2026年1月汰除。 新的來源將作為替代方案於今年晚些時候發行。 釋放新來源後，您必須在2026年1月底之前建立新的帳戶連線和資料流，以計畫移轉至新來源。

閱讀本指南，瞭解如何使用Experience Platform使用者介面中的來源工作區將您的[!DNL Salesforce Marketing Cloud]帳戶連結至Adobe Experience Platform。

## 快速入門

本教學課程需要您實際瞭解下列Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md)： [!DNL Experience Platform]用來組織客戶體驗資料的標準化架構。
   * [結構描述組合的基本概念](../../../../../xdm/schema/composition.md)：瞭解XDM結構描述的基本建置區塊，包括結構描述組合中的關鍵原則和最佳實務。
   * [結構描述編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md)：瞭解如何使用結構描述編輯器使用者介面建立自訂結構描述。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md)：根據來自多個來源的彙總資料，提供統一的即時消費者設定檔。

如果您已有[!DNL Salesforce Marketing Cloud]帳戶，可以略過本檔案的其餘部分，然後繼續進行[使用UI將行銷自動化資料帶入Experience Platform的教學課程](../../dataflow/marketing-automation.md)。

### 收集必要的認證

閱讀[[!DNL Salesforce Marketing Cloud] 總覽](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#prerequisites)以取得驗證的相關資訊。

## 瀏覽來源目錄

>[!IMPORTANT]
>
>[!DNL Salesforce Marketing Cloud]來源整合目前不支援自訂物件擷取。


在Experience Platform UI中，從左側導覽選取&#x200B;**[!UICONTROL 來源]**&#x200B;以存取&#x200B;*[!UICONTROL 來源]*&#x200B;工作區。 選擇類別或使用搜尋列來尋找您的來源。

若要連線到[!DNL Salesforce Marketing Cloud]，請移至&#x200B;*[!UICONTROL 行銷自動化]*&#x200B;類別，選取&#x200B;**[!UICONTROL Salesforce Marketing Cloud]**&#x200B;來源卡，然後選取&#x200B;**[!UICONTROL 設定]**。

>[!TIP]
>
>當指定的來源尚未具有已驗證的帳戶時，來源目錄中的來源會顯示&#x200B;**[!UICONTROL 設定]**&#x200B;選項。 建立已驗證的帳戶後，此選項會變更為&#x200B;**[!UICONTROL 新增資料]**。

![已選取Salesforce Marketing Cloud來源卡的來源目錄。](../../../../images/tutorials/create/salesforce-marketing-cloud/catalog.png)

## 使用現有帳戶 {#existing}

若要使用現有帳戶，請選取&#x200B;**[!UICONTROL 現有帳戶]**，然後選取您要使用的[!DNL Salesforce Marketing Cloud]帳戶。

![來源工作流程中已選取「現有帳戶」的現有帳戶介面。](../../../../images/tutorials/create/salesforce-marketing-cloud/existing.png)

## 建立新帳戶 {#new}

您可以使用[!DNL Salesforce Marketing Cloud]來源連線至[!DNL Azure]或[!DNL Amazon Web Services] (AWS)上的Experience Platform。

### 在[!DNL Azure]上連線到Experience Platform {#azure}

若要在[!DNL Azure]上連線至Experience Platform，請提供帳戶名稱、選擇性說明以及您的[帳戶驗證認證](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#azure)。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![來源工作流程中的新帳戶介面，用於連線至Azure上的Experience Platform。](../../../../images/tutorials/create/salesforce-marketing-cloud/new-azure.png)

### 在Amazon Web Services (AWS)上連線至Experience Platform {#aws}

>[!AVAILABILITY]
>
>本節適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](../../../../../landing/multi-cloud.md)。

若要在[!DNL AWS]上連線至Experience Platform，請確定您位於VA6沙箱，並提供帳戶名稱、選擇性說明以及您的[帳戶驗證認證](../../../../connectors/marketing-automation/salesforce-marketing-cloud.md#aws)。 完成後，請選取&#x200B;**[!UICONTROL 連線到來源]**，並等待一段時間以建立連線。

![來源工作流程中的新帳戶介面，用於連線至AWS上的Experience Platform](../../../../images/tutorials/create/salesforce-marketing-cloud/new-aws.png)

## 建立[!DNL Salesforce Marketing Cloud]資料的資料流

現在您已成功連線您的[!DNL Salesforce Marketing Cloud]，您現在可以[建立資料流，並將行銷自動化提供者的資料擷取到Experience Platform](../../dataflow/marketing-automation.md)。
