---
keywords: RTCDP;CDP;B2B版；Real-time Customer Data Platform；即時客戶資料平台；即時cdp;b2b;cdp
solution: Experience Platform
title: Real-time Customer Data PlatformB2B版入門
description: 在設定Adobe Real-time Customer Data PlatformB2B版的實現時，請以此示例方案為例。
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Real-time Customer Data PlatformB2B版入門

本文檔提供了一個高級端到端工作流，用於開始使用Real-time Customer Data Platform(CDP)B2B版，使用示例用例來說明關鍵概念。

科技公司Bodea希望將來自不同獨立資料源的個人和帳戶資料結合起來，以便通過電子郵件和LinkedIn針對其新產品的廣告活動有效地瞄準客戶。 Bodea將Marketo Engage作為其營銷自動化平台，需要從包含客戶資料的多個CRM中分割特定於B2B的受眾。

## 快速入門

本教程工作流依賴於幾個Adobe Experience Platform服務作為演示的一部分。 如果您想要遵循，建議您充分瞭解以下服務：

- [體驗資料模式(XDM)](../xdm/home.md)
- [來源](../sources/home.md)
- [區段](../segmentation/home.md)
- [目的地](../destinations/home.md)

## 為資料建立架構

作為初始設定的一部分， Bodea的IT部門需要建立XDM架構，以確保其資料在進入平台時遵循標準格式，並可跨不同的平台服務和Adobe Experience Cloud產品(如Adobe Analytics和Adobe Target)採取行動。

>[!WARNING]
>
>您必須遵循本教程中連結的相關源文檔中所述的攝取模式。 其他的欄位映射方法無法保證有效。

Adobe Experience Platform允許您自動生成B2B資料源所需的架構和命名空間。 此工具確保建立的架構以結構化的可重用方式描述資料。 關注 [B2B命名空間和模式自動生成實用程式文檔](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) 的子菜單。

在Adobe Experience PlatformUI中，Bodea營銷人員選擇 **[!UICONTROL 架構]** 左欄，後面是 **[!UICONTROL 瀏覽]** 頁籤。 由於它們使用了Marketo Engage自動生成實用程式，因此新的空架構將出現在清單中，並且所有架構都具有前置詞「B2B」。

![架構工作區瀏覽頁籤](./assets/b2b-tutorial/empty-b2b-schemas.png)

自動生成實用程式使用標準XDM B2B類(如 [XDM業務客戶](../xdm/classes/b2b/business-account.md) 和 [XDM業務機會](../xdm/classes/b2b/business-opportunity.md))捕獲基本B2B資料實體。 此外，在這些類上構建的自動生成的B2B模式具有預先建立的關係，允許高級分段使用案例。 通過UI，可以輕鬆建立資料結構所需的任何附加欄位組。 查看 [XDM UI指南，將欄位組添加到架構節](../xdm/ui/resources/schemas.md#add-field-groups) 的子菜單。

>[!NOTE]
> 
>如果您未使用自動生成器實用程式，或者需要建立新關係，請參閱上的教程 [建立B2B架構之間的關係](../xdm/tutorials/relationship-b2b.md)。

即時客戶配置檔案合併來自不同來源的資料以建立關鍵B2B實體的合併配置檔案。 由於概要檔案是基於單個類生成的，因此自動生成實用程式基於通用業務使用案例來設定方案之間的關係。 因此，Bodea團隊現在準備根據其B2B模式接收資料。

>[!NOTE]
> 
>自動生成實用程式為架構建立的預設標識命名空間、主鍵和關係可以輕鬆地在架構工作區中發現。
>
>![預設架構標識和關係UI顯示](./assets/b2b-tutorial/schema-identity-relationship.png)

## 將資料插入Experience Platform

接下來，Bodea的營銷人員使用 [Marketo Engage連接器](../sources/connectors/adobe-applications/marketo/marketo.md) 將資料導入平台，以用於下游服務。 您還可以使用Real-Time CDPB2B版的一個批准源來接收資料。

>[!NOTE]
> 
>要瞭解組織可以使用哪些源連接器，可以在平台UI中查看源目錄。 要訪問目錄，請選擇 **源** 在左側導航中，然後選擇 **目錄**。

要在Marketo帳戶和平台之間建立連接，必須獲取身份驗證憑據。 查看 [獲取Marketo源連接器身份驗證憑據指南](../sources/connectors/adobe-applications/marketo/marketo-auth.md) 的上界。

在獲取驗證憑據後，Bodea營銷人員在Marketo帳戶和其平台組織之間建立連接。 請參閱文檔以瞭解 [如何使用平台UI連接Marketo帳戶](../sources/tutorials/ui/create/adobe-applications/marketo.md)。

Marketo Engage源連接器提供了自動映射功能，使將所有資料欄位映射到新建立的架構的資料欄位的過程更容易。

>[!NOTE]
> 
>如果在XDM架構中建立了自定義欄位組，則在該流程的此階段，您可能沒有連接欄位。 確保檢查填充自定義欄位組的所有值。

Bodea商家檢查所有欄位組是否都經過適當映射，並通過初始化資料流繼續源設定過程。 通過建立資料流以引入Marketo資料，下游平台服務可以使用傳入資料。 在初始攝取過程中，將資料作為批量引入Experience Platform。 之後，隨後接收的資料隨後通過近乎即時的更新流入Profile。

## 建立段以評估資料

下一個任務是根據源資料中相關實體的特定屬性，為Bodea的新電子郵件營銷活動建立一個受眾。 在平台UI中，Bodea營銷人員首先選擇 **[!UICONTROL 段]** 的 **[!UICONTROL 建立段]**。

在此示例中，該段將查找在銷售部門工作且與任何具有至少一個未結銷售機會的帳戶相關的所有人員。 此段要求在XDM Individual Profile類、 XDM Business Account類和XDM Business Opportunity類之間建立連結。

![用例段](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>有關如何建立段以評估資料的說明，請參閱 [段生成器UI指南](../segmentation/ui/segment-builder.md)。 有關更具體的B2B分段使用案例，請參閱 [Real-Time CDPB2B版分段概述](./segmentation/b2b.md)。

段構建器允許您從即時客戶配置檔案資料建立有市場的受眾，並根據您定義的屬性、事件和現有受眾的組合查看對潛在受眾的估計。

## 將評估的資料激活到目標

成功建立段後，將在 [!UICONTROL 詳細資訊] 的子菜單。 由於當前沒有為該段激活目標，Bodea營銷人員需要將受眾導出到資料集，以便訪問該資料集並對其採取行動。

在 [!UICONTROL 段] 平台UI的工作區，Bodea商家選擇 **[!UICONTROL 激活到目標]**。

![將段激活到目標](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>請參閱上的教程 [激活到目標的段](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) 有關如何完成此操作的全面步驟。

Bodea營銷人員將段激活到Marketo目的地，這樣他們就可以以靜態清單的形式將段資料從平台推送到Marketo Engage。 請參閱 [Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) 的子菜單。

## 後續步驟

通過學完本教程，您成功地利用了Real-Time CDPB2B版使用的各種Adobe Experience Platform服務。 因此，您已學會將B2B資料作為可以跨不同渠道參與的可操作受眾進行接收、分段、評估和導出。
