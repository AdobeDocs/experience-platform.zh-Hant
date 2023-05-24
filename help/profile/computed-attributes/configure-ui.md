---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 如何配置計算屬性欄位
type: Documentation
description: 計算屬性是用於將事件級資料聚合到配置檔案級屬性中的函式。 要配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用架構欄位組將該欄位添加到現有架構，或通過選擇已在架構中定義的欄位來建立此欄位。
hide: true
hidefromtoc: true
source-git-commit: 5ae7ddbcbc1bc4d7e585ca3e3d030630bfb53724
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 1%

---


# (Alpha)在UI中配置計算屬性欄位

>[!IMPORTANT]
>
>計算屬性功能當前位於Alpha中，並且不適用於所有用戶。 文件和功能可能會有所變更。

要配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用架構欄位組將該欄位添加到現有架構，或通過選擇已在架構中定義的欄位來建立此欄位。

>[!NOTE]
>
>無法將計算屬性添加到Adobe定義的欄位組中的欄位。 欄位必須位於 `tenant` 命名空間，表示它必須是定義並添加到架構的欄位。

要成功定義計算屬性欄位，必須為 [!DNL Profile] 並作為該模式所基於的類的聯合模式的一部分出現。 有關 [!DNL Profile]-enabled schemas and unions，請查看 [!DNL Schema Registry] 開發人員指南部分 [為配置檔案和查看聯合架構啟用架構](../../xdm/api/getting-started.md)。 此外，還建議對 [工會一節](../../xdm/schema/composition.md) 在架構組合基礎文檔中。

本教程中的工作流使用 [!DNL Profile]-enabled schema ，並遵循定義包含計算屬性欄位的新欄位組並確保其是正確命名空間的步驟。 如果啟用了Profile的架構中已有一個位於正確命名空間的欄位，則可以直接繼續執行 [建立計算屬性](#create-a-computed-attribute)。

## 查看架構

後續步驟使用Adobe Experience Platform用戶介面查找架構、添加欄位組和定義欄位。 如果你想用 [!DNL Schema Registry] API，請參閱 [架構註冊表開發人員指南](../../xdm/api/getting-started.md) 有關如何建立欄位組、將欄位組添加到架構以及啟用用於的架構的步驟 [!DNL Real-Time Customer Profile]。

在用戶介面中，按一下 **[!UICONTROL 架構]** 在左欄上，使用 **[!UICONTROL 瀏覽]** 頁籤，快速查找要更新的架構。

![](../images/computed-attributes/Schemas-Browse.png)

找到架構後，按一下其名稱以開啟 [!DNL Schema Editor] 可以在其中編輯架構。

![](../images/computed-attributes/Schema-Editor.png)

## 建立欄位群組

要建立新欄位組，請按一下 **[!UICONTROL 添加]** 下 **[!UICONTROL 欄位組]** 的 **[!UICONTROL 組合]** 的上界。 開啟 **[!UICONTROL 添加欄位組]** 對話框，您可以在其中查看現有欄位組。 按一下的單選按鈕 **[!UICONTROL 建立新欄位組]** 來定義新欄位組。

為欄位組指定名稱和說明，然後按一下 **[!UICONTROL 添加欄位組]** 完成。

![](../images/computed-attributes/Add-field-group.png)

## 將計算屬性欄位添加到架構

您的新欄位組現在應出現在「 」中[!UICONTROL 欄位組]「 」部分[!UICONTROL 組合]。 按一下欄位組和多個欄位組的名稱 **[!UICONTROL 添加欄位]** 按鈕將出現在 **[!UICONTROL 結構]** 的子菜單。

選擇 **[!UICONTROL 添加欄位]** 在架構名稱旁邊添加頂級欄位，或選擇在您喜歡的架構內的任意位置添加該欄位。

按一下後 **[!UICONTROL 添加欄位]** 將開啟一個新對象，該對象以您的租戶ID命名，顯示該欄位位於正確的命名空間中。 在該對象中， **[!UICONTROL 新建欄位]** 的子菜單。 如果要定義計算屬性的欄位，則顯示此欄位。

![](../images/computed-attributes/New-field.png)

## 配置欄位

使用 **[!UICONTROL 欄位屬性]** 編輯器右側的「 」部分，提供新欄位的必要資訊，包括其名稱、顯示名稱和類型。

>[!NOTE]
>
>欄位的類型必須與計算的屬性值的類型相同。 例如，如果計算的屬性值是字串，則在架構中定義的欄位必須是字串。

完成後，按一下 **[!UICONTROL 應用]** 欄位的名稱及其類型將出現在 **[!UICONTROL 結構]** 的子菜單。

![](../images/computed-attributes/Apply.png)

## 啟用架構 [!DNL Profile]

在繼續之前，請確保已為 [!DNL Profile]。 按一下中的架構名稱 **[!UICONTROL 結構]** 的下界 **[!UICONTROL 架構屬性]** 按鈕 如果 **[!UICONTROL 配置檔案]** 滑塊為藍色，已為 [!DNL Profile]。

>[!NOTE]
>
>啟用架構 [!DNL Profile] 無法撤消，因此，如果在滑塊啟用後按一下它，則不必冒險禁用它。

![](../images/computed-attributes/Profile.png)

您現在可以按一下 **[!UICONTROL 保存]** 保存更新的架構，然後使用API繼續教程的其餘部分。

## 後續步驟

既然您已建立了一個欄位，計算屬性值將儲存到該欄位中，則可以使用 `/computedattributes` API終結點。 有關在API中建立計算屬性的詳細步驟，請按照中提供的步驟操作 [計算屬性API終結點指南](ca-api.md)。