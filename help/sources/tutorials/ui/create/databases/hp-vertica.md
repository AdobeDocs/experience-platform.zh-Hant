---
keywords: Experience Platform；首頁；熱門主題；HP Vertica
solution: Experience Platform
title: 在UI中建立HP Vertica源連接
type: Tutorial
description: 了解如何使用Adobe Experience Platform UI建立HP Vertica源連接。
exl-id: d7315ad4-9250-4e66-be33-016efabb512e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 1%

---

# 建立HP [!DNL Vertica] UI中的源連接

>[!NOTE]
>
> HP [!DNL Vertica] 連接器為測試版。 請參閱 [來源概觀](../../../../home.md#terms-and-conditions) 有關使用測試版標籤連接器的詳細資訊。

Adobe Experience Platform中的來源連接器可讓您依排程內嵌外部來源資料。 本教程提供了建立HP的步驟 [!DNL Vertica] 源連接器使用 [!DNL Platform] 使用者介面。

## 快速入門

本教學課程需要妥善了解下列Adobe Experience Platform元件：

* [[!DNL Experience Data Model (XDM)] 系統](../../../../../xdm/home.md):標準化框架 [!DNL Experience Platform] 組織客戶體驗資料。
   * [結構構成基本概念](../../../../../xdm/schema/composition.md):了解XDM結構描述的基本建置組塊，包括結構描述的主要原則和最佳實務。
   * [結構編輯器教學課程](../../../../../xdm/tutorials/create-schema-ui.md):了解如何使用結構編輯器UI建立自訂結構。
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯總資料，提供統一的即時消費者設定檔。

如果您已經擁有有效的HP [!DNL Vertica] 連線，您可以略過本檔案的其餘部分，並繼續進行有關 [配置資料流](../../dataflow/databases.md).

### 收集所需憑據

以下幾節提供了成功連接到HP所需了解的其他資訊 [!DNL Vertica] 使用 [!DNL Flow Service] API。

| 憑據 | 說明 |
| ---------- | ----------- |
| `connectionString` | 用於連接到HP的連接字串 [!DNL Vertica] 例項。 HP的連接字串模式 [!DNL Vertica] is `Server={SERVER};Port={PORT};Database={DATABASE};UID={USERNAME};PWD={PASSWORD}` |

如需快速入門的詳細資訊，請參閱 [此HP [!DNL Vertica] 檔案](https://www.vertica.com/docs/9.2.x/HTML/Content/Authoring/ConnectingToVertica/ClientJDBC/CreatingAndConfiguringAConnection.htm).

## 連接您的HP [!DNL Vertica] 帳戶

收集到所需的憑據後，您可以按照以下步驟連結HP [!DNL Vertica] 帳戶 [!DNL Platform].

登入 [Adobe Experience Platform](https://platform.adobe.com) 然後選取 **[!UICONTROL 來源]** 從左側導覽列存取 **[!UICONTROL 來源]** 工作區。 此 **[!UICONTROL 目錄]** 畫面會顯示您可以為其建立帳戶的各種來源。

您可以從畫面左側的目錄中選取適當的類別。 或者，您也可以使用搜尋選項找到您要使用的特定來源。

在 **[!UICONTROL 資料庫]** 類別，選擇 **[!UICONTROL HP Vertica]**. 如果這是您第一次使用此連接器，請選取 **[!UICONTROL 設定]**. 否則，請選取 **[!UICONTROL 新增資料]** 建立新HP [!DNL Vertica] 連接器。

![目錄](../../../../images/tutorials/create/hp-vertica/catalog.png)

此 **[!UICONTROL 連接到HP Vertica]** 頁。 在此頁面上，您可以使用新憑證或現有憑證。

### 新帳戶

如果使用新憑據，請選擇 **[!UICONTROL 新帳戶]**. 在顯示的輸入表單中，提供名稱、可選說明和您的HP [!DNL Vertica] 憑證。 完成後，請選取 **[!UICONTROL Connect]** 然後讓新連接建立一段時間。

![connect](../../../../images/tutorials/create/hp-vertica/new.png)

### 現有帳戶

要連接現有帳戶，請選擇HP [!DNL Vertica] 要連接的帳戶，然後選擇 **[!UICONTROL 下一個]** 來繼續。

![現有](../../../../images/tutorials/create/hp-vertica/existing.png)

## 後續步驟

按照本教程，您已建立了與HP的連接 [!DNL Vertica] 帳戶。 您現在可以繼續下一個教學課程，以及 [配置資料流以將資料帶入 [!DNL Platform]](../../dataflow/databases.md).
