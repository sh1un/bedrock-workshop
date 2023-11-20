# Bedrock 服務介紹
## 簡介
在接下來的段落，我們將為您著重介紹 Bedrcok，並展示一個「文檔生圖 API」，但由於 Bedrock 屬於比較新的服務 (2023/04 GA)，且現在也沒有 Free tier，因此在使用上務必要詳加了解該服務是如何計費的

> 因為 Bedrock 是比較新的服務，要使用 Bedrock 建議 Region 選擇 us-east-1 (N. Virginia)，享受最新的功能！

## Bedrock 是什麼?
![aws-bedrock](https://github.com/sh1un/bedrock-workshop/assets/85695943/7443c1af-6f44-4edc-8b94-7366e1b4a361)

### Amazon Bedrock 是一個全受管的服務，旨在簡化生成式人工智能（AI）應用程式的建立和擴充過程。以下是 Bedrock 的主要特點：

- 領先的基礎模型選項：Amazon Bedrock 提供多種高效能的基礎模型（FM），來自 AI21 Labs、Anthropic、Cohere、Meta、Stability AI 和 Amazon 等領先 AI 公司。這些模型可以透過單一 API 進行推論，並在最少的程式碼變更下獲得最新模型版本​​。

- 使用者數據自訂模型：使用者可以透過視覺化界面，利用自己的數據私有自訂這些模型。這涉及選取儲存在 Amazon S3 中的訓練和驗證數據集，並調整超參數以最佳化模型效能​​。
> 注意！截至 2023/11/20 資訊，目前只有 Titan 模型可以 Fine Tuning

- 全受管代理程式：Bedrock 使開發者能夠創建可執行複雜業務任務的代理程式，例如預訂差旅、處理保險索賠、建立廣告宣傳活動等。這些代理程式透過動態呼叫公司系統和 API 來擴展 FM 的推理功能​​。

- 原生支援 RAG：Bedrock 支援擷取擴增產生（RAG）技術，允許將 FM 連接到資料來源，以擴展其功能，從而使模型更深入了解特定的領域和組織​​。
> 可以想像成一位廚師在準備一道特別的菜餚。這位廚師（代表基礎模型）擁有廣泛的烹飪知識和技巧，但當他需要準備一道特定國家的特色菜時，他會參考那個國家的食譜（這裡的食譜代表連接到的數據源）。通過查閱這些特定的食譜，廚師不僅能夠利用他原本的廣泛烹飪知識，還能加入特定文化的獨特風味和技巧，從而創造出更符合該文化特色的菜餚。這就像是 Bedrock 利用 RAG 技術將基礎模型與特定的數據源相連接，使得模型能夠更深入地理解和應對特定領域或組織的需求。

- 資料安全與合規認證：Bedrock 提供多種功能以支援安全和隱私要求，並達到 HIPAA 資格和 GDPR 合規性。所有數據在傳輸和靜態期間均被加密，並且不會與第三方模型供應商共享​​。

- 簡化開發流程：Bedrock 是無伺服器的，因此開發者不需要管理任何基礎設施。它還可以使用熟悉的 AWS 服務，安全地整合並部署生成式 AI 功能到應用程式中​​。
> 重要！！後續的我將要展示的應用是完全 Serverless(無伺服器)，所有應用都在 AWS 雲上打造好，透過這個優勢，我省去了很多配置底層基礎建設的煩惱，要構建出一個能運作得應用真的相當快速

總之，Amazon Bedrock 提供了一個全面的解決方案，以簡化生成式 AI 應用程式的開發，同時確保資料的安全和合規性。

### Use cases
- 虛擬助理
- 智能客服
- 文字歸納與摘要
- 搜索
- 圖片生成
- 真的非常非常多種應用…



## 相關時事 - 2023 Summit Taiwan([連結](https://www.inside.com.tw/article/32357-AWSSummit2023_GenAIMusic))

![image](https://github.com/sh1un/bedrock-workshop/assets/85695943/8711ceec-6719-4231-b589-2bb9ebc237e7)

> Amazon Bedrock 提供的資源可用於多種應用，包括創作社交媒體貼文、網頁副本、開發聊天機器人和虛擬助理，以及在大型資料集中進行搜索和問題解答。




## 畫面
![BedrockScreeshot-1](https://github.com/sh1un/bedrock-workshop/assets/85695943/8625ff25-66e6-4701-b690-5c6e2d05f4d5)


## Model Providers
目前總共有 6 間公司提供基礎模型(FM)，但本工作坊在後面的應用只有用到 Claude, Stable Diffusion，因此只會著重介紹此兩個 FMs 
| 公司名稱     | AI 模型名稱      |
|------------|----------------|
| AI21 Labs  | Jurassic-2 series |
| Anthropic  | Claude         |
| Cohere     | Command        |
| Meta       | Llama 2        |
| Stability AI | Stable Diffusion |
| Amazon     | Titan          |


## Anthropic 公司介紹 
![apple-icon](https://github.com/sh1un/bedrock-workshop/assets/85695943/d27513ee-c8b1-4817-a8f6-15d3be1cd0af)

- Anthropic是一家總部位於美國的AI研發公司，於2021年1月創立。
- 創辦人是前 OpenAI 員工
- 主要產品就是「聊天機器人 Claude」([Claude 連結](https://claude.ai/login?returnTo=%2F))
- Claude 是目前公認 ChatGPT 的最大競爭對手


## Stability AI 公司介紹
![stabilityAI](https://github.com/sh1un/bedrock-workshop/assets/85695943/5964aa1e-87b6-4803-9b9c-b1d50560ef5a)

- Stability 是一家專注於 AI 研發公司，於2021年創立。
- 主要產品就是「Stable Diffusion」([Stable Diffusion 連結](https://stablediffusionweb.com/))
- 近期推出了 AI 音樂生成工具「Stable Audio」([連結](https://www.stableaudio.com/))
> 大家可以去玩看看 Stable Audio! 現在 AWS 上還沒有 Stable Audio 的 FM，筆者期待未來有機會能在 AWS Bedrock 上使用到 Stable Audio!


## Bedrock vs. Claude (or Others)
這邊主要是想比較，我今天身為一名開發者，在 AWS 上透過 Bedrock 使用 Claude 與直接從 Claude 獲取 API 之間的差異。
先講結論：**一般的獨立開發者我建議您直接去看看其他供應商是否有提供 API！然後使用該供應商提供的 API 即可**
| 特點             | Bedrock                                        | Claude (or Others)                    |
|----------------|------------------------------------------------|--------------------------------------|
| 目標用戶群        | 企業級用戶、開發者                                 | 一般消費級個人用戶                          |
| 平台性質         | 完整的 AI 開發和運行平台                               | 側重於娛樂、交流、資訊獲取的聊天機器人           |
| 服務整合         | 整合 AWS 各項服務，提供豐富的客製化彈性                     | 提供基本功能，缺乏進階客製化選項                    |
| 主要應用         | 適用於專業開發和商業應用                             | 主要用於個人用途，如娛樂和資訊交流                 |

## Pricing
### What is token?
![ClaudeV2MaxToken](https://github.com/sh1un/bedrock-workshop/assets/85695943/c658de1e-a3b7-4cff-99ec-4edaf9bfe87d)

**用來處理和理解自然語言的基本單位。** 
也就是說輸入的文字會先被轉換為 tokens 再進行分析，讓系統更好地理解並回應輸入
每個字耗費的平均 token數
    - 繁體中文 2.03	
    - 英文 1.25
 > 推薦大家可以去 OpenAI tokenizer([連結](https://platform.openai.com/tokenizer)) 感覺一下

> Claude V2 Max 100k tokens 差不多就是 40,000 ~ 60,000 個繁體中文字

## Demo
### 文檔生圖
本工作坊所展示的應用，會將一個 pdf 檔上傳，透過 Textract 解析文字作為 promt 傳送給 Claude，Claude 會歸納重點產生合適的 prompt，再將 Claude 產生的 prompt 傳給 Stable Diffusion 產生出圖片

![BedrockDemo3](https://github.com/sh1un/bedrock-workshop/assets/85695943/075ae312-1f86-4f14-959f-50007b02a43f)


## Tools
![image](https://github.com/sh1un/bedrock-workshop/assets/85695943/83d0072c-58fd-464e-8d67-a1eabb701538)

## Architechture
![image](https://github.com/sh1un/bedrock-workshop/assets/85695943/6b7d710a-ed7f-4e07-82be-28f62fd3ca5f)

> 本工作坊為了簡化教學，在架構方面才把所有業務邏輯集中在單一 Lambda Function，建議可以將其各功能獨立在不同的 Lambda Function 或是將共用邏輯拆出來放在 Lambda Layer 內會更好喔

## 其他資源
AWS Partyrock: https://partyrock.aws/
