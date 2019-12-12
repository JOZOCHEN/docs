# vscode

## 目录树/搜索排除   
修改/.vscode/settings.json  
```
{
    "search.exclude": {
        "**/node_modules": true,
        "**/bower_components": true,
    },
    "files.exclude": {
        "**/.git": true,
        "**/.svn": true,
        "**/.hg": true,
        "**/CVS": true,
        "**/.DS_Store": true,
    }
}
```