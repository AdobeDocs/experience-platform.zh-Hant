---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 如何配置計算屬性欄位
topic-legacy: guide
type: Documentation
description: 計算屬性是用於將事件層級資料匯總到設定檔層級屬性的函式。 要配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用架構欄位組建立此欄位，以將該欄位添加到現有架構，或者選擇已在架構中定義的欄位。
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alpha)在UI中設定計算屬性欄位

>[!IMPORTANT]
>
>計算屬性功能當前位於Alpha中，不適用於所有用戶。 文件和功能可能會有所變更。

要配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用架構欄位組建立此欄位，以將該欄位添加到現有架構，或者選擇已在架構中定義的欄位。

>[!NOTE]
>
>計算屬性無法添加到Adobe定義欄位組內的欄位。 欄位必須位於 `tenant` 命名空間，這表示它必須是您定義並新增至架構的欄位。

為了成功定義計算屬性欄位，必須為 [!DNL Profile] 和會作為架構所在類的聯合架構的一部分出現。 如需 [!DNL Profile]啟用的架構和聯合，請參閱 [!DNL Schema Registry] 開發人員指南一節 [啟用配置檔案和查看聯合架構](../../xdm/api/getting-started.md). 建議您檢閱 [工會一節](../../xdm/schema/composition.md) 在結構構成基礎檔案中。

本教學課程中的工作流程使用 [!DNL Profile]-enabled架構，並遵循以下步驟：定義包含計算屬性欄位的新欄位組，並確保該欄位是正確的命名空間。 如果您已在啟用設定檔的架構中擁有正確命名空間的欄位，您可以直接繼續進行 [建立計算屬性](#create-a-computed-attribute).

## 檢視結構

後續步驟使用Adobe Experience Platform使用者介面來尋找結構、新增欄位群組及定義欄位。 如果您偏好使用 [!DNL Schema Registry] API，請參閱 [Schema Registry開發人員指南](../../xdm/api/getting-started.md) 有關如何建立欄位組、將欄位組添加到架構以及啟用架構以便與 [!DNL Real-Time Customer Profile].

在使用者介面中，按一下 **[!UICONTROL 結構]** 並使用 **[!UICONTROL 瀏覽]** 頁簽，快速查找要更新的架構。

![](../images/computed-attributes/Schemas-Browse.png)

找到架構後，按一下其名稱以開啟 [!DNL Schema Editor] 您可以在此編輯結構。

![](../images/computed-attributes/Schema-Editor.png)

## 建立欄位群組

若要建立新欄位群組，請按一下 **[!UICONTROL 新增]** 下一頁 **[!UICONTROL 欄位群組]** 在 **[!UICONTROL 組合物]** 區段。 這會開啟 **[!UICONTROL 新增欄位群組]** 對話方塊中，您可以看到現有欄位群組。 按一下 **[!UICONTROL 建立新欄位組]** 以定義新欄位群組。

為欄位群組命名和說明，然後按一下 **[!UICONTROL 新增欄位群組]** 完成時。

![](../images/computed-attributes/Add-field-group.png)

## 將計算屬性欄位添加到架構

您的新欄位群組現在應會顯示在「[!UICONTROL 欄位群組]&quot;[!UICONTROL 組合物]」。 按一下欄位群組名稱及多個 **[!UICONTROL 新增欄位]** 按鈕將顯示在 **[!UICONTROL 結構]** 的子母體。

選擇 **[!UICONTROL 新增欄位]** 在架構名稱旁邊，以添加頂級欄位，或者您可以選擇將該欄位添加到您喜歡的架構中的任何位置。

按一下 **[!UICONTROL 新增欄位]** 隨即開啟新物件，根據您的租用戶ID命名，顯示欄位位於正確的命名空間中。 在該物件中， **[!UICONTROL 新欄位]** 框。 如果要定義計算屬性的欄位，則此欄位。

![](../images/computed-attributes/New-field.png)

## 設定欄位

使用 **[!UICONTROL 欄位屬性]** 區段，為新欄位提供必要的資訊，包括其名稱、顯示名稱和類型。

>[!NOTE]
>
>欄位的類型必須與計算屬性值的類型相同。 例如，如果計算屬性值是字串，則架構中定義的欄位必須是字串。

完成後，按一下 **[!UICONTROL 套用]** 和欄位名稱，及其類型會顯示在 **[!UICONTROL 結構]** 的子母體。

![](../images/computed-attributes/Apply.png)

## 為啟用架構 [!DNL Profile]

繼續之前，請確定已為 [!DNL Profile]. 按一下 **[!UICONTROL 結構]** 編輯器的區段，以便 **[!UICONTROL 架構屬性]** 頁簽。 若 **[!UICONTROL 設定檔]** 滑桿為藍色，已為 [!DNL Profile].

>[!NOTE]
>
>為 [!DNL Profile] 無法撤消，因此，如果在啟用滑桿後按一下滑桿，則不必冒險禁用它。

![](../images/computed-attributes/Profile.png)

您現在可以按一下 **[!UICONTROL 儲存]** 若要儲存更新的結構，並繼續使用API進行教學課程的其餘部分。

## 後續步驟

現在您已建立將計算屬性值儲存到其中的欄位，您可以使用 `/computedattributes` API端點。 如需在API中建立計算屬性的詳細步驟，請遵循 [計算屬性API端點指南](ca-api.md).