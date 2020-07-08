---
keywords: Experience Platform;troubleshooting;Data Science Workspace;popular topics
solution: Experience Platform
title: Data Science Workspace疑難排解指南
topic: Troubleshooting
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 0%

---


# [!DNL Data Science Workspace] troubleshooting guide

本檔案提供有關Adobe Experience Platform的常見問題解答 [!DNL Data Science Workspace]。 For questions and troubleshooting regarding [!DNL Platform] APIs in general, see the [Adobe Experience Platform API troubleshooting guide](../landing/troubleshooting.md).

## [!DNL JupyterLab] environment is not loading in [!DNL Google Chrome]

>[!IMPORTANT]
>
>此問題已解決，但仍可能存在於Google Chrome 80.x瀏覽器中。 請確定您的Chrome瀏覽器是最新的。

With the [!DNL Google Chrome] browser version 80.x, all third-party cookies are blocked by default. 此政策可防止 [!DNL JupyterLab] 在Adobe Experience Platform中載入。

要解決此問題，請使用以下步驟：

在您的 [!DNL Chrome] 瀏覽器中，導覽至右上角並選取「設定」 **** (或者，您也可以複製並貼上位址列中的「chrome://settings/」)。 接著，捲動至頁面底部，然後按一下「進階 **」下拉** 式清單。

![chrome進階](./images/faq/chrome-advanced.png)

此時會 *顯示「隱私與安全* 」區段。 接著，按一下「 **網站設定** 」，接 **著按Cookie和網站資料**。

![chrome進階](./images/faq/privacy-security.png)

![chrome進階](./images/faq/cookies.png)

最後，將「封鎖協力廠商Cookie」切換為「OFF」。

![chrome進階](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以停用協力廠商Cookie並新增 [*。]ds.adobe.net到允許清單。

導覽至您位址列中的「chrome://flags/」。 使用右側的下拉式選單， *搜尋並停用標題為「依預設設定SameSite* Cookie」的標幟。

![禁用樣本標幟](./images/faq/samesite-flag.png)

步驟2後，系統會提示您重新啟動瀏覽器。 重新啟動後， [!DNL Jupyterlab] 應可存取。

## 我為何無法在Safari中 [!DNL JupyterLab] 存取？

Safari預設會在Safari &lt; 12中停用協力廠商Cookie。 由於您 [!DNL Jupyter] 的虛擬機器實例位於與其父框架不同的網域上，因此Adobe Experience Platform目前要求啟用第三方Cookie。 請啟用協力廠商Cookie或切換至其他瀏覽器，例如 [!DNL Google Chrome]。

對於Safari 12，您需要將使用者代理切換為「[!DNL Chrome]」或「[!DNL Firefox]」。 若要切換您的使用者代理，請先開啟 *Safari* 功能表，然後選 **取偏好設定**。 出現首選項窗口。

![Safari偏好設定](./images/faq/preferences.png)

在Safari偏好設定視窗中，選取「進 **階」**。 然後，勾選選選 *單列中的「顯示開發」選單* 。 完成此步驟後，可關閉首選項窗口。

![Safari進階功能](./images/faq/advanced.png)

接著，從頂端導覽列選取「開 **發** 」功能表。 從「開發」下 *拉式清單* ，將滑鼠指標暫留在「使 *用者代理」上*。 您可以選擇 **[!DNL Chrome]** 要使用的 **[!DNL Firefox]** 或用戶代理字串。

![開發功能表](./images/faq/user-agent.png)

## 為什麼在嘗試上傳或刪除中的檔案時，會看到「403禁止」訊息 [!DNL JupyterLab]?

如果您的瀏覽器已啟用廣告封鎖軟體(例如 [!DNL Ghostery] 或 [!DNL AdBlock] Plus)，則必須允許每個廣告封鎖軟體中的網域「\*.adobe.net」，才能正 [!DNL JupyterLab] 常運作。 這是因為 [!DNL JupyterLab] 虛擬機運行在與域不同的域 [!DNL Experience Platform] 上。

## 為什麼我的部分外觀 [!DNL Jupyter Notebook] 被加亂，或者無法呈現為程式碼？

如果所討論的儲存格意外地從「程式碼」變更為「標籤」，就會發生這種情況。 當程式碼儲存格聚焦時，按鍵組合 **ESC+M** ，會將儲存格的類型變更為Markdown。 單元格的類型可以通過選定單元格的筆記本頂部的下拉清單指示器進行更改。 若要將儲存格類型變更為程式碼，請從選取您要變更的指定儲存格開始。 接著，按一下指示儲存格目前類型的下拉式清單，然後選取「程式碼」。

![](./images/faq/code_type.png)

## 如何安裝自訂程 [!DNL Python] 式庫？

內核 [!DNL Python] 已預先安裝許多常用的機器學習程式庫。 不過，您可以在程式碼儲存格中執行下列命令，以安裝其他自訂程式庫：

```shell
!pip install {LIBRARY_NAME}
```

有關預安裝庫的完整列 [!DNL Python] 表，請參 [閱JupyterLab使用手冊的附錄部分](./jupyterlab/overview.md#supported-libraries)。

## 我是否可安裝自訂PySpark程式庫？

很遺憾，您無法為PySpark內核安裝其他庫。 不過，您可以聯絡您的Adobe客戶服務代表，以便為您安裝自訂PySpark程式庫。

如需預先安裝之PySpark程式庫的清單，請參 [閱JupyterLab使用指南的附錄一節](./jupyterlab/overview.md#supported-libraries)。

## 是否可為PySpark內 [!DNL Spark] 核配置群 [!DNL JupyterLab] 集 [!DNL Spark] 資源？

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

有關群集資源配 [!DNL Spark] 置的詳細資訊，包括可配置屬性的完整清單，請參 [見JupyterLab User Guide](./jupyterlab/overview.md#kernels)。