---
keywords: Experience Platform；首頁；熱門主題；PSQL;psqlconnect到查詢服務；查詢服務；查詢服務；
solution: Experience Platform
title: 將PSQL連接到查詢服務
description: PSQL是在電腦上安裝PostgreSQL時提供的命令行介面。 您可以按照以下說明安裝它。
exl-id: ceb07128-409e-42be-8143-0cf681d435de
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# 將PSQL連接到查詢服務

PSQL是安裝時安裝的命令行介面 [!DNL PostgreSQL] 在你的機器上。 本文檔介紹將PSQL與Adobe Experience Platform連接的步驟 [!DNL Query Service]。

>[!NOTE]
>
> 本指南假定您已具有訪問 [!DNL PSQL] 並熟悉如何使用。 有關 [!DNL PSQL] 在 [官 [!DNL PSQL] 文檔](https://www.postgresql.org/docs/current/app-psql.html)。

在電腦上安裝PSQL後，您就可以將PSQL與查詢服務連接。 返回到 [!DNL Platform] UI，然後選擇 **[!UICONTROL 查詢]**，後跟 **[!UICONTROL 憑據]**。

在 **[!UICONTROL PSQL命令]** 的 **[!UICONTROL 複製到剪貼簿]** 表徵圖。![複製表徵圖](../images/clients/psql/copy-icon.png))以複製命令字串。

![「查詢」面板的「身份證明」頁籤，其中突出顯示了複製表徵圖。](../images/clients/psql/connect-bi.png)

將命令字串貼上到終端或命令行窗口中，然後按 **輸入** 鍵盤上。

>[!IMPORTANT]
>
>如果您在PC上，請使用文本編輯器刪除命令字串中的換行符，然後複製字串。 如果您使用12.0或更高版本，則需要添加 `PGGSSENCMODE=disable` 連接字串。 此外，如果您使用的是非過期憑據，請確保將密碼欄位替換為非過期憑據密碼。 要瞭解有關未過期憑據的詳細資訊，請閱讀 [憑據指南](../ui/credentials.md)。

您應看到這樣的結果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您至少看不到10.5版，則需要下載該版本或更新版本。

## 後續步驟

既然你已經和 [!DNL Query Service]，可以使用PSQL來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀上的指南 [運行查詢](../best-practices/writing-queries.md)。
