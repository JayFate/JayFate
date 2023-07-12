# work-plan




# toolkit 可以做的优化方案



1. 删除对小米 OPPO 的打包工具的集成
2. 在 IDE 切换路径时，才编译该路径对应的页面
3. 将 glob 检测到的 png 等图片资源在 app.js 中用 import 引入，使得 webpack 自动处理资源
3. 更完善的自动化测试方案

参考IDE显示模拟器传过来ws数据的逻辑，在测试中显示图片对比？

```txt
/Users/11104760/Documents/new-os/quickapp-ide

IDE仓库  https://gitlab.vmic.xyz/qafed/quickapp-ide

extensions/multi-device-previewer/frontend/src/helper/screen.js

```

5. 将 Vue、小程序转为快应用
6. 快应用 playground
7. Vite, Svelte 原理



# 其他

1. 支持 vue 的 dsl 及 composition-api



# 学习

1. 小程序、Vue、React
2. Rust
3. 算法、Leetcode


# vite

```ts
// 1. 简化 getDepHash 的查找链路
// 2. 优化 if (lockfilePath) {} 及上面的 lockfilePath ? fs$l.readFileSync(lockfilePath, 'utf-8') : '';
function getDepHash(config, ssr) {
    // 第一部分：获取配置文件初始化content
    const lockfilePath = lookupFile(config.root, lockfileNames);
    let content = lockfilePath ? fs$l.readFileSync(lockfilePath, 'utf-8') : '';
    // 第二部分：检测是否存在patches文件夹，增加content的内容
    if (lockfilePath) {
        //...
        const fullPath = path$o.join(path$o.dirname(lockfilePath), 'patches');
        const stat = tryStatSync(fullPath);
        if (stat?.isDirectory()) {
            content += stat.mtimeMs.toString();
        }
    }
    // 第三部分：将配置添加到content的后面
    const optimizeDeps = getDepOptimizationConfig(config, ssr);
    content += JSON.stringify({
        mode: process.env.NODE_ENV || config.mode,
        //...
    });
    return getHash(content);
}
```
