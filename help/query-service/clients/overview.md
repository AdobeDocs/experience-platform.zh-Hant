---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；連線；連線至查詢服務；aqua data Studio；Aqua Data Studio；Looker；looker；Postico；postico；Power BI；power bi；psql；rstudio；PSQL；RStudio；Tableau；tableau；
solution: Experience Platform
title: 將使用者端連線至查詢服務
description: 本檔案說明如何從各種案頭使用者端應用程式連線至查詢服務，以及如何驗證這些連線。
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 5e5a196074e844826579102fa6b36102c6481096
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 1%

---

# 將用戶端連線至查詢服務

本節說明如何從各種案頭使用者端應用程式連線到「查詢服務」，以及如何驗證這些連線。 Query Service使用PostgreSQL通訊協定，因此本節中的指示說明如何使用PostgreSQL工具和驅動程式來連線和寫入查詢。

>[!IMPORTANT]
>
>查詢服務互動式Postgres API的生產環境上的TLS/SSL憑證於2024年1月24日星期三更新。<br>雖然這是年度需求，但這次鏈結中的根憑證也已變更，因為Adobe的TLS/SSL憑證提供者已更新其憑證階層。 如果某些Postgres使用者端的憑證授權單位清單缺少根憑證，這可能會影響這些使用者端。 例如，PSQL CLI使用者端可能需要將根憑證新增至明確檔案`~/postgresql/root.crt`，否則可能會導致錯誤，例如`psql: error: SSL error: certificate verify failed`。 如需此問題的詳細資訊，請參閱[正式的PostgreSQL檔案](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES)。<br>可以從[https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem)下載要新增的根憑證。

為下列使用者端提供指示：

- [[!DNL Aqua Data Studio]](./aqua-data-studio.md)
- [[!DNL DbVisualizer]](./dbvisulaizer.md)
- [[!DNL Looker]](./looker.md)
- [[!DNL Postico (Mac)]](./postico.md)
- [[!DNL Power BI (PC)]](./power-bi.md)
- [[!DNL PSQL]](./psql.md)
- [[!DNL RStudio]](./rstudio.md)
- [[!DNL Tableau]](./tableau.md)

>[!IMPORTANT]
>
>身為Power BI和Tableau使用者，您可以使用查詢服務憑證標籤中提供的憑證，將Customer Journey Analytics連線至您的BI工具。 請參閱認證檔案，瞭解如何[將您的BI工具連線至Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics)的說明。
