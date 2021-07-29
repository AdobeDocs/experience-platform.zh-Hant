---
keywords: Experience Platform；首頁；熱門主題；客戶屬性連接器
solution: Experience Platform
title: 客戶屬性來源連接器概述
topic-legacy: overview
description: 了解如何使用API或使用者介面將客戶屬性連線至Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 8%

---

# 客戶屬性連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) 在「Experience Cloud」中，您可以上傳從客戶關係管理(CRM)資料庫擷取的企業資料。您可以將資料上傳至 Experience Cloud 中的客戶屬性資料來源，然後將資料用於 Adobe Analytics 和 Adobe Target。

Experience Platform支援將[!DNL Customer Attributes]設定檔資料擷取至Adobe Experience Platform。

## 資料集和結構

[!DNL Customer Attributes]來源會自動建立資料集，以便登陸。 此自動建立的資料集已修正，無法手動選取。 來源也會根據輸入資料來源自動建立資料集的結構。 此程式還涉及自動建立架構與來源資料之間的必要對應。

## 身分

資料集的主要身分會包含在來源資料之CSV檔案的第一欄中。 [!DNL Customer Attributes]源假定標識始終映射到[`CORE`命名空間](../../../identity-service/namespaces.md)，該命名空間是系統生成的命名空間，由[[!DNL Identity Service]](../../../identity-service/home.md)支援。

使用[!DNL Customer Attributes]源時，無法為標識選擇現有的命名空間，因為[!DNL Customer Attributes]假定架構的主標識始終位於標識映射中。 [!DNL Customer Attributes] 然後以自動方式建立來源ID與身分對應UUID的對應。

若要將[!DNL Customer Attributes]資料連結至其他[!DNL Profile]資料集，其資料和身分必須能與Experience CloudID相符。

您可以使用[Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en)、[Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)或[Experience CloudID服務API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)來設定訪客的Experience CloudID，借此建立`CORE`命名空間。

[!DNL Customer Attributes]檔案不會進一步填入任何其他身分關係。 例如，如果[!DNL Customer Attributes]來源資料集包含&#x200B;**電子郵件**&#x200B;和&#x200B;**忠誠度ID**&#x200B;欄位，則這些欄位必須在架構中標示為身分欄位，才能處理至[!DNL Identity Service]。

如需詳細資訊，請參閱UI](../../tutorials/ui/create/adobe-applications/customer-attributes.md)中[建立 [!DNL Customer Attributes] 來源連線的教學課程。
