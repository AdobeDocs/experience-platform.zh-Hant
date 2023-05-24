---
title: 將Jupyter筆記本連接到查詢服務
description: 瞭解如何將Jupyter筆記本與Adobe Experience Platform查詢服務連接。
exl-id: 358eab67-538f-4ada-931f-783b92db4a1c
source-git-commit: 1af89160cbf5b689396921869fec6c30a5bcfff0
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# 連接 [!DNL Jupyter Notebook] 查詢服務

本文檔介紹連接所需的步驟 [!DNL Jupyter Notebook] Adobe Experience Platform查詢服務。

## 快速入門

本指南要求您已具有訪問 [!DNL Jupyter Notebook] 並熟悉其介面。 下載 [!DNL Jupyter Notebook] 或有關詳細資訊，請參閱 [官 [!DNL Jupyter Notebook] 文檔](https://jupyter.org/)。

獲取連接所需的憑據 [!DNL Jupyter Notebook] Experience Platform，您必須 [!UICONTROL 查詢] 工作區。 如果您當前沒有訪問 [!UICONTROL 查詢] 工作區。

>[!TIP]
>
>[!DNL Anaconda Navigator] 是一種案頭圖形用戶介面(GUI)，它提供了一種更易於安裝和啟動的通用方法 [!DNL Python] 諸如 [!DNL Jupyter Notebook]。 它還有助於管理包、環境和通道，而無需使用命令行命令。
>按照其網站上的指導安裝過程 [安裝您首選的應用程式版本](https://docs.anaconda.com/anaconda/install/)。
>從Anaconda Navigator主螢幕中，選擇 **[!DNL Jupyter Notebook]** 從支援的應用程式清單啟動程式。
>有關詳細資訊，請參閱 [《蟒蛇》官方檔案](https://docs.anaconda.com/anaconda/navigator/)。

Jupyter官方文檔提供說明 [從命令行介面運行筆記本](https://docs.jupyter.org/en/latest/running.html#how-do-i-open-a-specific-notebook) (CLI)。

## Launch [!DNL Jupyter Notebook]

在您開啟新 [!DNL Jupyter Notebook] Web應用程式，選擇 **[!DNL New]** 從UI下拉，然後 **[!DNL Python 3]** 的子菜單。 的 [!DNL Notebook] 編輯器。

在 [!DNL Notebook] 編輯器，輸入以下值： `pip install psycopg2-binary` 選擇 **[!DNL Run]** 的雙曲餘切值。 輸入行下方顯示一條成功消息。

>[!IMPORTANT]
>
>作為此過程的一部分，您必須選擇 **[!DNL Run]** 執行每行代碼。

接下來，導入 [!DNL PostgreSQL] 資料庫適配器 [!DNL Python]。 輸入值： `import psycopg2`選擇 **[!DNL Run]**。 此進程沒有成功消息。 如果沒有錯誤消息，請繼續下一步。

您現在必須輸入以下值來提供您的Adobe Experience Platform憑據： `conn = psycopg2.connect("{YOUR_CREDENTIALS}")`。 您的連接憑據可在 [!UICONTROL 查詢] 的 [!UICONTROL 憑據] 頁籤。 請參閱有關如何 [查找組織憑據](../ui/credentials.md) 的上界。

在使用第三方客戶端時，建議使用非過期憑據，以節省重複輸入詳細資訊的工作量。 請參閱文檔以瞭解 [如何生成和使用非過期憑據](../ui/credentials.md#non-expiring-credentials)。

>[!IMPORTANT]
>
>從平台UI複製憑據時，無需對憑據進行其他格式設定。 它們可以在一行中提供，在屬性和值之間具有一個空格。 憑據用引號括起來， **不** 逗號分隔。

```python
conn = psycopg2.connect('''sslmode=require host=<YOUR_HOST_CREDENTIAL> port=80 dbname=prod:all user=<YOUR_ORGANIZATION_ID> password=<YOUR_PASSWORD>''')"
```

您 [!DNL Jupyter Notebook] 實例現在已連接到查詢服務。

## 查詢執行示例

既然你已連接 [!DNL Jupyter Notebook] 要查詢服務，可以使用 [!DNL Notebook] 輸入。 以下示例使用簡單查詢來演示該進程。

輸入以下值：

```python
cur = conn.cursor()
cur.execute('''<YOUR_QUERY_HERE>''')
data = [r for r in cur]
```

接下來，調用參數(`data` 在上例中)，以在未格式化的響應中顯示查詢結果。

要以更易於人學的方式格式化結果，請使用以下命令：

- `colnames = [desc[0] for desc in cur.description]`
- `import pandas as pd`
- `import numpy as np`
- `df = pd.DataFrame(samples,columns=colnames)`
- `df.fillna(0,inplace=True)`

這些命令不會生成成功消息。 如果沒有錯誤消息，則可以使用函式以表格格式輸出SQL查詢的結果。

輸入並運行 `df.head()` 函式，以查看表格化的查詢結果。

## 後續步驟

現在您已連接了Query Service，您可以使用 [!DNL Jupyter Notebook] 來編寫查詢。 有關如何編寫和運行查詢的詳細資訊，請閱讀 [運行查詢指南](../best-practices/writing-queries.md)。
