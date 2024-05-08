---
# try also 'default' to start simple
theme: seriph
background: https://assets-global.website-files.com/6009ec8cda7f305645c9d91b/62c461ddbb6e1687cffd528d_WhatIsJavascript_2022-07-05.jpg
# some information about your slides, markdown enabled
title: What's event loop?
info: |
  ## event loop
  ## javascript
# apply any unocss classes to the current slide
class: text-center
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# https://sli.dev/guide/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/guide/syntax#mdc-syntax
mdc: true
---

# 什麼是 Event Loop？

一起來看看ㄅ

---
transition: slide-left
---

# Event loop 是什麼？

> 是為了解決 JavaScript <span v-mark.circle.orange="1"> **單執行緒**</span>的設計而在<span v-mark.circle.orange="2">**特定執行環境**</span>中所提供的一個實現<span v-mark.circle.orange="3">**異步**</span>的解決機制。

<br>

<v-clicks>

- **單執行緒 Single Thread**：<br>
  JavaScript 這個語言在當初設計的時候就設定為單執行緒，而單執行序的意思即為每一行程式碼執行完畢後，才會往下一行的程式碼去執行。
  <br>
- **特定執行環境**：<br>
  JavaScript 是一個語言，它需要有執行環境才能夠使用。（像是世界上有很多語言，但需要透過人來說和寫才能應用該語言一樣）
除了我們常見的瀏覽器 Browser 以外，還有 Node.js 的環境也可以運行 JavaScript 程式碼。
所以換句話說， Event loop 這個機制是執行環境（也就是瀏覽器或是 Node.js ）所提供的，**JavaScript 本身並沒有 Event loop 這個功能**。
- **異步 asynchronous**：<br>
  異步是指當主要的線程在執行程式碼時，可以同時進行其他的程式碼的特性。

</v-clicks>

---
transition: slide-left
level: 2
---

# 為什麼需要 Event loop 呢？
<br>

如剛才提到的，事件循環 Event loop 的出現是為了要解決單執行緒的問題，因為如果每次執行一行程式碼的時候都要等前面的執行完才能再觸發下一行的話，這樣<span v-mark.red="1">使用者體驗會很大程度的被影響</span>。
<br>

舉例：延伸我們剛才提到的咖啡廳例子，如果老闆在甜點製作或是手沖咖啡的過程中都等到餐點做完才去進行下一個服務，可想而知門口在等的客人一定會客訴。

<br>

那 **Event loop 要做的事情**是什麼？
<br>

就是在老闆等待蛋糕烘焙的過程中去做接待客人或是清潔桌面甚至是點餐的服務，直到蛋糕烘焙結束後，老闆再去<span v-mark.red="2">做對應的後續動作</span>（可能是切蛋糕然後放進冰箱或是送餐到客人桌上）

---
layout: image-right
transition: slide-left
image: https://yeefun.github.io/static/e53e7455f561eeb2a702370fc75b7865/0a151/event-loop-process.jpg
---

# Event loop 的執行

要介紹 Event loop 的執行過程，那就免不了介紹這個機制背後的主要概念。

接下來我們就針對每一個功能來仔細介紹：

---
transition: slide-left
layout: two-cols
---

# 名詞介紹

- **Call Stack 呼叫堆疊**：<br>
  又稱作**上下文堆疊**，在 JavaScript 中只有一個 Call Stack ，所以所有的程式碼都會出現在這個地方且被執行。

- **Web API**：<br>
  是由瀏覽器提供的 API，常見的像是 `console.log` `setTimeOut` 等都是屬於這個範疇。（ `console.log` 實際上使用的是 `window.console.log`，只不過 `window` 是被允許省略的）

- **Callback Queue / Task Queue**：<br>
  這邊會放置使用 Web API 處理過後返回的函式（就是所謂的 callback function），按先進先出的順序透過 event loop 的機制移動到 Call Stack 中被執行。

---
transition: slide-left
layout: two-cols
---

# 名詞介紹
<v-clicks>

- **Macro task 宏任務** ：<br>
  在每一次的 event loop 循環中，只能提取一次的任務類型。常見的有 `script`(整體程式碼)、`setTimeout`、`setInterval`、`setImmediate` (Node.js)等。

- **Micro task 微任務** ：<br>
  在每一次的 event loop 循環中，會一直提取此類型任務到任務列隊沒有任務為止。常見的有 `Promise.then`、`await`後的程式碼 `MutationObserver`、`process.nextTick` (Node.js)。

</v-clicks>

---
layout: image-right
transition: slide-left
image: https://support.vectorsolutions.com/servlet/rtaImage?eid=ka04N000000VT3M&feoid=00N1K00000erVV1&refid=0EM4N00000255ag
---

# Event loop 的注意事項

到這邊應該對 Event loop 有一個很基礎的概念了，但是還是要特別注意前面提及過的重點：

<v-clicks>

- 根據瀏覽器的不同，執行順序是有可能不一樣的。
- Event loop <span v-mark.red="2">不是 JavaScript 的功能</span>，是執行環境所提供的一種機制。
- 所謂的 Macro task 宏任務其實就是本來的 Task 。
</v-clicks>

---
layout: image-left
image: https://assets-global.website-files.com/6009ec8cda7f305645c9d91b/62c461ddbb6e1687cffd528d_WhatIsJavascript_2022-07-05.jpg
transition: slide-left
---
# 謝謝大家！
發問時間