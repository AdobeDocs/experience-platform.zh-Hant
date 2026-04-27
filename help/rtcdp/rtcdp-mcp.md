---
solution: Real-Time Customer Data Platform
title: 使用MCP使用者端(Beta)
description: 瞭解如何使用MCP伺服器將Adobe Real-Time CDP連線至MCP使用者端
feature: Integrations
topic: Content Management, Artificial Intelligence
badge: label="Beta" type="Informative"
role: User, Developer
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 48dba0d2-7df9-4d76-bc87-5af49a8a40cc
source-git-commit: 8a9dd740bb210ef125bca65a8358bb6b51f6d28f
workflow-type: tm+mt
source-wordcount: '2379'
ht-degree: 0%

---

# 使用MCP使用者端(Beta) {#rtcdp-mcp}

您可以使用Adobe Real-Time CDP MCP整合，以純語言提示來查詢對象、目的地和啟動健康情況，而不需要撰寫API呼叫或導覽產品熒幕。 此頁面說明整合的運作方式、您可以執行哪些操作，以及如何開始使用。

>[!AVAILABILITY]
>
>Real-Time CDP MCP伺服器是以&#x200B;**遠端HTTP傳輸伺服器**&#x200B;的形式分佈，使用者可在支援的MCP使用者端和應用程式平台（例如Claude、ChatGPT、Claude Code、Codex、Cursor或VS Code）中進行安裝與設定。 驗證是透過&#x200B;**瀏覽器式登入流程**&#x200B;來處理 — 當您的使用者端首次連線到伺服器時，它會開啟您的預設瀏覽器，讓您可以使用您的Adobe憑證登入並授權存取。 請聯絡您的Adobe代表以存取此Beta方案。

## Beta、安全性和法律注意事項 {#mcp-notices}

**Beta檔案通知：**&#x200B;此檔案涵蓋Beta功能，不構成最終檔案。 此處描述的內容與Beta版本有關，且在正式發行前可能會有所變更。 Adobe不對本檔案的完整性或準確性發表任何宣告。

藉由使用Adobe Real-Time CDP MCP Server (Beta) (「Beta」)，您在此確認Beta係依&#x200B;**「原樣」提供，並無任何保固**。 Adobe沒有義務維護、更正、更新、變更、修改或以其他方式支援Beta。 建議您謹慎使用，切勿依賴這類Beta及/或隨附資料的正確運作或效能。 Beta視為Adobe的機密資訊。 任何「意見回饋」（有關Beta的資訊，包括但不限於您在使用Beta時遇到的問題或缺陷、建議、改進和建議）會在此指派給Adobe，包括所有權利、標題，以及對此等意見回饋的興趣。

>[!WARNING]
>
>模型內容通訊協定(MCP)是一種新興的開放原始碼標準，可能會帶來安全性或可靠性風險。 Adobe MCP伺服器整合和相關檔案係依「現況」提供，不提供任何形式的保證。
>
>將MCP使用者端或伺服器連線至Adobe產品是客戶選擇的設定。 客戶應負責評估任何MCP整合的安全性和適用性。 Adobe對於因設定錯誤、誤用MCP、協力廠商實作中的漏洞，或透過啟用MCP的工作流程執行的意外動作所引起的問題，概不負責。
>
>為了降低風險，Adobe鼓勵您在有效使用之前在沙箱環境中測試整合，並在確認或依賴之前，仔細檢閱及驗證所有MCP啟動的動作和回應。

## 什麼是模型內容通訊協定？ {#mcp-overview}

行銷、資料和客戶體驗團隊越來越仰賴聊天式應用程式和開發人員工具（例如Anthropic Claude、OpenAI ChatGPT、Cursor和Microsoft Copilot Studio）來簡化日常工作。 這些應用程式支援&#x200B;**模型內容通訊協定(MCP)**，這是開放標準，可讓應用程式以統一的方式將後端工具公開給大型語言模型(LLM)。

Real-Time CDP現在提供MCP伺服器，直接在任何MCP相容應用程式中顯示對象、目的地和啟用作業。 透過Real-Time CDP MCP整合，不同角色可以圍繞相同的細分和啟用資料共同作業，而不需要針對Adobe Experience Platform REST API編寫查詢或導覽多個UI畫面。 客戶可以用對話方式描述他們的意圖，讓LLM叫用適當的MCP工具。

## 主要功能 {#mcp-capabilities}

Real-Time CDP MCP伺服器可讓您直接從AI助理檢查、摘要和疑難排解對象和目標。 所有作業都是&#x200B;**唯讀** — MCP伺服器介面會擷取API作為純語言回答，因此您可以：

