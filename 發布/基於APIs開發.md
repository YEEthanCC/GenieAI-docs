# 基於APIs 開發
GenieAI 基於「**後端即服務**」理念為所有應用提供了API，為AI 應用開發者帶來了許多便利。透過這個理念，開發者可以直接在前端應用中獲得大型語言模型的強大能力，而無需關注複雜的後端架構和部署過程。

**使用GenieAI API 的好處**
- 讓前端應用直接安全地呼叫LLM 能力，省去後端服務的開發過程
- 在可視化的介面中設計應用，並在所有客戶端中即時生效
- 對LLM 供應商的基礎能力進行了良好封裝
- 隨時切換LLM 供應商，並對LLM 的金鑰進行集中管理
- 在視覺化的介面中運作你的應用，例如分析日誌、標註及觀察用戶活躍
- 持續為應用程式提供更多工具能力、插件能力和資料集

**如何使用**

選擇一個應用程式，在應用程式（Apps）左側導覽中可以找到**存取API（API Access）**。在該頁面中你可以查看GenieAI 提供的API 文檔，並管理可存取API 的憑證。

例如你是顧問公司的開發部分，你可以基於公司的私有資料庫提供AI 能力給終端使用者或開發者，但開發者無法掌握你的資料和AI 邏輯設計，這使得服務可以安全、可持續的交付並滿足商業目的。

在最佳實踐中，API 金鑰應透過後端調用，而不是直接以明文暴露在前端程式碼或請求中，這可以防止你的應用程式被濫用或攻擊。

你可以為一個應用程式**建立多個存取憑證**，以實現交付給不同的使用者或開發者。這意味著API 的使用者雖然使用了應用程式開發者提供的AI 能力，但背後的Promp 工程、資料集和工具能力是經過封裝的。

**文字生成型應用**

可用於產生高品質文字的應用，例如產生文章、摘要、翻譯等，透過呼叫completion-messages 接口，發送使用者輸入得到產生文字結果。用於產生文字的模型參數和提示詞模版取決於開發者在GenieAI 提示詞編排頁的設定。

你可以在**應用程式-> 存取API**中找到該應用程式的API 文件與範例請求。

例如，建立文字補全資訊的API 的呼叫範例：

```
curl -X POST 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/completion-messages' \
--header 'Authorization: Bearer {api_key}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputs": {"query": "電子郵件"},
    "response_mode": "streaming",
    "user": "abc-123"
}'
```
**對話型應用**

可用於大部分場景的對話型應用，採用一問一答模式與使用者持續對話。要開始一個對話請呼叫chat-messages 接口，透過繼續傳入返回的conversation_id 可持續保持該會話。

你可以在應用程式-> 存取API中找到該應用程式的API 文件與範例請求。

例如，發送對話訊息的API的呼叫範例：

```
curl -X POST 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/chat-messages' \
--header 'Authorization: Bearer {api_key}' \
--header 'Content-Type: application/json' \
--data-raw '{
    "inputs": {},
    "query": "What are the specs of the iPhone 13 Pro Max?",
    "response_mode": "streaming",
    "conversation_id": "",
    "user": "abc-123",
    "files": [
      {
        "type": "image",
        "transfer_method": "remote_url",
        "url": "https://cloud.dify.ai/logo/logo-site.png"
      }
    ]
}'
```