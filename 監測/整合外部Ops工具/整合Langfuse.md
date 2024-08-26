# 整合Langfuse
## 1 什麼是Langfuse
Langfuse 是一個開源的LLM 工程平台，可以幫助團隊協作調試、分析和迭代他們的應用程式。

Langfuse 官網介紹：[https://langfuse.com/](https://langfuse.com/)

## 2 如何配置Langfuse
1. 在[官網註冊](https://langfuse.com/)並登入Langfuse
2. 在Langfuse 內建立項目，登入後在主頁點擊New project，建立自己的項目，項目將用於與GenieAI 內的應用程式關聯進行資料監測。

![在Langfuse內建立項目](/監測/整合外部Ops工具/images/在Langfuse內建立項目.png)

為項目編輯一個名稱。

![編輯Langfuse項目名稱](/監測/整合外部Ops工具/images/編輯Langfuse項目名稱.png)

3. 建立專案API 憑證，在專案內左側邊欄點擊**Settings**開啟設置

![Langfuse_Dashboard](/監測/整合外部Ops工具/images/Langfuse_Dashboard.png)

在Settings 內點選**Create API Keys**建立一個專案API 憑證。

![Langfuse_Settings](/監測/整合外部Ops工具/images/Langfuse_Settings.png)

複製並保存**Secret Key，Public Key，Host**

![get_api_key](/監測/整合外部Ops工具/images/get_api_key.png)

4. 在GenieAI 內設定Langfuse，開啟需要監測的應用，在側邊選單開啟監測，在頁面中選擇設定。

![配置Langfuse](/監測/整合外部Ops工具/images/配置Langfuse.png)

成功儲存後可以在目前頁面查看到狀態，顯示已啟動即正在監測。

![查看配置狀態](/監測/整合外部Ops工具/images/查看配置狀態.png)

## 3 在Langfuse 內查看監測數據
配置完成後， GenieAI 內應用的調試或生產數據可以在Langfuse 查看監測數據。

![在Genie內調試應用](/監測/整合外部Ops工具/images/在Genie內調試應用.png)

![Langfuse_Traces](/監測/整合外部Ops工具/images/Langfuse_Traces.png)

![在Langfuse內查看應用程式數據](/監測/整合外部Ops工具/images/在Langfuse內查看應用程式數據.png)

## 4 監測資料清單

**工作流程/聊天流程追蹤訊息**

**用於追蹤workflow以及chatflow**

|**工作流程**|**LangFuse追蹤**|
||:---------|:---------------|
|workflow_app_log_id/workflow_run_id|ID|
|使用者會話 ID|使用者身分|
|工作流程_{id}|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|模型token消耗相關|用法|
|元數據|元數據|
|錯誤|等級|
|錯誤|狀態訊息|
|[工作流程]|標籤|
|conversation_id/workflow時無|會話ID|
|轉換id|父觀察 ID|

**工作流程追蹤訊息**

- workflow_id - Workflow的唯一標識
- conversation_id - 對話ID
- workflow_run_id - 這次運行的ID
- tenant_id - 租戶ID
- elapsed_time - 此次運行耗時
- status - 運作狀態
- version - Workflow版本
- total_tokens - 此次運行使用的token總數
- file_list - 處理的檔案列表
- triggered_from - 觸發此運行的來源
- workflow_run_inputs - 這次運行的輸入數據
- workflow_run_outputs - 這次運行的輸出數據
- error - 此次運行中發生的錯誤
- query - 運行時使用的查詢
- workflow_app_log_id - Workflow應用程式日誌ID
- message_id - 關聯的訊息ID
- start_time - 運行開始時間
- end_time - 運行結束時間
- workflow node executions - workflow節點運行信息
- 元數據
    - workflow_id - Workflow的唯一標識
    - conversation_id - 對話ID
    - workflow_run_id - 這次運行的ID
    - tenant_id - 租戶ID
    - elapsed_time - 此次運行耗時
    - status - 運作狀態
    - version - Workflow版本
    - total_tokens - 此次運行使用的token總數
    - file_list - 處理的檔案列表
    - triggered_from - 觸發來源

**Message Trace訊息**

**用於追蹤llm對話相關**

|**訊息**|**LangFuse 產生/跟踪**|
|:-------|:--------------------|
|訊息ID|ID|
|使用者會話 ID|使用者身分|
|訊息_{id}|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|模型token消耗相關|用法|
|元數據|元數據|
|錯誤|等級|
|錯誤|狀態訊息|
|[“訊息”，對話模式]|標籤|
|對話id|會話ID|
|轉換id|父觀察 ID|

**訊息追蹤訊息**

- message_id - 訊息ID
- message_data - 訊息數據
- user_session_id - 使用者的session_id
- conversation_model - 對話模式
- message_tokens - 訊息中的令牌數
- answer_tokens - 回答中的令牌數
- total_tokens - 訊息和回答中的總令牌數
- error - 錯誤訊息
- inputs - 輸入數據
- outputs - 輸出數據
- file_list - 處理的檔案列表
- start_time - 開始時間
- end_time - 結束時間
- message_file_data - 訊息關聯的文件數據
- conversation_mode - 對話模式
- 元數據
    - conversation_id - 訊息所屬對話的ID
    - ls_provider - 模型提供者
    - ls_model_name - 模型ID
    - status - 訊息狀態
    - from_end_user_id - 傳送使用者的ID
    - from_account_id - 發送帳號的ID
    - agent_based - 是否基於代理
    - workflow_run_id - 工作流程運行ID
    - from_source - 消息來源
    - message_id - 訊息ID

**Moderation Trace訊息**

**用於追蹤對話審查**

|**適度**|**LangFuse 產生/跟踪**|
|:-------|:--------------------|
|使用者身分|使用者身分|
|適度|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|元數據|元數據|
|[適度]|標籤|
|訊息ID|父觀察 ID|

**訊息追蹤訊息**

- message_id - 訊息ID
- user_id: 使用者id
- workflow_app_log_id 工作流程_app_log_id
- inputs - 審查的輸入數據
- message_data - 訊息數據
- flagged - 是否被標記為需要注意的內容
- action - 執行的具體行動
- preset_response - 預設回應
- start_time - 審查開始時間
- end_time - 審查結束時間
- 元數據
    - message_id - 訊息ID
    - action - 執行的具體行動
    - preset_response - 預設回應

**Suggested Question Trace訊息**

**用於追蹤建議問題**

|**建議問題**|**LangFuse 產生/跟踪**|
|:----------|:--------------------|
|使用者身分|使用者身分|
|建議問題|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|元數據|元數據|
|[建議問題]|標籤|
|訊息ID|父觀察 ID|

**訊息追蹤訊息**

- message_id - 訊息ID
- message_data - 訊息數據
- inputs - 輸入的內容
- outputs - 輸出的內容
- start_time - 開始時間
- end_time - 結束時間
- total_tokens - 令牌數量
- status - 訊息狀態
- error - 錯誤訊息
- from_account_id - 發送帳號的ID
- agent_based - 是否基於代理
- from_source - 消息來源
- model_provider - 模型提供者
- model_id - 模型ID
- suggested_question - 建議的問題
- level - 狀態級別
- status_message - 狀態訊息
- 元數據
    - message_id - 訊息ID
    - ls_provider - 模型提供者
    - ls_model_name - 模型ID
    - status - 訊息狀態
    - from_end_user_id - 傳送使用者的ID
    - from_account_id - 發送帳號的ID
    - workflow_run_id - 工作流程運行ID
    - from_source - 消息來源

**Dataset Retrieval Trace訊息**

**用於追蹤知識庫檢索**

|**資料集檢索**|**LangFuse 產生/跟蹤**|
|:------------|:--------------------|
|使用者身分|使用者身分|
|資料集檢索|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|元數據|元數據|
|[資料集檢索]|標籤|
|訊息ID|父觀察 ID|

**資料集檢索追蹤資訊**

- message_id - 訊息ID
- inputs - 輸入內容
- documents - 文件數據
- start_time - 開始時間
- end_time - 結束時間
- message_data - 訊息數據
- 元數據
    - message_id訊息ID
    - ls_provider模型提供者
    - ls_model_name模型ID
    - status訊息狀態
    - from_end_user_id發送使用者的ID
    - from_account_id發送帳號的ID
    - agent_based是否基於代理
    - workflow_run_id工作流程運行ID
    - from_source消息來源

**Tool Trace訊息**

**用於追蹤工具調用**

|**工具**|**LangFuse 產生/跟踪**|
|:-------|:--------------------|
|使用者身分|使用者身分|
|工具名稱|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|元數據|元數據|
|[“工具”，工具名稱]|標籤|
|訊息ID|父觀察 ID|

**工具追蹤訊息**

- message_id訊息ID
- tool_name工具名稱
- start_time開始時間
- end_time結束時間
- tool_inputs工具輸入
- tool_outputs工具輸出
- message_data訊息數據
- error錯誤訊息，如果存在
- inputs訊息的輸入內容
- outputs訊息的回答內容
- tool_config工具配置
- time_cost時間成本
- tool_parameters工具參數
- file_url關聯文件的URL
- 元數據
    - message_id訊息ID
    - tool_name工具名稱
    - tool_inputs工具輸入
    - tool_outputs工具輸出
    - tool_config工具配置
    - time_cost時間成本
    - error錯誤訊息
    - tool_parameters工具參數
    - message_file_id訊息檔案ID
    - created_by_role創建者角色
    - created_user_id創建者使用者ID

**Generate Name Trace訊息**

**用於追蹤會話標題生成**

|**產生名稱**|**LangFuse 產生/跟踪**|
|:-----------|:--------------------|
|使用者身分|使用者身分|
|產生名稱|姓名|
|開始時間|開始時間|
|結束時間|結束時間|
|輸入|輸入|
|輸出|輸出|
|元數據|元數據|
|[產生名稱]|標籤|

**產生名稱追蹤訊息**

- conversation_id對話ID
- inputs輸入數據
- outputs產生的會話名稱
- start_time開始時間
- end_time結束時間
- tenant_id租戶ID
- 元數據
    - conversation_id對話ID
    - tenant_id租戶ID