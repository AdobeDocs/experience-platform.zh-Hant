---
title: 設定Azure CMK的警報和IP允許清單
description: 瞭解如何將Adobe的靜態IP位址加入允許清單Azure Key Vault中，並瞭解Experience Platform警報如何協助偵測及解決客戶自控金鑰存取問題。
source-git-commit: 719273798954b70460c77711ef5eda5f9d22cdb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# 設定[!DNL Azure] CMK的警示和IP允許清單

為了提高透明度，Adobe提供[監控服務](../../../../observability/alerts/ui.md){target="_blank"}，可檢查您的金鑰儲存庫的存取狀態，並在發生問題時觸發警示。 這些警示可協助您快速回應，避免服務中斷。 若要啟用此服務，請將Adobe的靜態IP位址列入允許清單。

>[!IMPORTANT]
>
>如果您已停用公用網路存取或將[!DNL Azure]金鑰儲存庫設定為僅允許選取的網路，則必須將Adobe的靜態IP位址新增至允許清單。 如果沒有它，您可能無法收到可能影響您的Experience Platform執行個體的存取問題通知。

## 將[!DNL Azure]金鑰儲存庫中的Adobe靜態IP加入允許清單 {#add-adobe-static-ip}

若要在維持網路限制的同時啟用這些警示，請導覽至您的&#x200B;**[!DNL Azure Key Vault]** > **[!DNL Networking settings]**。 在&#x200B;**[!DNL Firewalls and virtual networks]**&#x200B;索引標籤中，選取&#x200B;**[!DNL Allow public access from specific virtual networks and IP addresses]**。

![[!DNL Azure]金鑰儲存庫網路設定畫面，顯示要在何處新增Adobe的靜態IP位址，並反白顯示「允許從存取」選項。](../../../images/governance-privacy-security/customer-managed-keys/key-vault-networking-settings.png)

### Adobe的靜態IP位址

>[!IMPORTANT]
>
>Adobe提供的靜態IP位址是： `20.88.123.53`。

接著，在&#x200B;**[!DNL Firewall]**&#x200B;區段中，選取&#x200B;**[!DNL Add your current IP address]**&#x200B;並將其取代為Adobe的靜態IP位址。 所有輸出連線都會被視為生產環境，因此這個靜態IP位址必須列入允許清單，以確保在受限制的網路設定中，對您的金鑰儲存庫的存取不會中斷。

>[!NOTE]
>
>在[!DNL Azure]金鑰儲存庫設定中新增或更新靜態IP位址後，最多允許10分鐘讓變更生效。 新增IP後，CMK應用程式會存取金鑰儲存庫以驗證許可權。

將Adobe的靜態IP加入允許清單後，Experience Platform可以監控對您金鑰儲存庫的存取並在發生問題時觸發警報。 這些警報會提供早期警告，讓您能夠在服務受到影響之前採取行動。 下一節詳細說明您可以收到的警示型別以及如何回應。

## 監視警報 {#monitor-alerts}

平台警示會通知您可能會中斷金鑰存取的問題，例如&#x200B;**[!UICONTROL 金鑰存取失敗]**&#x200B;或&#x200B;**[!UICONTROL 金鑰停用]**。 這些警示可協助您快速識別移除的靜態IP或設定錯誤的防火牆等問題。 若要還原存取權，請檢閱您的[!DNL Azure]防火牆設定，並重新新增必要的IP位址。

<!-- For a complete list of alert types and recommended resolutions, see the [CMK alert resolution reference](../alert-resolution-reference.md). -->

訂閱Adobe I/O事件通知，以在您的監視工具中接收即時警報。 如需設定指示，請參閱[訂閱Adobe I/O事件通知](../../../../observability/alerts/subscribe.md)。 您也可以參閱[警報UI指南](../../../../observability/alerts/ui.md)，瞭解如何在Experience Platform中檢視和管理警報。

## 後續步驟

您現在已為[!DNL Azure]金鑰儲存庫設定IP允許清單和警報監視。 若要在[!DNL Azure]中完成客戶自控金鑰的設定，請遵循這些設定指南。

- [設定 [!DNL Azure] 金鑰儲存庫](./azure-key-vault-config.md)
- [使用API設定CMK](./api-set-up.md)
- [使用UI設定CMK](./ui-set-up.md)
