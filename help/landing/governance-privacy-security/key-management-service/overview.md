---
title: 如何使用Amazon Web Services金鑰管理服務進行Adobe Experience Platform資料加密
description: 瞭解如何使用Amazon Web Services金鑰管理服務，為儲存在Adobe Experience Platform中的資料設定加密金鑰。
role: Developer, Admin, User
hide: true
hidefromtoc: true
source-git-commit: 7c37ce72eecbcbc9e49aa4135a21ef4649d9bfa5
workflow-type: tm+mt
source-wordcount: '2663'
ht-degree: 0%

---

# 如何使用Amazon Web Services金鑰管理服務進行Adobe Experience Platform資料加密

>[!AVAILABILITY]
>
>本檔案適用於在Amazon Web Services (AWS)上執行的Experience Platform實作。 在AWS上執行的Experience Platform目前可供有限數量的客戶使用。 若要深入瞭解支援的Experience Platform基礎結構，請參閱[Experience Platform多雲端總覽](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud)。
>
>AWS上的[客戶自控金鑰](../customer-managed-keys/overview.md) (CMK)支援Privacy and Security Shield，但不適用於Healthcare Shield。 Azure上的CMK同時支援Privacy和Security Shield以及Healthcare Shield。

使用本指南，透過Amazon Web Services (AWS)金鑰管理服務(KMS)建立、管理和控制Adobe Experience Platform的加密金鑰，來保護您的資料。 此整合可簡化法規遵循、透過自動化簡化作業，並免除維護您自己的關鍵管理基礎建設的必要性。

如需Customer Journey Analytics特定指示，請參閱[Customer Journey AnalyticsCMK檔案](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-privacy/cmk)

>[!IMPORTANT]
>
>Adobe Experience Platform預設會使用系統管理的金鑰加密靜態資料。 啟用客戶自控金鑰(CMK)後，您就可以完全控制資料安全性。 不過，此變更是不可逆的，一旦CMK啟用，您就無法回復到系統管理的金鑰。 您有責任安全地管理您的金鑰，以確保對資料的存取不會受到干擾，並防止可能無法存取。

本指南詳細說明在AWS KMS中建立和管理加密金鑰的程式，以保護Experience Platform中的資料。

## 先決條件 {#prerequisites}

在繼續閱讀本檔案之前，您應該充分瞭解下列重要概念和功能：

