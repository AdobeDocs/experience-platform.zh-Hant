---
keywords: Experience Platform;home;popular topics;PSQL;psqlconnect to query service;Query service;query service;
solution: Experience Platform
title: 使用PSQL連接
topic: connect
description: 'PSQL是命令行介面，在電腦上安裝Postgres時會出現。 您可依照下列指示進行安裝。 '
translation-type: tm+mt
source-git-commit: 8ffe7c68c87cacb6b54d9634a5204fa24a9986ac
workflow-type: tm+mt
source-wordcount: '209'
ht-degree: 0%

---


# 使用PSQL連接

PSQL是命令行介面，安裝在電腦上 [!DNL Postgres] 時會出現。 您可依照下列指示進行安裝。

## 在Mac上安裝Postgres

開啟終端窗口並發出以下三個命令：

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

發出這些命令後，您應看到以下內容：

```shell
/usr/local/bin/psql
```

## 安裝 [!DNL Postgres] 在PC上

從此位置下 [!DNL Postgres] 載和安 [裝](https://www.postgresql.org/download/windows/)。

編輯路徑變數：

![影像](../images/clients/psql/path.png)

新增顯示的兩行，其中包[!DNL Postgres]括&quot;。

儲存更新，然後開啟命令提示符並輸入：

```shell
psql -V
```

您應該看到這樣的情況：

```shell
psql (PostgreSQL) 9.5.14
```

## 連接PSQL和 [!DNL Query Service]

返回「連 [!DNL Platform] 接BI工 **[!UICONTROL 具」頁上的]** UI。

按一下 **[!UICONTROL 「復]** 制PSQL命令」 ****。

![影像](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]
>
>如果您在PC上，請使用文本編輯器刪除命令字串中的分行符，然後複製該字串。 此外，如果您使用12.0版或更新版本，則需要新增至 `PGGSSENCMODE=disable` 連線字串。

將命令字串貼上到終端或命令窗口中，然後按Enter鍵。

您應該會看到這樣的結果：

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

如果您至少看不到10.5版，則需要下載該版本或更新版本。