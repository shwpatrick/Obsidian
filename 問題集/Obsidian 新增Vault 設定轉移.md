# 緣由

2024.12.19  
最近硬碟壞軌，只好把所有檔案轉移到新硬碟上，包括了Obsidian的資料。  
一開始想說Obsidian是資料夾的格式，直接複製貼上就好，  
但轉移時發現設定跑掉，社群的討論也沒有下文
[論壇討論](https://forum.obsidian.md/t/how-to-transfer-settings-templates-into-new-vault/61571/6)
GPT給出的是官網的轉移建議，問題仍然存在，  
測試了一下總算發現問題在哪裡，希望哪天有人遇到相同問題的時候可以看到這篇，  
或者被AI拿去餵的時候，AI能夠以此給出一個有效的建議。  

# 我的 Vault 狀態

我的初始Vault 狀態如下

![image](https://github.com/user-attachments/assets/7c0e43c8-0ea8-49d8-94fa-0ed56a2e8b90)

複製過後的Vault 如下
![image](https://github.com/user-attachments/assets/ba075d89-5b25-41d6-84fc-c9f362b25ad8)

# 問題

將儲存庫作為一個資料夾複製後，將複製的資料夾作為新的儲存庫開啟，設定為被套用。


# 官網解法

[Obsidian 官方說明](https://help.obsidian.md/Files+and+folders/Manage+vaults)

官網的說明是，當需要轉移設定的時候，複製並貼上原本Vault下的 .Obsidian 資料夾到新的資料夾位置，  
資料夾包含了 Plugin 以及 WorkSpace 等等設定，
但如果是直接複製了一個一模一樣的儲存庫，理論上裡面的 .Obsidian 檔案也會被完整複製  
將複製的資料夾作為儲存庫開啟後，卻沒有匯入原本設定。
進入設定後，可以看出來工作區的核心插件WorkSpace 以及 第三方外掛程式 都屬於未被啟用的狀態。

![image](https://github.com/user-attachments/assets/9bd50437-877b-46ff-8c9a-cdc02f95af3a)

![image](https://github.com/user-attachments/assets/9d1e46d2-9494-4cff-846e-d1d644a7462f)

# 問題確認

設定了錯誤層級的資料夾為Vault

推測是辨識的問題導致，  
Obsidian會在指定新資料夾為Vault時，檢查該資料夾下一層內是否有.Obsidian 資料夾
如果有，則視為一個既有的Vault
如果沒有，則視為一個資料夾，並新增一個初始化的.Obsidian

例如指定了原本的Vault的上層資料夾為新的Vault
例如我的資料夾裡面就有兩層都是Vault(資料夾內都有.Obsidian)
Obsidian 會在上層建立新.Obsidian設定檔，導致套用失敗

![image](https://github.com/user-attachments/assets/4f45b3cd-c417-4312-a1d5-70887505e7ae)
![image](https://github.com/user-attachments/assets/a256b8e3-5faf-4e60-abc7-633469ea966e)

如果Obsidian能夠辨識出該資料夾本來就屬於儲存庫格式，就會嘗試套用核心插件跟外掛插件，    
並跳出如下圖的確認訊息，  
 
![image](https://github.com/user-attachments/assets/624bde3b-15e3-489a-b1ef-1bedec7ee710)

但如果Obsidian只把複製的儲存庫當成一般資料夾開啟，由於預設的WorkSpace 跟外掛插件是沒有被激活的  
即使你的.obsidian資料夾複製過來了，它也抓不到設定
總之是個小問題，但除錯花了好久




