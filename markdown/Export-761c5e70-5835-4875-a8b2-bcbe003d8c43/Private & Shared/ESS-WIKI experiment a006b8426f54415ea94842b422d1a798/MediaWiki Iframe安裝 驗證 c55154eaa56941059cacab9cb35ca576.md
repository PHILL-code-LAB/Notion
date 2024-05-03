# MediaWiki Iframe安裝/驗證

目前(2022/04/11) ess-wiki 所使用的 xampp 版本

xampp-win32-5.6.40-0-VC11.7z

xampp-win32-5.6.40-0-VC11-installer.exe

目前(2022/04/11) ess-wiki 所使用的 mediawiki 版本 1.24.2

將新版的 MediaWiki 直接覆蓋舊的，tarball 內的第一層目錄名稱被非 wiki

- 基準 (MediaWiki 版本 1.24.2)
    
    [ ess-wiki c:\xampp ] 拷貝到 [ nb100205 d:\xampp ]
    
- 更新到 MediaWike 1.25.0 ([https://www.mediawiki.org/wiki/MediaWiki_1.25](https://www.mediawiki.org/wiki/MediaWiki_1.25))
    - mediawiki-1.25.0.tar.gz
        
        解壓縮並覆蓋原本的 d:\xampp\htdocs\wiki
        
    - 安裝 Extension Iframe ([https://www.mediawiki.org/wiki/Extension:Iframe](https://www.mediawiki.org/wiki/Extension:Iframe))
        
        採用 `git checkout 'master@{2021-06-01 00:00:00}'` 的版本
        
        d:\xampp\htdocs\wiki\LocalSettings.php
        
        ![Untitled](MediaWiki%20Iframe%E5%AE%89%E8%A3%9D%20%E9%A9%97%E8%AD%89%20c55154eaa56941059cacab9cb35ca576/Untitled.png)
        
    - 每個頁面都會出現如下警告訊息 (可解決)
        
        ![Untitled](MediaWiki%20Iframe%E5%AE%89%E8%A3%9D%20%E9%A9%97%E8%AD%89%20c55154eaa56941059cacab9cb35ca576/Untitled%201.png)
        
        Warning: array_merge_recursive(): Argument #1 is not an array in D:\xampp\htdocs\wiki\includes\registration\ExtensionProcessor.php on line 295
        
        據此([this](https://gerrit.wikimedia.org/r/c/mediawiki/core/+/218787/1/includes/registration/ExtensionProcessor.php#84))可解決
        
        ![Untitled](MediaWiki%20Iframe%E5%AE%89%E8%A3%9D%20%E9%A9%97%E8%AD%89%20c55154eaa56941059cacab9cb35ca576/Untitled%202.png)
        
        ```bash
        		'manifest_version',
        ```
        
    - 但 Special Pages 的 <Iframe> 仍會出現如下錯誤訊息 (可解決)
- 繼續更新到 MediaWiki 1.26.4 ([https://www.mediawiki.org/wiki/MediaWiki_1.26](https://www.mediawiki.org/wiki/MediaWiki_1.26))
    - mediawiki-1.26.4.tar.gz
        
        解壓縮並覆蓋原本的 d:\xampp\htdocs\wiki
        
    - Extension:WYSIWYG 的運作有點問題 (可解決)
- 繼續更新到 MediaWiki 1.27.7 ([https://www.mediawiki.org/wiki/MediaWiki_1.27](https://www.mediawiki.org/wiki/MediaWiki_1.27))
    - mediawiki-1.27.7.tar.gz
        
        解壓縮並覆蓋原本的 d:\xampp\htdocs\wiki
        
    - Extension:Iframe ([https://www.mediawiki.org/wiki/Extension:Iframe](https://www.mediawiki.org/wiki/Extension:Iframe))
- 繼續更新到 MediaWiki 1.28.3 ([https://www.mediawiki.org/wiki/MediaWiki_1.28](https://www.mediawiki.org/wiki/MediaWiki_1.28))
    - mediawiki-1.28.3.tar.gz
        
        解壓縮並覆蓋原本的 d:\xampp\htdocs\wiki
        
    
    首頁顯示、Iframe 顯示、編輯功能 → 運作正常
    
- ~~繼續更新到 MediaWiki 1.29~~ ([https://www.mediawiki.org/wiki/MediaWiki_1.29](https://www.mediawiki.org/wiki/MediaWiki_1.29))
    - mediawiki-1.29.3.tar.gz
        
        解壓縮並覆蓋原本的 d:\xampp\htdocs\wiki
        
    - 首頁顯示、Iframe 顯示 → 發生錯誤
        
        ![Untitled](MediaWiki%20Iframe%E5%AE%89%E8%A3%9D%20%E9%A9%97%E8%AD%89%20c55154eaa56941059cacab9cb35ca576/Untitled%203.png)