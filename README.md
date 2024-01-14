# Nuxt 3 Gemini  

今だけ無料だと思うのでNuxt3でGeminiを簡単に試してみた。  
「今日のご飯」をクリックするとボーダー内にAIからの返答としてメニューとレシピが出力される。  
Geminiの返答はマークダウン形式なので、markedで変換する必要がある。

## 環境
Nodejs v20  
Nuxt v3  
Gemini API KEY

## API key  
google ai stadioから取得します。  
https://makersuite.google.com/

## インストール  

    npm i

## /.envにAPIkeyを設定

    NUXT_API_KEY="key"


## 起動

    npm run dev