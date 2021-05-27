---
keywords: Experience Platform；疑難排解；Data Science Workspace；熱門主題
solution: Experience Platform
title: Data Science Workspace疑難排解指南
topic-legacy: Troubleshooting
description: 本檔案提供Adobe Experience Platform Data Science Workspace常見問題的解答。
exl-id: fbc5efdc-f166-4000-bde2-4aa4b0318b38
source-git-commit: c2c2b1684e2c2c3c76dc23ad1df720abd6c4356c
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 0%

---

# [!DNL Data Science Workspace] 疑難排解指南

本檔案提供Adobe Experience Platform [!DNL Data Science Workspace]常見問題的解答。 如需[!DNL Platform] API的一般問題和疑難排解，請參閱[Adobe Experience Platform API疑難排解指南](../landing/troubleshooting.md)。

## [!DNL JupyterLab] 環境未載入  [!DNL Google Chrome]

>[!IMPORTANT]
>
>此問題已解決，但Google Chrome 80.x瀏覽器中仍可能存在。 請確定您的Chrome瀏覽器為最新。

使用[!DNL Google Chrome]瀏覽器80.x版時，所有第三方Cookie都預設為封鎖。 此原則可防止[!DNL JupyterLab]在Adobe Experience Platform內載入。

若要解決此問題，請使用下列步驟：

在[!DNL Chrome]瀏覽器中，導覽至右上角並選取&#x200B;**設定**(或者，您也可以複製並貼上位址列中的&quot;chrome://settings/&quot;)。 接下來，捲動至頁面底部，然後按一下「**進階**」下拉式清單。

![chrome advanced](./images/faq/chrome-advanced.png)

**隱私權與安全性**&#x200B;區段隨即顯示。 接下來，按一下&#x200B;**網站設定**，後面接著&#x200B;**Cookie和網站資料**。

![chrome advanced](./images/faq/privacy-security.png)

![chrome advanced](./images/faq/cookies.png)

最後，將「封鎖第三方Cookie」切換為「關閉」。

![chrome advanced](./images/faq/toggle-off.png)

>[!NOTE]
>
>或者，您也可以停用第三方Cookie並新增[*。]ds.adobe.net至允許清單。

導覽至您位址列中的「chrome://flags/」。 使用右側的下拉式功能表，搜尋並停用標題為&#x200B;*&quot;SameSite依預設Cookie&quot;*&#x200B;的標幟。

![停用samesite標幟](./images/faq/samesite-flag.png)

步驟2後，系統會提示您重新啟動瀏覽器。 重新啟動後，應可存取[!DNL Jupyterlab]。

## 為何無法在Safari中存取[!DNL JupyterLab]?

Safari預設會在Safari &lt; 12中停用第三方Cookie。 由於您的[!DNL Jupyter]虛擬機實例位於與其父幀不同的域上，因此Adobe Experience Platform當前要求啟用第三方Cookie。 請啟用第三方Cookie或切換到其他瀏覽器，如[!DNL Google Chrome]。

若是Safari 12，您需要將使用者代理切換為「[!DNL Chrome]」或「[!DNL Firefox]」。 若要切換使用者代理，請從開啟&#x200B;*Safari*&#x200B;功能表開始，然後選取&#x200B;**偏好設定**。 將出現首選項窗口。

![Safari偏好設定](./images/faq/preferences.png)

在Safari偏好設定視窗中，選取&#x200B;**Advanced**。 然後勾選功能表列&#x200B;*中的*&#x200B;顯示開發功能表方塊。 完成此步驟後，可以關閉首選項窗口。

![Safari進階](./images/faq/advanced.png)

接下來，從頂端導覽列選取&#x200B;**Develop**&#x200B;功能表。 從&#x200B;**Develop**&#x200B;下拉式清單中，暫留在&#x200B;**User Agent**&#x200B;上。 您可以選取要使用的&#x200B;**[!DNL Chrome]**&#x200B;或&#x200B;**[!DNL Firefox]**&#x200B;使用者代理字串。

![開發功能表](./images/faq/user-agent.png)

## 嘗試上傳或刪除[!DNL JupyterLab]中的檔案時，為何會看到「403 Forbidden」訊息？

如果您的瀏覽器啟用了播發阻止軟體，如[!DNL Ghostery]或[!DNL AdBlock] Plus，則每個播發阻止軟體中必須允許域&quot;\*.adobe.net&quot;,[!DNL JupyterLab]才能正常運行。 這是因為[!DNL JupyterLab]虛擬機運行在與[!DNL Experience Platform]域不同的域上。

## 為什麼我的[!DNL Jupyter Notebook]的某些部分看起來有亂碼，或未呈現為程式碼？

