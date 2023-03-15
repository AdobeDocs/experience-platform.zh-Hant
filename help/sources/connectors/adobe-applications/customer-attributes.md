---
keywords: Experience Platform；首頁；熱門主題；客戶屬性連接器
solution: Experience Platform
title: 客戶屬性來源連接器概述
description: 了解如何使用API或使用者介面將客戶屬性連線至Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 10%

---

# 客戶屬性連接器

Adobe Experience Platform可讓您從外部來源擷取資料，同時使用Platform服務來建構、加標籤及增強傳入資料。 您可以從多種來源(如Adobe應用程式、雲儲存、資料庫等)內嵌資料。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) 在「Experience Cloud」中，您可以上傳從客戶關係管理(CRM)資料庫擷取的企業資料。 您可以將資料上傳至 Experience Cloud 中的客戶屬性資料來源，然後將資料用於 Adobe Analytics 和 Adobe Target。

Experience Platform支援擷取 [!DNL Customer Attributes] 設定檔資料匯入Adobe Experience Platform。

## 資料集和結構

此 [!DNL Customer Attributes] 來源會自動建立資料集，以便登陸。 此自動建立的資料集已修正，無法手動選取。 來源也會根據輸入資料來源自動建立資料集的結構。 此程式還涉及自動建立架構與來源資料之間的必要對應。

## 身分

資料集的主要身分會包含在來源資料之CSV檔案的第一欄中。 此 [!DNL Customer Attributes] 來源會假設身分一律對應至 [`CORE` 命名空間](../../../identity-service/namespaces.md)，此系統產生的命名空間支援 [[!DNL Identity Service]](../../../identity-service/home.md).

使用 [!DNL Customer Attributes] 源 [!DNL Customer Attributes] 假設架構的主要身分一律位於身分對應中。 [!DNL Customer Attributes] 然後以自動方式建立來源ID與身分對應UUID的對應。

針對 [!DNL Customer Attributes] 連結至其他 [!DNL Profile] 資料集、其資料和身分必須能與Experience CloudID相符。

您可以建立 `CORE` 命名空間，方法是使用 [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [行動SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)，或 [Experience CloudID服務API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant).

此 [!DNL Customer Attributes] 檔案不會進一步填入任何其他身分關係。 例如，若 [!DNL Customer Attributes] 來源資料集包含 **電子郵件** 和 **忠誠度ID** 欄位，則這些欄位必須標示為架構中的身分欄位，才能加以處理 [!DNL Identity Service].

請參閱 [建立 [!DNL Customer Attributes] UI中的源連接](../../tutorials/ui/create/adobe-applications/customer-attributes.md) 以取得更多資訊。
