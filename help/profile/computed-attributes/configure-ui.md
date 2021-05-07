---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；故障排除；API
title: 如何配置計算屬性欄位
topic-legacy: guide
type: Documentation
description: 計算屬性是用於將事件級別資料聚合到配置檔案級別屬性的函式。 為了配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用架構欄位組建立此欄位，以將該欄位添加到現有架構中，或通過選擇已在架構中定義的欄位來建立此欄位。
translation-type: tm+mt
source-git-commit: 6e0f7578d0818f88e13b963f64cb2de6729f0574
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 1%

---


# (Alpha)在UI中設定計算屬性欄位

>[!IMPORTANT]
>
>計算屬性功能目前位於alpha值中，並非所有使用者都能使用。 文件和功能可能會有所變更。

為了配置計算屬性，首先需要標識將保存計算屬性值的欄位。 可以使用架構欄位組建立此欄位，以將該欄位添加到現有架構中，或通過選擇已在架構中定義的欄位來建立此欄位。

>[!NOTE]
>
>計算屬性不能添加到Adobe定義欄位組內的欄位。 欄位必須位於`tenant`命名空間中，這表示欄位必須是您定義並新增至架構的欄位。

要成功定義計算屬性欄位，必須為[!DNL Profile]啟用模式，並作為模式所基於類的聯合模式的一部分出現。 有關[!DNL Profile]啟用架構和聯合的詳細資訊，請查看[!DNL Schema Registry]開發人員指南中有關[啟用描述檔和查看聯合架構的章節](../../xdm/api/getting-started.md)。 還建議在架構構成基礎文檔中查看關於union](../../xdm/schema/composition.md)的[部分。

本教程中的工作流使用[!DNL Profile]啟用的模式，並遵循定義包含計算屬性欄位的新欄位組並確保其為正確的命名空間的步驟。 如果已在啟用概要檔案的架構中有一個欄位處於正確的命名空間中，則可以直接執行[建立計算屬性](#create-a-computed-attribute)的步驟。

## 檢視結構

以下步驟使用Adobe Experience Platform用戶介面查找方案、添加欄位組和定義欄位。 如果您偏好使用[!DNL Schema Registry] API，請參閱[方案註冊表開發人員指南](../../xdm/api/getting-started.md)以取得如何建立欄位群組、新增欄位群組至架構以及啟用與[!DNL Real-time Customer Profile]搭配使用之架構的步驟。

在使用者介面中，按一下左側導軌中的&#x200B;**[!UICONTROL Schemas]**，然後使用&#x200B;**[!UICONTROL Browse]**&#x200B;標籤上的搜尋列，快速找到您要更新的架構。

![](../images/computed-attributes/Schemas-Browse.png)

找到架構後，按一下其名稱以開啟[!DNL Schema Editor] ，您可以在其中編輯架構。

![](../images/computed-attributes/Schema-Editor.png)

## 建立欄位群組

若要建立新欄位群組，請按一下編輯器左側&#x200B;**[!UICONTROL Composition]**&#x200B;區段中&#x200B;**[!UICONTROL Field groups]**&#x200B;旁的&#x200B;**[!UICONTROL Add]**。 這會開啟&#x200B;**[!UICONTROL Add field group]**&#x200B;對話方塊，您可在其中看到現有欄位群組。 按一下&#x200B;**[!UICONTROL Create new field group]**&#x200B;的單選按鈕以定義新欄位組。

為欄位組提供名稱和說明，完成後按一下&#x200B;**[!UICONTROL Add field group]**。

![](../images/computed-attributes/Add-field-group.png)

## 將計算屬性欄位添加到方案

您的新欄位群組現在應會出現在「[!UICONTROL Composition]」下方的「[!UICONTROL Field groups]」區段中。 按一下欄位群組的名稱，編輯器的&#x200B;**[!UICONTROL Structure]**&#x200B;區段中會出現多個&#x200B;**[!UICONTROL Add field]**&#x200B;按鈕。

選擇方案名稱旁的&#x200B;**[!UICONTROL Add field]**&#x200B;以添加頂層欄位，或者可以選擇將該欄位添加到方案內任意位置。

按一下&#x200B;**[!UICONTROL Add field]**&#x200B;後，會開啟新物件（以您的租用戶ID命名），顯示欄位在正確的命名空間中。 在該對象中，將顯示&#x200B;**[!UICONTROL New field]**。 如果要定義計算屬性的欄位為此欄位，則為此欄位。

![](../images/computed-attributes/New-field.png)

## 設定欄位

使用編輯器右側的&#x200B;**[!UICONTROL Field properties]**&#x200B;區段，為新欄位提供必要資訊，包括其名稱、顯示名稱和類型。

>[!NOTE]
>
>欄位的類型必須與計算的屬性值相同。 例如，如果計算的屬性值是字串，則方案中定義的欄位必須是字串。

完成後，按一下&#x200B;**[!UICONTROL Apply]** ，欄位的名稱及其類型將顯示在編輯器的&#x200B;**[!UICONTROL Structure]**&#x200B;部分。

![](../images/computed-attributes/Apply.png)

## 為[!DNL Profile]啟用模式

繼續之前，請確定[!DNL Profile]的架構已啟用。 按一下編輯器&#x200B;**[!UICONTROL Structure]**&#x200B;部分中的架構名稱，以便顯示&#x200B;**[!UICONTROL Schema Properties]**&#x200B;頁籤。 如果&#x200B;**[!UICONTROL Profile]**&#x200B;滑桿為藍色，則[!DNL Profile]的架構已啟用。

>[!NOTE]
>
>為[!DNL Profile]啟用架構無法撤消，因此，如果在啟用滑塊後按一下該滑塊，則不必冒險禁用它。

![](../images/computed-attributes/Profile.png)

您現在可以按一下&#x200B;**[!UICONTROL Save]**&#x200B;來儲存更新的架構，並使用API繼續教學課程的其餘部分。

## 後續步驟

現在，您已經建立了一個欄位，計算屬性值將儲存到該欄位中，您可以使用`/computedattributes` API端點建立計算屬性。 有關在API中建立計算屬性的詳細步驟，請遵循[計算屬性API端點指南](ca-api.md)中提供的步驟。