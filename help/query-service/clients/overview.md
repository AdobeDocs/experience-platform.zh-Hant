---
keywords: Experience Platform；首頁；熱門主題；查詢服務；查詢服務；連線；連線至查詢服務；aqua data Studio；Aqua Data Studio；Looker；looker；Postico；postico；Power BI；power bi；psql；rstudio；PSQL；RStudio；Tableau；tableau；
solution: Experience Platform
title: 將使用者端連線至查詢服務
description: 本檔案說明如何從各種案頭使用者端應用程式連線至查詢服務，以及如何驗證這些連線。
exl-id: 2ba20179-5adb-4259-a120-231a40e78054
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# 將使用者端連線至 [!DNL Query Service]

本節說明如何連線至 [!DNL Query Service] 各種案頭使用者端應用程式，以及如何驗證這些連線。 [!DNL Query Service] 使用 [!DNL PostgreSQL] 通訊協定，因此本節中的指示會說明如何使用 [!DNL PostgreSQL] 用來連線和寫入查詢的工具和驅動程式。

>[!IMPORTANT]
>
>查詢服務互動式Postgres API的生產環境上的TLS/SSL憑證於2024年1月24日星期三更新。<br>雖然這是年度需求，但這次鏈結中的根憑證也有所變更，因為Adobe的TLS/SSL憑證提供者已更新其憑證階層。 如果某些Postgres使用者端的憑證授權單位清單遺失根憑證，這可能會影響這些使用者端。 例如，PSQL CLI使用者端可能需要將根憑證新增至明確檔案 `~/postgresql/root.crt`，否則可能會導致錯誤。 例如 `psql: error: SSL error: certificate verify failed`。請參閱 [PostgreSQL官方檔案](https://www.postgresql.org/docs/current/libpq-ssl.html#LIBQ-SSL-CERTIFICATES) 以取得此問題的詳細資訊。<br>新增的根憑證可從下載 [https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem](https://cacerts.digicert.com/DigiCertGlobalRootG2.crt.pem).

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
>身為Power BI和Tableau使用者，您可以從「查詢服務」憑證標籤將Customer Journey Analytics連線至您的BI工具。 如需認證檔案的操作說明，請參閱認證檔案 [將您的BI工具連線至Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics).
