---
keywords: Experience Platform；首頁；熱門主題；PSQL;psqlconnect到查詢服務；查詢服務；查詢服務；
solution: Experience Platform
title: 將PSQL連接到查詢服務
topic-legacy: connect
description: PSQL是命令行介面，在電腦上安裝PostgreSQL時會提供此介面。 您可以依照下列指示進行安裝。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 910a38ccb556ec427584d9b522e29f6877d1c987
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# 將PSQL連接到查詢服務

PSQL是在電腦上安裝[!DNL PostgreSQL]時安裝的命令行介面。 本檔案說明將PSQL與Adobe Experience Platform [!DNL Query Service]連接的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL PSQL]的存取權，且熟悉如何使用。 有關[!DNL PSQL]的更多資訊，請參見[官方的[!DNL PSQL]文檔](https://www.postgresql.org/docs/current/app-psql.html)。

在電腦上安裝PSQL後，您就可以使用Query Service連接PSQL了。 返回[!DNL Platform] UI，然後選擇&#x200B;**[!UICONTROL 查詢]**，後跟&#x200B;**[!UICONTROL 憑據]**。

![影像](../images/clients/psql/connect-bi.png)

選擇表徵圖以複製標籤為&#x200B;**[!UICONTROL PSQL命令]**&#x200B;的部分，然後將命令字串貼到終端或命令行窗口中，然後再按enter鍵。

>[!IMPORTANT]
>
>如果您在PC上，請使用文本編輯器刪除命令字串中的分行符，然後複製該字串。 如果您使用12.0版或更新版本，則需要將`PGGSSENCMODE=disable`新增至連線字串。 此外，如果您使用的是非到期憑據，請確保將密碼欄位替換為非到期憑據密碼。 若要進一步了解未到期的憑證，請參閱[憑證指南](../ui/credentials.md)。

您應該會看到這樣的結果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您未看到至少10.5版，則需要下載該版本或更新版本。

## 後續步驟

現在您已連接[!DNL Query Service]，可以使用PSQL編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀[運行查詢](../best-practices/writing-queries.md)的指南。
