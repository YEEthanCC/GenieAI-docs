# 透過API 維護知識庫
鑑權、呼叫方式與應用程式Service API 保持一致，不同的是一個資料集API token 可操作所有資料集

## 使用資料集API的優勢
- 將您的資料系統同步至GenieAI資料集，建立強大的工作流程。
- 提供資料集列表，文件列表及詳情查詢，方便建立您自己的資料管理頁面。
- 同時支援純文字和文件兩種上傳和更新文件的接口，並支援分段級的批次新增和修改，便捷您的同步方式。
- 減少文件手動處理同步的時間,提高您對GenieAI 的軟體和服務的可見度。

## 如何使用
進入資料集頁面，你可以在左側的導覽中切換至**API**頁面。在該頁面中你可以查看GenieAI 提供的資料集API 文檔，並且可以在API 金鑰中管理可存取資料集API 的憑證。

![Knowledge_API_Document](/知識庫/images/Knowledge_API_Document.png)

## API 呼叫範例

**建立空資料集**

僅用來建立空資料集

```
curl --location --request POST 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets' \
--header 'Authorization: Bearer {api_key}' \
--header 'Content-Type: application/json' \
--data-raw '{"name": "name"}'
```

**資料集列表**

```
curl --location --request GET 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets?page=1&limit=20' \
--header 'Authorization: Bearer {api_key}'
```

**透過文字建立文檔**

```
curl --location --request POST 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets/{dataset_id}/document/create_by_text' \
--header 'Authorization: Bearer {api_key}' \
--header 'Content-Type: application/json' \
--data-raw '{"name": "text","text": "text","indexing_technique": "high_quality","process_rule": {"mode": "automatic"}}'
```

**透過文件建立文檔**

```
curl --location --request POST 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets/{dataset_id}/document/create_by_file' \
--header 'Authorization: Bearer {api_key}' \
--form 'data="{"indexing_technique":"high_quality","process_rule":{"rules":{"pre_processing_rules":[{"id":"remove_extra_spaces","enabled":true},{"id":"remove_urls_emails","enabled":true}],"segmentation":{"separator":"###","max_tokens":500}},"mode":"custom"}}";type=text/plain' \
--form 'file=@"/path/to/file"'
```

**取得文件嵌入狀態（進度）**

```
curl --location --request GET 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets/{dataset_id}/documents/{batch}/indexing-status' \
--header 'Authorization: Bearer {api_key}'
```

**刪除文檔**

```
curl --location --request DELETE 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets/{dataset_id}/documents/{document_id}' \
--header 'Authorization: Bearer {api_key}'
```

**資料集文件列表**

```
curl --location --request GET 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets/{dataset_id}/documents' \
--header 'Authorization: Bearer {api_key}'
```

**新增分段**
```
curl --location --request POST 'https://api-chatbase-chatbase-ensaas.dev003.wise-paas.com/v1/datasets/{dataset_id}/documents/{document_id}/segments' \
--header 'Authorization: Bearer {api_key}' \
--header 'Content-Type: application/json' \
--data-raw '{"segments": [{"content": "1","answer": "1","keywords": ["a"]}]}'
```

## 錯誤訊息
- ```document_indexing```，文檔索引失敗
- ```provider_not_initialize```， Embedding 模型未配置
- ```not_found```，文檔不存在
- ```dataset_name_duplicate```，資料集名稱重複
- ```provider_quota_exceeded```，模型額度超過限制
- ```dataset_not_initialized```，資料集還未初始化
- ```unsupported_file_type```，不支援的文件類型
    - 目前只支援：txt, markdown, md, pdf, html, htm, xlsx, docx, csv
- ```too_many_files```，文件數量過多，暫時只支援單一文件上傳
- ```file_too_large```，文件太大，支援15M以下