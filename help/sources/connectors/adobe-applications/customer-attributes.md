---
keywords: Experience Platform；首頁；熱門主題；客戶屬性聯結器
solution: Experience Platform
title: 客戶屬性Source聯結器總覽
description: 瞭解如何使用API或使用者介面將客戶屬性連結至Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 7%

---

# 客戶屬性聯結器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(例如Adobe應用程式、雲端儲存、資料庫和許多其他來源)內嵌資料。

Experience Cloud中的[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html)可讓您上傳從客戶關係管理(CRM)資料庫擷取的企業資料。 您可以將資料上傳至 Experience Cloud 中的客戶屬性資料來源，然後將資料用於 Adobe Analytics 和 Adobe Target。

Experience Platform支援將[!DNL Customer Attributes]設定檔資料擷取至Adobe Experience Platform。

## 資料集和結構描述

[!DNL Customer Attributes]來源會自動建立資料集以供資料著陸。 此自動建立的資料集是固定的，無法手動選取。 來源也會根據輸入資料來源自動建立資料集的結構描述。 此程式也涉及在結構描述和來源資料之間自動建立必要的對應。

## 身分

資料集的主要身分包含在來源資料的CSV檔案的第一欄。 [!DNL Customer Attributes]來源假設身分一律對應到[`CORE`名稱空間](../../../identity-service/features/namespaces.md)，這是系統產生的名稱空間，受[[!DNL Identity Service]](../../../identity-service/home.md)支援。

使用[!DNL Customer Attributes]來源時，您無法選取身分的現有名稱空間，因為[!DNL Customer Attributes]假設結構描述的主要身分一律在身分對應中。 [!DNL Customer Attributes]接著以自動方式建立來源ID與身分對應UUID的對應。

若要將[!DNL Customer Attributes]資料與其他[!DNL Profile]資料集繫結，其資料和身分必須能夠與Experience Cloud識別碼相符。

您可以使用[Web SDK](/help/web-sdk/identity/overview.md)、[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)或[Experience CloudID服務API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)來設定訪客的Experience CloudID，以建立`CORE`名稱空間。

[!DNL Customer Attributes]檔案未進一步填入任何其他身分關係。 例如，如果[!DNL Customer Attributes]來源資料集包含&#x200B;**電子郵件**&#x200B;和&#x200B;**忠誠度識別碼**&#x200B;欄位，則這些欄位必須在結構描述中標示為身分欄位，才能處理為[!DNL Identity Service]。

如需詳細資訊，請參閱有關[在UI](../../tutorials/ui/create/adobe-applications/customer-attributes.md)中建立 [!DNL Customer Attributes] 來源連線的教學課程。