* **立即取得對象可見度** — 以簡單語言詢問對象定義、生命週期狀態和名稱空間，無需瀏覽功能表或手動提取報表。
* **在啟用前預估對象規模** — 在您承諾建立對象之前，先預覽PQL或SDD區段查詢的成員資格計數和信賴區間。
* **稽核您的啟用組合** — 檢閱已設定的目的地、提供這些目的地的資料流程，以及每個流程背後的來源/目標連線 — 而不需要剖析JSON或跨產品畫面跳轉。
* **提早啟動點問題** — 表面失敗或進行中的目的地會在您要求時執行，讓您的團隊可以快速採取行動。
* **圍繞即時資料共同作業** — 行銷人員、資料工程師和利害關係人可以透過其AI助理查詢相同的即時Real-Time CDP資料，更輕鬆地保持一致、決定和移動。

## 可用的工具 {#mcp-tools}

當我們啟用新工具時，工具可用性正在迅速改變。 請聯絡您的Adobe代表以取得最新可用工具的清單。

>[!NOTE]
>
>所有工具都是&#x200B;**唯讀**。 目前的Beta版本不支援寫入操作（建立、更新或刪除對象、目的地或資料流）。

## 使用案例 {#mcp-use-cases}

下列範例顯示如何使用自然語言與[!DNL Adobe Real-Time CDP] MCP伺服器互動：

| 目標 | 範例提示 |
| --- | --- |
| **目的地目錄探索** | 「TikTok可以當做我沙箱中的目的地嗎？」 /「我已設定哪些目的地型別的帳戶？」 |
| **目的地清查（依型別）** | 「列出我的所有Amazon S3目的地。」 / 「我是否設定了任何資料集匯出目的地？」 |
| **目的地組態稽核** | 「我的`Loyalty S3 Export`目的地要寫入哪個貯體？」 /「顯示資料流[ID]的目標路徑和檔案格式。」 |
| **帳戶健康狀況** | 「我的哪些目的地帳戶擁有過期的認證？」 / 「是否有任何Pinterest或Facebook帳戶處於錯誤狀態？」 |
| **啟用狀況 — 過去24小時** | 「列出過去24小時內執行失敗的每個目的地。」 / 「我的資料集匯出目的地在過去24小時內是否傳送任何資料？」 |
| **依據目的地的啟用歷程記錄** | 「在過去30天內，`Weekly Loyalty Export`是否匯出任何專案？」 /「顯示目的地{NAME}的完整執行記錄。」 |
| **失敗分析** | 「我本週檔案型目的地最常見的失敗原因為何？」 / 「依錯誤型別將最近失敗的回合分組。」 |
| **對象探索和篩選** | 「列出`marketing-prod`沙箱中每個以CSV為基礎的對象。」 / 「哪些對象已定義外部對象ID？」 |
| **對象規模調整稽核** | 「以0顯示每個對象。」 / 「哪些對象大於1,000個設定檔？」 |
| **對象到期稽核** | 「哪些目的地的對象結束日期已過？」 / 「列出排程在未來7天內到期的對象。」 |
| **對象啟用足跡** | 「哪些目的地有10個以上的對象已啟用？」 / 「哪一個對象已啟用至最多目的地？」 |
| **跨篩選器：對象×啟動** | 「顯示大小超過1,000且至少在2個目的地啟用的對象。」 /「僅對單一目的地啟用的大型對象。」 |
| **對象會籍預覽** | 「預覽對象`High-Value Loyalty Members`的成員人數大小。」 / 「在我儲存此PQL查詢之前，先估計其大小： {EXPRESSION}。」 |

## 先決條件 {#mcp-prerequisites}

在將Real-Time CDP MCP伺服器連線至您的MCP使用者端之前，請確定下列事項：

* 您擁有使用中的Real-Time CDP授權。
* 您可以存取可連線至遠端MCP伺服器或自訂MCP應用程式的支援使用者端，例如Claude、ChatGPT、Claude Code、Codex、Cursor或VS Code。
* 您有組織ID以及要查詢的沙箱名稱。
* 您在Adobe Experience Platform中擁有檢視對象、目的地和流程服務實體的必要許可權。

## 連線Real-Time CDP MCP伺服器 {#mcp-connect}

>[!NOTE]
>
>這項整合位於Beta中。 使用者端功能表、計畫需求和管理控制項可能會因應用程式和版本而異。

開始之前，請確定您具備下列條件：

