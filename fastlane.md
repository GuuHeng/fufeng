## 关键词 iCloudContainerEnvironment
```
项目里用到了iCloud Services功能，在运行打包命令时报以下错误：
exportArchive: exportOptionsPlist error for key 'iCloudContainerEnvironment': expected one of {Development, Production}, but no value was provided

在项目中实际是找不到exportOptionsPlist文件的，需要在Fastfile文件中export_options中增加一个键值对 "iCloudContainerEnvironment": "Production或者Development"

```
