---
title: 帳戶對象
description: 瞭解如何建立和使用帳戶對象，以定位下游目的地中的帳戶設定檔。
badgeLimitedAvailability: label="可用性限制" type="Caution"
badgeB2B: label="B2B版本" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
source-git-commit: 77ba3bd55c2f2ac217612880b83b731919aa14af
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 0%

---


# 帳戶對象

>[!AVAILABILITY]
>
>帳戶對象僅適用於 [Real-time Customer Data Platform的B2B版本](../../rtcdp/b2b-overview.md). 此外，帳戶對象功能目前正在 **可用性限制**. 請聯絡Adobe客戶服務或您的Adobe代表，以要求存取此功能。

透過帳戶細分，Adobe Experience Platform可讓您從以人物為基礎的受眾到以帳戶為基礎的受眾，使用完整且精密的行銷細分體驗。

帳戶對象可用於作為以帳戶為基礎的目的地的輸入，讓您在下游服務中鎖定這些帳戶內的人員。 例如，您可以使用以帳戶為基礎的受眾來擷取所有已建立帳戶的記錄 **非** 擁有首席營運官(COO)或首席行銷官(CMO)職銜之人員的聯絡資訊。

## 術語 {#terminology}

開始使用帳戶對象之前，請先檢閱不同對象型別之間的差異：

- **帳戶對象**：帳戶對象是使用建立的對象 **帳戶** 設定檔資料。 帳戶設定檔資料可用來建立受眾，將下游帳戶內的人員設為目標。 如需帳戶設定檔的詳細資訊，請參閱 [帳戶設定檔概述](../../rtcdp/accounts/account-profile-overview.md).
- **People對象**：People對象是使用建立的對象 **客戶** 設定檔資料。 客戶設定檔資料可用來建立以您企業的客戶為目標之對象。 如需客戶設定檔的詳細資訊，請參閱 [即時客戶個人檔案總覽](../../profile/home.md).
- **潛在客戶對象**：潛在客戶對象是使用建立的對象 **潛在客戶** 設定檔資料。 潛在客戶設定檔資料可用來從未經驗證的使用者建立對象。 如需潛在客戶設定檔的詳細資訊，請參閱 [潛在客戶設定檔概述](../../profile/ui/prospect-profile.md).

## 存取 {#access}

若要存取帳戶對象，請選取「 」 **[!UICONTROL 受眾]** 在 **[!UICONTROL 帳戶]** 區段。

![Accounts區段內的Audiences按鈕會醒目提示。](../images/ui/account-audiences/select.png)

此 [!UICONTROL 瀏覽] 頁面隨即顯示，顯示組織所有帳戶對象的清單。

![隨即顯示屬於組織的帳戶對象。](../images/ui/account-audiences/browse.png)

此檢視會列出對象的相關資訊，包括名稱、設定檔計數、來源、生命週期狀態、建立日期和上次更新日期。

## 建立對象 {#create}

若要建立帳戶對象，請選取 **[!UICONTROL 建立對象]** 於 [!UICONTROL 瀏覽] 頁面。

![此 [!UICONTROL 建立對象] 按鈕會在帳戶對象瀏覽頁面上反白顯示。](../images/ui/account-audiences/select-create-audience.png)

「區段產生器」隨即顯示。 帳戶屬性會顯示在左側導覽列上。

![隨即顯示「區段產生器」。 請注意，只會顯示屬性。](../images/ui/account-audiences/segment-builder.png)

建立帳戶對象時，請注意，事件會列於 **[!UICONTROL 人員]**，而非他們自己的標籤，因為這些屬性會與人員相關聯。

![尋找事件的位置，位於 [!UICONTROL 人員] 資料夾)會反白顯示。](../images/ui/account-audiences/attributes.png)

如需使用「區段產生器」的詳細資訊，請參閱 [區段產生器UI指南](./segment-builder.md).

## 啟用對象 {#activate}

>[!NOTE]
>
>只有有限數量的目的地可支援帳戶對象。 在繼續此程式之前，請確定您要啟用的目的地可支援帳戶對象。

建立帳戶對象後，您可以對其他下游服務啟用對象。

選取您要啟用的對象，然後 **[!UICONTROL 啟用到目的地]**.

![此 [!UICONTROL 啟用到目的地] 在所選對象的「快速動作」功能表中，按鈕會反白顯示。](../images/ui/account-audiences/activate.png)

此 [!UICONTROL 啟用目的地] 頁面便會顯示。 如需啟用程式的詳細資訊，包括支援的目的地和欄位對應的詳細資訊，請參閱 [啟用帳戶對象](/help/destinations/ui/activate-account-audiences.md) 教學課程。

## 後續步驟 {#next-steps}

閱讀本指南後，您現在已更瞭解如何在Adobe Experience Platform中建立和使用您的帳戶對象。 若要瞭解如何在Platform中使用其他型別的對象，請參閱 [Segmentation Service UI指南](./overview.md).
