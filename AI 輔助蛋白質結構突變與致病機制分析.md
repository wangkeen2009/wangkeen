

# AI 輔助蛋白質結構突變與致病機制分析

## 18週詳細學習與研究計畫（強化版）

---

## 第一階段：基礎知識建構與研究主題熟悉（1-4週）

---

### **第1週：主題導論與背景建構**

**主要目標**：認識阿茲海默症與蛋白質突變在疾病中的角色

#### 具體操作流程：

1. **阿茲海默症病理初步搜尋**：
   
   - Google「阿茲海默症 病理」閱讀前3個醫療機構或學協會的介紹。
   
   - 筆記阿茲海默症的致病蛋白和已知基因變異。

2. **選定重點蛋白質**：
   
   - 記下APP、PSEN1、MAPT三個蛋白質的全名、功能與常見相關疾病。

3. **繪製思維導圖**：
   
   - 使用XMind或手繪，繪出阿茲海默症-蛋白-突變三者關聯圖。

4. **週小測驗**：
   
   - 嘗試向ChatGPT或老師解釋：  
     「為什麼蛋白質突變對阿茲海默症研究很重要？」

#### 進階範例：

- 用Markdown整理重點筆記，或嘗試在Notion上製作「知識庫」。

---

### **第2週：查找阿茲海默症致病蛋白及常見突變**

**主要目標**：利用資料庫查詢，鎖定研究對象

#### 具體操作流程：

