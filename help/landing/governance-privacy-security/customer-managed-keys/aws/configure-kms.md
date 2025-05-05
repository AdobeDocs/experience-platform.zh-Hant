---
title: 設定客戶自控金鑰的AWS KMS
description: 瞭解如何設定Amazon Web Services金鑰管理服務(KMS)，以便與Adobe Experience Platform中的客戶自控金鑰搭配使用。
exl-id: 0cf0deab-dc30-412f-b511-dee5504c3953
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1571'
ht-degree: 0%

---

# 設定客戶自控金鑰的AWS KMS

>[!AVAILABILITY]
>
>本檔案適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 目前有限數量的客戶可使用在AWS上執行的Experience Platform 。 若要進一步瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/landing/multi-cloud)。
>
>AWS上的[客戶自控金鑰](../overview.md) (CMK)支援Privacy and Security Shield，但不適用於Healthcare Shield。 Azure上的CMK同時支援Privacy和Security Shield以及Healthcare Shield。

使用本指南，透過Amazon Web Services (AWS)金鑰管理服務(KMS)建立、管理和控制Adobe Experience Platform的加密金鑰，來保護您的資料。 此整合可簡化法規遵循、透過自動化簡化作業，並免除維護您自己的關鍵管理基礎建設的必要性。

如需Customer Journey Analytics的特定指示，請參閱[Customer Journey Analytics CMK檔案](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/cja-privacy/cmk)

>[!IMPORTANT]
>
>Adobe Experience Platform預設會使用系統管理的金鑰加密靜態資料。 啟用客戶自控金鑰(CMK)後，您就可以完全控制資料安全性。 不過，此變更是不可逆的，一旦CMK啟用，您就無法回復到系統管理的金鑰。 您有責任安全地管理您的金鑰，以確保對資料的存取不會受到干擾，並防止可能無法存取。

使用AWS KMS，透過Adobe Experience Platform的整合式加密金鑰管理來增強資料安全性。 按照本指南建立和管理加密金鑰，確保您的資料受到保護。

## 先決條件 {#prerequisites}

在繼續閱讀本檔案之前，您應該充分瞭解下列重要概念和功能：

