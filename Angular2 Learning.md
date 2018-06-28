[使用VS code開發Angular 4 -- 從頭開始包含建置與安裝](https://blog.johnwu.cc/article/angular-4-%E6%95%99%E5%AD%B8-%E5%BE%9E%E9%A0%AD%E9%96%8B%E5%A7%8B.html)

---

* ng serve --open --port 1234  
可以再`.angular-cli.json` 檔案中  
新增defaults.serve.port = 1234即可  
```
"defaults": {
    "styleExt": "=scss",
    "component": {},
    "serve": {
      "port": 1234  
    }
  }
```

`--open`代表直接再瀏覽器開啟該頁面

---

在ng serve時可以使用前端的debug  
但是如果想要同時連後端一起debug則使用Cross site  
這樣會出現正是區額外不必要的程式碼  

如果一直使用ng build，則會花費大量時間在等待  
經查詢之後可以使用  
從`ng serve`變成`ng build --watch`  
可以達到擁有ng serve的即時編譯  
以及由後端run IIS，避免了cross site issue  
也不必等待re build的時間  

---
