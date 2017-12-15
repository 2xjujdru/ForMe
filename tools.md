**前端js小工具**

仿造C# string檢查字串
```
function IsNullOrEmpty(_str: string): boolean {
    if (_str != "" && _str != undefined && _str != null) {
        return false;
    } else {
        return true;
    }
}
```


Jquery的Ajax簡易function，搭配promise
```
export class Json {
    public static GetData(_url: string, _data, _async: boolean = true) {
        return $.ajax({
            url: _url,
            type: 'post',
            data: _data,
            dataType: 'json',
            async: _async,
            success: function (_json) {
                if (_json != undefined)
                    return _json;
            },
            error: function (jqXHR, textStatus, errorThrown) {
                return { Result: jqXHR.status, Message: jqXHR.statusText, Success: false };
            }
        });
    }
}
```

將url的param轉成Json格式
```
function GetUrlParam(_url): any {
        var idx = _url.lastIndexOf("?");
        if (idx > 0) {
            var param = _url.substring(idx + 1);
            var params = {};
            if (param != undefined && param != "") {
                var arrs: string[] = param.split("&");
                for (var i = 0; i < arrs.length; i++) {
                    var a = arrs[i].split("=");
                    eval("params." + decodeURIComponent(a[0]) + " = '" + decodeURIComponent(a[1]) + "'");
                }
            }
            return params;
        }
        return {};
    }
```


**後端C#小工具**


實作SQL的IN功能
```
    static class Extensions
    {
        public static bool In<T>(this T item, params T[] items)
        {
            if (items == null)
                throw new ArgumentNullException("items");
            return items.Contains(item);
        }
    }
```


Dapper
存取DB，非EntityFramework的好物


```
public List<T> Read<T>(string SQL, object Object = null)
    {
        List<T> result = new List<T>();
        using (var cn = new Oracle.ManagedDataAccess.Client.OracleConnection(cnstr))
        {
            var ret = cn.Query<T>(SQL, Object);
            result = ret.ToList();
        }
        return result;
    }
```

```
public MessageObject Execute(string SQL, object Object = null)
    {
        MessageObject ret = new MessageObject();
        using (var cn = new Oracle.ManagedDataAccess.Client.OracleConnection(cnstr))
        {
            ret.Result = cn.Execute(SQL, Object);
            ret.Message = "執行成功";
            ret.Success = true;
        }
        return ret;
    }
```

```
    public void Execute_Func(string SQL, ref DynamicParameters Object)
    {
        using (var cn = new Oracle.ManagedDataAccess.Client.OracleConnection(cnstr))
        {
            cn.Execute(SQL, Object, commandType: CommandType.StoredProcedure);
        }
    }
    
    var p = new DynamicParameters();
    p.Add("P_OFFICE", USER.OFFICE_CODE, direction: ParameterDirection.Input);
    p.Add("P_DIVISION", USER.DIVISION, direction: ParameterDirection.Input);
    p.Add("RET", "", dbType: DbType.String, direction: ParameterDirection.ReturnValue, size: 4000);
    com.Execute_Func("FRT.NEW_DOCREF", ref p);
    TMP_NEW_DOCREF = p.Get<string>("RET");
    
```
