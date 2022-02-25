# HowtoexecutefromTerminal003

---

---

- ターミナルから実行（CONDA環境）
    
    任意のディレクトリに移動します（事例：./youtube_dl）
    
    ```bash
    cd youtube_dl
    ```

    アクティベート
    ```bash
    source youtube/bin/activate
    ``` 

    次のコマンドによりYouTube動画から音声部を抽出、MP3化
    ```bash
    youtube-dl --extract-audio --audio-format mp3 "動画URL"
    ```

    
    >>> 結果
    youtube_dlディレクトリ内にMP3ファイルが生成されます。  
    
    ![IMGSSytmp3.jpg](IMG/IMGSSytmp3.jpg)  
    

---
