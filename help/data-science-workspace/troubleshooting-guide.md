---
keywords: Experience Platform；疑難排解；資料科學工作區；熱門主題
solution: Experience Platform
title: Data Science Workspace疑難排解指南
topic-legacy: Troubleshooting
description: 本檔案提供有關Adobe Experience Platform資料科學工作區的常見問題解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑難排解指南

本檔案提供有關Adobe Experience Platform[!DNL Data Science Workspace]的常見問題解答。 有關[!DNL Platform] API的一般問題和疑難排解，請參閱[Adobe Experience PlatformAPI疑難排解指南](../landing/troubleshooting.md)。

## [!DNL JupyterLab] 環境未載入  [!DNL Google Chrome]

>[!IMPORTANT]
>
>此問題已解決，但仍可能存在於Google Chrome 80.x瀏覽器中。 請確定您的Chrome瀏覽器是最新的。

在[!DNL Google Chrome]瀏覽器版本80.x中，所有協力廠商Cookie都預設會遭到封鎖。 此策略可防止[!DNL JupyterLab]在Adobe Experience Platform內載入。

要解決此問題，請使用以下步驟：

在您的[!DNL Chrome]瀏覽器中，導覽至右上角並選取&#x200B;**Settings**(或者，您可以複製並貼上位址列中的&quot;chrome://settings/&quot;)。 接著，捲動至頁面底部，然後按一下&#x200B;**Advanced**&#x200B;下拉式清單。

![chrome進階](./images/faq/chrome-advanced.png)

出現&#x200B;**隱私和安全**&#x200B;部分。 接著，按一下「**網站設定**」，後面接著「**Cookie」和「網站資料**」。

![chrome進階](./images/faq/privacy-security.png)

![chrome進階](./images/faq/cookies.png)

最後，將「封鎖協力廠商Cookie」切換為「OFF」。

![chrome進階](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以停用協力廠商Cookie並新增[*。]ds.adobe.net到允許清單。

導覽至您位址列中的「chrome://flags/」。 使用右側的下拉式功能表，搜尋並停用標題為&#x200B;*「SameSite by default cookies」*&#x200B;的旗標。

![禁用樣本標幟](./images/faq/samesite-flag.png)

步驟2後，系統會提示您重新啟動瀏覽器。 重新啟動後，應該可以訪問[!DNL Jupyterlab]。

## 為什麼我無法在Safari中存取[!DNL JupyterLab]?

Safari預設會在Safari &lt; 12中停用協力廠商Cookie。 由於您的[!DNL Jupyter]虛擬機實例位於與其父幀不同的域上，因此Adobe Experience Platform當前要求啟用第三方Cookie。 請啟用協力廠商Cookie或切換至不同的瀏覽器，例如[!DNL Google Chrome]。

對於Safari 12，您必須將使用者代理切換為「[!DNL Chrome]」或「[!DNL Firefox]」。 若要切換使用者代理，請先開啟&#x200B;*Safari*&#x200B;功能表，然後選取&#x200B;**偏好設定**。 出現首選項窗口。

![Safari偏好設定](./images/faq/preferences.png)

在Safari偏好設定視窗中，選取&#x200B;**Advanced**。 然後勾選功能表列&#x200B;*方塊中的「顯示開發」功能表。*&#x200B;完成此步驟後，可關閉首選項窗口。

![Safari進階功能](./images/faq/advanced.png)

接著，從頂端導覽列選擇&#x200B;**Develop**&#x200B;功能表。 從&#x200B;**Develop**&#x200B;下拉式清單中，將滑鼠指標暫留在&#x200B;**User Agent**&#x200B;上。 您可以選擇要使用的&#x200B;**[!DNL Chrome]**&#x200B;或&#x200B;**[!DNL Firefox]**&#x200B;使用者代理字串。

![開發功能表](./images/faq/user-agent.png)

## 嘗試上傳或刪除[!DNL JupyterLab]中的檔案時，為什麼會看到「403 Forbidden」（403禁止）訊息？

如果您的瀏覽器已啟用廣告封鎖軟體，例如[!DNL Ghostery]或[!DNL AdBlock] Plus，則必須允許每個廣告封鎖軟體中的網域&quot;\*.adobe.net&quot;,[!DNL JupyterLab]才能正常運作。 這是因為[!DNL JupyterLab]虛擬機運行在與[!DNL Experience Platform]域不同的域上。

## 為什麼[!DNL Jupyter Notebook]的某些部分看起來有亂碼，或未呈現為程式碼？

如果所討論的儲存格意外地從「程式碼」變更為「標籤」，就會發生這種情況。 當代碼單元格被聚焦時，按鍵組合&#x200B;**ESC+M**&#x200B;將單元格的類型更改為Markdown。 單元格的類型可以通過選定單元格的筆記本頂部的下拉清單指示器進行更改。 若要將儲存格類型變更為程式碼，請從選取您要變更的指定儲存格開始。 接著，按一下指示儲存格目前類型的下拉式清單，然後選取「程式碼」。

![](./images/faq/code_type.png)

## 如何安裝自訂[!DNL Python]程式庫？

[!DNL Python]內核已預先安裝許多常用的機器學習庫。 不過，您可以在程式碼儲存格中執行下列命令，以安裝其他自訂程式庫：

```shell
!pip install {LIBRARY_NAME}
```

有關預安裝的[!DNL Python]庫的完整清單，請參閱《JupyterLab使用手冊》的[附錄部分。](./jupyterlab/overview.md#supported-libraries)

## 我是否可安裝自訂PySpark程式庫？

很遺憾，您無法為PySpark內核安裝其他庫。 不過，您可以聯絡Adobe客戶服務代表，以便為您安裝自訂PySpark程式庫。

如需預先安裝的PySpark程式庫清單，請參閱JupyterLab使用指南的[附錄一節。](./jupyterlab/overview.md#supported-libraries)

## 是否可為[!DNL JupyterLab] [!DNL Spark]或PySpark內核配置[!DNL Spark]群集資源？

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

有關[!DNL Spark]群集資源配置的詳細資訊，包括可配置屬性的完整清單，請參見[JupyterLab使用手冊](./jupyterlab/overview.md#kernels)。

## 為什麼在嘗試執行大型資料集的特定工作時收到錯誤訊息？

如果您收到錯誤，原因如`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`，這通常表示驅動程式或執行器記憶體不足。 有關資料限制以及如何在大型資料集上執行任務的詳細資訊，請參閱JupyterLab Notebooks [資料存取](./jupyterlab/access-notebook-data.md)文檔。 通常，將`mode`從`interactive`變更為`batch`可解決此錯誤。

## [!DNL Docker Hub] 資料科學工作區的限制限制

自2020年11月20日起，Docker Hub的匿名免費驗證使用費率限制生效。 匿名和免費[!DNL Docker Hub]使用者每六小時只能收到100個容器影像提取要求。 如果您受到這些變更的影響，將會收到以下錯誤訊息：`ERROR: toomanyrequests: Too Many Requests.`或`You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`。

目前，此限制僅會影響您的組織，前提是您要在6小時內建立100份「從筆記型電腦到方式」，或是您在資料科學工作區中使用經常放大或縮小的Spark型筆記型電腦。 但是，這不太可能，因為上運行的群集在空閒前保持活動狀態兩小時。 這樣可減少群集處於活動狀態時所需的提取數。 如果您收到上述任何錯誤，則需要等到[!DNL Docker]限制重設為止。

有關[!DNL Docker Hub]速率限制的詳細資訊，請訪問[ DockerHub文檔](https://www.docker.com/increase-rate-limits)。 解決方案正在開發中，並預期在後續版本中提供。
