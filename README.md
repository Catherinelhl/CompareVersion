# CompareVersion
This is a class about compare apk's version

```
 /**
     *
     * 0：数据异常，未完成比较
     * 1：需要
     * -1:不需要
     */
    fun compareVersion(currentVersion: String, remoteVersion: String): Int {
        //Step 1:判空
        if (TextUtils.isEmpty(currentVersion) || TextUtils.isEmpty(remoteVersion)) {
            return 0
        }
        //Step 2:判断是否相等
        if (currentVersion == remoteVersion) {
            return 0
        }
        //Step 3:拆分版本名
        val oldVersionArray = currentVersion.split(".")
        val remoteVersionArray = remoteVersion.split(".")
        //Step 4:获取最小长度值
        val minLen = oldVersionArray.size.coerceAtMost(remoteVersionArray.size)
        var diff = 0
        var index = 0
        //Step 5:循环进行单个字符串比较
        while (index < minLen
            && (oldVersionArray[index].toInt() - remoteVersionArray[index].toInt())
                .also { diff = it } == 0
        ) {
            index++
        }
        //Step 6:如果并没有比出大小，再比较多余的位数
        if (diff == 0) {
            for (i in index until oldVersionArray.size) {
                if (oldVersionArray[i].toInt() > 0) {
                    return -1
                }
            }
            for (i in index until remoteVersionArray.size) {
                if (remoteVersionArray[i].toInt() > 0) {
                    return 1
                }
            }
        }
        return if (diff > 0) -1 else 1
    }
    
 ```