- **AWS金鑰管理服務(KMS)**：瞭解AWS KMS的基礎知識，包括如何建立、管理和輪換加密金鑰。 如需瞭解詳細資訊，請參閱[官方KMS檔案](https://docs.aws.amazon.com/kms/)。
- **AWS中的識別與存取管理(IAM)原則**： IAM是一項可讓您安全地管理AWS服務與資源存取的服務。 使用IAM可以：
   - 定義哪些使用者、群組和角色可以存取特定資源。
   - 指定允許或拒絕使用者執行的動作。
   - 使用IAM原則指派許可權，實作微調存取控制。
如需詳細資訊，請參閱[適用於AWS KMS的IAM原則](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html)。
- **Experience Platform中的資料安全性**：探索Platform如何確保資料安全性，以及如何與AWS KMS等外部服務整合以進行加密。 Platform使用HTTPS TLS v1.2保護資料以便傳輸、雲端提供者靜態加密、隔離儲存以及可自訂的驗證和加密選項。 如需如何確保資料安全的詳細資訊，請參閱[治理、隱私權及安全性總覽](../overview.md)，或Platform中[資料加密](../encryption.md)的檔案。
- **AWS Management Console**：中央樞紐，您可從一個Web應用程式存取及管理所有AWS服務。 使用搜尋列快速尋找工具、檢查通知、管理您的帳戶和帳單，以及自訂您的設定。 如需詳細資訊，請參閱[官方AWS管理主控台檔案](https://docs.aws.amazon.com/awsconsolehelpdocs/latest/gsg/what-is.html)。

## 快速入門 {#get-started}

本指南要求您已擁有Amazon Web Services帳戶的存取權和管理主控台的存取權。 請依照下列步驟開始：

1. **驗證許可權**：確定您擁有必要的AWS Identity and Access Management (IAM)許可權，才能在KMS中建立、管理及使用加密金鑰。 若要驗證您的許可權：
   1. 存取[IAM原則模擬器](https://policysim.aws.amazon.com/)。
   1. 選取您的使用者帳戶或角色。
   1. 模擬KMS動作，例如`kms:CreateKey`或`kms:Encrypt`。
如果模擬傳回錯誤或您不確定自己的許可權，請洽詢AWS管理員以取得協助。

1. **檢查您的AWS帳戶設定**：確認您的AWS帳戶已啟用使用AWS KMS服務。 大部分的帳戶預設已啟用KMS存取，但您可以造訪[AWS管理主控台](https://aws.amazon.com/console/)來檢閱您的帳戶設定。 如需詳細資訊，請參閱[AWS Key Management Service開發人員指南](https://docs.aws.amazon.com/kms/latest/developerguide/overview.html)。

1. **選取支援的地區**：AWS KMS可在特定地區使用。 請確定您在支援KMS的區域中作業。 您可以在[AWS KMS端點與配額清單](https://aws.amazon.com/about-aws/global-infrastructure/regional-product-services/)中檢視支援地區的完整清單。

### 導覽至AWS KMS以開始金鑰設定

>[!IMPORTANT]
>
>確保加密金鑰的安全儲存、存取及可用性。 您有責任管理金鑰並防止平台作業中斷。

若要開始設定和管理您的加密金鑰，請登入您的AWS帳戶並導覽至AWS金鑰管理服務(KMS)。 從AWS管理主控台，從服務功能表選取&#x200B;**金鑰管理服務(KMS)**。

![反白顯示金鑰管理服務之AWS Management Console的搜尋下拉式功能表。](../../images/governance-privacy-security/key-management-service/navigate-to-kms.png)

## 建立新金鑰 {#create-a-key}

[!DNL Key Management Service (KMS)]工作區會出現。 選擇「**[!DNL Create a key]**」。

![含有[建立金鑰]的金鑰管理服務工作區反白顯示。](../../images/governance-privacy-security/key-management-service/create-a-key.png)

## 設定金鑰設定 {#configure-key}

[!DNL Configure Key]工作流程隨即顯示。 依預設，金鑰型別設為&#x200B;**[!DNL Symmetric]**，而金鑰使用方式設為&#x200B;**[!DNL Encrypt and Decrypt]**。 在繼續之前，請確定已選取這些選項。

![使用[對稱]和[加密與解密]基本選項來設定[金鑰]工作流程的第一步。](../../images/governance-privacy-security/key-management-service/configure-key-basic-options.png)

展開&#x200B;**[!DNL Advanced options]**&#x200B;下拉式功能表。 建議您使用&#x200B;**[!DNL KMS]**&#x200B;選項，此選項可讓AWS建立和管理金鑰資料。 預設會選取&#x200B;**[!DNL KMS]**&#x200B;選項。

>[!NOTE]
>
>如果您已有金鑰，可以匯入外部金鑰資料或使用AWS [!DNL CloudHSM]金鑰存放區。 本檔案未涵蓋這些選項。

接著，選取[!DNL Regionality]設定，以指定金鑰的區域範圍。 選取&#x200B;**[!DNL Single-Region key]**，接著選取&#x200B;**[!DNL Next]**&#x200B;以繼續執行步驟二。

>[!IMPORTANT]
>
>AWS會強制對KMS金鑰施加地區限制。 此區域限制表示金鑰必須位於與您的Adobe帳戶相同的區域。 Adobe只能存取位於您帳戶地區內的KMS金鑰。 確定您選取的區域符合您Adobe單一租使用者帳戶的地區。

![在AWS地區、KMS和單一地區金鑰進階選項強調顯示的設定金鑰工作流程的第一步。](../../images/governance-privacy-security/key-management-service/configure-key-advanced-options.png)

## 標籤並標籤您的金鑰 {#add-labels-and-tags-to-key}

工作流程的第二個[!DNL Add labels]階段隨即顯示。 您可在此設定[!DNL Alias]和[!DNL Tags]欄位，協助您從AWS KMS主控台管理並尋找您的加密金鑰。

在&#x200B;**[!DNL Alias]**&#x200B;輸入欄位中輸入索引鍵的描述性標籤。 別名可做為使用者易記的識別碼，使用AWS KMS主控台中的搜尋列快速找到金鑰。 為避免混淆，請選擇可反映金鑰用途的有意義名稱，例如「Adobe平台金鑰」或「客戶加密金鑰」。 如果金鑰別名不足以說明其用途，您也可以包含金鑰的說明。

最後，透過在[!DNL Tags]區段中新增索引鍵/值組，將中繼資料指派給您的索引鍵。 此步驟為選用，但您應新增標籤以分類及篩選AWS資源，以便於管理。 例如，如果貴組織使用多個Adobe相關資源，您可使用「Adobe」或「Experience-Platform」加以標籤。 這個額外的步驟可讓您在AWS Management Console中輕鬆搜尋及管理所有相關的資源。 選取&#x200B;**[!DNL Add tag]**&#x200B;以開始處理程式。

<!-- I do not have an AWS account with which to document the Add tag process as yet. -->

當您對設定感到滿意時，請選取&#x200B;**[!DNL Next]**&#x200B;以繼續工作流程。

![ Configure金鑰工作流程的第二步，並醒目提示別名、說明、標籤和下一步。](../../images/governance-privacy-security/key-management-service/add-labels.png)

## 定義主要管理許可權 {#define-key-admins}

金鑰建立工作流程的步驟三隨即顯示。 為確保安全且受控制的存取權，您可以選擇哪些IAM使用者和角色可以管理金鑰。 此階段有兩個選項： [!DNL Key administrators]和[!DNL Key deletion]。 在&#x200B;**[!DNL Key administrators]**&#x200B;區段中，選取您要授與此金鑰的管理員許可權之任何使用者或角色名稱旁的一或多個核取方塊。

>[!NOTE]
>
>您無法在此工作流程階段建立管理員。

在&#x200B;**[!DNL Key deletion]**&#x200B;區段中，啟用核取方塊以允許金鑰管理員刪除此金鑰。 如果您未核取核取方塊，則不允許管理員使用者執行該操作。

選取&#x200B;**[!DNL Next]**&#x200B;以繼續工作流程。

![工作流程的[定義主要管理許可權]階段，核取方塊和下一個會反白顯示。](../../images/governance-privacy-security/key-management-service/define-key-admins.png)

## 授予關鍵使用者存取權 {#assign-key-users}

在工作流程的步驟四中，您可以[!DNL Define key usage permissions]。 從&#x200B;**[!DNL Key users]**&#x200B;清單中，選取您要擁有使用此金鑰之許可權的所有IAM使用者和角色的核取方塊。

從這個檢視中，您也可以[!DNL Add another AWS account]；不過，強烈建議不要新增其他AWS帳戶。 新增另一個帳戶可能會帶來風險，並使加密和解密操作的許可權管理複雜化。 透過將金鑰與單一AWS帳戶相關聯，Adobe可確保與AWS KMS的安全整合，將風險降至最低，並確保可靠的運作。

選取&#x200B;**[!DNL Next]**&#x200B;以繼續工作流程。

![工作流程的「定義金鑰使用許可權」階段，核取方塊和下一個反白顯示。](../../images/governance-privacy-security/key-management-service/define-key-users.png)

## 檢閱金鑰組態 {#review}

關鍵組態的檢閱階段隨即顯示。 驗證[!DNL Key configuration]和[!DNL Alias and description]區段中的金鑰詳細資料。

>[!NOTE]
>
>確認主要區域與AWS帳戶相同。

![工作流程的[檢閱]階段，其中的[金鑰組態]和[別名]及說明區段會反白顯示。](../../images/governance-privacy-security/key-management-service/review-key-configuration-details.png)

### 更新金鑰原則以將金鑰與Experience Platform整合

接下來，編輯「**[!DNL Key Policy]**」區段中的JSON，將金鑰與Experience Platform整合。 預設金鑰原則看起來類似於以下JSON。

<!-- The AWS ID below is fake. Q) Can I refer to it simply as AWS_ACCOUNT_ID ? Is that suitable? -->

```JSON
{
  "Id": "key-consolepolicy-3",
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Enable IAM User Permissions",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::123464903283:root" // this is a mock AWS Principal ID, your ID will differ
      },
      "Action": "kms:*",
      "Resource": "*"
    }
  ]
}
```

在上述範例中，相同帳戶(`Principal.AWS`)中的所有資源(`"Resource": "*"`)都可以存取此金鑰。 此原則允許相同帳戶中的其他服務使用金鑰進行加密和解密。 服務僅具有此帳戶的許可權。

接下來，將新陳述式新增至此原則，將存取權授予您的Platform單一租使用者帳戶。 您可以從Platform UI取得JSON原則，並將其套用至您的AWS KMS金鑰，以安全地將其連結至平台。

導覽至Platform UI。 在左側導覽邊欄的&#x200B;**[!UICONTROL 管理]**&#x200B;區段中，選取&#x200B;**[!UICONTROL 加密]**。 [!UICONTROL 加密組態]工作區出現。 然後選取[!UICONTROL 客戶自控金鑰]卡片中的&#x200B;**[!UICONTROL 設定]**。

![具有設定的Platform Encryption Configuration Workspace在[客戶管理的金鑰]卡中反白顯示。](../../images/governance-privacy-security/key-management-service/encryption-configuration.png)

[!UICONTROL Customer Managed Keys組態]出現。 選取復製圖示(![復製圖示。](../../../images/icons/copy.png))將CMK KMS原則複製到剪貼簿。 綠色快顯通知會確認已複製原則。

![顯示CMK KMS原則且復本圖示醒目提示的客戶受管理金鑰組態。](../../images/governance-privacy-security/key-management-service/copy-cmk-policy.png)

<!-- This part of the workflow was in contention at the time of the demo.  -->

接著，返回AWS KMS工作區並更新下方顯示的金鑰原則。

![工作流程的稽核階段，其中已更新原則及完成已反白顯示。](../../images/governance-privacy-security/key-management-service/updated-cmk-policy.png)

從[!UICONTROL 平台加密組態]工作區新增四個陳述式，如下所示： `Enable IAM User Permissions`、`CJA Flow IAM User Permissions`、`CJA Integrity IAM User Permissions`、`CJA Oberon IAM User Permissions`。

```json
{
    "Version": "2012-10-17",
    "Id": "key-consolepolicy",
    "Statement": [
        {
            "Sid": "Enable IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::975049898882:root" // this is a mock AWS Principal ID, your ID will differ
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "975049898882" // this is a mock AWS Principal ID, your ID will differ
                }
            }
        },
        {
            "Sid": "CJA Flow IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::767397686373:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "767397686373"
                }
            }
        },
        {
            "Sid": "CJA Integrity IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::730335345392:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "730335345392"
                }
            }
        },
        {
            "Sid": "CJA Oberon IAM User Permissions",
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::891377157113:root"
            },
            "Action": [
                "kms:Decrypt",
                "kms:Encrypt",
                "kms:ReEncrypt*",
                "kms:GenerateDataKey*",
                "kms:DescribeKey",
                "kms:CreateGrant"
            ],
            "Resource": "*",
            "Condition": {
                "StringEquals": {
                    "aws:PrincipalAccount": "891377157113"
                }
            }
        }
    ]
}
```



選取&#x200B;**[!DNL Finish]**&#x200B;以使用您更新的原則確認您的金鑰詳細資料並建立金鑰。 金鑰和原則現在已設定總共5個陳述式，以允許您的AWS帳戶與您的Experience Platform帳戶通訊。 效果是即時的。

AWS [!DNL Key Management Service]的已更新[!DNL Customer managed keys]工作區隨即顯示。

### 將AWS加密金鑰詳細資料新增至平台

接下來，若要啟用加密，請將金鑰的Amazon資源名稱(ARN)新增至您的平台[!UICONTROL 客戶自控金鑰組態]。 在AWS的[!DNL Customer Managed Keys]區段中，從[!DNL Key Management Service]的清單中選取新金鑰的別名。

![反白顯示新金鑰別名的AWS KMS客戶自控金鑰工作區。](../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

您的金鑰的詳細資訊隨即顯示。 AWS中的所有專案都有Amazon資源名稱(ARN)，其中
是用於跨AWS服務指定資源的唯一識別碼。 它遵循標準化格式： `arn:partition:service:region:account-id:resource`。

選取復製圖示以複製您的ARN。 確認對話方塊隨即顯示。

![醒目提示ARN的AWS KMS客戶管理金鑰的金鑰詳細資料。](../../images/governance-privacy-security/key-management-service/keys-details-arn.png)

現在，導覽回平台[!UICONTROL 客戶自控金鑰組態] UI。 在&#x200B;**[!UICONTROL 新增AWS加密金鑰詳細資料]**&#x200B;區段中，新增您從AWS UI複製的&#x200B;**[!UICONTROL 設定名稱]**&#x200B;和&#x200B;**[!UICONTROL KMS金鑰ARN]**。

![新增AWS加密金鑰詳細資訊區段中反白顯示具有設定名稱和KMS金鑰ARN的平台加密設定工作區。](../../images/governance-privacy-security/key-management-service/add-encryption-key-details.png)

接著，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以提交組態名稱、KMS金鑰ARN，並開始驗證金鑰。

![已反白儲存的平台加密設定工作區。](../../images/governance-privacy-security/key-management-service/save.png)

您返回[!UICONTROL 加密設定]工作區。 加密組態的狀態會顯示在&#x200B;**[!UICONTROL 客戶受管理的金鑰]**&#x200B;卡片底部。

![在客戶自控金鑰卡上反白顯示處理功能的平台UI中的加密設定工作區。](../../images/governance-privacy-security/key-management-service/configuration-status.png)

在驗證金鑰後，金鑰儲存庫識別碼將新增到所有沙箱的Data Lake和設定檔資料存放區。

>[!NOTE]
>
>流程的持續時間取決於您的資料大小。 一般而言，程式會在24小時內完成。 每個沙箱通常會在2到3分鐘內更新。

## 金鑰撤銷 {#key-revocation}

>[!IMPORTANT]
>
>在撤銷任何存取權之前，請先瞭解金鑰撤銷對下游應用程式的影響。

以下是金鑰撤銷的主要考量事項：

- 撤銷或停用金鑰將會使您的Platform資料無法存取。 此動作不可逆，應謹慎執行。
- 在撤銷加密金鑰存取權時，請考慮傳輸時間表。 主要資料存放區在幾分鐘到24小時內變得無法存取。 快取或暫時性資料存放區在7天內無法存取。

若要撤銷金鑰，請導覽至AWS KMS工作區。 **[!DNL Customer managed keys]**&#x200B;區段會顯示您AWS帳戶的所有可用金鑰。 從清單中選取金鑰的別名。

![反白顯示新金鑰別名的AWS KMS客戶自控金鑰工作區。](../../images/governance-privacy-security/key-management-service/customer-managed-keys-on-aws.png)

您的金鑰的詳細資訊隨即顯示。 若要停用金鑰，請選取&#x200B;**[!DNL Key actions]**，然後從下拉式功能表中選取&#x200B;**[!DNL Disable]**。

![AWS KMS UI中AWS金鑰的詳細資料，其中的「金鑰動作」和「停用」會反白顯示。](../../images/governance-privacy-security/key-management-service/disable-key.png)

確認對話方塊隨即顯示。 選取&#x200B;**[!DNL Disable key]**&#x200B;以確認您的選擇。 大約五分鐘內，Platform應用程式和UI應會反映停用金鑰的影響。

>[!NOTE]
>
>停用金鑰後，您可以視需要使用上述相同方法再次啟用金鑰。 此選項可從&#x200B;**[!DNL Key actions]**&#x200B;下拉式清單中取得。

![反白顯示[停用金鑰]的[停用金鑰]對話方塊。](../../images/governance-privacy-security/key-management-service/disable-key-dialog.png)

或者，如果您的金鑰用於其他服務，您可以直接從金鑰原則中移除Experience Platform的存取權。 在&#x200B;**[!DNL Key Policy]**&#x200B;區段中選取&#x200B;**[!UICONTROL 編輯]**。

![在[金鑰原則]區段中反白顯示[編輯的AWS金鑰的詳細資訊區段。](../../images/governance-privacy-security/key-management-service/edit-key-policy.png)

**[!DNL Edit key policy]**&#x200B;頁面隨即顯示。 反白標示並刪除從平台UI複製的原則宣告，以移除客戶自控金鑰應用程式的許可權。 然後，選取&#x200B;**[!DNL Save changes]**&#x200B;以完成程式。

![AWS上的Edit key policy workspace以陳述式JSON物件和Save變更強調顯示。](../../images/governance-privacy-security/key-management-service/delete-statement-and-save-changes.png)

## 金鑰輪換 {#key-rotation}

AWS提供自動和隨選金鑰輪換。 為了降低金鑰洩露的風險或符合安全性法規要求，您可以視需要或定期自動產生新的加密金鑰。 排程自動金鑰輪換以限制金鑰的使用壽命，並確保如果金鑰受損，輪換後將無法使用。 雖然現代加密演演算法高度安全，但金鑰輪換是一項重要的安全性合規措施，並表明遵循安全性最佳實務。

### 自動金鑰輪換 {#automatic-key-rotation}

自動金鑰輪換預設為停用。 若要從KMS工作區排程自動金鑰輪換，請選取&#x200B;**[!DNL Key rotation]**&#x200B;索引標籤，然後在&#x200B;**[!DNL Automatic key rotation section]**&#x200B;中選取&#x200B;**[!DNL Edit]**。

![AWS金鑰的詳細資訊區段（金鑰輪換與編輯已反白顯示）。](../../images/governance-privacy-security/key-management-service/key-rotation.png)

**[!DNL Edit automatic key rotation]**&#x200B;工作區會出現。 從這裡，選取選項按鈕以啟用或停用自動金鑰輪換。 然後使用文字輸入欄位或下拉式功能表，選擇按鍵旋轉的時間段。 選取&#x200B;**[!DNL Save]**&#x200B;以確認您的設定並返回金鑰詳細資料工作區。

>[!NOTE]
>
>金鑰輪換的最小週期為90天，最大週期為2560天。

![編輯自動金鑰輪換工作區，並反白顯示輪換期間和儲存。](../../images/governance-privacy-security/key-management-service/automatic-key-rotation.png)

### 隨選金鑰輪換 {#on-demand-key-rotation}

如果目前的金鑰遭到破壞，請選取&#x200B;**[!DNL Rotate Now]**&#x200B;立即輪換金鑰。 AWS僅允許10次隨選輪換。 使用排定的金鑰輪換，除非安全性已受損。

![現在輪換的AWS金鑰的詳細資訊區段會反白顯示。](../../images/governance-privacy-security/key-management-service/on-demand-key-rotation.png)

## 後續步驟

閱讀本檔案後，您已瞭解如何在AWS KMS中建立、設定和管理加密金鑰，以與Adobe Experience Platform搭配使用。 接下來，請考慮檢閱組織的安全性及法規遵循政策，以確保適當的金鑰管理實務，例如排程的金鑰輪換及安全的金鑰儲存。
