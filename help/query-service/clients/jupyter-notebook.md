---
title: 將Jupyter Notebook連線至查詢服務
description: 瞭解如何連結Jupyter Notebook與Adobe Experience Platform查詢服務。
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 0%

---

# 將[!DNL Jupyter Notebook]連線至查詢服務

本檔案說明連線[!DNL Jupyter Notebook]與Adobe Experience Platform查詢服務所需的步驟。

## 快速入門

本指南要求您已擁有[!DNL Jupyter Notebook]的存取權並熟悉其介面。 若要下載[!DNL Jupyter Notebook]或如需詳細資訊，請參閱[正式 [!DNL Jupyter Notebook] 檔案](https://jupyter.org/)。

若要取得連線[!DNL Jupyter Notebook]至Experience Platform所需的認證，您必須能存取Platform UI中的[!UICONTROL 查詢]工作區。 如果您目前無法存取[!UICONTROL 查詢]工作區，請連絡組織管理員。

>[!TIP]
>
>[!DNL Anaconda Navigator]是案頭圖形化使用者介面(GUI)，可讓您更輕鬆地安裝和啟動一般[!DNL Python]程式，例如[!DNL Jupyter Notebook]。 它還有助於在不使用命令列命令的情況下管理套件、環境和通道。
>請依照其網站上的引導式安裝程式，以[安裝您偏好的應用程式版本](https://docs.anaconda.com/anaconda/install/)。
>在「Anaconda導覽器」首頁畫面中，從支援的應用程式清單中選取&#x200B;**[!DNL Jupyter Notebook]**以啟動程式。
>如需詳細資訊，請參閱[Anaconda官方檔案](https://docs.anaconda.com/anaconda/navigator/)。

官方Jupyter檔案提供從命令列介面](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI) [執行筆記本的指示。

## Launch [!DNL Jupyter Notebook]

開啟新的[!DNL Jupyter Notebook] Web應用程式後，從UI選取&#x200B;**[!DNL New]**&#x200B;下拉式清單，接著選取&#x200B;**[!DNL Python 3]**&#x200B;以建立新的Notebook。 [!DNL Notebook]編輯器出現。

在[!DNL Notebook]編輯器的第一行，輸入下列值： `pip install psycopg2-binary`並從命令列選取&#x200B;**[!DNL Run]**。 成功訊息會顯示在輸入行的下方。

>[!IMPORTANT]
>
>在此建立連線的程式中，您必須選取&#x200B;**[!DNL Run]**&#x200B;以執行每一行程式碼。

接下來，為[!DNL Python]匯入[!DNL PostgreSQL]資料庫配接器。 輸入值： `import psycopg2`並選取&#x200B;**[!DNL Run]**。 此程式沒有成功訊息。 如果沒有錯誤訊息，請繼續進行下一個步驟。

您現在必須輸入值來提供您的Adobe Experience Platform認證： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`。 您可以在Platform UI的[!UICONTROL 認證]標籤下的[!UICONTROL 查詢]區段中找到您的連線認證。 如需詳細指示，請參閱有關如何[尋找組織認證](../ui/credentials.md)的檔案。

使用協力廠商使用者端時，建議使用不會到期的認證，以省下重複輸入詳細資料的時間。 請參閱檔案以瞭解[如何產生及使用不會到期的認證](../ui/credentials.md#non-expiring-credentials)的說明。

>[!IMPORTANT]
>
>從Platform UI複製認證時，不需要其他認證格式。 它們可以在一行中指定，屬性和值之間有單一空格。 認證以引號括住，且&#x200B;**不是**&#x200B;逗號分隔。

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

您的[!DNL Jupyter Notebook]執行個體現在已連線至查詢服務。

## 範例查詢執行

現在您已將[!DNL Jupyter Notebook]連線至查詢服務，您可以使用[!DNL Notebook]輸入對資料集執行查詢。 下列範例使用簡單查詢來示範此程式。

輸入下列值：

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

接著，呼叫引數（上述範例中的`data`），以未格式化的回應顯示查詢結果。

若要以更易讀的方式格式化結果，請使用下列命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

這些命令不會產生成功訊息。 如果沒有錯誤訊息，您可以使用函式以表格格式輸出SQL查詢的結果。

輸入並執行`df.head()`函式，以檢視表格化的查詢結果。

## 後續步驟

現在您已連線到查詢服務，您可以使用[!DNL Jupyter Notebook]來撰寫查詢。 如需如何撰寫和執行查詢的詳細資訊，請參閱[執行查詢指南](../best-practices/writing-queries.md)。