如果意外將相關儲存格從「程式碼」變更為「Markdown」，就會發生此情況。 當程式碼儲存格聚焦時，按下鍵組合&#x200B;**ESC+M**&#x200B;會將儲存格的類型變更為Markdown。 通過筆記本頂部的下拉指示器，可以更改所選單元格的類型。 若要將儲存格類型變更為程式碼，請從選取您要變更的指定儲存格開始。 接下來，按一下指出儲存格目前類型的下拉式清單，然後選取「程式碼」。

![](./images/faq/code_type.png)

## 如何安裝自訂[!DNL Python]程式庫？

[!DNL Python]內核已預裝了許多常用的機器學習庫。 不過，您可以在程式碼儲存格內執行下列命令，以安裝其他自訂程式庫：

```shell
!pip install {LIBRARY_NAME}
```

如需預先安裝的[!DNL Python]庫的完整清單，請參閱JupyterLab使用手冊](./jupyterlab/overview.md#supported-libraries)的[附錄部分。

## 我可以安裝自訂的PySpark程式庫嗎？

很遺憾，無法為PySpark內核安裝其他庫。 不過，您可以聯絡Adobe客戶服務代表，為您安裝自訂PySpark程式庫。

有關預先安裝的PySpark庫的清單，請參閱《JupyterLab使用手冊》的[附錄部分](./jupyterlab/overview.md#supported-libraries)。

## 是否可為[!DNL JupyterLab] [!DNL Spark]或PySpark內核配置[!DNL Spark]群集資源？

通過將以下塊添加到筆記本的第一個單元格中，可以配置資源：

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

有關[!DNL Spark]群集資源配置（包括可配置屬性的完整清單）的詳細資訊，請參閱[JupyterLab User Guide](./jupyterlab/overview.md#kernels)。

## 嘗試對較大的資料集執行特定任務時，為何出現錯誤？

如果您收到錯誤，原因如`Reason: Remote RPC client disassociated. Likely due to containers exceeding thresholds, or network issues.`，這通常表示驅動程式或執行器記憶體不足。 有關資料限制以及如何在大型資料集上執行任務的詳細資訊，請參閱JupyterLab Notebooks [資料存取](./jupyterlab/access-notebook-data.md)檔案。 通常，此錯誤可通過將`mode`從`interactive`更改為`batch`來解決。

此外，在寫入大型Spark/PySpark資料集時，在執行寫入代碼之前快取資料(`df.cache()`)可以大大提高效能。

<!-- remove this paragraph at a later date once the sdk is updated -->

如果您在讀取資料時遇到問題，並將轉換套用至資料，請嘗試在轉換之前快取資料。 快取資料可防止網路上出現多次讀取。 從讀取資料開始。 接下來，快取(`df.cache()`)資料。 最後，執行轉換。

## Spark/PySpark筆記本為何花了這麼長的時間才讀取和寫入資料？

如果要對資料執行轉換，例如使用`fit()`，則轉換可能執行多次。 若要提高效能，請在執行`fit()`之前，使用`df.cache()`快取您的資料。 這可確保轉換只執行一次，並防止網路上出現多次讀取。

**建議的順序：** 從讀取資料開始。接下來，執行轉換，然後快取(`df.cache()`)資料。 最後，執行`fit()`。

## 為什麼我的Spark/PySpark筆記本無法運行？

如果您收到下列任何錯誤：

- 作業因預備失敗而中止……只能壓縮每個分區中元素數量相同的RDD。
- 遠程RPC客戶端斷開關聯和其他記憶體錯誤。
- 讀取和寫入資料集時效能不佳。

在寫入資料之前，請檢查以確定您正在快取資料(`df.cache()`)。 在筆記本中執行代碼時，在`fit()`等操作之前使用`df.cache()`可以大大提高筆記本的效能。 在寫入資料集之前使用`df.cache()` ，可確保轉換只執行一次，而非執行多次。

## [!DNL Docker Hub] Data Science Workspace的限制限制

自2020年11月20日起，Docker Hub的匿名免費驗證使用率限制已生效。 匿名和免費[!DNL Docker Hub]使用者每六小時最多只能有100個容器影像提取請求。 如果您受到這些變更的影響，將會收到此錯誤訊息：`ERROR: toomanyrequests: Too Many Requests.`或`You have reached your pull rate limit. You may increase the limit by authenticating and upgrading: https://www.docker.com/increase-rate-limits.`。

目前，此限制僅在您試圖在6小時內構建100個筆記型電腦至配方，或在Data Science Workspace中使用Spark筆記型電腦（經常放大和縮小）時，才會影響您的組織。 但是，這不太可能，因為這些運行在上的群集在空閒之前保持活動狀態兩小時。 這會減少叢集作用中時所需的提取數。 如果您收到上述任何錯誤，則需要等待[!DNL Docker]限制重設。

如需[!DNL Docker Hub]速率限制的詳細資訊，請造訪[DockerHub檔案](https://www.docker.com/increase-rate-limits)。 解決方案正在運作中，且預期會在後續版本中推出。
