---
title: 將Jupyter筆記本連接到查詢服務
description: 了解如何使用Adobe Experience Platform Query Service連線Jupyter筆記型電腦。
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Connect [!DNL Jupyter Notebook] 查詢服務

本檔案涵蓋連線所需的步驟 [!DNL Jupyter Notebook] Adobe Experience Platform查詢服務。

## 快速入門

本指南要求您已具備 [!DNL Jupyter Notebook] 並熟悉其介面。 若要下載 [!DNL Jupyter Notebook] 或，請參閱 [官方 [!DNL Jupyter Notebook] 檔案](https://jupyter.org/).

獲取連接所需的憑據 [!DNL Jupyter Notebook] 若要Experience Platform，您必須擁有 [!UICONTROL 查詢] 工作區。 如果您目前沒有 [!UICONTROL 查詢] 工作區。

>[!TIP]
>
>[!DNL Anaconda Navigator] 是案頭圖形用戶介面(GUI)，它提供了安裝和啟動常見功能的更簡單方式 [!DNL Python] 方案，如 [!DNL Jupyter Notebook]. 它還有助於管理包、環境和通道，而無需使用命令行命令。
>請依照網站上的引導式安裝程式，前往 [安裝您偏好的應用程式版本](https://docs.anaconda.com/anaconda/install/).
>從「阿納康達導航器」主螢幕中，選擇 **[!DNL Jupyter Notebook]** 從支援的應用程式清單中啟動程式。
>如需詳細資訊，請參閱 [阿納康達官方檔案](https://docs.anaconda.com/anaconda/navigator/).

官方的Jupyter檔案提供 [從命令行介面運行筆記本](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI)。

## Launch [!DNL Jupyter Notebook]

在您開啟新 [!DNL Jupyter Notebook] web應用程式，請選擇 **[!DNL New]** 從UI的下拉式清單，隨後 **[!DNL Python 3]** 建立新筆記本。 此 [!DNL Notebook] 編輯器隨即出現。

在 [!DNL Notebook] 編輯器，輸入下列值： `pip install psycopg2-binary` 選取 **[!DNL Run]** 中。 輸入行下方會顯示成功訊息。

>[!IMPORTANT]
>
>在此過程中，您必須選擇 **[!DNL Run]** 執行每行程式碼。

接下來，匯入 [!DNL PostgreSQL] 資料庫適配器 [!DNL Python]. 輸入值： `import psycopg2`選取 **[!DNL Run]**. 此程式沒有成功訊息。 如果沒有錯誤訊息，請繼續下一個步驟。

您現在必須輸入值，以提供Adobe Experience Platform憑證： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`. 在 [!UICONTROL 查詢] 部分，在 [!UICONTROL 憑證] 頁簽。 請參閱如何 [查找組織憑據](../ui/credentials.md) 以取得詳細指示。

使用協力廠商用戶端時，建議使用未到期的認證，以免重複輸入您的詳細資訊。 如需相關指示，請參閱本檔案。 [如何生成和使用非到期憑據](../ui/credentials.md#non-expiring-credentials).

>[!IMPORTANT]
>
>從Platform UI複製憑證時，不需要設定其他格式的憑證。 它們可以以一行指定，在屬性和值之間只有一個空格。 憑證以引號括住，並 **not** 逗號分隔。

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

您的 [!DNL Jupyter Notebook] 執行個體現在已連線至查詢服務。

## 查詢執行範例

既然你已經聯繫了 [!DNL Jupyter Notebook] 若要查詢服務，您可以使用 [!DNL Notebook] 輸入。 下列範例使用簡單查詢來示範程式。

輸入下列值：

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

接下來，呼叫參數(`data` 在上例中)，以在未格式化的回應中顯示查詢結果。

若要以更人類看得懂的方式格式化結果，請使用下列命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

這些命令不會生成成功消息。 如果沒有錯誤消息，則可以使用函式以表格式輸出SQL查詢的結果。

輸入並執行 `df.head()` 函式來查看已加表的查詢結果。

## 後續步驟

現在您已連線Query Service，可以使用 [!DNL Jupyter Notebook] 來寫入查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md).
