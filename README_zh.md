## 精通 AI 智能體工程 - 構建自主 AI 智能體

### 6 週旅程：使用 OpenAI Agents SDK、CrewAI、LangGraph、AutoGen 和 MCP 編碼和部署 AI 智能體

![自主智能體](assets/autonomy.png)

_如果您在 Cursor 中查看此文件，請右鍵點擊左側資源管理器中的文件名，然後選擇「打開預覽」，以查看格式化版本。_

非常興奮歡迎您的到來！這是您進入強大、驚人且常常超現實的智能體 AI 世界的 6 週冒險之旅的開始。

### 開始之前

我在這裡幫助您取得最大的成功！如果需要幫助，請隨時通過平台或直接發郵件（ed@edwarddonner.com）與我聯繫。在 LinkedIn 上與人們聯繫以建立社群總是很棒的 - 您可以在這裡找到我：  
https://www.linkedin.com/in/eddonner/  
這對我來說是新的嘗試，但我也在試用 X/Twitter [@edwarddonner](https://x.com/edwarddonner) - 如果您在 X 上，請教我如何使用 😂  

### 不那麼可怕的設置說明

也許是最後的話：但我真的希望我整理的環境設置不會太可怕！

- Windows 用戶，您的說明在[這裡](setup/SETUP-PC.md)
- Mac 用戶，您的說明在[這裡](setup/SETUP-mac.md)
- Linux 用戶，您的說明在[這裡](setup/SETUP-linux.md)

如有任何問題，請聯繫我。

### CrewAI 週（第 3 週）的重要說明

Windows PC 用戶：您需要檢查 [SETUP-PC](setup/SETUP-PC.md) 說明頂部的「gotcha #4」-- 安裝 Microsoft Build Tools。  
如果不這樣做，CrewAI 將因涉及 Chroma 的模糊錯誤而失敗。

然後，您需要在項目根目錄的 Cursor 終端中運行此命令以運行 Crew 命令：  
`uv tool install crewai`   
如果您以前使用過 Crew，可能值得執行此操作以確保您擁有最新版本：  
`uv tool upgrade crewai`  

關於 Crew 請記住：

1. 在第 3 週，您可以通過兩種方式處理 CrewAI 項目。要麼在我構建時查看每個項目的代碼，然後執行 `crewai run` 查看其運行情況。或者，如果您喜歡更多動手操作，則從頭開始創建自己的 Crew 項目來反映我的項目；例如，創建 `my_debate` 來配合 `debate`，並與我一起編寫代碼。兩種方法都可行！  
2. Windows 用戶：最近由 Crew 的一個庫引入了新問題。在修復之前，當您嘗試運行 `crewai create crew` 時可能會出現「unicode」錯誤。如果發生這種情況，請先在終端中運行此命令：`$env:PYTHONUTF8 = "1"`  
3. Gemini 用戶：除了在 `.env` 文件中設置 `GOOGLE_API_KEY` 外，您還需要設置相同的 `GEMINI_API_KEY`

### 超級有用的資源

- 課程[資源](https://edwarddonner.com/2025/04/21/the-complete-agentic-ai-engineering-course/)和視頻
- [指南](guides/01_intro.ipynb)部分的許多必要指南
- [故障排除](setup/troubleshooting.ipynb)筆記本

### API 成本 - 請務必閱讀！

本課程涉及調用 OpenAI 和其他前沿模型，需要 API 密鑰和少量花費，我們在設置說明中設置了這些。如果您不想在 API 調用上花費，還有更便宜的替代方案，如 DeepSeek，以及免費替代方案，如使用 Ollama！

詳情請見[這裡](guides/09_ai_apis_and_ollama.ipynb)。

請務必監控您的 API 成本，以確保您對任何花費都完全滿意。對於 OpenAI，儀表板在[這裡](https://platform.openai.com/usage)。

### 最重要的是 -

務必享受這門課程的樂趣！您選擇學習智能體 AI 的時機再好不過了。希望您享受每一分鐘！如果在任何時候遇到困難 - [聯繫我](https://www.linkedin.com/in/eddonner/)。