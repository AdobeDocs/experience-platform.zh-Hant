---
title: 使用Python和SQLAlchemy管理平台資料
description: 瞭解如何使用SQLAlchemy來管理Platform資料，而不使用SQL。
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# 使用[!DNL Python]和[!DNL SQLAlchemy]管理平台資料

瞭解如何使用SQLAlchemy，以更靈活地管理Adobe Experience Platform資料。 對於不熟悉SQL的使用者，SQLAlchemy可以在使用關聯式資料庫時大幅縮短開發時間。 本檔案提供將[!DNL SQLAlchemy]連線至Query Service並開始使用Python與您的資料庫互動的指示和範例。

[!DNL SQLAlchemy]是物件關聯對應程式(ORM)和[!DNL Python]程式碼程式庫，可將儲存在SQL資料庫中的資料傳輸至[!DNL Python]物件。 接著，您可以使用[!DNL Python]程式碼，對Platform Data Lake中保留的資料執行CRUD作業。 如此一來，您就不需要只使用PSQL來管理資料。

## 快速入門

若要取得連線[!DNL SQLAlchemy]至Experience Platform的必要認證，您必須擁有平台UI中查詢工作區的存取權。 如果您目前無法存取查詢工作區，請聯絡您的組織管理員。

## [!DNL Query Service]認證 {#credentials}

若要尋找您的認證，請登入Platform UI並從左側導覽選取&#x200B;**[!UICONTROL 查詢]**，接著選取&#x200B;**[!UICONTROL 認證]**。 如需如何尋找登入認證的完整指示，請參閱[認證指南](../ui/credentials.md)。

![已醒目提示[認證]索引標籤的[查詢服務]認證即將到期。](../images/use-cases/credentials.png)

雖然連線埠80是連線至查詢服務的建議連線埠，但您也可以使用連線埠5432。

>[!IMPORTANT]
>
>如果您使用即將到期的認證（如上圖所示）來連線至查詢服務，則連線的工作階段期限會在貴組織的設定中定義的設定時段後到期。 依預設，此期間為24小時。 請參閱檔案以瞭解如何[使用不會到期的認證](../ui/credentials.md#non-expiring-credentials)連線使用者端，或如何[變更您即將到期的認證的工作階段存留期](../ui/credentials.md#expiring-credentials)。

存取您的QS認證後，請開啟您選擇的[!DNL Python]編輯器。

### 在[!DNL Python]中儲存認證 {#store-credentials}

在您的[!DNL Python]編輯器中，匯入`urllib.parse.quote`資料庫並將每個認證變數儲存為引數。 `urllib.parse`模組提供標準介面，可將URL字串分成元件。 引號函式會取代URL字串中的特殊字元，讓資料可安全用作URL元件。 以下是必要程式碼的範例：

>[!TIP]
>
>使用[!DNL Python]的三引號輸入您的多行密碼字串。

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>如果您使用即將到期的認證，您提供用來連線[!DNL SQLAlchemy]至Experience Platform的密碼將會到期。 如需詳細資訊，請參閱[認證區段](#credentials)。

### 建立引擎執行個體[#create-engine]

建立變數之後，匯入`create_engine`函式並建立字串，以編譯並格式化您在SQLAlchemy中的查詢服務認證。 接著會使用`create_engine`函式來建構引擎執行個體。

>[!NOTE]
>
>`create_engine`傳回引擎的執行個體。 但是，在呼叫需要連線的查詢之前，它不會開啟到查詢服務的連線。

使用協力廠商使用者端存取Platform時，必須啟用SSL。 做為引擎的一部分，請使用`connect_args`輸入其他關鍵字引數。 建議您將SSL模式設定為`require`。 如需接受值的詳細資訊，請參閱[SSL模式檔案](../clients/ssl-modes.md)。

下列範例顯示初始化引擎和連線字串所需的[!DNL Python]程式碼。

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>如果您使用即將到期的認證，您提供用來連線[!DNL SQLAlchemy]至Experience Platform的密碼將會到期。 如需詳細資訊，請參閱[認證區段](#credentials)。

您現在可以使用[!DNL Python]來查詢Platform資料。 下列範例會傳回查詢服務資料表名稱的陣列。

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
