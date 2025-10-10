## Tool 1-- Prettier

安装Prettier到项目中：
```
npm install --save-dev prettier
```
安装到开发环境，因为Prettier是一个代码格式化工具，我们只需要在开发环境中安装它即可。

Prettier的基本指令：
```
npx prettier --write "**/*.{js,jsx,ts,tsx,json,css,scss,md}"
```
这个指令会格式化项目中的所有JavaScript、TypeScript、JSON、CSS、SCSS和Markdown文件。

npx prettier --check .
```
这个指令会检查项目中的所有JavaScript、TypeScript、JSON、CSS、SCSS和Markdown文件是否符合Prettier的格式化规范。如果有不符合规范的文件，会输出错误信息。