- **AWS金鑰管理服務(KMS)**：瞭解AWS KMS的基礎知識，包括如何建立、管理和輪換加密金鑰。 如需瞭解詳細資訊，請參閱[官方KMS檔案](https://docs.aws.amazon.com/kms/)。
- **AWS中的識別與存取管理(IAM)原則**： IAM是一項可讓您安全地管理AWS服務與資源存取的服務。 使用IAM可以：
   - 定義哪些使用者、群組和角色可以存取特定資源。
   - 指定允許或拒絕使用者執行的動作。
   - 使用IAM原則指派許可權，實作微調存取控制。
如需詳細資訊，請參閱[適用於AWS KMS的IAM原則](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html)。
- **Experience Platform的資料安全性**：探索Experience Platform如何確保資料安全性，以及如何與AWS KMS等外部服務整合以進行加密。 Experience Platform使用HTTPS TLS v1.2保護資料以進行傳輸、停止使用雲端提供者加密、隔離儲存以及可自訂的驗證和加密選項。 如需如何確保資料安全的詳細資訊，請參閱[治理、隱私權及安全性總覽](../overview.md)，或Experience Platform中[資料加密](../../encryption.md)的檔案。
- **AWS Management Console**：中央樞紐，您可從一個Web應用程式存取及管理所有AWS服務。 使用搜尋列快速尋找工具、檢查通知、管理您的帳戶和帳單，以及自訂您的設定。 如需詳細資訊，請參閱[官方AWS管理主控台檔案](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)。

## 快速入門 {#get-started}

本指南要求您已擁有Amazon Web Services帳戶的存取權和管理主控台的存取權。 請依照下列步驟開始：

### 選取支援的區域 {#select-supported-region}

AWS KMS僅於特定地區提供。 請確定您在支援KMS的區域中作業。 您可以在[AWS KMS端點與配額清單](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)中檢視支援地區的完整清單。

確保您的AWS KMS加密金鑰與Adobe Experience Platform執行個體位於相同地區，以維持資料駐留要求的合規性、最佳化效能，並避免額外的跨地區成本。 未對齊的區域可能會導致資料無法存取和整合失敗。

### 驗證許可權 {#verify-permissions}

確保您擁有必要的AWS Identity and Access Management (IAM)許可權，以便在KMS中建立、管理及使用加密金鑰。 若要驗證您的許可權：

1. 存取[IAM原則模擬器](https://policysim.aws.amazon.com/)。
2. 選取您的使用者帳戶或角色。
3. 模擬KMS動作，例如`kms:CreateKey`或`kms:Encrypt`。

如果模擬傳回錯誤或您不確定自己的許可權，請洽詢AWS管理員以取得協助。

### 檢查您的AWS帳戶設定

確認您的AWS帳戶已啟用以使用AWS KMS服務。 大部分的帳戶預設已啟用KMS存取，但您可以造訪[AWS管理主控台](https://aws.amazon.com/console/)來檢閱您的帳戶設定。 如需詳細資訊，請參閱[AWS Key Management Service開發人員指南](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)。

### 導覽至AWS KMS以開始金鑰設定

若要開始設定和管理您的加密金鑰，請登入您的AWS帳戶並導覽至AWS金鑰管理服務(KMS)。 從AWS管理主控台，從服務功能表選取&#x200B;**金鑰管理服務(KMS)**。

![反白顯示金鑰管理服務之AWS Management Console的搜尋下拉式功能表。](../../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## 建立新金鑰 {#create-a-key}

>[!IMPORTANT]
>
>確保加密金鑰的安全儲存、存取及可用性。 您有責任管理您的金鑰，並防止Experience Platform作業中斷。

在[!DNL Key Management Service (KMS)]工作區中，選取&#x200B;**[!DNL Create a key]**。

![含有[建立金鑰]的金鑰管理服務工作區反白顯示。](../../../images/governance-privacy-security/key-management-service/create-a-key.png)

## 設定金鑰設定 {#configure-key}

[!DNL Configure Key]工作流程隨即顯示。 依預設，金鑰型別設為&#x200B;**[!DNL Symmetric]**，而金鑰使用方式設為&#x200B;**[!DNL Encrypt and Decrypt]**。 在繼續之前，請確定已選取這些選項。

![使用[對稱]和[加密與解密]基本選項來設定[金鑰]工作流程的第一步。](../../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

展開&#x200B;**[!DNL Advanced options]**&#x200B;下拉式功能表。 建議您使用&#x200B;**[!DNL KMS]**&#x200B;選項，此選項可讓AWS建立和管理金鑰資料。 預設會選取&#x200B;**[!DNL KMS]**&#x200B;選項。

>[!NOTE]
>
>如果您已有金鑰，可以匯入外部金鑰資料或使用AWS [!DNL CloudHSM]金鑰存放區。 本檔案未涵蓋這些選項。

接著，選取[!DNL Regionality]設定，以指定金鑰的區域範圍。 選取&#x200B;**[!DNL Single-Region key]**，接著選取&#x200B;**[!DNL Next]**&#x200B;以繼續執行步驟二。

>[!IMPORTANT]
>
>AWS會強制對KMS金鑰施加地區限制。 此區域限制表示金鑰必須位於與您的Adobe帳戶相同的區域。 Adobe只能存取位於您帳戶地區內的KMS金鑰。 確認您選取的區域符合Adobe單一租使用者帳戶的地區。

![在AWS地區、KMS和單一地區金鑰進階選項強調顯示的設定金鑰工作流程的第一步。](../../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## 標籤並標籤您的金鑰 {#add-labels-and-tags-to-key}

工作流程的第二個[!DNL Add labels]階段隨即顯示。 您可在此設定[!DNL Alias]和[!DNL Tags]欄位，協助您從AWS KMS主控台管理並尋找您的加密金鑰。

在&#x200B;**[!DNL Alias]**&#x200B;輸入欄位中輸入索引鍵的描述性標籤。 別名可做為使用者易記的識別碼，使用AWS KMS主控台中的搜尋列快速找到金鑰。 為避免混淆，請選擇可反映金鑰用途的有意義名稱，例如「Adobe-Experience-Platform-Key」或「Customer-Encryption-Key」。 如果金鑰別名不足以說明其用途，您也可以包含金鑰的說明。

最後，透過在[!DNL Tags]區段中新增索引鍵/值組，將中繼資料指派給您的索引鍵。 此步驟為選用，但您應新增標籤以分類及篩選AWS資源，以便於管理。 例如，如果貴組織使用多個Adobe相關資源，您可使用「Adobe」或「Experience-Platform」加以標籤。 這個額外的步驟可讓您在AWS Management Console中輕鬆搜尋及管理所有相關的資源。 選取&#x200B;**[!DNL Add tag]**&#x200B;以開始處理程式。

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

當您對設定感到滿意時，請選取&#x200B;**[!DNL Next]**&#x200B;以繼續工作流程。

![ Configure金鑰工作流程的第二步，並醒目提示別名、說明、標籤和下一步。](../../../images/governance-privacy-security/key-management-service/add-labels.png)

## 定義主要管理許可權 {#define-key-admins}

金鑰建立工作流程的步驟三隨即顯示。 為確保安全且受控制的存取權，您可以選擇哪些IAM使用者和角色可以管理金鑰。 此階段有兩個選項： [!DNL Key administrators]和[!DNL Key deletion]。 在&#x200B;**[!DNL Key administrators]**&#x200B;區段中，選取您要授與此金鑰的管理員許可權之任何使用者或角色名稱旁的一或多個核取方塊。

>[!NOTE]
>
>您無法在此工作流程階段建立管理員。

在&#x200B;**[!DNL Key deletion]**&#x200B;區段中，啟用核取方塊以允許金鑰管理員刪除此金鑰。 如果您未核取核取方塊，則不允許管理員使用者執行該操作。

選取&#x200B;**[!DNL Next]**&#x200B;以繼續工作流程。

![工作流程的[定義主要管理許可權]階段，核取方塊和下一個會反白顯示。](../../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## 授予關鍵使用者存取權 {#assign-key-users}

在工作流程的步驟四中，您可以[!DNL Define key usage permissions]。 從&#x200B;**[!DNL Key users]**&#x200B;清單中，選取您要擁有使用此金鑰之許可權的所有IAM使用者和角色的核取方塊。

從這個檢視中，您也可以[!DNL Add another AWS account]；不過，強烈建議不要新增其他AWS帳戶。 新增另一個帳戶可能會帶來風險，並使加密和解密操作的許可權管理複雜化。 藉由保留與單一AWS帳戶相關聯的金鑰，Adobe可確保與AWS KMS的安全整合，將風險降到最低並確保可靠的運作。

選取&#x200B;**[!DNL Next]**&#x200B;以繼續工作流程。

![工作流程的「定義金鑰使用許可權」階段，核取方塊和下一個反白顯示。](../../../images/governance-privacy-security/key-management-service/define-key-users.png)

## 檢閱金鑰組態 {#review}

關鍵組態的檢閱階段隨即顯示。 驗證[!DNL Key configuration]和[!DNL Alias and description]區段中的金鑰詳細資料。

>[!NOTE]
>
>確認主要區域與AWS帳戶相同。

![工作流程的[檢閱]階段，其中的[金鑰組態]和[別名]及說明區段會反白顯示。](../../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

選取&#x200B;**[!DNL Confirm]**&#x200B;以完成程式。 您會返回列出所有可用金鑰的KMS客戶自控金鑰工作區。

## 後續步驟

設定AWS KMS後，請使用[!UICONTROL 平台加密設定] UI或Adobe Experience Platform API繼續設定整合。 若要繼續設定客戶自控金鑰功能的一次性程式，請繼續[UI設定指南](./ui-set-up.md)。
