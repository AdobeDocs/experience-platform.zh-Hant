---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；oracle;
title: （測試版）使用Platform UI建立OracleResponsys來源連線
description: 了解如何使用Platform UI將Adobe Experience Platform連線至OracleResponsys。
source-git-commit: ff3cac5f18ea49b93b3d76e4cd8fb0d597d02be4
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 1%

---

# （測試版）建立 [!DNL Oracle Responsys] 使用Platform UI的來源連線

>[!NOTE]
>
>此 [!DNL Oracle Responsys] 來源為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

本教學課程提供建立 [[!DNL Oracle Responsys]](../../../../connectors/marketing-automation/oracle-responsys.md) 源連接(使用Adobe Experience Platform用戶介面)。

## 快速入門

本指南需要妥善了解Platform的下列元件：

* [來源](../../../../home.md):Platform可讓您從各種來源擷取資料，同時使用Platform服務來建構、加上標籤，以及增強傳入資料。
* [沙箱](../../../../../sandboxes/home.md):Platform提供的虛擬沙箱可將單一Platform執行個體分割成個別的虛擬環境，以協助開發及改進數位體驗應用程式。

如果您已驗證 [!DNL Oracle Responsys] 帳戶，則您可以略過本檔案的其餘部分，並繼續進行 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).

### 收集所需憑據

為了連接 [!DNL Oracle Responsys] 若要使用Platform，您必須提供下列驗證屬性的值：

| 憑據 | 說明 |
| --- | --- |
| 端點 | 您的 [!DNL Oracle Responsys] 例項。 |
| 用戶端ID | 您 [!DNL Oracle Responsys] 例項。 |
| 用戶端密碼 | 您的用戶端密碼 [!DNL Oracle Responsys] 例項。 |

有關的身份驗證憑據的詳細資訊 [!DNL Oracle Responsys]，請參閱 [[!DNL Oracle Responsys] 驗證指南](https://docs.oracle.com/en/cloud/saas/marketing/responsys-develop/API/GetStarted/authentication.htm).

收集完所需憑證後，您可以依照下列步驟連結您的 [!DNL Oracle Responsys] 帳戶至Platform。

## 連接您的 [!DNL Oracle Responsys] 帳戶

在平台UI中，選取 **[!UICONTROL 來源]** 從左側導覽器存取 [!UICONTROL 來源] 工作區。 此 [!UICONTROL 目錄] 畫面會顯示您可建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 [!UICONTROL 行銷自動化] 類別，選擇 **[!UICONTROL OracleResponsys]**，然後選取 **[!UICONTROL 新增資料]**.

![Adobe Experience Platform來源目錄，並反白顯示OracleResponsys來源。](../../../../images/tutorials/create/oracle-responsys/catalog.png)

此 **[!UICONTROL 連線OracleResponsys帳戶]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 現有帳戶

若要使用現有帳戶，請選取 [!DNL Oracle Responsys] 要使用建立新資料流的帳戶，然後選擇 **[!UICONTROL 下一個]** 繼續。

![oracleResponsys的現有帳戶驗證畫面。](../../../../images/tutorials/create/oracle-responsys/existing.png)

### 新帳戶

要建立新帳戶，請選擇 **[!UICONTROL 新帳戶]**，然後提供名稱、選用說明和您的 [!DNL Oracle Responsys] 憑證。 完成後，請選取 **[!UICONTROL 連接到源]** 然後讓新連接建立一段時間。

![oracleResponsys的新帳戶驗證畫面。](../../../../images/tutorials/create/oracle-eloqua/new.png)

## 後續步驟

依照本教學課程，您已驗證並建立來源連線，連線位於 [!DNL Oracle Responsys] 帳戶和平台。 您現在可以繼續下一個教學課程，以及 [建立資料流，將行銷自動化資料帶入Platform](../../dataflow/marketing-automation.md).
