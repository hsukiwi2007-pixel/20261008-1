---
title: 選擇題測驗卷網站講義（學生版）.md

---

---
title: 選擇題測驗卷網站講義（學生版）

---

---
title: 選擇題測驗卷網站講義（學生版）
tags: [114程式設計與實習_上學期]

---

# 選擇題測驗卷網站講義（學生版）

學號：＿＿＿＿＿＿＿＿　　姓名：＿＿＿＿＿＿＿＿

> **填寫方式**
> 1. 每個學習都要放：**執行截圖**、**三次問 AI 的提示詞**、**最後採用的程式碼**。
> 2. 問 AI 的提示詞請**逐字貼上**自己實際輸入的內容（不要寫摘要），第一次、第二次、第三次依序記錄。
> 3. 程式碼貼在「點開貼上」的收合區塊裡，貼上**你最後真正採用、而且能執行**的版本。

---

## 學習1：產生一個選擇題測驗卷網站

https://cfchen58.synology.me/115/week4/stage1/

**這個階段的目標：** 用 p5.js 做出一個一次顯示一題、四個選項、答完會顯示對錯與總分的測驗網站（題目先寫在程式裡）。
**這個階段會修改的檔案：** index.html、sketch.js

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）
### 未作答
![螢幕擷取畫面 2026-10-08 142454](https://hackmd.io/_uploads/SyL-_hEoMx.png)
### 答對
![螢幕擷取畫面 2026-10-08 142934](https://hackmd.io/_uploads/rk-_u2VsGe.png)
### 答錯
![螢幕擷取畫面 2026-10-08 142838](https://hackmd.io/_uploads/Hk5EO3NoMx.png)
### 答錯動畫
![答錯動畫](https://hackmd.io/_uploads/H1lpaK24iGe.gif)


### 第一次問 AI

```tex!
使用p5.js撰寫一個選擇題測驗系統，我已經產生一個p5.js專案，請把程式碼寫在sketch.js檔案內，每條指令都需要加上中文註解。測驗系統題目設定為五題，測驗題目的內容為程式設計p5.js簡易指令練習測驗，系統採用全螢幕畫布，使用者答錯時，系統會在正確答案選項上，加上ccd5ae背景顏色，該選項要上下跳動，答錯的選項採用dd2d4a背景顏色，選項左右移動，選擇題選項共有四個選項，當五題結束後，需要顯示答對的題數，每次顯示一個題目，需要有下一題的按鈕。
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習1的程式碼
```javascript=
let questions = []; // 儲存所有測驗題目
let currentQuestion = 0; // 記錄目前顯示的題目索引
let score = 0; // 記錄答對的題數
let selectedAnswer = -1; // 記錄使用者選擇的答案索引
let answered = false; // 記錄目前題目是否已作答
let totalQuestions = 5; // 設定測驗總題數
let optionAreas = []; // 儲存四個選項的點擊範圍
let nextButtonArea; // 儲存下一題按鈕的點擊範圍
let restartButtonArea; // 儲存重新開始按鈕的點擊範圍

function setup() { // p5.js 初始化函式
  createCanvas(windowWidth, windowHeight); // 建立符合視窗大小的全螢幕畫布
  textFont("Arial"); // 設定文字字型
  textAlign(CENTER, CENTER); // 設定文字水平與垂直置中
  rectMode(CORNER); // 設定矩形使用左上角作為座標
  setupQuestions(); // 建立測驗題目
}

function windowResized() { // 當瀏覽器視窗大小改變時執行
  resizeCanvas(windowWidth, windowHeight); // 重新調整畫布大小
}

function setupQuestions() { // 建立五題 p5.js 指令練習題
  questions = [ // 設定題目陣列
    { // 第一題資料
      question: "下列哪一個函式可以建立 p5.js 畫布？", // 設定第一題題目
      options: ["drawCanvas()", "createCanvas()", "newCanvas()", "makeCanvas()"], // 設定第一題選項
      answer: 1 // 設定第一題正確答案索引
    }, // 結束第一題資料

    { // 第二題資料
      question: "p5.js 中哪一個函式會持續重複執行？", // 設定第二題題目
      options: ["setup()", "start()", "draw()", "loopCanvas()"], // 設定第二題選項
      answer: 2 // 設定第二題正確答案索引
    }, // 結束第二題資料

    { // 第三題資料
      question: "哪一個函式可以設定畫布的背景顏色？", // 設定第三題題目
      options: ["fill()", "background()", "color()", "setBackground()"], // 設定第三題選項
      answer: 1 // 設定第三題正確答案索引
    }, // 結束第三題資料

    { // 第四題資料
      question: "哪一個函式可以繪製矩形？", // 設定第四題題目
      options: ["square()", "box()", "rect()", "rectangle()"], // 設定第四題選項
      answer: 2 // 設定第四題正確答案索引
    }, // 結束第四題資料

    { // 第五題資料
      question: "哪一個函式可以繪製圓形或橢圓形？", // 設定第五題題目
      options: ["circle()", "ellipse()", "round()", "oval()"], // 設定第五題選項
      answer: 1 // 設定第五題正確答案索引
    } // 結束第五題資料
  ]; // 結束題目陣列

  currentQuestion = 0; // 將題目索引重設為第一題
  score = 0; // 將分數重設為零
  selectedAnswer = -1; // 清除使用者選擇的答案
  answered = false; // 將作答狀態重設為尚未作答
  optionAreas = []; // 清除選項點擊範圍
  nextButtonArea = null; // 清除下一題按鈕範圍
  restartButtonArea = null; // 清除重新開始按鈕範圍
}

function draw() { // p5.js 每一幀都會執行的函式
  background("#f8f9fa"); // 設定畫布背景顏色

  if (currentQuestion < totalQuestions) { // 判斷是否仍在測驗階段
    drawQuiz(); // 繪製測驗畫面
  } else { // 如果所有題目都已完成
    drawResult(); // 繪製測驗結果畫面
  }
}

function drawQuiz() { // 繪製題目與選項
  let questionData = questions[currentQuestion]; // 取得目前題目的資料
  let contentWidth = min(width * 0.86, 900); // 設定內容區域最大寬度
  let optionWidth = min(width * 0.76, 760); // 設定選項寬度
  let optionHeight = constrain(height * 0.085, 54, 82); // 設定選項高度
  let optionGap = constrain(height * 0.025, 14, 24); // 設定選項之間的間距
  let startX = (width - optionWidth) / 2; // 計算選項起始 X 座標
  let startY = height * 0.28; // 計算第一個選項的起始 Y 座標

  fill("#263238"); // 設定標題文字顏色
  textSize(constrain(width * 0.035, 22, 38)); // 設定標題文字大小
  text("p5.js 程式設計簡易指令測驗", width / 2, height * 0.08); // 顯示測驗標題

  fill("#546e7a"); // 設定題號文字顏色
  textSize(constrain(width * 0.022, 16, 24)); // 設定題號文字大小
  text("第 " + (currentQuestion + 1) + " 題 / 共 " + totalQuestions + " 題", width / 2, height * 0.15); // 顯示目前題號

  fill("#263238"); // 設定題目文字顏色
  textSize(constrain(width * 0.026, 18, 30)); // 設定題目文字大小
  text(questionData.question, width / 2, height * 0.22, contentWidth, 80); // 顯示目前題目

  optionAreas = []; // 清除上一幀的選項點擊範圍

  for (let i = 0; i < questionData.options.length; i++) { // 依序繪製四個選項
    let baseY = startY + i * (optionHeight + optionGap); // 計算目前選項的基本 Y 座標
    let offsetX = 0; // 設定選項預設水平位移
    let offsetY = 0; // 設定選項預設垂直位移
    let optionColor = color("#ffffff"); // 設定選項預設背景顏色

    if (answered) { // 判斷使用者是否已經作答
      if (i === questionData.answer && selectedAnswer !== questionData.answer) { // 判斷目前選項是否為答錯後的正確答案
        optionColor = color("#ccd5ae"); // 將正確答案設定為指定的背景顏色
        offsetY = sin(frameCount * 0.18) * 8; // 讓正確答案上下跳動
      }

      if (i === selectedAnswer && selectedAnswer !== questionData.answer) { // 判斷目前選項是否為使用者答錯的選項
        optionColor = color("#dd2d4a"); // 將錯誤選項設定為指定的背景顏色
        offsetX = sin(frameCount * 0.22) * 8; // 讓錯誤選項左右移動
      }

      if (i === questionData.answer && selectedAnswer === questionData.answer) { // 判斷使用者是否答對
        optionColor = color("#ccd5ae"); // 將答對的選項設定為正確背景顏色
      }
    }

    let optionX = startX + offsetX; // 計算選項實際 X 座標
    let optionY = baseY + offsetY; // 計算選項實際 Y 座標

    optionAreas.push({ // 儲存目前選項的點擊範圍
      x: optionX, // 儲存選項 X 座標
      y: optionY, // 儲存選項 Y 座標
      width: optionWidth, // 儲存選項寬度
      height: optionHeight // 儲存選項高度
    }); // 結束選項點擊範圍資料

    noStroke(); // 移除選項外框
    fill(optionColor); // 套用選項背景顏色
    rect(optionX, optionY, optionWidth, optionHeight, 12); // 繪製選項矩形

    fill("#263238"); // 設定選項文字顏色
    textSize(constrain(width * 0.021, 16, 24)); // 設定選項文字大小
    text(questionData.options[i], optionX + optionWidth / 2, optionY + optionHeight / 2); // 顯示選項文字
  }

  if (answered) { // 判斷是否已完成目前題目
    drawNextButton(); // 顯示下一題按鈕
  } else { // 如果尚未作答
    fill("#78909c"); // 設定提示文字顏色
    textSize(constrain(width * 0.018, 14, 20)); // 設定提示文字大小
    text("請點選一個答案", width / 2, height * 0.86); // 顯示作答提示
  }
}

function drawNextButton() { // 繪製下一題按鈕
  let buttonWidth = 180; // 設定按鈕寬度
  let buttonHeight = 58; // 設定按鈕高度
  let buttonX = (width - buttonWidth) / 2; // 計算按鈕 X 座標
  let buttonY = height * 0.85; // 計算按鈕 Y 座標

  nextButtonArea = { // 儲存下一題按鈕點擊範圍
    x: buttonX, // 儲存按鈕 X 座標
    y: buttonY, // 儲存按鈕 Y 座標
    width: buttonWidth, // 儲存按鈕寬度
    height: buttonHeight // 儲存按鈕高度
  }; // 結束按鈕點擊範圍資料

  noStroke(); // 移除按鈕外框
  fill("#457b9d"); // 設定按鈕背景顏色
  rect(buttonX, buttonY, buttonWidth, buttonHeight, 12); // 繪製下一題按鈕

  fill("#ffffff"); // 設定按鈕文字顏色
  textSize(21); // 設定按鈕文字大小
  text("下一題", buttonX + buttonWidth / 2, buttonY + buttonHeight / 2); // 顯示下一題文字
}

function drawResult() { // 繪製測驗結果畫面
  fill("#263238"); // 設定結果標題文字顏色
  textSize(constrain(width * 0.045, 28, 48)); // 設定結果標題文字大小
  text("測驗結束！", width / 2, height * 0.3); // 顯示測驗結束文字

  fill("#546e7a"); // 設定分數文字顏色
  textSize(constrain(width * 0.03, 20, 32)); // 設定分數文字大小
  text("你答對了 " + score + " 題，共 " + totalQuestions + " 題", width / 2, height * 0.42); // 顯示答對題數

  let buttonWidth = 200; // 設定重新開始按鈕寬度
  let buttonHeight = 60; // 設定重新開始按鈕高度
  let buttonX = (width - buttonWidth) / 2; // 計算重新開始按鈕 X 座標
  let buttonY = height * 0.58; // 計算重新開始按鈕 Y 座標

  restartButtonArea = { // 儲存重新開始按鈕點擊範圍
    x: buttonX, // 儲存按鈕 X 座標
    y: buttonY, // 儲存按鈕 Y 座標
    width: buttonWidth, // 儲存按鈕寬度
    height: buttonHeight // 儲存按鈕高度
  }; // 結束重新開始按鈕資料

  noStroke(); // 移除按鈕外框
  fill("#457b9d"); // 設定重新開始按鈕背景顏色
  rect(buttonX, buttonY, buttonWidth, buttonHeight, 12); // 繪製重新開始按鈕

  fill("#ffffff"); // 設定按鈕文字顏色
  textSize(21); // 設定按鈕文字大小
  text("重新開始", buttonX + buttonWidth / 2, buttonY + buttonHeight / 2); // 顯示重新開始文字
}

function mousePressed() { // 處理滑鼠點擊事件
  if (currentQuestion >= totalQuestions) { // 判斷是否位於結果畫面
    if (isInsideArea(mouseX, mouseY, restartButtonArea)) { // 判斷是否點擊重新開始按鈕
      setupQuestions(); // 重新初始化測驗
    }

    return; // 結束本次滑鼠事件
  }

  if (!answered) { // 判斷目前題目是否尚未作答
    for (let i = 0; i < optionAreas.length; i++) { // 逐一檢查四個選項
      if (isInsideArea(mouseX, mouseY, optionAreas[i])) { // 判斷滑鼠是否點擊目前選項
        selectedAnswer = i; // 記錄使用者選擇的答案
        answered = true; // 將目前題目設定為已作答

        if (selectedAnswer === questions[currentQuestion].answer) { // 判斷使用者是否答對
          score++; // 答對時增加分數
        }

        break; // 完成選項判斷後離開迴圈
      }
    }

    return; // 結束本次滑鼠事件
  }

  if (isInsideArea(mouseX, mouseY, nextButtonArea)) { // 判斷是否點擊下一題按鈕
    currentQuestion++; // 移動到下一題
    selectedAnswer = -1; // 清除上一題的選擇答案
    answered = false; // 將下一題設定為尚未作答
  }
}

function isInsideArea(pointX, pointY, area) { // 判斷座標是否位於指定區域內
  if (!area) { // 判斷區域資料是否存在
    return false; // 沒有區域資料時回傳否
  }

  return pointX >= area.x && pointX <= area.x + area.width && pointY >= area.y && pointY <= area.y + area.height; // 回傳座標是否位於區域內
}

```
:::


---

## 學習2：網頁設定為響應式網頁

https://cfchen58.synology.me/115/week4/stage2/

**這個階段的目標：** 讓網站在電腦、平板、手機（直向與橫向）都能正常顯示，視窗大小改變時版面自動調整。
**這個階段會修改的檔案：** index.html、sketch.js

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![螢幕擷取畫面 2026-10-08 151246](https://hackmd.io/_uploads/Byf6G64sGl.png)


### 第一次問 AI

```tex!
網頁設定為響應式網頁，讓網站在電腦、平板、手機（直向與橫向）都能正常顯示，視窗大小改變時版面自動調整
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習2的程式碼
```javascript=
let questions = []; // 儲存所有測驗題目
let currentQuestion = 0; // 儲存目前題目索引
let score = 0; // 儲存答對題數
let selectedAnswer = -1; // 儲存使用者選擇的答案索引
let answered = false; // 記錄目前題目是否已作答
let totalQuestions = 5; // 設定測驗總題數
let optionAreas = []; // 儲存選項點擊區域
let nextButtonArea = null; // 儲存下一題按鈕點擊區域
let restartButtonArea = null; // 儲存重新開始按鈕點擊區域
let layout = {}; // 儲存響應式版面資料

function setup() { // p5.js 初始化函式
  createCanvas(windowWidth, windowHeight); // 建立符合視窗大小的畫布
  pixelDensity(1); // 設定畫布像素密度
  textFont("Arial"); // 設定文字字型
  textAlign(CENTER, CENTER); // 設定文字水平與垂直置中
  textWrap(WORD); // 設定文字自動換行
  rectMode(CORNER); // 設定矩形使用左上角座標
  setupQuestions(); // 初始化題目資料
  updateLayout(); // 初始化響應式版面
}

function windowResized() { // 當瀏覽器視窗尺寸改變時執行
  resizeCanvas(windowWidth, windowHeight); // 重新調整畫布大小
  updateLayout(); // 重新計算版面
}

function updateLayout() { // 計算響應式版面
  let shortSide = min(width, height); // 取得畫布較短的一邊

  let titleSize = constrain(shortSide * 0.07, 20, 38); // 設定測驗標題大小
  let numberSize = constrain(shortSide * 0.04, 14, 22); // 設定題號大小
  let questionSize = constrain(shortSide * 0.05, 16, 28); // 設定選擇題題目文字大小
  let optionTextSize = constrain(shortSide * 0.04, 14, 22); // 設定選項文字大小
  let buttonTextSize = constrain(shortSide * 0.04, 16, 22); // 設定按鈕文字大小
  let hintSize = constrain(shortSide * 0.032, 12, 18); // 設定提示文字大小

  let questionBoxWidth = min(width * 0.84, 760); // 設定題目方框寬度
  let questionBoxHeight = constrain(shortSide * 0.18, 76, 125); // 設定題目方框高度
  let optionWidth = min(width * 0.84, 760); // 設定選項寬度
  let optionHeight = constrain(shortSide * 0.105, 46, 74); // 設定選項高度
  let optionGap = constrain(shortSide * 0.022, 8, 16); // 設定選項間距
  let buttonWidth = constrain(width * 0.42, 140, 210); // 設定按鈕寬度
  let buttonHeight = constrain(shortSide * 0.105, 48, 62); // 設定按鈕高度

  let titleHeight = titleSize + 16; // 計算標題區域高度
  let numberHeight = numberSize + 16; // 計算題號區域高度
  let titleToNumberGap = 8; // 設定標題與題號之間的間距
  let numberToQuestionGap = 18; // 設定題號與題目方框之間的間距
  let questionToOptionGap = 22; // 設定題目方框與選項之間的間距
  let optionBlockHeight = optionHeight * 4 + optionGap * 3; // 計算選項區域高度
  let optionToButtonGap = 22; // 設定選項與按鈕之間的間距
  let hintHeight = answered ? 0 : hintSize + 20; // 計算提示文字高度

  let totalHeight = titleHeight + titleToNumberGap + numberHeight + numberToQuestionGap + questionBoxHeight + questionToOptionGap + optionBlockHeight + optionToButtonGap + buttonHeight + hintHeight; // 計算全部內容高度
  let startY = (height - totalHeight) / 2; // 計算整體內容垂直置中起始位置

  if (startY < 12) { // 判斷畫布高度是否不足
    let scaleRatio = (height - 24) / totalHeight; // 計算內容縮放比例

    titleSize = max(16, titleSize * scaleRatio); // 縮小標題文字
    numberSize = max(12, numberSize * scaleRatio); // 縮小題號文字
    questionSize = max(14, questionSize * scaleRatio); // 縮小題目文字
    optionTextSize = max(12, optionTextSize * scaleRatio); // 縮小選項文字
    hintSize = max(10, hintSize * scaleRatio); // 縮小提示文字
    questionBoxHeight = max(60, questionBoxHeight * scaleRatio); // 縮小題目方框高度
    optionHeight = max(38, optionHeight * scaleRatio); // 縮小選項高度
    optionGap = max(5, optionGap * scaleRatio); // 縮小選項間距
    buttonHeight = max(42, buttonHeight * scaleRatio); // 縮小按鈕高度

    titleHeight = titleSize + 16; // 重新計算標題區域高度
    numberHeight = numberSize + 16; // 重新計算題號區域高度
    optionBlockHeight = optionHeight * 4 + optionGap * 3; // 重新計算選項區域高度
    hintHeight = answered ? 0 : hintSize + 20; // 重新計算提示文字高度

    totalHeight = titleHeight + titleToNumberGap + numberHeight + numberToQuestionGap + questionBoxHeight + questionToOptionGap + optionBlockHeight + optionToButtonGap + buttonHeight + hintHeight; // 重新計算全部高度
    startY = max(12, (height - totalHeight) / 2); // 重新計算垂直置中位置
  }

  layout = { // 儲存響應式版面資料
    titleSize: titleSize, // 儲存標題文字大小
    numberSize: numberSize, // 儲存題號文字大小
    questionSize: questionSize, // 儲存選擇題題目文字大小
    optionTextSize: optionTextSize, // 儲存選項文字大小
    buttonTextSize: buttonTextSize, // 儲存按鈕文字大小
    hintSize: hintSize, // 儲存提示文字大小
    questionBoxWidth: questionBoxWidth, // 儲存題目方框寬度
    questionBoxHeight: questionBoxHeight, // 儲存題目方框高度
    optionWidth: optionWidth, // 儲存選項寬度
    optionHeight: optionHeight, // 儲存選項高度
    optionGap: optionGap, // 儲存選項間距
    buttonWidth: buttonWidth, // 儲存按鈕寬度
    buttonHeight: buttonHeight, // 儲存按鈕高度
    titleHeight: titleHeight, // 儲存標題高度
    numberHeight: numberHeight, // 儲存題號高度
    titleToNumberGap: titleToNumberGap, // 儲存標題與題號間距
    numberToQuestionGap: numberToQuestionGap, // 儲存題號與題目間距
    questionToOptionGap: questionToOptionGap, // 儲存題目與選項間距
    optionBlockHeight: optionBlockHeight, // 儲存選項區域高度
    optionToButtonGap: optionToButtonGap, // 儲存選項與按鈕間距
    startY: startY // 儲存整體內容起始 Y 座標
  }; // 完成版面資料設定
}

function setupQuestions() { // 建立五題測驗題目
  questions = [ // 設定測驗題目陣列
    { // 第一題資料
      question: "下列哪一個函式可以建立 p5.js 畫布？", // 設定第一題題目
      options: ["drawCanvas()", "createCanvas()", "newCanvas()", "makeCanvas()"], // 設定第一題選項
      answer: 1 // 設定第一題正確答案索引
    }, // 結束第一題資料

    { // 第二題資料
      question: "p5.js 中哪一個函式會持續重複執行？", // 設定第二題題目
      options: ["setup()", "start()", "draw()", "loopCanvas()"], // 設定第二題選項
      answer: 2 // 設定第二題正確答案索引
    }, // 結束第二題資料

    { // 第三題資料
      question: "哪一個函式可以設定畫布的背景顏色？", // 設定第三題題目
      options: ["fill()", "background()", "color()", "setBackground()"], // 設定第三題選項
      answer: 1 // 設定第三題正確答案索引
    }, // 結束第三題資料

    { // 第四題資料
      question: "哪一個函式可以繪製矩形？", // 設定第四題題目
      options: ["square()", "box()", "rect()", "rectangle()"], // 設定第四題選項
      answer: 2 // 設定第四題正確答案索引
    }, // 結束第四題資料

    { // 第五題資料
      question: "哪一個函式可以繪製圓形或橢圓形？", // 設定第五題題目
      options: ["circle()", "ellipse()", "round()", "oval()"], // 設定第五題選項
      answer: 1 // 設定第五題正確答案索引
    } // 結束第五題資料
  ]; // 結束題目陣列

  currentQuestion = 0; // 將目前題目重設為第一題
  score = 0; // 將答對題數重設為零
  selectedAnswer = -1; // 清除使用者選擇
  answered = false; // 設定目前尚未作答
  optionAreas = []; // 清除選項點擊區域
  nextButtonArea = null; // 清除下一題按鈕區域
  restartButtonArea = null; // 清除重新開始按鈕區域
}

function draw() { // p5.js 每一幀執行的函式
  background("#f8f9fa"); // 設定畫布背景顏色

  if (currentQuestion < totalQuestions) { // 判斷是否仍在測驗階段
    drawQuiz(); // 繪製測驗畫面
  } else { // 如果所有題目已完成
    drawResult(); // 繪製結果畫面
  }
}

function drawQuiz() { // 繪製測驗內容
  let questionData = questions[currentQuestion]; // 取得目前題目資料
  let centerX = width / 2; // 設定畫布水平中心
  let titleY = layout.startY + layout.titleHeight / 2; // 計算標題中心 Y 座標
  let numberY = layout.startY + layout.titleHeight + layout.titleToNumberGap + layout.numberHeight / 2; // 計算題號中心 Y 座標
  let questionBoxX = centerX - layout.questionBoxWidth / 2; // 計算題目方框左側 X 座標
  let questionBoxY = layout.startY + layout.titleHeight + layout.titleToNumberGap + layout.numberHeight + layout.numberToQuestionGap; // 計算題目方框上方 Y 座標
  let questionBoxCenterX = questionBoxX + layout.questionBoxWidth / 2; // 計算題目方框中心 X 座標
  let questionBoxCenterY = questionBoxY + layout.questionBoxHeight / 2; // 計算題目方框中心 Y 座標
  let optionsStartY = questionBoxY + layout.questionBoxHeight + layout.questionToOptionGap; // 計算選項起始 Y 座標

  fill("#263238"); // 設定測驗標題顏色
  textSize(layout.titleSize); // 設定測驗標題文字大小
  text("p5.js 程式設計簡易指令測驗", centerX, titleY); // 顯示測驗標題

  fill("#546e7a"); // 設定題號文字顏色
  textSize(layout.numberSize); // 設定題號文字大小
  text("第 " + (currentQuestion + 1) + " 題 / 共 " + totalQuestions + " 題", centerX, numberY); // 顯示目前題號

  noStroke(); // 移除題目方框外框
  fill("#e9f5db"); // 設定題目方框背景顏色
  rect(questionBoxX, questionBoxY, layout.questionBoxWidth, layout.questionBoxHeight, 14); // 繪製題目方框背景

  stroke("#a3b18a"); // 設定題目方框邊框顏色
  strokeWeight(2); // 設定題目方框邊框粗細
  noFill(); // 設定方框內部不填色
  rect(questionBoxX, questionBoxY, layout.questionBoxWidth, layout.questionBoxHeight, 14); // 繪製題目方框邊框

  noStroke(); // 移除文字外框
  fill("#263238"); // 設定選擇題題目文字顏色
  textSize(layout.questionSize); // 設定選擇題題目文字大小
  textAlign(CENTER, CENTER); // 設定題目文字水平與垂直置中
  text(questionData.question, questionBoxCenterX, questionBoxCenterY, layout.questionBoxWidth - 36, layout.questionBoxHeight - 20); // 將題目文字區域中心與題目方框中心完全對齊

  optionAreas = []; // 清除上一幀選項點擊區域

  for (let i = 0; i < questionData.options.length; i++) { // 逐一繪製四個選項
    let baseY = optionsStartY + i * (layout.optionHeight + layout.optionGap); // 計算選項基本 Y 座標
    let offsetX = 0; // 設定選項水平位移
    let offsetY = 0; // 設定選項垂直位移
    let optionColor = color("#ffffff"); // 設定選項預設背景顏色

    if (answered) { // 判斷目前題目是否已作答
      if (i === questionData.answer && selectedAnswer !== questionData.answer) { // 判斷是否為答錯後的正確選項
        optionColor = color("#ccd5ae"); // 設定正確選項背景顏色
        offsetY = sin(frameCount * 0.18) * 8; // 讓正確選項上下跳動
      }

      if (i === selectedAnswer && selectedAnswer !== questionData.answer) { // 判斷是否為使用者答錯的選項
        optionColor = color("#dd2d4a"); // 設定錯誤選項背景顏色
        offsetX = sin(frameCount * 0.22) * 8; // 讓錯誤選項左右移動
      }

      if (i === questionData.answer && selectedAnswer === questionData.answer) { // 判斷使用者是否答對
        optionColor = color("#ccd5ae"); // 將答對選項設定為正確顏色
      }
    }

    let optionX = centerX - layout.optionWidth / 2 + offsetX; // 計算選項實際 X 座標
    let optionY = baseY + offsetY; // 計算選項實際 Y 座標

    optionAreas.push({ // 儲存選項點擊範圍
      x: optionX, // 儲存選項 X 座標
      y: optionY, // 儲存選項 Y 座標
      width: layout.optionWidth, // 儲存選項寬度
      height: layout.optionHeight // 儲存選項高度
    }); // 完成選項點擊範圍資料

    noStroke(); // 移除選項外框
    fill(optionColor); // 套用選項背景顏色
    rect(optionX, optionY, layout.optionWidth, layout.optionHeight, 12); // 繪製選項方框

    fill("#263238"); // 設定選項文字顏色
    textSize(layout.optionTextSize); // 設定選項文字大小
    text(questionData.options[i], centerX + offsetX, optionY + layout.optionHeight / 2); // 顯示置中的選項文字
  }

  let buttonY = optionsStartY + layout.optionBlockHeight + layout.optionToButtonGap; // 計算下一題按鈕 Y 座標

  if (answered) { // 判斷是否已經作答
    drawNextButton(buttonY); // 繪製下一題按鈕
  } else { // 如果尚未作答
    fill("#78909c"); // 設定提示文字顏色
    textSize(layout.hintSize); // 設定提示文字大小
    text("請點選一個答案", centerX, buttonY + layout.hintSize / 2); // 顯示作答提示
  }
}

function drawNextButton(buttonY) { // 繪製下一題按鈕
  let buttonX = (width - layout.buttonWidth) / 2; // 計算按鈕 X 座標

  nextButtonArea = { // 儲存下一題按鈕點擊區域
    x: buttonX, // 儲存按鈕 X 座標
    y: buttonY, // 儲存按鈕 Y 座標
    width: layout.buttonWidth, // 儲存按鈕寬度
    height: layout.buttonHeight // 儲存按鈕高度
  }; // 完成按鈕區域資料

  noStroke(); // 移除按鈕外框
  fill("#457b9d"); // 設定按鈕背景顏色
  rect(buttonX, buttonY, layout.buttonWidth, layout.buttonHeight, 12); // 繪製下一題按鈕

  fill("#ffffff"); // 設定按鈕文字顏色
  textSize(layout.buttonTextSize); // 設定按鈕文字大小
  text("下一題", buttonX + layout.buttonWidth / 2, buttonY + layout.buttonHeight / 2); // 顯示下一題文字
}

function drawResult() { // 繪製測驗結果
  let centerX = width / 2; // 設定結果畫面水平中心
  let resultTitleSize = constrain(min(width, height) * 0.09, 28, 48); // 設定結果標題文字大小
  let resultTextSize = constrain(min(width, height) * 0.06, 20, 32); // 設定結果文字大小
  let buttonX = (width - layout.buttonWidth) / 2; // 計算重新開始按鈕 X 座標
  let buttonY = height * 0.58; // 計算重新開始按鈕 Y 座標

  fill("#263238"); // 設定結果標題顏色
  textSize(resultTitleSize); // 設定結果標題文字大小
  text("測驗結束！", centerX, height * 0.3); // 顯示測驗結束文字

  fill("#546e7a"); // 設定分數文字顏色
  textSize(resultTextSize); // 設定結果文字大小
  text("你答對了 " + score + " 題，共 " + totalQuestions + " 題", centerX, height * 0.42); // 顯示答對題數

  restartButtonArea = { // 儲存重新開始按鈕區域
    x: buttonX, // 儲存按鈕 X 座標
    y: buttonY, // 儲存按鈕 Y 座標
    width: layout.buttonWidth, // 儲存按鈕寬度
    height: layout.buttonHeight // 儲存按鈕高度
  }; // 完成重新開始按鈕區域資料

  noStroke(); // 移除按鈕外框
  fill("#457b9d"); // 設定按鈕背景顏色
  rect(buttonX, buttonY, layout.buttonWidth, layout.buttonHeight, 12); // 繪製重新開始按鈕

  fill("#ffffff"); // 設定按鈕文字顏色
  textSize(layout.buttonTextSize); // 設定按鈕文字大小
  text("重新開始", buttonX + layout.buttonWidth / 2, buttonY + layout.buttonHeight / 2); // 顯示重新開始文字
}

function mousePressed() { // 處理滑鼠點擊事件
  if (currentQuestion >= totalQuestions) { // 判斷是否位於結果畫面
    if (isInsideArea(mouseX, mouseY, restartButtonArea)) { // 判斷是否點擊重新開始按鈕
      setupQuestions(); // 重新開始測驗
      updateLayout(); // 重新計算版面
    }

    return; // 結束滑鼠事件
  }

  if (!answered) { // 判斷目前題目是否尚未作答
    for (let i = 0; i < optionAreas.length; i++) { // 逐一檢查四個選項
      if (isInsideArea(mouseX, mouseY, optionAreas[i])) { // 判斷是否點擊選項
        selectedAnswer = i; // 記錄使用者選擇
        answered = true; // 設定目前題目為已作答

        if (selectedAnswer === questions[currentQuestion].answer) { // 判斷答案是否正確
          score++; // 答對時增加分數
        }

        updateLayout(); // 重新計算作答後版面
        break; // 離開選項檢查迴圈
      }
    }

    return; // 結束滑鼠事件
  }

  if (isInsideArea(mouseX, mouseY, nextButtonArea)) { // 判斷是否點擊下一題按鈕
    currentQuestion++; // 移至下一題
    selectedAnswer = -1; // 清除上一題選擇
    answered = false; // 將下一題設定為尚未作答
    updateLayout(); // 重新計算下一題版面
  }
}

function isInsideArea(pointX, pointY, area) { // 判斷座標是否位於指定區域
  if (!area) { // 判斷指定區域是否存在
    return false; // 沒有指定區域時回傳錯誤
  }

  return pointX >= area.x && pointX <= area.x + area.width && pointY >= area.y && pointY <= area.y + area.height; // 回傳座標是否位於區域內
}

```
:::


---

## 學習3：設定嵌入 Google 字型，網頁文字採用這些字型

https://cfchen58.synology.me/115/week4/stage3/

**這個階段的目標：** 從 Google Fonts 嵌入繁體中文字型，並讓畫布上的題目與選項文字使用這些字型。
**這個階段會修改的檔案：** index.html、sketch.js

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![學習3截圖](請貼上截圖)

### 第一次問 AI

```tex!
（逐字貼上你第一次問 AI 的提示詞）
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習3的程式碼
```javascript=
//學習3程式碼所在

```
:::


---

## 學習4：設定題庫並抽題顯示題目網頁（CSV 檔案）

https://cfchen58.synology.me/115/week4/stage4/

**這個階段的目標：** 把題目移到 questions.csv，網站讀取題庫後每次隨機抽出 5 題。
**這個階段會修改的檔案：** index.html、sketch.js、questions.csv

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![學習4截圖](請貼上截圖)

### 第一次問 AI

```tex!
（逐字貼上你第一次問 AI 的提示詞）
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習4的程式碼
```javascript=
//學習4程式碼所在

```
:::


---

## 學習5：利用 Google Sheets 當題庫

https://cfchen58.synology.me/115/week4/stage5/

**這個階段的目標：** 把題庫放在 Google 試算表，網站直接讀取，老師改試算表，網站題目就跟著更新。
**這個階段會修改的檔案：** index.html、sketch.js（questions.csv 當備用題庫）

### 執行截圖

（把截圖拖曳到這裡，或貼上圖片連結）

![學習5截圖](請貼上截圖)

### 第一次問 AI

```tex!
（逐字貼上你第一次問 AI 的提示詞）
```

### 第二次問 AI

```tex!
（逐字貼上你第二次問 AI 的提示詞）
```

### 第三次問 AI

```tex!
（逐字貼上你第三次問 AI 的提示詞）
```

### 程式碼內容

:::info
:::spoiler 點開貼上學習5的程式碼
```javascript=
//學習5程式碼所在

```
:::


---

## 我的心得

這五個學習中，哪一個最困難？你是怎麼解決的？（請寫出實際發生的事）

＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿＿
