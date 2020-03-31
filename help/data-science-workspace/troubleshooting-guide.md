---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Data Science Workspace疑難排解指南
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: 1f756e7bc71c9ff227757aee64af29e0772c24af

---


# Data Science Workspace疑難排解指南

本檔案提供有關Adobe Experience Platform Data Science Workspace常見問題的解答。 如需有關Platform API的一般問題和疑難排解，請參閱 [Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md)。

## Google Chrome中未載入JupyterLab環境

透過Google Chrome瀏覽器的最新80.x版更新，所有第三方Cookie都預設會遭到封鎖。 此新政策可防止JupyterLab在Adobe Experience Platform中載入。

>[!NOTE] 這是暫時的問題。 第三方Cookie的依賴性已設定為在未來版本中移除。

要解決此問題，請使用以下步驟：

在您的Chrome瀏覽器中，導覽至右上角並選取「 **Settings** 」(或者，您可以在位址列中複製並貼上「chrome://settings/」)。 接著，捲動至頁面底部，然後按一下「進階 **」下拉** 式清單。

![chrome進階](./images/faq/chrome-advanced.png)

此時會 *顯示「隱私與安全* 」區段。 接著，按一下「 **網站設定** 」，接 **著按Cookie和網站資料**。

![chrome進階](./images/faq/privacy-security.png)

![chrome進階](./images/faq/cookies.png)

最後，將「封鎖協力廠商Cookie」切換為「OFF」。

![chrome進階](./images/faq/toggle-off.png)

>[!NOTE] 或者，您也可以停用協力廠商Cookie和白名 [單*。]ds.adobe.net

導覽至您位址列中的「chrome://flags/」。 使用右側的下拉式選單， *搜尋並停用標題為「依預設設定SameSite* Cookie」的標幟。

![禁用樣本標幟](./images/faq/samesite-flag.png)

步驟2後，系統會提示您重新啟動瀏覽器。 重新啟動後，Jupyterlab應該可供存取。

## 我為何無法在Safari中存取JupyterLab?

Safari預設會停用協力廠商Cookie。 由於您的Jupyter虛擬機器實例位於與其父框架不同的域上，因此Adobe Experience Platform目前要求啟用第三方Cookie。 請啟用協力廠商Cookie或切換至其他瀏覽器，例如Google Chrome。

## 為什麼在JupyterLab中嘗試上傳或刪除檔案時，會看到「403 Forbidden」訊息？

如果您的瀏覽器已啟用廣告封鎖軟體（例如Ghostery或AdBlock Plus），網域&quot;\*.adobe.net&quot;必須列入每個廣告封鎖軟體的白名單，JupyterLab才能正常運作。 這是因為JupyterLab虛擬機運行在與Experience Platform域不同的域上。

## 為什麼Jupyter筆記本的某些部分看起來亂了，或者沒有顯示為代碼？

如果所討論的儲存格意外地從「程式碼」變更為「標籤」，就會發生這種情況。 當程式碼儲存格聚焦時，按鍵組合 **ESC+M** ，會將儲存格的類型變更為Markdown。 單元格的類型可以通過選定單元格的筆記本頂部的下拉清單指示器進行更改。 若要將儲存格類型變更為程式碼，請從選取您要變更的指定儲存格開始。 接著，按一下指示儲存格目前類型的下拉式清單，然後選取「程式碼」。

![](./images/faq/code_type.png)

## 如何安裝自訂Python程式庫？

Python內核已預先安裝許多常用的機器學習庫。 不過，您可以在程式碼儲存格中執行下列命令，以安裝其他自訂程式庫：

```shell
!pip install {LIBRARY_NAME}
```

有關預安裝Python庫的完整清單，請參 [閱JupyterLab使用手冊的附錄部分](./jupyterlab/overview.md#supported-libraries)。

## 我是否可安裝自訂PySpark程式庫？

很遺憾，您無法為PySpark內核安裝其他庫。 不過，您可以聯絡您的Adobe客戶服務代表，以便為您安裝自訂PySpark程式庫。

如需預先安裝之PySpark程式庫的清單，請參 [閱JupyterLab使用指南的附錄一節](./jupyterlab/overview.md#supported-libraries)。

## 是否可為JupyterLab Spark或PySpark內核配置Spark群集資源？

通過將以下塊添加到筆記本的第一個單元格，可以配置資源：

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

有關Spark群集資源配置的詳細資訊（包括可配置屬性的完整清單），請參 [閱JupyterLab使用手冊](./jupyterlab/overview.md#pyspark-spark-execution-resource)。