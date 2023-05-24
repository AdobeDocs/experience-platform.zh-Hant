---
keywords: Experience Platform；首頁；熱門主題；客戶屬性連接器
solution: Experience Platform
title: 客戶屬性來源連接器概覽
description: 瞭解如何使用API或用戶介面將客戶屬性連接到Adobe Experience Platform
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 10%

---

# 客戶屬性連接器

Adobe Experience Platform允許從外部源接收資料，同時讓您能夠使用平台服務構建、標籤和增強傳入資料。 您可以從多種源(如Adobe應用程式、基於雲的儲存、資料庫和許多其他源)接收資料。

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) inExperience Cloud使您能夠從客戶關係管理(CRM)資料庫上載捕獲的企業資料。 您可以將資料上傳至 Experience Cloud 中的客戶屬性資料來源，然後將資料用於 Adobe Analytics 和 Adobe Target。

Experience Platform為攝取提供支援 [!DNL Customer Attributes] 記錄資料到Adobe Experience Platform。

## 資料集和架構

的 [!DNL Customer Attributes] 源自動建立資料集，以便資料登錄。 此自動建立的資料集是固定的，無法手動選擇。 源還基於輸入資料源自動建立資料集的模式。 此過程還涉及在架構和源資料之間自動建立必要的映射。

## 身分

資料集的主標識包含在源資料的CSV檔案的第一列中。 的 [!DNL Customer Attributes] 源假定標識始終映射到 [`CORE` 命名空間](../../../identity-service/namespaces.md)，系統生成的命名空間，支援 [[!DNL Identity Service]](../../../identity-service/home.md)。

使用時，無法為標識選擇現有命名空間 [!DNL Customer Attributes] 源 [!DNL Customer Attributes] 假定架構的主標識始終位於標識映射中。 [!DNL Customer Attributes] 然後以自動方式建立源ID到標識映射UUID的映射。

對於 [!DNL Customer Attributes] 與其他 [!DNL Profile] 資料集，其資料和標識必須能夠與Experience CloudID匹配。

您可以 `CORE` 命名空間，方法是使用 [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en)。 [移動SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)，或 [Experience CloudID服務API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=zh-Hant)。

的 [!DNL Customer Attributes] 檔案不會進一步填充任何其他身份關係。 例如，如果 [!DNL Customer Attributes] 源資料集包含 **電子郵件** 和 **會員ID** 欄位，則必須將這些欄位標籤為架構中的標識欄位，以便處理到 [!DNL Identity Service]。

請參閱上的教程 [建立 [!DNL Customer Attributes] UI中的源連接](../../tutorials/ui/create/adobe-applications/customer-attributes.md) 的子菜單。
