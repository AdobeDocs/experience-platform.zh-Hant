---
keywords: Experience Platform；首頁；熱門主題；Analytics來源連接器；Analytics
solution: Experience Platform
title: Adobe Analytics報表套裝資料的來源連接器
topic-legacy: overview
description: 本檔案概述Analytics並說明Analytics資料的使用案例。
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 9defe1c3087c2f1284ceedede9d274a51cf97b96
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 1%

---

# Adobe Analytics報表套裝資料的來源連接器

Adobe Experience Platform可讓您透過Analytics來源連接器內嵌Adobe Analytics資料。 [!DNL Analytics]源連接器即時將[!DNL Analytics]收集的資料流到Platform，將SCDS格式的[!DNL Analytics]資料轉換為[!DNL Experience Data Model](XDM)欄位，供Platform使用。

本檔案概述[!DNL Analytics]並說明[!DNL Analytics]資料的使用案例。

## Adobe Analytics與Analytics資料

[!DNL Analytics] 是一款功能強大的引擎，可協助您進一步了解客戶、客戶如何與您的Web屬性互動、了解您的數位行銷支出有何成效，以及找出需要改善的領域。[!DNL Analytics] 每年處理數萬億個Web交易，而 [!DNL Analytics] 來源連接器可讓您輕鬆利用這些豐富的行為資料，並在幾分 [!DNL Real-time Customer Profile] 鐘內豐富交易內容。

![](./images/analytics-data-experience-platform.png)

[!DNL Analytics]從世界各地的各種數字通道和多個資料中心收集資料。 收集資料後，會套用訪客身分識別、分段和轉換架構(VISTA)規則及處理規則，以塑造傳入資料。 在原始資料經過此輕量化處理後，[!DNL Real-time Customer Profile]會將其視為可供使用。 在與上述程式平行的程式中，相同的處理資料會微批處理並擷取至Platform資料集，供[!DNL Data Science Workspace]、[!DNL Query Service]和其他資料探索應用程式使用。

如需處理規則的詳細資訊，請參閱[處理規則概述](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) 。

## Experience Data Model(XDM)

XDM是公開記錄的規範，為應用程式提供通用結構和定義，以便與Experience Platform上的服務進行通信。

遵循XDM標準，即可統一整合資料，更輕鬆傳送資料和收集資訊。

若要深入了解XDM，請參閱[XDM系統概述](../../../xdm/home.md)。

## 如何將欄位從Adobe Analytics對應至XDM?

當建立源連接以使用Platform用戶介面將[!DNL Analytics]資料Experience Platform時，資料欄位將在數分鐘內自動映射並內嵌到[!DNL Real-time Customer Profile]中。 有關使用Platform UI建立[!DNL Analytics]源連接的說明，請參閱[Analytics源連接器教程](../../tutorials/ui/create/adobe-applications/analytics.md)。

有關[!DNL Analytics]和Experience Platform之間的欄位映射的詳細資訊，請參閱[Adobe Analytics欄位映射](./mapping/analytics.md)指南。

## 平台上Analytics資料的預期延遲為何？

下表列出Platform上Analytics資料的預期延遲。 延遲會因客戶配置、資料量和消費者應用程式而異。 例如，如果Analytics實作設定了`A4T` ,Pipeline的延遲會增加至5-10分鐘。

| Analytics 資料 | 預期延遲 |
| -------------- | ---------------- |
| 新資料至[!DNL Real-time Customer Profile]（A4T **未啟用**） | &lt; 2 分鐘 |
| 新資料至[!DNL Real-time Customer Profile]（A4T **is**&#x200B;已啟用） | &lt; 15 分鐘 |
| 資料湖的新資料 | &lt; 90 分鐘 |
| 回填資料（13個月的資料或100億個事件，以較低者為準） | &lt; 4 週 |

>[!NOTE]
>
>Analytics回填資料不會內嵌至[!DNL Profile]，因此不會計入授權設定檔中。

## [!DNL Analytics]資料中的主要標識符

[!DNL Analytics]來源連接器的每次點擊都包含主要識別碼，視ECID或AAID是否存在而定。 如果有ECID，系統會將ECID指定為主要識別碼。 如果有AAID，則將AAID指定為主要。
