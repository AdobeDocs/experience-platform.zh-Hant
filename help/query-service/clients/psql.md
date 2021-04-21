---
keywords: Experience Platform;home；熱門主題；PSQL;psqlconnect到查詢服務；查詢服務；查詢服務；
solution: Experience Platform
title: 將PSQL連接到查詢服務
topic-legacy: connect
description: PSQL是命令行介面，在電腦上安裝PostgreSQL時將提供此介面。 您可依照下列指示進行安裝。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 1%

---

# 將PSQL連接到查詢服務

PSQL是命令行介面，在電腦上安裝[!DNL PostgreSQL]時會安裝該介面。 本文檔介紹將PSQL與Adobe Experience Platform[!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL PSQL]的存取權，並熟悉如何使用它。 有關[!DNL PSQL]的更多資訊，請參閱[official [!DNL PSQL] documentation](https://www.postgresql.org/docs/current/app-psql.html)。

在電腦上安裝PSQL後，您可以將PSQL與查詢服務連接。 返回[!DNL Platform] UI，然後選擇&#x200B;**[!UICONTROL Queries]**，然後選擇&#x200B;**[!UICONTROL Credentials]**。

![影像](../images/clients/psql/connect-bi.png)

選擇該表徵圖以複製標有&#x200B;**[!UICONTROL PSQL Command]**&#x200B;的部分，然後將命令字串貼上到終端或命令行窗口中，然後再按Enter鍵。

>[!IMPORTANT]
>
>如果您在PC上，請使用文本編輯器刪除命令字串中的分行符，然後複製該字串。 此外，如果您使用12.0版或更新版本，則需要將`PGGSSENCMODE=disable`新增至連線字串。

您應該會看到這樣的結果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您至少看不到10.5版，則需要下載該版本或更新版本。

## 後續步驟

現在您已連接[!DNL Query Service]，您可以使用PSQL來編寫查詢。 有關如何寫入和運行查詢的詳細資訊，請閱讀[運行查詢](../best-practices/writing-queries.md)的指南。
