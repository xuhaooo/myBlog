# 一、介绍
WebStorm 是一个非常好用的 IDE。
当然你也可以使用 VSCode 或其他编辑器，自己喜欢、用的舒服即可。
# 二、硬件要求
使用 WebStorm 需要满足以下硬件条件：

- 内存至少 4G，当然多多益善
- CPU 至少 i5
- 系统盘（C）是 SSD 硬盘

如果没有达到要求，使用起来体验不会很好。
# 三、下载
去 WebStrom [官网](https://www.jetbrains.com/webstorm/)下载即可，可以免费使用 30 天。
# 四、配合使用 Cmder 或 Git Bash
如果你是 Mac 或 Linux 用户，可以跳过这一部分。
强烈建议 Windows 用户按下面的步骤进行配置，因为 WebStorm 默认的终端是 cmd，非常难用，建议换成 Cmder 或 Git Bash。
## 1. 配置终端

-  打开设置，依次进入 Tools ⇒ Terminal 
-  将 Shell Path 改为你的 bash.exe 的绝对路径，比如我的路径是 `C:\自己找路径\cmder\vendor\git-for-windows\bin\bash.exe`，如下图（如果找不对路径，可以使用 everything 软件搜索 bash.exe，从搜索结果里找和我的路径近似的）
![1.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287712568-ba6ff8b1-56e0-42bf-9f84-36bd8b699816.png#clientId=ufe32f1ab-28aa-4&from=paste&height=883&id=uca179c24&margin=%5Bobject%20Object%5D&name=1.png&originHeight=883&originWidth=1227&originalType=binary&ratio=1&size=47862&status=done&style=none&taskId=uba9f2747-efca-4b3d-8b38-3dc5423b625&width=1227)
-  建议 cmder 用户将提示符从 λ 改为 $（Git bash 用户请跳过此步骤），用 VSCode 打开文件 `C:\自己找路径\cmder\vendor\git-for-windows\etc\profile.d\[git-prompt.sh](http://git-prompt.sh/)`，改其中第 36 行，将 λ 改为 $
![1 1.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287736674-41b6792a-720b-43c1-9839-b514cbb2b592.png#clientId=ufe32f1ab-28aa-4&from=paste&height=274&id=uaf14e2dc&margin=%5Bobject%20Object%5D&name=1%201.png&originHeight=274&originWidth=894&originalType=binary&ratio=1&size=17866&status=done&style=none&taskId=ud7d354ec-3b39-4971-bbc8-ef33e8f7e7e&width=894)
-  这样之后就可以愉快地在 WebStorm 中使用终端了 
## 2.配置 Git

-  打开设置，依次进入 Version Control => Git 
-  将 Path to Git 改为 git.exe 的绝对路径，比如我的路径是 `C:\请自己找到对应的目录\cmder\vendor\git-for-windows\bin\git.exe`
![1 2.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287779016-5caa297d-cf4b-4c43-bdd2-873b174fc38b.png#clientId=ufe32f1ab-28aa-4&from=paste&height=883&id=uaf48a5c4&margin=%5Bobject%20Object%5D&name=1%202.png&originHeight=883&originWidth=1227&originalType=binary&ratio=1&size=54470&status=done&style=none&taskId=u465a63a0-2b00-4df7-92e7-9ec732b0f60&width=1227)
# 五、界面美化
## 1. 将用不到的界面隐藏起来
依次进入 View => Appearance，进行如下勾选
![1 3.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287787761-f972066a-3a3b-4569-843c-052ddfad493f.png#clientId=ufe32f1ab-28aa-4&from=paste&height=394&id=u36eb0600&margin=%5Bobject%20Object%5D&name=1%203.png&originHeight=394&originWidth=974&originalType=binary&ratio=1&size=26436&status=done&style=none&taskId=u4e0ff52f-0d72-4975-914c-f9e68573d71&width=974)
## 2. 安装 Material Theme UI 主题
依次进入 File => Settings => Plugins => Marketplace => 搜索 Material Theme UI 并安装
安装完成后进入 File => Settings => Appearance & Behavior => Material Theme，仿照我下面的配置即可
![1 4.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287799291-182e0608-5b4f-494f-832f-0f25b3d00ea7.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1162&id=u203e5871&margin=%5Bobject%20Object%5D&name=1%204.png&originHeight=1162&originWidth=1444&originalType=binary&ratio=1&size=43063&status=done&style=none&taskId=u97b57730-68bf-48e7-b069-0fc77138f5b&width=1444)
![1 5.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287807817-5a244518-b39f-4c90-9746-9149b677a922.png#clientId=ufe32f1ab-28aa-4&from=paste&height=475&id=uf302cd40&margin=%5Bobject%20Object%5D&name=1%205.png&originHeight=475&originWidth=1449&originalType=binary&ratio=1&size=14450&status=done&style=none&taskId=u770640a5-72b0-4233-be5a-da377b6c905&width=1449)
![1 6.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287824010-59cda14f-d7dc-45c6-9c24-792509aa1fd8.png#clientId=ufe32f1ab-28aa-4&from=paste&height=555&id=u1bfc0ac7&margin=%5Bobject%20Object%5D&name=1%206.png&originHeight=555&originWidth=1433&originalType=binary&ratio=1&size=12794&status=done&style=none&taskId=u9121ee5f-f29d-4d9c-a8bd-7088ed09794&width=1433)
![1 7.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287830386-53b166c7-9113-4cda-811b-58aab0871d13.png#clientId=ufe32f1ab-28aa-4&from=paste&height=790&id=ubbe52b43&margin=%5Bobject%20Object%5D&name=1%207.png&originHeight=790&originWidth=1455&originalType=binary&ratio=1&size=33244&status=done&style=none&taskId=u0d84ede5-1766-4137-bc7b-4e7f90c9cd8&width=1455)
![1 8.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287836752-94cf33a6-c3fa-466e-a580-3cc802cf97c9.png#clientId=ufe32f1ab-28aa-4&from=paste&height=574&id=u1a9e3981&margin=%5Bobject%20Object%5D&name=1%208.png&originHeight=574&originWidth=1463&originalType=binary&ratio=1&size=24301&status=done&style=none&taskId=u8bc68501-0aee-49f4-99d8-51622052407&width=1463)
## 3. 改变以下选项
![1 9.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287843852-296848dc-bd33-4544-96d0-1b8597e187a9.png#clientId=ufe32f1ab-28aa-4&from=paste&height=883&id=u633d7cc5&margin=%5Bobject%20Object%5D&name=1%209.png&originHeight=883&originWidth=1227&originalType=binary&ratio=1&size=46333&status=done&style=none&taskId=u63a13ffc-ba1f-490c-842f-12e86684293&width=1227)
# 六、代码美化
## 1. 挑选一个好看的字体配色
依次进入 Editor => Color Scheme，选择一个你喜欢的配色，点击 OK，就可以预览这个配色了，比如 Molokai 或 Darcula
## 2. 设置字体
将字体设置为 JetBrains Mono、Source Code Pro 或者 Fira Code，方法为：打开 Editor => Font，然后如下图所示设置一下
![1 10.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287857771-d583dc4e-a4cc-4947-ac51-7c4ba0836330.png#clientId=ufe32f1ab-28aa-4&from=paste&height=756&id=ue45843f5&margin=%5Bobject%20Object%5D&name=1%2010.png&originHeight=756&originWidth=1587&originalType=binary&ratio=1&size=62070&status=done&style=none&taskId=u03b007c7-ba09-4589-9ab2-e311a6b7ba3&width=1587)
注意需要把 Fallback 字体设置为 Microsoft Yahei 之类的中文字体
## 3. 还有 2 处字体需要设置

- 进入 Editor => Color Scheme => Color Scheme Font，取消勾选 Use color scheme font instead of ...
- 进入 Editor => Color Scheme => Console Font，取消勾选 Use color scheme font instead of ...
- 点击保存，这样一来，所有字体就统一了
# 七、快捷键 & Git 快捷操作
## 1. 查看快捷键

- 按两下 Shift，是的，按两下，你会得到一个搜索框，这个搜索框可以搜索任何东西
- 在搜索框里输入你想要的功能名称，比如 reformat （代码格式化），然后你就看到对应的操作（Action）
- Action 后面就跟着对应的快捷键

![1 11.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287872750-e8e809ef-0001-42af-bc11-2182257fbfdd.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1116&id=u919ba71e&margin=%5Bobject%20Object%5D&name=1%2011.png&originHeight=1116&originWidth=1924&originalType=binary&ratio=1&size=372144&status=done&style=none&taskId=u8f28886f-de85-449a-b3ee-064c02cef53&width=1924)
不过这个方式的缺点是只能搜英文，所以可以看第二个方式：查看菜单栏，快捷键就写在菜单栏每一项 Action 的后面
![1 11.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287885574-7d7ba67a-4167-4b28-96a3-aec8ea87dea5.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1116&id=u54ce693d&margin=%5Bobject%20Object%5D&name=1%2011.png&originHeight=1116&originWidth=1924&originalType=binary&ratio=1&size=372144&status=done&style=none&taskId=ue9e60664-57cb-4825-acf0-73fd12fef7d&width=1924)
## 2.修改快捷键
在 Settings 里的 keymap 里的搜索栏搜索即可
![1 13.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287901119-cb5e31f3-6b07-4a0e-949c-6a50acb9ed4a.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1583&id=uc98031e2&margin=%5Bobject%20Object%5D&name=1%2013.png&originHeight=1583&originWidth=2184&originalType=binary&ratio=1&size=200856&status=done&style=none&taskId=u63582ce6-f44f-4a04-9996-98a53005d8a&width=2184)
## 3. 常见设置
我的常用快捷键设置：（Mac 用户将 Ctrl 换成 Cmd）
如果设置时提示有冲突，可以将其他的快捷键 Remove

-  查找文件：Ctrl + P
![1 14.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287910595-17b5744f-5799-45eb-9348-1a4b2663c457.png#clientId=ufe32f1ab-28aa-4&from=paste&height=502&id=ub2563bdb&margin=%5Bobject%20Object%5D&name=1%2014.png&originHeight=502&originWidth=968&originalType=binary&ratio=1&size=21679&status=done&style=none&taskId=u0962d3b2-5431-419c-8180-5f22d9c0b8d&width=968)
-  项目文件列表窗口：Alt + 1
![1 15.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287924003-85bac394-9bbd-4d74-8d9f-260ac459968f.png#clientId=ufe32f1ab-28aa-4&from=paste&height=603&id=u66d397d5&margin=%5Bobject%20Object%5D&name=1%2015.png&originHeight=603&originWidth=1300&originalType=binary&ratio=1&size=34136&status=done&style=none&taskId=u3fc02a34-3a7e-4690-98d0-cec43cf1346&width=1300)
-  终端窗口：Alt + 2 
-  关闭当前窗口：Ctrl + W
![1 16.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287931081-6e231c69-e236-4ced-bc8b-cd95df57881b.png#clientId=ufe32f1ab-28aa-4&from=paste&height=875&id=u50f53983&margin=%5Bobject%20Object%5D&name=1%2016.png&originHeight=875&originWidth=1324&originalType=binary&ratio=1&size=46868&status=done&style=none&taskId=u66fcfd52-4def-423e-92f0-9c23d6d104e&width=1324)
-  在 Keymap 里将 Main Menu => Edit => Extend Selection 设为 Alt + W，将 Main Menu => Edit => Shrink Selection 设为 Alt + Shift + W，这两个快捷键自己试试，非常有用 
-  加强 Emmet
![1 17.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287937980-7b2d9c42-09b3-40a0-9de3-50629dd54334.png#clientId=ufe32f1ab-28aa-4&from=paste&height=299&id=ua4e3209b&margin=%5Bobject%20Object%5D&name=1%2017.png&originHeight=299&originWidth=960&originalType=binary&ratio=1&size=17249&status=done&style=none&taskId=u1a6544ea-3d18-4e8b-ac4d-3944fba79c1&width=960)
-  撤销与重做：撤销的默认快捷键是 Ctrl + Z，不需要改；但是重做的默认快捷键是 Ctrl + Shift + Z，建议在 keymap 里把给 redo 添加一个快捷键 Ctrl + Y 
-  最后，如果你忘记了快捷键，可以通过万能快捷键 Shift Shift 来搜索 
# 八、格式化代码
## 1. 初始化
在任意 JS 文件，使用 Show Reformat File Dialog 功能（快捷键你要自己用 Shift Shift 搜索一下），会弹出一个对话框
![1 18.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287948586-fbf21128-1c7a-4b9e-a771-c705fd143378.png#clientId=ufe32f1ab-28aa-4&from=paste&height=371&id=u3ae95e67&margin=%5Bobject%20Object%5D&name=1%2018.png&originHeight=371&originWidth=640&originalType=binary&ratio=1&size=32129&status=done&style=none&taskId=u1ba13f27-13d1-462c-bc5a-de98f73c91c&width=640)
我们一般选择 Whole file 来格式化整个文件，但如果当前文件是别人的代码，你可能就要选择 Only VCS changed text，以防修改别的人代码，只格式化刚写的代码
你可以在任何时候使用 Show Reformat File Dialog 功能重新弹出这个对话框进行修改配置
## 2. 快捷键
使用 Reformat Code 功能（快捷键你要自己用 Shift Shift 搜索一下），就会立即格式化当前文件
如果你对格式化后的文件不满意，那么你可以

-  进入 Editor => Code Style => TypeScript进行自定义（JavaScript同理），可以看我下面用红色箭头推荐的配置
![1 19.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287957839-18cfef71-9ad2-4e5b-bdde-adc135abdc64.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1399&id=u2e812364&margin=%5Bobject%20Object%5D&name=1%2019.png&originHeight=1399&originWidth=2122&originalType=binary&ratio=1&size=125134&status=done&style=none&taskId=u2e945f09-8e16-40ac-be72-9649ea5445b&width=2122)
![1 20.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287967727-d754e6ba-437f-4e0a-8da1-a3cfb08d8120.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1399&id=u672637ed&margin=%5Bobject%20Object%5D&name=1%2020.png&originHeight=1399&originWidth=2122&originalType=binary&ratio=1&size=180816&status=done&style=none&taskId=uc0ea8854-f48c-415e-ad2c-b4546251974&width=2122)
![1 21.png](https://cdn.nlark.com/yuque/0/2021/png/385743/1636287980959-97d0e5fa-e2c8-42ad-9d06-2ed911fd0d39.png#clientId=ufe32f1ab-28aa-4&from=paste&height=1399&id=u69233569&margin=%5Bobject%20Object%5D&name=1%2021.png&originHeight=1399&originWidth=2122&originalType=binary&ratio=1&size=191937&status=done&style=none&taskId=uc2a17404-7348-4d5e-8d86-5c9f1389cc2&width=2122)
-  可选：个人建议把 JS、CSS、SCSS、TypeScript、HTML 代码缩进全改成 2、2、2，这样代码更紧凑。建议 JS 不加分号，TS 加分号 
# 九、其他选项
可以开启以下功能（直接在 Shift Shift 后输入对应的英文即可开启）

- Show tree indent guides，这个功能会在编辑器里添加竖线，方便代码对齐
- Show method separators，这个功能会在每个方法上面添加横线，便于阅读代码
- Breadcrumbs，搜索这个选项，然后选择 Dont't Show，用于隐藏面包屑，你也可以右键点击面包屑查看更多选项
- Show CSS color preview as background

可以关闭以下功能

- Show gutter icons，关闭此功能可能让编辑器更简洁

可能用到的功能

- Soft wrap，用于折行
