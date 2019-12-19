# vscode

## 目录树/搜索排除   
修改/.vscode/settings.json  
```
{
    /*以下文件不搜索*/
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
    },
    /*以下文件不在左侧目录显示*/
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true,
    }
}
```
## 头文件路径  
Crtl+Shift+P C/C++: Edit configurations(JSON)  
