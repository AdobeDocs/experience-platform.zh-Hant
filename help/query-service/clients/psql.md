---
keywords: Experience Platform；首頁；熱門主題；PSQL;psqlconnect到查詢服務；查詢服務；查詢服務；
solution: Experience Platform
title: 將PSQL連接到查詢服務
topic-legacy: connect
description: PSQL是命令行介面，在電腦上安裝PostgreSQL時會提供此介面。 您可以依照下列指示進行安裝。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 06d3a8aa6f2f73c2d5392a76fb5b36b18691cf0d
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 1%

---

# 將PSQL連接到查詢服務

PSQL是安裝時安裝的命令行介面 [!DNL PostgreSQL] 在你的機器上。 本檔案說明將PSQL與Adobe Experience Platform連接的步驟 [!DNL Query Service].

>[!NOTE]
>
> 本指南假設您已擁有 [!DNL PSQL] 並熟悉如何使用。 有關 [!DNL PSQL] 可在 [官方 [!DNL PSQL] 檔案](https://www.postgresql.org/docs/current/app-psql.html).

在電腦上安裝PSQL後，您就可以使用Query Service連接PSQL了。 返回 [!DNL Platform] UI，然後選取 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑證]**.

![影像](../images/clients/psql/connect-bi.png)

選取要複製標示為的區段的圖示 **[!UICONTROL PSQL命令]**，然後在按下enter之前，將命令字串貼入終端機或命令列視窗中。

>[!IMPORTANT]
>
>如果您在PC上，請使用文本編輯器刪除命令字串中的分行符，然後複製該字串。 如果您使用12.0版或更新版本，則需要新增 `PGGSSENCMODE=disable` 連線字串。 此外，如果您使用的是非到期憑據，請確保將密碼欄位替換為非到期憑據密碼。 若要進一步了解未到期的憑證，請參閱 [認證指南](../ui/credentials.md).

您應該會看到這樣的結果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您未看到至少10.5版，則需要下載該版本或更新版本。

## 後續步驟

既然你已經和 [!DNL Query Service]，您可以使用PSQL來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢](../best-practices/writing-queries.md).
