[使用VS code開發Angular 4](https://blog.johnwu.cc/article/angular-4-%E6%95%99%E5%AD%B8-%E5%BE%9E%E9%A0%AD%E9%96%8B%E5%A7%8B.html)

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
