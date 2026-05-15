# AI 自動遊玩 Chrome 恐龍遊戲

這是一個基於深度強化學習 (Dueling DDQN) 訓練的 Chrome 離線恐龍遊戲自動遊玩程式。本專案載入已訓練好的模型權重，並透過 Selenium 控制瀏覽器進行自動遊玩。

遊戲本體採用了開源的 Chrome 恐龍專案：[t-rex-runner](https://github.com/wayou/t-rex-runner)。

## 檔案結構

- `play_dino.py`: 遊戲執行主程式，負責啟動本地伺服器、開啟瀏覽器並載入 AI 模型來自動遊玩。
- `dino_ddqn_dueling_best.pth`: 訓練完成的 Dueling DDQN 神經網路模型權重檔。
- `t-rex-runner/`: 遊戲本地端網頁前端原始碼。
- `requirements.txt`: Python 依賴套件清單。
- `README.md`: 專案使用說明。

## 系統與環境需求

- **作業系統**: Windows / macOS / Linux
- **Python**: 3.7 或以上版本
- **瀏覽器**: 必須安裝 **Google Chrome** 瀏覽器，程式會使用 Selenium 透過 Chrome 進行遊戲。

## 安裝與執行步驟

### 1. 安裝依賴套件

請開啟終端機 (命令提示字元或 PowerShell)，並將路徑切換至本專案所在的資料夾，執行以下指令來安裝所需的 Python 套件：

```bash
git clone https://github.com/HungTaWang/Jumping_Dino
git clone https://github.com/wayou/t-rex-runner
```

```bash
pip install -r requirements.txt
```

> **💡 提示 (GPU 支援)**：如果你擁有 NVIDIA 顯示卡並希望使用 GPU 進行神經網路運算，建議前往 [PyTorch 官方網站](https://pytorch.org/get-started/locally/) 依照你的 CUDA 版本安裝對應的 `torch`。如果不特別設定，預設的 CPU 版本也能順暢執行。

### 2. 執行程式

環境設定完成後，在終端機輸入以下指令啟動 AI 自動遊玩：

```bash
python play_dino.py
```

### 3. 執行過程說明

1. **啟動伺服器**：程式會在背景啟動一個本地端網頁伺服器（預設為 `http://localhost:8000`）來載入 `t-rex-runner` 的遊戲畫面。
2. **開啟瀏覽器**：自動開啟一個新的 Google Chrome 視窗，並進入遊戲頁面。
3. **AI 開始遊玩**：載入 `dino_ddqn_dueling_best.pth` 模型權重，AI 將自動開始控制恐龍跳躍或下蹲以閃避障礙物。
4. **查看分數**：終端機視窗將會即時印出每回合遊戲結束後所獲得的分數。
5. **結束程式**：若想停止遊玩，可以直接關閉 Chrome 視窗，或在終端機中按下 `Ctrl + C` 中止程式。

## 注意事項

- **保持視窗開啟**：程式執行時，請勿將 Chrome 瀏覽器最小化。Selenium 和網頁中的 JavaScript 需要視窗保持活動狀態才能穩定抓取遊戲特徵與執行控制。
- **自動降級機制**：如果程式找不到本機的 `t-rex-runner` 資料夾，會自動嘗試連線至線上的 Chrome 恐龍遊戲網站執行。