* MCP伺服器端點URL： `Available to Beta customers through your Adobe representative`。
* 確認您的Adobe使用者有權存取目標Experience Platform組織和沙箱。

Real-Time CDP MCP伺服器是&#x200B;**遠端HTTP MCP伺服器**。 在每個使用者端中，設定遵循相同的模式：

1. 新增伺服器URL。
2. 儲存或啟用連線。
3. 在使用者端第一次叫用工具時完成&#x200B;**瀏覽器式Adobe登入**。
4. 提供每個請求的`imsOrgId`和`sandboxName`。

### 在UI型使用者端中安裝 {#mcp-connect-ui}

#### 克勞德

對於`claude.ai`和Claude Desktop，請使用Real-Time CDP代表提供的端點將Adobe MCP伺服器新增為&#x200B;**自訂聯結器**。 在個別的Claude計畫中，將其新增到&#x200B;**自訂>聯結器**&#x200B;下。 在Team和Enterprise計畫中，擁有者可能需要先在&#x200B;**組織設定> Connectors**&#x200B;底下新增它，之後每個使用者會使用他們自己的Claude設定連線它。 設定之後，請在交談中啟用聯結器，並在第一次使用時完成Adobe瀏覽器登入。

#### ChatGPT

在ChatGPT中，使用您的Real-Time CDP代表提供的端點，將Adobe MCP伺服器新增為&#x200B;**自訂應用程式/聯結器**。 根據您的ChatGPT計畫，這可能需要開發人員模式&#x200B;**和工作區管理員核准。**&#x200B;建立或啟用應用程式/聯結器後，從&#x200B;**設定>應用程式**&#x200B;或&#x200B;**設定>應用程式和聯結器**&#x200B;連線，然後在出現提示時透過Adobe瀏覽器登入進行驗證。

#### 游標

在「游標」中，使用Real-Time CDP代表提供的端點，將Adobe MCP伺服器新增為遠端MCP伺服器。 開啟&#x200B;**設定> MCP**、新增伺服器，並貼上端點URL。 新增之後，選取&#x200B;**連線**&#x200B;以透過瀏覽器驗證，啟用您工作區的伺服器。

#### 其他以UI為基礎的使用者端

對於具有遠端MCP支援的使用者端（例如VS Code或其他案頭和Web應用程式），請使用Real-Time CDP代表提供的端點，將Adobe MCP伺服器新增為&#x200B;**遠端HTTP**&#x200B;伺服器。 如果使用者端支援選用的標頭或持有人權杖，請將它們留空，除非Adobe另有指示；驗證會在第一次使用時透過瀏覽器型Adobe登入流程處理。

### 在技術使用者端安裝 {#mcp-connect-technical}

#### 克勞德程式碼

從終端機新增伺服器：

```bash
claude mcp add --transport http rtcdp <endpoint provided by your Adobe representative>
```

然後啟動Claude程式碼並執行：

```text
/mcp
```

選取`rtcdp`伺服器並在瀏覽器中完成Adobe登入流程。 如果您已在`claude.ai`中新增伺服器，當兩者使用相同帳戶時，伺服器也會自動出現在Claude程式碼中。

#### 法典

從終端機新增伺服器：

```bash
codex mcp add rtcdp --url <endpoint provided by your Adobe representative>
```

驗證伺服器：

```bash
codex mcp login rtcdp
```

驗證設定：

```bash
codex mcp list
```

您也可以直接將伺服器新增至`~/.codex/config.toml`：

```toml
[mcp_servers.rtcdp]
url = "<endpoint provided by your Adobe representative>"
```

### 必要的請求引數 {#mcp-connect-params}

每個工具呼叫都需要兩個引數來限定請求的範圍：

* `imsOrgId` — 您的組織ID，已對應至下游Experience Platform API呼叫上的`x-gw-ims-org-id`標題。
* `sandboxName` — Experience Platform沙箱名稱，已對應至`x-sandbox-name`標頭。

## 已知限制(Beta) {#mcp-limitations}

下列限制適用於[!DNL Adobe Real-Time CDP] MCP伺服器的目前Beta版本：

