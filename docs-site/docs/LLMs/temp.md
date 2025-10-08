


## Claude commonds
`/init` to create the 'claude.md' file.

`/compact` to compress the 'claude.md' file. make the AI concentrate

`/clear` to clear conversation history and free up context


when you talk, add `think` `think hard` `think harder` `ultra think`to let the AI think about the question.
`!` for the bash mode, and let the AI know if you installed an app and void repeat the installation.
`#` Add to memory and be AI's long-term memory.

`/ide`

`claude -p` to start the temp conversation.

`/agents` create a sub-agent for the project

`/resume`  

### mcp的基本命令

`claude mcp add mcpname` 添加一个新的MCP，查找网址：[awsome mcps](https://github.com/punkpeye/awesome-mcp-servers/blob/main/README-zh.md)

`claude mcp list` 查看所有MCP

`claude mcp remove mcpname` 删除一个MCP



### 权限管理

Allow, Deny 
还可以添加mcp ,用法：eg`mcp__neon`

### 自定义命令
在`.claude`文件中添加自定义命令文件夹，创建命令文件，文件的名字即为命令的名字，并使用自然语言描述这个命令要做的事情：
eg:
```dash title="code_review.md"
对比这个分支$ARGUMENTS，与main 分支的差异，提出review意见
```