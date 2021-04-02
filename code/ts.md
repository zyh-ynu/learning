### TypeScript

---

是JavaScript 的一个超集，在编译时执行静态类型检查，js是一种解释型脚本语言，一边编译一边执行

[文档](https://www.typescriptlang.org/zh/docs/)   [代码](https://github.com/microsoft/TypeScript) 

##### nodejs环境中使用ts

```sh
# 安装 node
# 使用淘宝源
$ npm config set registry https://registry.npm.taobao.org
# 安装typescript
$ npm install -g typescript
# 编译成js代码 使用es6编译时加 --target es6
$ tsc --target es6 main.ts
# 执行js
$ node main.js
```

##### ts模块

ts任何包含顶级import或者export的文件都被当成一个模块。相反地，如果一个文件不带有顶级的import或者export声明，那么它的内容被视为**全局可见**的，因此对模块也是可见的，不需要显示导入。全局就是以`tsconfig.json`文件为根目录`baseUrl`的所有文件都能访问到。

[tsconfig](https://www.typescriptlang.org/zh/tsconfig) 

```json
/*tsconfig.json属性*/
/*设置编译结果中使用的模块化标准*/
"module": "commonjs",
/*用于设置解析非相对模块名称的基本目录，相对模块不会受到baseUrl的影响*/
"baseUrl": "./",
/*用于设置模块名到基于baseUrl的路径映射*/
"paths": {
    "*":["./node_modules/@types", "./typings/*"]
},
/*用于选择模块解析策略，有"node"和"classic"两种类型*/
"moduleResolution": "node",
```

[module resolution](https://www.typescriptlang.org/docs/handbook/module-resolution.html) 

```typescript
/*文件/root/src/moduleA.ts 模块解析 非相对导入 node类型*/
import { b } from "moduleB"

/*查找策略
/root/src/node_modules/moduleB.ts
/root/src/node_modules/moduleB.tsx
/root/src/node_modules/moduleB.d.ts
/root/src/node_modules/moduleB/package.json (if it specifies a "types" property)
/root/src/node_modules/@types/moduleB.d.ts
/root/src/node_modules/moduleB/index.ts
/root/src/node_modules/moduleB/index.tsx
/root/src/node_modules/moduleB/index.d.ts

/root/node_modules/moduleB.ts
/root/node_modules/moduleB.tsx
/root/node_modules/moduleB.d.ts
/root/node_modules/moduleB/package.json (if it specifies a "types" property)
/root/node_modules/@types/moduleB.d.ts
/root/node_modules/moduleB/index.ts
/root/node_modules/moduleB/index.tsx
/root/node_modules/moduleB/index.d.ts

/node_modules/moduleB.ts
/node_modules/moduleB.tsx
/node_modules/moduleB.d.ts
/node_modules/moduleB/package.json (if it specifies a "types" property)
/node_modules/@types/moduleB.d.ts
/node_modules/moduleB/index.ts
/node_modules/moduleB/index.tsx
/node_modules/moduleB/index.d.ts
*/
```

##### Map

```typescript
map.set() /*设置键值对，返回该 Map 对象*/
map.get() /*返回键对应的值，如果不存在，则返回 undefined*/
map.has() /*返回一个布尔值，用于判断 Map 中是否包含键对应的值*/
map.delete() /*删除 Map 中的元素，删除成功返回 true，失败返回 false*/
map.clear() /*移除 Map 对象的所有键/值对*/
map.size /*返回 Map 对象键/值对的数量*/
map.keys() /*返回一个 Iterator 对象， 包含了 Map 对象中每个元素的键 */
map.values() /*返回一个 Iterator 对象，包含了 Map 对象中每个元素的值*/
map.entries() /*返回一个 Iterator 对象，包含了 Map 对象中每个元素的键值对*/

let m = new Map()
m.set("aa", 1)
m.set("bb", 2)
m.set("cc", 3)
console.log(m.get("aa"))	//1
console.log(m.has("bb"))	//true
console.log(m.size)			//3

// 迭代 Map 中的 key
for (let key of m.keys()) {
    console.log(key)
}
// 迭代 Map 中的 value
for (let value of m.values()) {
    console.log(value)
}
// 迭代 Map 中的 key => value
for (let entry of m.entries()) {
    console.log(entry[0], entry[1])
}
// 使用对象解析
for (let [key, value] of m) {
    console.log(key, value)
}
```