| 限制 | 說明 | 因應措施 |
| --- | --- | --- |
| **唯讀表面** | MCP伺服器只會公開擷取API。 您無法建立、更新、啟動或刪除對象、目的地或資料流。 | 使用Real-Time CDP UI或AEP REST API進行寫入操作。 |
| **沒有參與或傳遞量度** | MCP伺服器不會傳回目的地平台的下游傳遞統計資料、參與或轉換量度。 | 使用目的地平台自己的報告、Customer Journey Analytics MCP或Adobe Analytics MCP來取得參與和轉換資料。 |
| **區段查詢必須在外部撰寫** | `Preview Audience Membership`需要有效的PQL或SDD運算式作為輸入；MCP伺服器不會為您撰寫查詢。 | 在區段產生器UI中或透過分段服務API編寫PQL/SDD運算式，然後貼到MCP提示字元中。 |
| **透過接續權杖分頁** | 清單工具會傳回分頁結果。 非常大的沙箱中的完整列舉需要鏈結`continuationToken`呼叫。 | 使用篩選器（名稱、狀態、連線規格、時間範圍）來縮小查詢，而非列舉完整清單。 |
| **啟動回合篩選僅以時間為基礎** | `Inspect Activation Runs`支援依狀態和完成時間戳記（紀元毫秒UTC）篩選，但無法直接依錯誤型別或目的地平台篩選。 | 依`flowId`先篩選（從`List Configured Destinations`取得），將執行範圍設定到特定目的地。 |
| **需要地區設定** | 如果未針對您使用者的地區設定MCP閘道，則工具呼叫將失敗，並出現HTTP 403「使用者地區遺失」。 | 在首次使用之前，請聯絡您的Adobe代表，以確認已為您的地區設定閘道。 |

## 常見問題 {#mcp-faq}

+++支援哪些MCP使用者端？

Real-Time CDP MCP伺服器可搭配支援的使用者端運作，這些使用者端可連線到遠端MCP伺服器或自訂MCP應用程式，包括Claude、ChatGPT、Claude Code、Codex、Cursor和VS Code。 設定流程取決於使用者端：以UI為基礎的使用者端通常會從設定中新增伺服器，而技術使用者端（例如Claude Code和Codex）可以從命令列或設定檔案中新增伺服器。
+++

+++驗證如何運作？

驗證是透過&#x200B;**瀏覽器登入**&#x200B;處理。 您的MCP使用者端首次叫用工具時，會開啟預設瀏覽器至Adobe登入頁面。 在您驗證並授權使用者端後，工作階段就會建立，而後續的工具呼叫會重複使用它。 使用者端設定中不需要儲存API金鑰或長效認證。
+++

+++我可以透過MCP存取哪些Real-Time CDP物件？

您可以存取對象、目的地型別、設定的目的地帳戶、目的地資料流程、來源和目標連線，以及啟動執行記錄。 操作是唯讀的（擷取API）；目前版本不支援寫入操作。
+++

+++我需要開發人員存取權才能使用Real-Time CDP MCP伺服器嗎？

不會。 MCP伺服器是專為行銷和技術人員所設計。 行銷人員可以在任何支援的MCP使用者端中使用自然語言提示與其互動，而資料工程師和開發人員則可以在支援MCP的開發人員工具中使用它。
+++

+++我的資料是否傳送給MCP使用者端提供者？

當您提交提示時，MCP使用者端可能會將相關的內容（包括MCP伺服器傳回的Real-Time CDP資料）傳送至其模型以供處理。 在連線到生產資料之前，請檢閱MCP使用者端提供者的隱私權和資料處理原則。
+++

+++在Real-Time CDP中需要哪些許可權？

您要查詢的物件（對象、目的地和流程服務實體）至少需要&#x200B;**檢視**&#x200B;許可權。 不需要寫入許可權，因為MCP伺服器只會執行讀取作業。 如果您不確定目前的存取層級，請連絡您的[!DNL Adobe Experience Platform]系統管理員。
+++

+++我可以在沙箱環境中使用MCP伺服器嗎？

可以。 每個工具呼叫都需要`sandboxName`引數，因此MCP伺服器一律會遵從您的[!DNL Adobe Experience Platform]沙箱設定。 您可以在提示中指定沙箱的名稱，以查詢您有權存取的任何沙箱。
+++

+++預覽對象成員資格與搜尋現有對象之間有何差異？

`Search Existing Audiences`會傳回已編寫並儲存在沙箱中的對象。 `Preview Audience Membership`採用原始PQL或SDD區段運算式，並傳回其大小估計值 — 對於您儲存為對象的&#x200B;*之前的查詢*&#x200B;大小調整很有用。
+++

+++我可以查詢帳戶對象以及設定檔對象嗎？

是。 `Search Existing Audiences`和`Preview Audience Membership`都支援實體型別引數。 設定檔對象可以用PQL或SDD表示；帳戶對象一律使用SDD （關聯式）語法。
+++
