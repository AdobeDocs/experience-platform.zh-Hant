---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；oracle;oracle雄辯；雄辯
solution: Experience Platform
title: 使用Platform UI建立OracleEloqua來源連線
description: 了解如何使用Platform UI將Adobe Experience Platform連線至OracleEloqua。
exl-id: c4431d85-5948-4122-9a99-dbacdde5a09f
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 1%

---

# 建立 [!DNL Oracle Eloqua] 使用Platform UI的來源連線

本教學課程提供建立 [!DNL Oracle Eloqua] 來源連接器(使用Adobe Experience Platform使用者介面)。

## 快速入門

本指南需要妥善了解Platform的下列元件：

* [來源](../../../../home.md):Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加上標籤，以及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。

如果您已驗證 [!DNL Oracle Eloqua] 帳戶，則您可以略過本檔案的其餘部分，並繼續進行 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).

### 收集所需憑據

為了連接 [!DNL Oracle Eloqua] 若要使用Platform，您必須提供下列驗證屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 端點 | 您 [!DNL Oracle Eloqua]. |
| 使用者名稱 | 您的 [!DNL Oracle Eloqua] 帳戶。 使用者名稱的格式必須為 `siteName + \\ + username`，其中 `siteName` 是您用來登入的公司名稱 [!DNL Oracle Eloqua] 和 `username` 是您的使用者名稱。 例如，您的登入使用者名稱可以是： `adobe\\emily`. |
| 密碼 | 與您的 [!DNL Oracle Eloqua] 使用者名稱。 |

有關的身份驗證憑據的詳細資訊 [!DNL Oracle Eloqua]，請參閱 [[!DNL Oracle Eloqua] 驗證指南](https://docs.oracle.com/en/cloud/saas/marketing/eloqua-rest-api/Authentication_Basic.html).

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Oracle Eloqua] 帳戶至Platform。

## 連接您的 [!DNL Oracle Eloqua] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 行銷自動化] 類別，選擇 **[!UICONTROL Oracle雄辯]**，然後選取 **[!UICONTROL 新增資料]**.

![目錄](../../../../images/tutorials/create/oracle-eloqua/catalog.png)

此 **[!UICONTROL 連接OracleEloqua帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Oracle Eloqua] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![現有](../../../../images/tutorials/create/oracle-eloqua/existing.png)

### 新帳戶

如果您要建立新帳戶，請選取 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的 [!DNL Oracle Eloqua] 憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![new](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 後續步驟

依照本教學課程，您已驗證並建立來源連線，連線位於 [!DNL Oracle Eloqua] 帳戶和平台。 您現在可以繼續下一個教學課程，以及 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).