1. **UniProt查詢**：
   
   - 前往 [UniProt](https://www.uniprot.org/)，搜尋「APP human」，點進P05067條目。
   
   - 點擊「Variants」標籤，複製其中3-5個已知致病突變（如V717I、A673T）。

2. **Alzforum查詢**：
   
   - 進入 [Alzforum APP mutation database](https://www.alzforum.org/mutations/app)
   
   - 記錄每個突變的「蛋白質位置」、「氨基酸變化」與「已知臨床意義」。

3. **建立突變表格**：
   
   - Excel建檔：蛋白名稱、突變名稱、位置、類型、臨床關聯。

4. **備份FASTA序列**：
   
   - 在UniProt頁面下載APP蛋白的FASTA檔案。

#### 進階範例：

- 使用Python pandas整理突變資訊成DataFrame格式。
  
  ```python
  import pandas as pd
  mutations = [{"protein":"APP", "mutation":"V717I", "pos":717, "from":"V", "to":"I"}]
  df = pd.DataFrame(mutations)
  print(df)
  ```

---

### **第3週：學習蛋白質序列與結構基本知識**

**主要目標**：熟悉蛋白質序列格式與結構檔案

#### 具體操作流程：

1. **FASTA格式解析**：
   
   - 用記事本或Notepad++開啟FASTA檔案，認識>開頭的描述行與胺基酸序列。

2. **定位突變點**：
   
   - 利用Python腳本或Excel計算出FASTA序列的對應位置（注意頭部描述行不算在內）。

3. **人工or程式改序列**：
   
   - 用文字編輯器手動將第n個氨基酸替換為突變後的氨基酸。
   
   - 或用下列Python函數：
     
     ```python
     def mutate_fasta(seq, pos, new_aa):
        return seq[:pos-1] + new_aa + seq[pos:]
     ```

4. **PDB格式初步認識**：
   
   - 下載一個PDB結構檔（如1AAP.pdb），用記事本打開，觀察ATOM/HETATM等欄位。

#### 進階範例：

- 比較不同蛋白質（APP, PSEN1, MAPT）序列，發現保守區域。

---

### **第4週：AI蛋白質結構預測工具學習與環境設置**

**主要目標**：建立AI預測工具的基礎操作能力

#### 具體操作流程：

1. **註冊Google帳號並登入Colab**：
   
   - 訪問 [ColabFold Notebook](https://colab.research.google.com/github/sokrypton/ColabFold/blob/main/AlphaFold2.ipynb)。

2. **學習ColabFold步驟**：
   
   - 依照Notebook指示安裝必要的依賴。
   
   - 上傳自己的FASTA檔，執行預測。
   
   - 記錄每步出現的變數、設定（如模板使用、迭代次數）。

3. **下載PDB結果**：
   
   - 在Colab下方選單選擇「檔案」→ 下載生成的PDB檔。

4. **查看錯誤處理**：
   
   - 預測失敗時，學習從輸出訊息定位錯誤原因（如序列過長、格式錯誤等）。

#### 進階範例：

- 用自己編輯的突變型FASTA做一遍預測練習，比較輸出文件結構。

---

## 第二階段：蛋白質突變建模與結構分析（5-12週）

---

### **第5週：野生型蛋白質結構預測與可視化**

**主要目標**：熟練結構預測及基礎三維可視化

#### 具體操作流程：

1. **將FASTA序列貼到ColabFold運算，取得PDB結構檔**。

2. **下載ChimeraX並安裝**，開啟PDB結構。

3. **旋轉、縮放結構**，學習基本的ChimeraX操作（點選、選區、顯示/隱藏側鏈）。

4. **標註特定區域**：
   
   - 用命令列輸入 `select :A673` 選取第673號氨基酸。
   
   - 設置不同顏色 `color red sel`

5. **截圖存檔**：
   
   - 使用ChimeraX「File → Save Image」功能，將截圖存為png。

#### 進階範例：

- 使用ChimeraX的「surface」指令將結構繪製成分子表面模式。

- 學習ChimeraX腳本（.cxc檔），一次性自動載入+上色+標註。

---

### **第6週：突變型蛋白質序列建構與結構預測**

**主要目標**：自行產生突變型結構，並用AI預測

#### 具體操作流程：

1. **用第3週Python函數批次製作不同突變型FASTA序列**。

2. **上傳每個突變型FASTA到ColabFold進行預測**（可同時跑2-3個，節省時間）。

3. **下載所有PDB結構檔，按突變名稱存檔**（如APP_V717I.pdb）。

4. **記錄預測花費的時間與資源**。

#### 進階範例：

- 比較預測不同突變型時，AI模型對結構信心值（plDDT分數）的變化。

---

### **第7週：野生型與突變型蛋白質結構對比**

**主要目標**：觀察結構變異，掌握結構對比技能

#### 具體操作流程：

1. **同時在ChimeraX載入野生型和突變型PDB檔案**。

2. **執行結構疊合**：
   
   - 命令列輸入 `matchmaker #1 #2`（#1、#2分別為不同PDB的ID）。

3. **比對RMSD值**：
   
   - 用 `rmsd #1 #2` 計算結構差異。

4. **放大突變位點區域，觀察局部結構改變**。

5. **將疊合前後結構用不同顏色表示，便於截圖比較**。

#### 進階範例：

- 用ChimeraX script自動比對多組突變（.cxc範例可提供）。

---

### **第8週：蛋白質結構功能域與致病相關區域分析**

**主要目標**：理解突變點與蛋白質功能的關聯

#### 具體操作流程：

1. **UniProt查詢功能區域**：
   
   - 對應功能域（如β-sheet、活性中心、跨膜區）與結構上的氨基酸編號。

2. **ChimeraX標記功能域**：
   
   - 用 `select` + `color` 指令標註功能域與突變點。

3. **Google Scholar查找該區域與疾病的關聯**。

4. **總結突變點是否落在重要功能區**，並附圖說明。

#### 進階範例：

- 嘗試利用 [InterPro](https://www.ebi.ac.uk/interpro/) 或 Pfam 對蛋白進行結構域自動註釋。

---

### **第9週：深入文獻查證突變與致病性的關聯**

**主要目標**：蒐集與整理每個突變的研究現況

#### 具體操作流程：

1. **在Google Scholar用突變名稱關鍵字檢索**（如「APP V717I」）。

2. **下載2-3篇重點文獻並製作重點摘要表**。

3. **填寫「突變-功能-致病關聯」Excel表格**。

4. **若發現爭議/新發現，記錄於「進階討論」區塊**。

#### 進階範例：

- 用Zotero或Mendeley管理文獻，生成自動引用格式。

---

### **第10週：多突變型結構批次建構（自動化進階）**

**主要目標**：用程式批量處理多個突變，提高效率

#### 具體操作流程：

1. **建立突變批次清單（如CSV檔案）**，內容如：`蛋白,突變點,原胺基酸,突變胺基酸`

2. **用Python自動產生多個突變FASTA並保存**。
   
   ```python
   import pandas as pd
   muts = pd.read_csv('mut_list.csv')
   for idx, row in muts.iterrows():
      seq = mutate_fasta(base_seq, row['突變點'], row['突變胺基酸'])
      with open(f"{row['蛋白']}_{row['突變點']}{row['突變胺基酸']}.fasta","w") as f:
          f.write(seq)
   ```

3. **批次上傳ColabFold運算，統一命名與下載**。

4. **整理所有結構檔進同一資料夾，方便後續分析**。

#### 進階範例：

- 批量產生結構後，自動寫入一份「樣本管理表」記錄預測時間、信心分數、檔名等資訊。

---

### **第11週：結構可視化自動化與統整**

**主要目標**：批次可視化，提升統整效率

#### 具體操作流程：

1. **撰寫ChimeraX腳本，自動載入多個PDB，標註突變點並截圖**。
   
   - 範例腳本：
     
     ```
     open 1 wildtype.pdb
     color blue
     open 2 mutant.pdb
     color red
     select :717
     color yellow sel
     save wildtype_vs_mutant.png
     ```

2. **統一檔名與圖檔管理**。

3. **做成「突變對照圖集」PPT或PDF**，標示異同。

#### 進階範例：

- 用Python PIL或ImageMagick自動拼圖，將比對圖整理成大圖。

---

### **第12週：結構差異對功能可能影響的推論**

**主要目標**：從結構推論生物功能與致病性

#### 具體操作流程：

1. **比對功能區域與突變區的重疊度**。

2. **以表格/圖示整理各突變對結構的影響（RMSD、氫鍵變化、構型變動等）**。

3. **用簡單生物學語言推測功能變化（如結構穩定度下降/上升、可能失去某種結合能力）**。

4. **撰寫小結：本週發現/尚未解答的問題/未來驗證方向**。

#### 進階範例：

- 用PyMOL量化突變點鄰近氫鍵數目的變化（可額外學習）。

---

## 第三階段：進階分析與成果整合（13-18週）

---

### **第13週：討論進階分析方法（如分子對接）**

**主要目標**：引入分子對接，探索突變對結合能力的影響

#### 具體操作流程：

1. **下載AutoDockTools-1.5.7，學習安裝與基本操作**。

2. **下載一個已知阿茲海默症配體（如Aβ抑制劑）結構檔（可在PubChem找到）**。

3. **分別用野生型與突變型結構做對接分析**。
   
   - 操作步驟：設定Grid box → 準備PDBQT → 執行對接 → 分析結果。

4. **比較結合能（binding affinity）分數，判斷突變是否影響結合**。

#### 進階範例：

- 嘗試用其他開源對接軟體（如SwissDock），對比結果。

---

### **第14週：數據彙整與圖表製作**

**主要目標**：將所有數據成果視覺化，製作圖表

#### 具體操作流程：

1. **用Excel製作「突變-RMSD-結合能」三欄圖**。

2. **用Google Sheets、Python matplotlib/seaborn製作結構差異折線圖、熱圖**。

3. **彙整截圖、可視化圖表，製成整理型PPT**。

#### 進階範例：

- 用Python自動生成多突變分析報表。
  
  ```python
  import matplotlib.pyplot as plt
  plt.bar(['WT','V717I','A673T'], [0.5,0.9,1.3])
  plt.xlabel('突變型')
  plt.ylabel('RMSD')
  plt.title('不同突變型結構差異')
  plt.savefig('diff_rmsd.png')
  ```

---

### **第15週：撰寫成果初稿（研究背景、方法、初步結果）**

**主要目標**：將研究過程與初步結果文字化

#### 具體操作流程：

1. **依下列大綱撰寫Word或Markdown文件：**
   
   - 研究動機
   
   - 研究背景
   
   - 研究目標
   
   - 研究方法（圖示流程、使用工具、分析方法）
   
   - 初步實驗/預測結果

2. **插入流程圖與代表性截圖**。

3. **段落內容可參考學術論文的寫作方式**。

#### 進階範例：

- 用draw.io或Canva設計精美流程圖。

---

### **第16週：撰寫討論與結論**

**主要目標**：深度分析與展望

#### 具體操作流程：

1. **結構與致病性的綜合討論**：
   
   - 挑選1~2個突變案例做重點討論，結合文獻觀點。

2. **探討實驗與AI預測的差異/優缺點**。

3. **撰寫結論與未來研究建議**。

4. **檢查所有引用與圖表**，確保標註完整。

#### 進階範例：

- 以表格形式對比「AI預測 vs 傳統濕實驗」在蛋白質突變研究中的利弊。

---

### **第17週：簡報製作與口頭報告練習**

**主要目標**：成果視覺化，增強表達力

#### 具體操作流程：

1. **PowerPoint設計：以流程為主軸，配合圖表與結構圖**。

2. **

擬定3-5分鐘口頭報告稿（中文/英文皆可）**。  
3. **邀請同學/家人聆聽，進行模擬答辯與回饋**。  
4. **可錄影或錄音自我檢討**。

#### 進階範例：

- 嘗試製作動畫式簡報（PowerPoint動畫、Canva、Prezi）。

---

### **第18週：專題成果檢查與最終整合**

**主要目標**：完善所有學習成果，準備公開分享

#### 具體操作流程：

1. **自檢論文/簡報/數據表/程式碼完整性**。

2. **將所有材料整理進「專案資料夾」**（可依：文獻、結構、程式、圖表分類）。

3. **學習GitHub Pages部署（有空可將所有材料製成靜態網頁）**。

4. **製作「學習心得」1頁A4、200字總結本計畫收穫與反思**。

#### 進階範例：

- 使用 [Notion](https://www.notion.so/) 或 [Obsidian](https://obsidian.md/) 製作專題Wiki，持續補充未來學習紀錄。

---

## 課外補充材料（推薦資源大集合）

- **蛋白質結構基礎/線上課程**
  
  - [Protein Structure and Function (edX, 英文)](https://www.edx.org/learn/biology/harvard-university-protein-structure-and-function)
  
  - [Coursera-蛋白質生物資訊學（中文）](https://www.coursera.org/learn/protein-bioinformatics)
  
  - [台灣大學開放式課程-生物化學](https://ocw.ntu.edu.tw/ntu-ocw/ocw/cou/102S208)

- **生物資訊&AI工具學習**
  
  - [ColabFold中文社群教程](https://zhuanlan.zhihu.com/p/570578836)
  
  - [AlphaFold2基礎教學影片](https://www.youtube.com/watch?v=cdtz2dB4N6I)
  
  - [PyMOL/ChimeraX社群與範例程式](https://pymolwiki.org/index.php/Main_Page)

- **分子對接、結構分析社群**
  
  - [Molecular Docking基礎影片](https://www.youtube.com/watch?v=Udq5vsHcMcc)
  
  - [AutoDockTools官方文件](http://autodock.scripps.edu/)

- **蛋白質突變資料庫、阿茲海默症學會**
  
  - [Alzforum Mutation Database](https://www.alzforum.org/mutations)
  
  - [UniProt蛋白質變異專區](https://www.uniprot.org/docs/humsavar)
  
  - [Alzheimer’s Association（國際學會）](https://www.alz.org/)

- **程式碼/AI社群討論區**
  
  - [Kaggle生物資訊競賽](https://www.kaggle.com/search?q=protein)
  
  - [Stack Overflow Python專區](https://stackoverflow.com/questions/tagged/python)

- **GitHub Pages教學**
  
  - [GitHub Pages新手指南（中文）](https://ithelp.ithome.com.tw/articles/10265716)
  
  - [用Notion自架科學網頁](https://www.notion.so/zh-tw/help/guides/add-a-custom-domain)

---






