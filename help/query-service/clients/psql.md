---
keywords: Experience Platform；首頁；熱門主題；PSQL；psqlconnect至查詢服務；查詢服務；查詢服務；
solution: Experience Platform
title: 將PSQL連線至查詢服務
description: 瞭解如何將PSQL使用者端連線至Adobe Experience Platform查詢服務，包括支援的PostgreSQL版本和設定指示。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 74f4ac5a3ca4c06e81111ef453ae0effd21b3f16
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 0%

---

# 將PSQL連線至查詢服務

PSQL是與PostgreSQL一併安裝在電腦上的命令列介面。 本文介紹將PSQL連線至Adobe Experience Platform查詢服務的步驟。

>[!IMPORTANT]
>
>查詢服務僅支援以PSQL 14.x版連線。 14.x之前的版本（例如10.x到13.x）和更新版本（15.x及更高版本）不正式支援。 確定您已安裝相容的使用者端版本。 如需參考，請參閱[PostgreSQL生命週期結束日期](https://endoflife.date/postgresql)。

開始之前，請確定您有權存取PSQL，並且熟悉使用使用者端。 有關PSQL的詳細資訊，請參閱[正式PSQL檔案](https://www.postgresql.org/docs/current/app-psql.html)。

>[!IMPORTANT]
>
>下載PostgreSQL時，請務必選取14.x版。依預設，PostgreSQL網站會提供最新版本，可能與Query Service不相容。

安裝PSQL之後，您就可以將它連線到查詢服務。 返回Experience Platform UI，然後選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。

在&#x200B;**[!UICONTROL PSQL命令]**&#x200B;區段下，選取&#x200B;**[!UICONTROL 複製到剪貼簿]**&#x200B;圖示（![復製圖示](/help/images/icons/copy.png)）以複製命令字串。

![反白顯示復本圖示的[查詢儀表板認證]索引標籤。](../images/clients/psql/connect-bi.png)

將命令字串貼到您的終端機中，然後按鍵盤上的&#x200B;**Enter**。

>[!IMPORTANT]
>
>如果您在PC上，請使用文字編輯器移除命令字串中的分行符號，然後複製字串。 如果您使用12.0版或更新版本，則必須將`PGGSSENCMODE=disable`新增至您的連線字串。 此設定會停用GSSAPI加密，因為這對於連線到查詢服務而言是不必要的，而且可能會導致連線錯誤。<br>此外，如果您使用不會到期的認證，請確定您以不會到期的認證密碼取代密碼欄位。 若要進一步瞭解不會到期的認證，請閱讀[認證指南](../ui/credentials.md)。

您應該會看到如下的結果：

```shell
psql (14.4, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您沒有看到14.x版，請從[官方PostgreSQL下載頁面](https://www.postgresql.org/download/)下載並安裝支援的14.x版PSQL。

>[!NOTE]
>
>請依照作業系統的安裝指示執行，然後在終端機執行`psql --version`以驗證已安裝的PSQL版本。

## 後續步驟

現在您已連線至查詢服務，您可以使用PSQL來撰寫查詢。 如需詳細資訊，請參閱[執行查詢](../best-practices/writing-queries.md)的指南。
