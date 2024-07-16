---
keywords: Experience Platform；首頁；熱門主題；PSQL；psqlconnect至查詢服務；查詢服務；查詢服務；
solution: Experience Platform
title: 將PSQL連線至查詢服務
description: PSQL是命令列介面，當您在電腦上安裝PostgreSQL時便會提供。 您可以依照這些指示進行安裝。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---

# 將PSQL連線至查詢服務

PSQL是當您在電腦上安裝[!DNL PostgreSQL]時所安裝的命令列介面。 本檔案說明將PSQL連線至Adobe Experience Platform [!DNL Query Service]的步驟。

>[!NOTE]
>
> 本指南假設您已擁有[!DNL PSQL]的存取權並熟悉其使用方法。 有關[!DNL PSQL]的更多資訊可在[正式 [!DNL PSQL] 檔案](https://www.postgresql.org/docs/current/app-psql.html)中找到。

在電腦上安裝PSQL之後，您就可以使用Query Service連線PSQL。 返回[!DNL Platform] UI，然後選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。

在&#x200B;**[!UICONTROL PSQL命令]**&#x200B;區段下，選取&#x200B;**[!UICONTROL 複製到剪貼簿]**&#x200B;圖示（![復製圖示](../images/clients/psql/copy-icon.png)）以複製命令字串。

![反白顯示復本圖示的[查詢儀表板認證]索引標籤。](../images/clients/psql/connect-bi.png)

將命令字串貼到終端機或命令列視窗中，然後按鍵盤上的&#x200B;**Enter**。

>[!IMPORTANT]
>
>如果您在PC上，請使用文字編輯器移除命令字串中的分行符號，然後複製字串。 如果您使用12.0版或更新版本，則必須將`PGGSSENCMODE=disable`新增至您的連線字串。 此外，如果您使用不會到期的認證，請確定您以不會到期的認證密碼取代密碼欄位。 若要進一步瞭解不會到期的認證，請閱讀[認證指南](../ui/credentials.md)。

您應該會看到如下的結果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您沒有看到至少10.5版，則需要下載該版本或更新版本。

## 後續步驟

現在您已連線到[!DNL Query Service]，您可以使用PSQL來撰寫查詢。 如需如何撰寫和執行查詢的詳細資訊，請閱讀[執行查詢](../best-practices/writing-queries.md)的指南。
