# 030 · ORTG · task-run

sphinx-doc__sphinx.e347e59c.test_ext_doctest.530dec5f.lv1

输入留存情况：事件未记录初始user；本episode内未发现独立正式输入文件

以下保留已记录的模型消息与工具活动；未完成记录不补写最终回复。

# Public model conversation

Private reasoning is omitted; credential-bearing content is redacted.

## 1. tool / event

```
{
  "name": "thread.started",
  "output": {
    "type": "thread.started",
    "session_ref": "ref-002700"
  }
}
```

## 2. tool / event

```
{
  "name": "error",
  "output": {
    "id": "item_0",
    "type": "error",
    "message": "`--dangerously-bypass-hook-trust` is enabled. Enabled hooks may run without review for this invocation."
  },
  "message_ref": "item_0"
}
```

## 3. tool / event

```
{
  "name": "error",
  "output": {
    "id": "item_1",
    "type": "error",
    "message": "`--dangerously-bypass-hook-trust` is enabled. Enabled hooks may run without review for this invocation."
  },
  "message_ref": "item_1"
}
```

## 4. tool / event

```
{
  "name": "turn.started",
  "output": {
    "type": "turn.started"
  }
}
```

## 5. assistant / message

```
对账结果：纲要与代码已对齐（2017 个文件对齐、0 个观察、0 个过期/无纲要，另忽略 3 个）。我先读取仓库纲要定位 doctest 实现与相关测试，再只恢复指定谓词并运行针对性验证。
```

## 6. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_4",
    "type": "mcp_tool_call",
    "server": "ortg",
    "tool": "ortg_overview",
    "arguments": {},
    "result": null,
    "error": null,
    "status": "in_progress"
  }
}
```

## 7. assistant / tool_call

```
{
  "name": "ortg_overview",
  "server": "ortg",
  "arguments": {},
  "call_ref": "item_4"
}
```

## 8. tool / tool_output

```
{
  "output": {
    "result": {
      "content": [
        {
          "type": "text",
          "text": "ortg: 当前为任务维护模式(task)。按当前任务阅读并维护相关源码纲要，无需先补齐全部文档；未覆盖文件继续保留裸行与未知状态，实时对账仍报告无纲要，不代表全库初始化完成。\n\n#ORTG-TSV: 2\n#====项目纲要====\n#【部署】Python 3.11+ 包，使用 Flit 构建并从 PyPI 安装；控制台入口为 sphinx-build、sphinx-quickstart、sphinx-apidoc、sphinx-autogen，也支持 python -m sphinx。文档以源目录、可选 conf.py、输出目录与 doctree 缓存目录运行；开发验证由 pytest、静态类型检查、Ruff 与 Node/Jasmine 工具链承担。\n#【系统】Sphinx 是以 Docutils 文档树为中间表示的可扩展文档生成器 | CLI 解析构建参数并创建应用；应用依次加载配置、内置与用户扩展、组件注册表、项目和缓存环境，再实例化 Builder；环境发现并解析源文档、持久化跨文档与域状态，Builder 按读取、缓存、一致性、引用解析和写出阶段生成 HTML、LaTeX、EPUB、文本、手册页等输出 | 必须保持配置及扩展注册先于环境与构建器、事件按稳定优先级驱动扩展、缓存版本或加载失败回退新环境、根文档与路径语义统一、读写并行由全部扩展安全声明共同决定、多输出格式隔离。\n#【整体规范】\n#纲要格式：文件名[标签]: Role:职责 | Uses:依赖 | API:对外契约 | Constraints:约束 ；文件名不带路径；四字段必填,无内容写-\n#骨架规则：只有裸文件名没有纲要的行是尚未建立认知的文件,读取时顺便生成纲要并调用 ortg_update 提交\n#目标规则：条目下一行 #目标: 是目标纲要(改完后应有的纲要,不写待核查事项)；#目标:删除 计划删除；#计划新建 文件尚不存在\n#测试契约规则：被测试锁定的对外行为写成\"必须保持 X(测试名)\"并写清期望结果；只涉及一个文件的写进它的 Constraints,跨模块的登记进【契约】；需求与守护测试冲突时按证据裁决:需求点名该测试或说旧行为错→改测试,需求说测试权威/行为不变/只是迁移→保持,有命令与期望输出的验收例→按实跑结果,都没有→先求两全,不能两全按需求实现,并把选择与理由记进纲要\n#契约规则：跨模块、不靠调用关系的约定(同一概念由多层共同实现、协议与消息格式、单位、兼容性、HTTP/WebSocket 路由与消息类型、配置键)在纲要头登记一行 #【契约】键：正文(正文写约定与守护测试,只写这一处)；每个参与文件在纲要行末尾加 | Keys:键(角色),… 声明它；路由、消息、事件、配置、环境变量类的键写成 route:/ws:/msg:/event:/topic:/cfg:/env: 加字面值\n#【契约】cfg:c_id_attributes：C 域环境配置，值为 list 或 tuple；扩展入口注册，C DefinitionParser 将这些名字交给公共 C-family 属性解析作为可直接跟随标识符的属性。\n#【契约】cfg:c_paren_attributes：C 域环境配置，值为 list 或 tuple；扩展入口注册，C DefinitionParser 将这些名字交给公共 C-family 属性解析作为带括号属性。\n#【契约】cfg:c_extra_keywords：C 域环境配置，值为 frozenset、list、set 或 tuple，默认含 C 头文件提供的宏式关键字；解析器禁止其成员作为标识符，并仅在已配置时把 bool、complex、imaginary 识别为基础类型。\n#【契约】cfg:c_maximum_signature_line_length：C 域环境配置，值为 int 或 None；对象指令以其非零值优先于全局 maximum_signature_line_length 决定参数列表多行显示，single-line-parameter-list 指令选项可强制单行。\n#【契约】cfg:cpp_id_attributes：C++ 域环境配置，值为 list 或 tuple；扩展入口注册，C++ DefinitionParser 将这些名字交给公共 C-family 属性解析作为额外的无括号属性。\n#【契约】cfg:cpp_paren_attributes：C++ 域环境配置，值为 list 或 tuple；扩展入口注册，C++ DefinitionParser 把这些名字识别为可带一个平衡括号内容的属性。\n#【契约】cfg:cpp_index_common_prefix：C++ 域环境配置，值为 list；builder-inited 时逆序排序，建立全局索引文本时从首个匹配项剥除前缀，不改变对象规范名与锚点。\n#【契约】cfg:cpp_maximum_signature_line_length：C++ 域环境配置，值为 int 或 None；对象指令以其非零值优先于全局 maximum_signature_line_length 决定参数列表多行显示，single-line-parameter-list 指令选项可强制单行。\n#【契约】cfg:cpp_debug_lookup：C++ 域布尔诊断配置；builder-inited 时写入 Symbol.debug_lookup，控制符号查找调试输出，不触发环境重建。\n#【契约】cfg:cpp_debug_show_tree：C++ 域布尔诊断配置；builder-inited 时写入 Symbol.debug_show_tree，控制符号树生命周期调试输出，不触发环境重建。\n#【契约】inventory:objects.inv：HTML Builder 系列写出对象清单，Intersphinx 读取；v1 为明文 Python 类型记录，v2 头依次声明格式、项目、版本和 zlib，压缩正文每行是 name、domain:objtype、priority、URI、display-name；v2 URI 尾随 $ 展开为对象名，display-name 等于全名时写 -，相对 URI 以 POSIX 规则拼接基址。写出按域和对象稳定排序并可把锚点末尾全名压成 $；读取保留 v1 锚点兼容、忽略无效类型，旧版重复 py:module 取首项，std:label/std:term 大小写冲突仅记 info。必须保持 HTML/dirhtml 清单 URI 与显示名、v1/v2/空版本解析和歧义诊断级别（test_build_html、test_build_dirhtml、test_read_inventory_v1、test_read_inventory_v2、test_read_inventory_v2_not_having_version、test_ambiguous_definition_warning）。\n#===代码纲要规范===\n#【标签】[C A B D… E] 重要度数字在前,其后层级、模块、特征(0到多个),规模,空格分隔,每个是一个大写字母(模块可两个)\n#A层级: E入口 C核心 S服务 D数据 I集成 U工具 T测试 B构建 X配置 O文档\n#B模块: C核心编排 B构建器与写出 D语义域与解析 X扩展生态 U基础工具 T测试体系 O文档与社区 P打包发布 L本地化与资源\n#C重要度: 9核心 8高频 7业务 5常规 3辅助 1边缘\n#D特征: C命令行 E扩展机制 P解析转换 H网页输出 A异步并行 I国际化 V版本兼容 S安全边界\n#E规模: L大>400 M中200-400 S小100-200 T微<100\n#Constraints配额: C9≤2000字 C8≤1200字 C7-4≤500字 C3-1≤100字\n#===代码纲要规范完毕===\n\nortg: 上面是纲要头，下面是模块清单（整份纲要估约 254135 token、2017 个文件，超过上下文窗口（258400 token）的一半）。按用户的问题用 ortg_overview 的 module 参数取相关模块的纲要（可多次，只发上下文里还没有的条目）；module=\"*\" 取全部。模块清单（B 标签 / 文件数 / 大小 / 已在上下文的条目数，模块名见纲要头 #B 字典）：\n- T  1114 个文件  约 99109 token  已在上下文 0\n- B  243 个文件  约 41355 token  已在上下文 0\n- L  261 个文件  约 33193 token  已在上下文 0\n- X  86 个文件  约 18563 token  已在上下文 0\n- D  51 个文件  约 14520 token  已在上下文 0\n- O  111 个文件  约 10780 token  已在上下文 0\n- U  41 个文件  约 10304 token  已在上下文 0\n- C  43 个文件  约 9485 token  已在上下文 0\n- P  67 个文件  约 7463 token  已在上下文 0\n## 对账报告\n- 对齐 2017, 观察 0, 忽略 3, 已清除 0\n\n纲要与代码已对齐。\n\n以上是模块清单，纲要正文还没发；按问题用 module 参数取。"
        }
      ],
      "structured_content": null
    },
    "error": null,
    "status": "completed"
  },
  "call_ref": "item_4"
}
```

## 9. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_6",
    "type": "mcp_tool_call",
    "server": "ortg",
    "tool": "ortg_overview",
    "arguments": {
      "module": "X"
    },
    "result": null,
    "error": null,
    "status": "in_progress"
  }
}
```

## 10. assistant / tool_call

```
{
  "name": "ortg_overview",
  "server": "ortg",
  "arguments": {
    "module": "X"
  },
  "call_ref": "item_6"
}
```

## 11. tool / tool_output

```
{
  "output": {
    "result": {
      "content": [
        {
          "type": "text",
          "text": "ortg: 当前为任务维护模式(task)。按当前任务阅读并维护相关源码纲要，无需先补齐全部文档；未覆盖文件继续保留裸行与未知状态，实时对账仍报告无纲要，不代表全库初始化完成。\n\n#代码纲要\n\n===/testbed/doc/usage/advanced/websupport/===\napi.rst[7 O X S]: Role:说明 sphinxcontrib.websupport.WebSupport 的构建、文档读取、评论、投票与搜索主接口及目录和适配器参数 | Uses:doc/usage/advanced/websupport/searchadapters.rst, doc/usage/advanced/websupport/storagebackends.rst | API:- | Constraints:所有 Web Support 交互经 WebSupport；未提供 storage 时创建 SQLite；staticdir 非 /static 时通常同步设置 staticroot；该类已移至独立 sphinxcontrib-websupport 依赖\nindex.rst[5 O X T]: Role:作为将 Sphinx 文档嵌入 Web 应用的 sphinxcontrib-websupport Python API 指南入口 | Uses:doc/usage/advanced/websupport/quickstart.rst, doc/usage/advanced/websupport/api.rst, doc/usage/advanced/websupport/searchadapters.rst, doc/usage/advanced/websupport/storagebackends.rst | API:- | Constraints:Web Support 功能由 sphinxcontrib-websupport 提供\nquickstart.rst[7 O X H M]: Role:指导用 sphinxcontrib WebSupport 构建文档数据并将页面、搜索、认证、评论、投票和审核接入 Web 应用 | Uses:doc/usage/advanced/websupport/api.rst, doc/usage/advanced/websupport/searchadapters.rst, doc/usage/advanced/websupport/storagebackends.rst | API:- | Constraints:构建目录包含 data 与默认从 /static 服务的 static；每套文档复用一个 WebSupport 实例；get_document 与 get_search_results 返回同形模板上下文；用户名必须唯一，改名须调用 update_username；直接挂节点的评论 parent_id 为空，回复评论的 node_id 为空；投票应要求认证，审核身份由宿主应用决定并传入\nsearchadapters.rst[5 O X S]: Role:说明通过继承 BaseSearch 并传给 WebSupport 创建自定义 Web Support 搜索适配器 | Uses:doc/usage/advanced/websupport/api.rst | API:- | Constraints:自定义类必须实现 add_document 与 handle_query；BaseSearch 位于 sphinxcontrib.websupport.search\nstoragebackends.rst[5 O X S]: Role:说明通过继承 StorageBackend 并传给 WebSupport 创建自定义评论与投票存储后端 | Uses:doc/usage/advanced/websupport/api.rst | API:- | Constraints:StorageBackend 位于 sphinxcontrib.websupport.storage；后端契约涵盖构建前后、节点、评论、数据、投票、用户名及审核操作\n\n===/testbed/doc/usage/extensions/===\napidoc.rst[7 O X E S]: Role:说明 apidoc 扩展如何在构建期间扫描 Python 包、生成 autodoc 源文件并以配置控制目录、过滤和页面布局 | Uses:sphinx/ext/apidoc/, sphinx/ext/autodoc/ | API:- | Constraints:apidoc_modules 每项必须提供 path 与相对源目录的 destination，未给键回退到全局 apidoc 配置；path 可绝对或相对配置目录；生成源最终由 autodoc 导入模块，导入副作用会执行，脚本主逻辑应受 __main__ 守卫；PEP 420 隐式命名空间须显式启用\nautodoc.rst[9 O X E L]: Role:定义 autodoc 通过导入和内省生成模块、类、函数、数据与类型别名文档的指令、成员筛选、类型呈现和事件扩展契约 | Uses:sphinx/ext/autodoc/, sphinx/domains/python/, sphinx/ext/napoleon/, sphinx/events.py | API:- | Constraints:autodoc 会真实导入目标及执行副作用，源码须可导入且脚本入口应受 __main__ 守卫；#: 文档注释同行只能单行，多行必须紧邻定义之前，定义后 docstring 只能在下一行；默认只纳入有文档的公开自有成员，__all__ 决定模块公开集，imported-members 不会发现导入模块属性；指令级成员列表覆盖默认值，前置 + 才扩展，no-选项可禁用默认；no-index 禁止目标而 no-index-entry 仅抑制索引；bysource 要求可用 Python 源；装饰器替换函数时须复制 __doc__，否则无法取文档；inherited-members 参数表示排除哪些基类成员，无参数默认排除 object 而 None 纳入；annotation 与 no-value 同时使用时前者优先；type_aliases 仅配合延迟注解；docstring lines 与 bases 事件就地修改，signature 事件返回替代元组，skip-member 采用首个非 None 返回值\nautosectionlabel.rst[5 O X E S]: Role:说明 autosectionlabel 如何从章节标题自动生成 ref 标签及其消歧、深度和调试配置 | Uses:sphinx/ext/autosectionlabel.py | API:- | Constraints:默认同名标题可能任取一个目标；prefix_document 为真时标签格式为 docname:标题；maxdepth=None 标记全部层级；-vvv 输出生成标签供排查未定义引用\nautosummary.rst[8 O X E L]: Role:定义 autosummary 摘要表、autodoc 存根生成、递归扫描、模板上下文和 autolink 行为 | Uses:sphinx/ext/autosummary/, sphinx/ext/autodoc/, sphinx/ext/autosummary/templates/autosummary/, doc/man/sphinx-autogen.rst | API:- | Constraints:摘要和签名经过 autodoc-process-docstring 与 autodoc-process-signature；toctree 选项既纳入目录也指定存根输出位置；autosummary_generate 默认开启且 overwrite 默认覆盖既有存根；ignore_module_all 为假时只文档化 __all__ 所列成员并使 imported_members 对这些成员失效；大小写不敏感文件系统的对象冲突须用 filename_map；模板使用 RST 转义的 escape 而非 HTML escape；autolink 解析失败静默退化为强调且同名对象可能误链\ncoverage.rst[7 O X E S]: Role:说明 CoverageBuilder 如何统计 Python 与 C API 文档覆盖率及筛选和报告配置 | Uses:sphinx/ext/coverage.py, doc/man/sphinx-apidoc.rst | API:- | Constraints:Builder 会导入模块并执行导入副作用；目标须在 sys.path；未设 coverage_modules 时仅统计已知 py:module 或 automodule；忽略项为匹配完整导入路径任意部分的正则\ndoctest.rst[7 O X E L]: Role:定义 doctest Builder 的分组执行模型、测试与输出指令、条件跳过和全局运行配置 | Uses:sphinx/ext/doctest.py, sphinx/ext/autodoc/ | API:- | Constraints:每个文档内各组先执行全部 setup、再按出现顺序执行测试并最后 cleanup，空组名为 default 而 * 属于所有组；testcode 整块执行，裸表达式不产出且普通输出不能与异常消息混合；skipif 作为 Python 表达式求值，为真时指令如同不存在；标准 RST doctest 块不能含空行且只有 doctest 指令能局部剥离 BLANKLINE 和 flags；doctest_path 必须使用绝对路径；默认比较允许省略号、忽略异常细节并拒绝 True 代替 1\nduration.rst[3 O X E T]: Role:介绍统计 Sphinx 各文档处理耗时并在构建末尾报告的 duration 扩展 | Uses:sphinx/ext/duration.py | API:- | Constraints:用于定位构建缓慢的文档\nexample_google.py[3 O X M]: Role:提供可下载的 Google 风格 docstring 示例，覆盖模块变量、函数、生成器、异常、类属性、属性方法和 PEP 526 注解 | Uses:doc/usage/extensions/napoleon.rst, doc/usage/extensions/example_google.rst | API:- | Constraints:Google 风格章节以带冒号标题和缩进正文组成；模块变量、构造器和属性各自只选类/模块级或内联一种位置记录且保持一致；Args 不列 self 但须原样列 *args 与 **kwargs；生成器使用 Yields；property 文档写在 getter；私有和特殊有 docstring 成员是否纳入由 Napoleon 对应配置控制\nexample_google.rst[3 O X T]: Role:展示并可下载 Napoleon 支持的 Google 风格 Python docstring 完整示例 | Uses:doc/usage/extensions/example_google.py, doc/usage/extensions/example_numpy.rst | API:- | Constraints:下载链接仅在 HTML Builder 中出现，正文通过 literalinclude 引用同目录 Python 源\nexample_numpy.py[3 O X M]: Role:提供可下载的 NumPy 风格 docstring 示例，覆盖模块变量、函数、生成器、异常、类属性和属性方法 | Uses:doc/usage/extensions/napoleon.rst, doc/usage/extensions/example_numpy.rst | API:- | Constraints:NumPy 风格章节由标题与等长下划线组成，通常以两个空行分节；Parameters 不列 self 但须原样列 *args 与 **kwargs；Returns 的类型必填且即使已有 PEP 484 返回注解也重复；生成器使用 Yields；模块变量、构造器与属性文档位置不可混用，property 文档写在 getter\nexample_numpy.rst[3 O X T]: Role:展示并可下载 Napoleon 支持的 NumPy 风格 Python docstring 完整示例 | Uses:doc/usage/extensions/example_numpy.py, doc/usage/extensions/example_google.rst | API:- | Constraints:下载链接仅在 HTML Builder 中出现，正文通过 literalinclude 引用同目录 Python 源\nextlinks.rst[7 O X E S]: Role:说明 extlinks 如何用配置别名将短角色目标展开为重复使用的外部 URL 与标题 | Uses:sphinx/ext/extlinks.py | API:- | Constraints:extlinks 映射值为含一个 %s 的基础 URL及可空标题；标题为 None 时显示完整 URL，显式标题覆盖配置标题，字面百分号写 %%；硬编码链接检测默认关闭\ngithubpages.rst[5 O X E T]: Role:说明 githubpages 扩展为生成的 HTML 创建 GitHub Pages 控制文件 | Uses:sphinx/ext/githubpages.py | API:- | Constraints:总是生成 .nojekyll；仅设置 html_baseurl 自定义域名时生成 CNAME\ngraphviz.rst[7 O X E S]: Role:说明 graphviz、graph、digraph 指令如何调用 Graphviz 为 HTML 和 LaTeX 渲染内嵌或外部图 | Uses:sphinx/ext/graphviz.py | API:- | Constraints:绝对外部图路径按源目录相对解析；HTML 只支持 PNG 或 SVG，LaTeX 输出 PDF；graph 和 digraph 名称原样传入 Graphviz，含非字母数字字符时须双引号；SVG 内 URL 要可用须在 DOT 链接设置合适 target；graphviz_dot 的机器相关路径宜通过 -D 提供\nifconfig.rst[5 O X E S]: Role:说明 ifconfig 指令如何按项目配置命名空间中的 Python 表达式条件包含正文 | Uses:sphinx/ext/ifconfig.py, sphinx/application.py | API:- | Constraints:ifconfig 仅控制内容，不能控制章节、标签等结构；自定义配置值应以 rebuild='env' 注册以在变化时重读文档\nimgconverter.rst[5 O X E S]: Role:说明 imgconverter 如何调用 ImageMagick 将文档图像转换为 Builder 支持的格式及命令配置 | Uses:sphinx/ext/imgconverter.py | API:- | Constraints:未安装 ImageMagick 时扩展不可工作；SVG 经 ImageMagick 转换会栅格化并失去缩放性；Unix 默认 convert，Windows 默认 magick 且附加 convert 参数\nindex.rst[7 O X S]: Role:组织 Sphinx 内置扩展文档并说明社区扩展的发现、安装位置和项目内模块搜索路径配置 | Uses:sphinx/ext/, doc/extdev/index.rst | API:- | Constraints:内置扩展通过 extensions 配置按模块名启用；项目本地扩展目录须显式加入 sys.path；第三方扩展既可位于项目内也可正常安装到 site-packages\ninheritance.rst[7 O X E M]: Role:说明 inheritance-diagram 如何导入模块或类、遍历继承关系并经 Graphviz 生成可配置图 | Uses:sphinx/ext/inheritance_diagram.py, sphinx/ext/graphviz.py, sphinx/domains/python/ | API:- | Constraints:非限定类名按当前 py:module 解析；parts 正数保留右侧段、负数删除左侧段；默认排除下划线开头基类，private-bases 可纳入；top-classes 截断向上遍历，但同模块祖先可能仍显示为孤立节点，需只列目标类以规避；include-subclasses 纳入后代但不加入模块中其他无关类；inheritance_alias 以完全限定类名映射展示名\nintersphinx.rst[8 O X E M]: Role:说明 Intersphinx 通过对象清单为缺失引用或 external 角色解析外部项目目标及其缓存、筛选和诊断 | Uses:sphinx/ext/intersphinx/, sphinx/util/inventory.py | API:- | Constraints:每个 HTML 构建生成 objects.inv；mapping 键必须唯一，目标相对路径按构建输出根解释而 inventory 相对路径按源目录解释；多个 inventory 依次取首个成功项；普通引用只在本项目未命中时回退且受 disabled_reftypes 限制，显式 external 不受该限制并只查外部；缓存负天数表示无限期；超时是服务器无响应间隔而非总下载期限；Basic Auth 凭据从生成链接剥离\nlinkcode.rst[5 O X E S]: Role:说明 linkcode 如何按域对象信息调用用户解析器并为描述项添加外部源码链接 | Uses:sphinx/ext/linkcode.py | API:- | Constraints:linkcode_resolve(domain, info) 返回 URL 或 None；py、c、cpp、javascript 域保证的 info 键不同；第三方域须用 add_linkcode_domain 登记信息键\nmath.rst[7 O X H M]: Role:说明 HTML 数学以 imgmath 图像、MathJax 或旧 jsMath 渲染时的工具链和配置契约 | Uses:sphinx/ext/imgmath.py, sphinx/ext/mathjax.py, sphinx/templates/imgmath/ | API:- | Constraints:imgmath 先运行 LaTeX 再按 PNG/SVG 调用 dvipng/dvisvgm，预览深度需 preview 包；imgmath_latex 只放可执行文件，附加参数必须放 latex_args；dvilualatex 或 xelatex 路径要求 SVG，xelatex 还需 -no-pdf 且不支持 latexmk -xelatex；MathJax 内容必须用 Sphinx math 指令/角色而非原生分隔符；相对 mathjax/jsmath 路径基于构建 _static；MathJax 2 与 3 配置入口不同\nnapoleon.rst[7 O X E L]: Role:说明 Napoleon 如何把 Google 与 NumPy 风格 docstring 预处理为 reStructuredText 并以配置控制成员、章节、字段和类型转换 | Uses:sphinx/ext/napoleon/, sphinx/ext/autodoc/, doc/usage/extensions/example_google.py, doc/usage/extensions/example_numpy.py | API:- | Constraints:Napoleon 在 autodoc 解析前转换但不改源码 docstring；Google 以缩进分节、NumPy 以标题下划线分节，同一项目不应混用风格；私有成员默认不纳入而有文档的特殊成员默认纳入，构造器单独列出默认关闭；singular Note 始终转为 note 指令而 Notes 才受 admonition 配置控制；type_aliases 仅在 use_param 为真时生效；属性 docstring 无类型时可由启用的 PEP 526 类注解补足；自定义章节可作为通用、现有别名、参数式或返回式呈现\ntodo.rst[5 O X E S]: Role:说明 todo 与 todolist 指令、显示和警告配置以及 todo-defined 事件 | Uses:sphinx/ext/todo.py | API:- | Constraints:todo_include_todos 默认为假并同时控制两类指令是否输出；todo_link_only 隐藏文件路径与行号；todo-defined 在定义项目时携带 todo_node 发出\nviewcode.rst[7 O X E S]: Role:说明 viewcode 为 Python 对象生成带高亮源码页、双向链接及可替代导入的事件契约 | Uses:sphinx/ext/viewcode.py | API:- | Constraints:默认导入模块并执行副作用；支持 HTML 类 Builder 但排除 singlehtml，EPUB 默认关闭；find-source 返回源码与对象类型及行区间映射；follow-imported 解析导入成员原模块\n\n===/testbed/sphinx/ext/===\n__init__.py[3 C X E T]: Role:标识包含默认不启用 Sphinx 功能的内置扩展包 | Uses:- | API:- | Constraints:扩展须由配置或其他扩展显式加载\nautosectionlabel.py[7 S X E S]: Role:把文档章节标题自动登记为标准域 ref 标签并支持文档名前缀和深度限制 | Uses:sphinx/domains/std/__init__.py, sphinx/util/nodes.py, sphinx/environment/__init__.py | API:setup(app) | Constraints:标签名取标题 rawsource 并规范化，显示名取清理后的标题；启用 prefix_document 时以 docname:标题命名；maxdepth 非空时深度大于等于该值的章节不登记；重复名告警但仍覆盖标准域 labels 与 anonlabels。必须保持普通与文档前缀标签链接、智能引号显示以及 maxdepth=3 时前三层可解析而第四层产生 undefined label（test_ext_autosectionlabel.py）\ncoverage.py[8 C X E P L]: Role:实现 coverage Builder，通过运行时内省 Python 包和正则扫描 C 头文件报告未文档化 API、覆盖率统计及可机读结果 | Uses:sphinx/builders/__init__.py, sphinx/domains/python/, sphinx/domains/c/, sphinx/util/inspect.py, sphinx/_cli/util/colour.py | API:CoverageBuilder、setup(app)；builder 名 coverage | Constraints:会真实递归导入 coverage_modules 及子包并可能执行副作用，跳过 __main__；未配置模块清单时只扫描已文档化模块，显式配置时同时警告配置外已文档化模块和配置内未文档化模块，导入失败进入报告而不中断；模块/函数/类忽略正则用 match，coverage_ignore_pyobjects 对完整限定名用 search；Python 仅检查目标模块自己定义的公开函数和类，已文档化类再检查自身字典中的公开方法，coverage_skip_undoc_in_source 可排除源码无 docstring 项；C 文件按配置 glob，正则首捕获组为对象名，分类别应用忽略规则；每次写 python.txt、c.txt，finish 以固定四元组 py_undoc/c_undoc/py_undocumented/py_documented 写 undoc.pickle；统计表按模块排序、百分比两位小数，无对象模块为 100%，全空 TOTAL 文本为 100；coverage_show_missing_items 在正常 verbosity 写彩色状态，负 verbosity 改写 warning。必须保持报告标题、表格边框和空行、未文档化函数/类/方法分组、C 类型右对齐、pickle 结构及普通/quiet 日志精确文本（test_ext_coverage.py）\ndoctest.py[8 C X E P L]: Role:提供执行文档代码示例并比较输出的 doctest Builder 与 testsetup、testcleanup、doctest、testcode、testoutput 指令 | Uses:sphinx/builders/__init__.py, sphinx/util/docutils.py | API:TestDirective、TestsetupDirective、TestcleanupDirective、DoctestDirective、TestcodeDirective、TestoutputDirective、TestGroup、TestCode、SphinxDocTestRunner、DocTestBuilder、setup(app)；builder 名 doctest；五个同名指令 | Constraints:当前源码的指令 run、TestGroup/TestCode 初始化及 Builder 执行、统计、报告主体被遮罩，具体实现未知，不得据接口补造；可见初始化会把 doctest.compile 全局替换为 Builder.compile、把 doctest_path 前插 sys.path、打开 UTF-8 output.txt并写带当前时间的标题，所有发现文档均视为过期且目标 URI 为空；公开文档规定同一文档各组先执行全部 setup、再按出现顺序执行测试、最后 cleanup，空组名为 default而 * 归入所有组，skipif 真值使对应指令不参与，testcode 整块执行且由 testoutput 给预期输出；默认 flags 为 DONT_ACCEPT_TRUE_FOR_1、ELLIPSIS、IGNORE_EXCEPTION_DETAIL，doctest_fail_fast 默认假，成功展示默认真，扩展只声明并行读取安全；pyversion、hide、trim/no-trim 和 options 的可见选项由各指令分别限制。遮罩区域中的异常处理、命名空间共享、失败计数、状态码、output.txt 其余格式及 fail-fast 细节未知\nduration.py[5 S X E S]: Role:测量每个文档的读取耗时并在构建结束时报告最慢文档 | Uses:sphinx/domains/__init__.py, sphinx/application.py, sphinx/environment/__init__.py | API:DurationDomain、setup(app) | Constraints:builder-inited 必须清除上次构建数据，source-read 使用 monotonic 记录起点而 doctree-read 计算当前文档时长；并行合并只接受指定 docnames；构建结束按耗时降序最多输出五项且固定三位小数，无记录时不输出标题。必须保持状态输出含 slowest reading durations 且文档行格式为三位小数加 docname（test_ext_duration.py）\nextlinks.py[7 C X E P S]: Role:从 extlinks 配置动态注册外链角色，并可诊断能改写为这些角色的硬编码外链 | Uses:sphinx/transforms/post_transforms/__init__.py, sphinx/util/nodes.py, sphinx/util/rst.py, sphinx/application.py | API:make_link_role()、ExternalLinksChecker、setup(app) | Constraints:base URL 与非空 caption 都按 %s 替换角色目标，caption=None 时隐式标题显示完整 URL，显式标题始终优先；生成 reference 必须 internal=False 并带 extlink-<name> 类；硬编码检测默认关闭，只检查无 internal 且有 refuri 的引用，匹配值不得含斜杠，同一 URI 命中多个模板时每个都告警，显式显示文字须 RST 转义后进入建议。必须保持关闭时零警告、三类隐式/内联/命名链接的精确建议及多个可替换模板产生全部六条警告（test_ext_extlinks.py）\ngithubpages.py[5 I X E T]: Role:为 HTML 输出维护 GitHub Pages 所需的 .nojekyll 与自定义域 CNAME 文件 | Uses:sphinx/application.py, sphinx/builders/html/__init__.py | API:setup(app) | Constraints:仅 format=html 的构建器执行；每次都创建 .nojekyll，html_baseurl 有非 *.github.io 主机名时写 CNAME 且不带末尾换行，否则删除已有 CNAME。必须保持默认和 github.io 域不生成 CNAME，自定义域文件内容仅为 hostname（test_ext_githubpages.py）\ngraphviz.py[8 C X E H L]: Role:实现 Graphviz 扩展，将内联或外部 DOT 图经 dot 渲染为 HTML PNG/SVG、LaTeX PDF、Texinfo PNG，并为文本输出提供替代描述 | Uses:sphinx/application.py, sphinx/util/i18n.py, sphinx/writers/html5.py, sphinx/writers/latex.py, sphinx/templates/graphviz/ | API:GraphvizError、ClickableMapDefinition、graphviz 节点、Graphviz、GraphvizSimple、render_dot()、render_dot_html()、render_dot_latex()、render_dot_texinfo()、setup(app)；指令 graphviz、graph、digraph | Constraints:外部 DOT 文件按语言查找并登记依赖，指令不得同时给文件和正文；layout 覆盖旧 graphviz_dot 选项；渲染缓存键包含源码、选项、dot 命令及参数，PNG 同时生成 cmapx，SVG 须把相对图像与链接改为相对输出图片目录；命令不存在只警告且同一 Builder 不再重试，命令失败或未产物抛 GraphvizError；HTML 输出格式仅支持 png/svg，LaTeX 固定 PDF，Texinfo 固定 PNG。必须保持 caption/align/class、PNG map、SVG 相对路径、LaTeX 内联与 figure 输出，以及空 map 的 %3 ID 由 DOT 内容哈希稳定替换（test_ext_graphviz.py）；本地验证盲区：真实渲染测试在 Graphviz 命令不可启动时由 if_graphviz_found 跳过\nifconfig.py[7 C X E P T]: Role:实现按项目配置 Python 表达式条件保留或删除文档内容的 ifconfig 指令 | Uses:sphinx/util/docutils.py, sphinx/config.py, sphinx/application.py | API:ifconfig 节点、IfConfig、setup(app)；指令 ifconfig | Constraints:表达式在包含全部配置值、配置对象属性和 builder 名的命名空间求值；真值用原子节点子项替换包装，假值删除全部子项，求值异常转换为带原异常类别文本的 reporter error；指令内容允许章节且须保留来源行号。必须保持真假分支只输出 spam 不输出 ham，并使正文第 3 行引用报告 index.rst:3（test_ext_ifconfig.py）\nimgconverter.py[7 I X E P S]: Role:注册基于 ImageMagick 的图像后转换器，把 Builder 不支持的 SVG、GIF、PDF、Illustrator 和 WebP 输入栅格化为 PNG | Uses:sphinx/transforms/post_transforms/images.py, sphinx/errors.py | API:ImagemagickConverter、setup(app) | Constraints:可用性探测以配置命令加 -version 运行，命令缺失或非零均警告并返回假；转换命令参数顺序为可执行文件、image_converter_args、带 [0] 的源路径、目标路径，以确保动画或多页输入只取首帧/首页；启动失败警告并返回假，子进程非零则把 stderr/stdout 包装为 ExtensionError；Windows 默认 magick 且参数含 convert，其他平台默认 convert 且无附加参数，两项配置均触发 env 重建；声明并行读写安全。必须保持 LaTeX 已支持 PDF 原样使用而 SVG 转为 PNG且不复制原 SVG（test_ext_imgconverter.py）；本地验证盲区：真实转换测试在 image_converter 命令不可执行时跳过\nimgmath.py[8 C X E H L]: Role:实现 imgmath HTML 数学渲染器，将 LaTeX 公式经 latex/tectonic 与 dvipng 或 dvisvgm 转为缓存图片或内嵌 data URI | Uses:sphinx/application.py, sphinx/util/math.py, sphinx/util/png.py, sphinx/util/template.py, sphinx/templates/imgmath/ | API:MathExtError、InvokeError、read_svg_depth()、write_svg_depth()、generate_latex_macro()、compile_math()、convert_dvi_to_image()、convert_dvi_to_png()、convert_dvi_to_svg()、render_math()、render_maths_to_base64()、setup(app)；数学渲染器 imgmath | Constraints:格式只接受 png/svg；模板先查用户 templates_path 的 .jinja 与兼容 _t，再用内置模板；输出文件名取完整 LaTeX 文本哈希，preview 模式把基线深度写入 PNG 元数据或 SVG 末尾注释并用于内联垂直对齐；命令缺失只警告并使当前 Builder 后续公式回退文本，命令存在但执行失败抛带 stdout/stderr 的 MathExtError；xelatex/tectonic 产出 XDV，SVG tightpage 使用 dvips；embed 成功构建后删除中间 math 图片目录，失败构建保留。必须保持 PNG/SVG 文件输出、SVG base64 内嵌、公式编号链接与 alt 文本（test_ext_math.py）；本地验证盲区：PNG/SVG 真实渲染分别在 dvipng、dvisvgm 或 LaTeX 命令不可用时跳过\ninheritance_diagram.py[8 C X E P H L]: Role:导入类或模块、遍历继承与可选子类关系，生成带 Python 对象链接的 Graphviz 继承图并接入 HTML、LaTeX 和 Texinfo 写出 | Uses:sphinx/ext/graphviz.py, sphinx/domains/python/, sphinx/util/docutils.py, sphinx/builders/html/__init__.py, sphinx/builders/latex/__init__.py | API:InheritanceException、InheritanceGraph、InheritanceDiagram、inheritance_diagram、import_classes()、try_import()、setup(app)；指令 inheritance-diagram | Constraints:导入先尝试当前 py:module 加输入名再尝试绝对名，会真实导入并执行模块副作用；模块入口只收定义于该模块自身的类，类入口只返回该类，缺失目标、非类非模块及最终无类均抛 InheritanceException并由指令降为文档警告；默认排除内置类和下划线开头基类，private-bases 才纳入后者，include-subclasses 递归遍历运行时 __subclasses__；parts 正数保留右侧段，负数删除左侧段，0 显示完整名；inheritance_alias 同时改节点名和用于关系/链接的 fullname；top-classes 按处理后的 fullname 截止上溯但不移除已由模块入口先加入的祖先；tooltip 取 docstring 首个非空行并转义双引号，异常静默忽略；DOT 节点、边和属性稳定排序，默认属性先被调用参数覆盖、再被配置覆盖；指令为每个完整类名创建 py:class 待解析引用，caption 时包装 figure且 name 落在 figure，否则落在图节点；图哈希只取原始类名文本和 parts；HTML 外部引用按 URI 片段匹配类名，内部 SVG 链接带当前输出文件名而 PNG image map 使用页内片段；LaTeX/Texinfo 强制默认 6×6 图尺寸但配置仍可覆盖，text/man 跳过节点。必须保持模块/类/当前模块导入的返回与错误语义、基础/parts/top-classes/嵌套类图元组、alias 后继承边，以及 PNG/SVG 外部和相对链接、caption HTML 与 LaTeX figure 输出（test_ext_inheritance_diagram.py）；本地验证盲区：渲染测试在 Graphviz 不可用时跳过\nlinkcode.py[7 C X E S]: Role:为已登记对象描述调用用户解析器并在签名后附加外部源码链接 | Uses:sphinx/addnodes.py, sphinx/errors.py, sphinx/application.py, sphinx/builders/__init__.py | API:add_linkcode_domain()、LinkcodeError、setup(app) | Constraints:linkcode_resolve 必须为可调用对象，否则 doctree-read 抛 LinkcodeError；内置 py、c、cpp、js 域各只传约定的签名属性字典，未登记域跳过；解析器返回假值不加链接，同一 desc 内相同 URI 只加一次；链接文字为 [source] 且置于 only 节点，表达式默认 html 但 Builder.supported_linkcode 可覆盖；add_linkcode_domain 默认不覆盖已有域，override=True 才替换且复制 keys。必须保持 Python、JavaScript、C、C++ 与扩展登记的 RST 对象均生成对应外部 URL（test_linkcode）\nmathjax.py[8 I X H E S]: Role:注册 MathJax HTML 数学渲染器，输出内联与块级公式标记并按页面需要注入配置和脚本 | Uses:sphinx/util/math.py, sphinx/builders/html/__init__.py, sphinx/writers/html5.py, sphinx/errors.py | API:MATHJAX_URL、html_visit_math()、html_visit_displaymath()、install_mathjax()、setup(app)；数学渲染器 mathjax | Constraints:仅 format=html 且实际 math renderer 为 mathjax 时装载资源，mathjax_path 为空抛 ExtensionError；默认只在页面上下文 has_maths_elements 为真时加载，HTML 资源策略 always 强制全部页面加载；mathjax2_config 在脚本前写 MathJax.Hub.Config 且配默认 v3 CDN 时警告，mathjax3_config 写 window.MathJax；用户 async/defer 优先，否则 v3 配置默认 defer，其余默认 async；no-wrap 公式原样输出，多式以空段分割并包 align/aligned，含换行的单式包 split，具编号公式输出 eqno 与永久链接。必须保持脚本属性与配置体、相对路径查询串、按页/include/singlehtml 加载策略、对齐公式 HTML 及编号格式（test_ext_math.py）\ntodo.py[8 C X E P M]: Role:实现可配置显隐的 todo 告示、跨文档持久收集与 todolist 汇总、原条目回链及 HTML/LaTeX 等写出支持 | Uses:sphinx/directives/admonitions.py, sphinx/domains/__init__.py, sphinx/environment/__init__.py, sphinx/writers/html5.py, sphinx/writers/latex.py | API:todo_node、todolist、Todo、TodoList、TodoDomain、TodoListProcessor、setup(app)；指令 todo/todolist；事件 todo-defined(app,todo_node) | Constraints:todo 未显式 class 时使用 admonition-todo，首子节点插入本地化 Todo 标题，并记录 docname、source、line 和显式目标；域按文档保存节点，清理删除整文档集合，并行合并只合入指定 docnames；process_doc 无论是否显示都为每项发 todo-defined，todo_emit_warnings 另以正文告警；todo_include_todos 为假时原告示和汇总占位均移除但收集、事件与告警不受影响；汇总时按域值顺序深拷贝每项、清空副本 ID、把 pending_xref 的 refdoc 改为汇总文档后解析，并紧随原条目回链；todo_link_only 只隐藏来源路径和行号，不移除链接；Builder 抛 NoUri 时回链保留无 refuri 的强调文字；带 ID 的 todolist 替换时须先保留 target 以免丢目标；LaTeX 访问器写 sphinxtodo、建立 hypertarget、转义标题并禁止浮动，离开时恢复计数；扩展 env_version=2且只声明并行读取安全。必须保持显示开关下三项事件与警告均产生、显示时各页和两份汇总内容正确、隐藏时无 Todo HTML，以及 LaTeX 四个 foo 回链共享且只命中一个真实标签（test_ext_todo.py）\nviewcode.py[8 C X E H L]: Role:为 Python 对象建立源码链接，收集模块源码标签并生成带文档回链的高亮模块页面与总览 | Uses:sphinx/pycode/__init__.py, sphinx/transforms/post_transforms/__init__.py, sphinx/builders/html/__init__.py, sphinx/util/nodes.py, sphinx/environment/__init__.py | API:viewcode_anchor、ViewcodeAnchorTransform、is_supported_builder()、get_module_filename()、should_generate_module_page()、setup(app)；事件 viewcode-find-source、viewcode-follow-imported | Constraints:仅 Python desc 签名参与，默认跟随导入成员并先询问事件、再通过真实导入对象 __module__ 追踪；导入可触发任意副作用并捕获 BaseException，失败不得中止构建；每个对象名只加一个链接，源码/标签按模块缓存在环境，清理文档后无使用项的模块须移除，并行合并不得覆盖主环境已有使用映射；支持 format=html、排除 singlehtml，EPUB 仅在 viewcode_enable_epub 时启用，不支持 Builder 删除 anchor；自定义 find-source 时无法取得文件 mtime而总是重生成，普通模块页仅源码新于输出时重生成；源码块依据嵌套良好的标签区间插入 [docs] 回链，模块与父模块页按排序生成总览；默认高亮语言 default/none 原样使用，其余强制 python，行号配置使用 inline。必须保持源码页链接计数、装饰器和属性内容、行号开关、EPUB 默认/启用、事件提供源码与本地包路径的精确输出（test_ext_viewcode.py）\n\n===/testbed/sphinx/ext/apidoc/===\n__init__.py[7 I X E T]: Role:公开 apidoc 命令入口并将构建期 API 文档生成扩展接入 Sphinx | Uses:sphinx/ext/apidoc/_cli.py, sphinx/ext/apidoc/_extension.py, sphinx/ext/autodoc/ | API:main、setup(app) | Constraints:setup 必须先加载 autodoc，登记全部 apidoc_* 配置并在 builder-inited 生成源码；配置变化按 env 重建，扩展声明并行读写安全\n__main__.py[3 E X C T]: Role:将 python -m sphinx.ext.apidoc 参数交给 apidoc CLI 并以返回码退出 | Uses:sphinx/ext/apidoc/_cli.py | API:python -m sphinx.ext.apidoc | Constraints:传入参数不含程序名\n_cli.py[8 E X C M]: Role:解析 sphinx-apidoc 命令行、驱动模块扫描与目录页生成，并可委托 quickstart 建完整项目 | Uses:sphinx/ext/apidoc/_generate.py, sphinx/ext/apidoc/_shared.py, sphinx/cmd/quickstart.py, sphinx/util/osutil.py | API:sphinx-apidoc；main(argv)、get_parser() | Constraints:module_path 必须是目录，否则记录错误并以 1 退出；exclude pattern 在当前目录解析为绝对 fnmatch 正则并去重；suffix 去前导点，非 dry-run 预建输出目录；未显式 automodule options 时保留空集合以触发生成层默认值；--remove-old 与 --full 互斥；full 模式以顶层模块构造 index，并生成 conf、Makefile 与批处理脚本，默认启用 autodoc/viewcode/todo且逗号扩展需拆分；release 未给时回退 version。必须保持多字节项目元数据和扩展开关进入生成配置、模块/包/目录页文本及 private/no-headings/separate/module-first 行为（test_ext_apidoc.py）\n_extension.py[8 I X E M]: Role:把 apidoc_modules 配置逐项校验、正规化为生成选项并在 Builder 初始化时生成 API 源 | Uses:sphinx/ext/apidoc/_generate.py, sphinx/ext/apidoc/_shared.py, sphinx/application.py | API:run_apidoc(app) | Constraints:每项必须是 dict 且含 path、destination；path 相对 confdir 或绝对，必须为现存目录；destination 必须相对 srcdir且可创建；exclude_patterns 相对 confdir；集合配置只接受字符串组成的 list/tuple/set/frozenset，非法值警告后回退全局默认；max_depth 与布尔项类型错误同样回退，未知键告警；构建期固定 quiet、force、remove_old 并以模块目录名作页头；每模块 automodule_options 可覆盖全局默认。必须保持构建期生成目录页和包页、尊重 max_depth 与 automodule options且重复构建无警告（test_sphinx_extension）\n_generate.py[8 C X E M]: Role:遍历 Python 包、模块和 PEP 420 命名空间，按模板生成模块、包与顶层目录 reStructuredText 文件 | Uses:sphinx/ext/apidoc/_shared.py, sphinx/templates/apidoc/, sphinx/util/template.py, sphinx/util/osutil.py | API:PY_SUFFIXES、OPTIONS、is_initpy()、module_join()、is_package_dir()、write_file()、create_module_file()、create_package_file()、create_modules_toc_file()、walk()、recurse_tree()、is_excluded() | Constraints:Python 后缀包含 .py、.pyx 与平台扩展模块后缀；默认跳过点目录和私有目录/模块，private 只放开下划线而不放开点目录；普通子目录必须有 __init__，implicit_namespaces 才把无 __init__ 层视为命名空间且空层不生成；同一 basename 的多种扩展只列一次；排除项在遍历文件、目录和包内容判断中一致生效；用户模板目录优先于内置模板，ReSTRenderer 仍兼容旧 .rst_t；force=false 保留已有文件，FileAvoidWrite 避免相同内容改 mtime，dry-run 不写文件；目录页排序并只保留最顶层模块；separate 才为每个子模块单独生成页。必须保持 PEP 420 开关、排除后空包、嵌套空父包、尾下划线、多后缀去重和生成 toctree 不引用缺失文件（test_ext_apidoc.py）\n_shared.py[7 D X T]: Role:定义 apidoc 的不可变选项/默认值模型并清理未在本轮生成的旧文档 | Uses:sphinx/config.py | API:ApidocOptions、ApidocDefaults | Constraints:remove_old 只删除目标目录中匹配当前 suffix 且不在 written_files 的文件，删除失败只警告；配置默认值须复制 exclude_patterns 并规范 automodule_options 为 frozenset\n\n===/testbed/sphinx/ext/autodoc/===\n__init__.py[9 E X E S]: Role:作为 autodoc 扩展入口兼容重导出文档器、选项、哨兵与监听器工厂，并注册文档器、配置、事件和配套扩展 | Uses:sphinx/ext/autodoc/_documenters.py, sphinx/ext/autodoc/_directive_options.py, sphinx/ext/autodoc/_event_listeners.py, sphinx/ext/autodoc/_member_finder.py, sphinx/application.py | API:setup(app)；Documenter 及各内置 Documenter、Options、cut_lines、between、选项转换函数、ALL/EMPTY/INSTANCEATTR/SLOTSATTR/SUPPRESS/UNINITIALIZED_ATTR、ObjectMember、py_ext_sig_re、special_member_re | Constraints:兼容导出名称和别名不可随内部拆分移除；setup 注册 module/class/exception/data/function/decorator/method/attribute/property/type alias 十类文档器，autoclass_content、成员顺序、类签名、默认选项、docstring 签名、模拟导入、类型提示展示/目标/格式、别名、警告和继承 docstring 配置均影响 env；五个 autodoc 事件须在配套扩展加载前登记，随后加载 preserve_defaults、type_comment、typehints；仅声明并行读取安全\n_directive_options.py[8 U X P S]: Role:解析、规范化并合并 autodoc 指令选项与全局默认选项，提供字典和属性两种访问表示 | Uses:sphinx/ext/autodoc/_sentinels.py, sphinx/locale/__init__.py | API:_AutoDocumenterOptions、Options、members_option()、exclude_members_option()、inherited_members_option()、member_order_option()、class_doc_from_option()、annotation_option()、bool_option()、merge_members_option()、_process_documenter_options() | Constraints:成员列表按逗号分割并去空白，裸 members 映射 ALL、裸 exclude-members 映射 EMPTY、裸 inherited-members 映射 object；非法 member-order 和 class-doc-from 必须抛带本地化文字的 ValueError；默认选项可由 no-<name> 否定，只有可扩展选项支持前导 + 与默认值合并，无默认值时须去掉 +；缺失属性访问返回 None\n_docstrings.py[8 S X P M]: Role:按对象种类、源码注释、继承策略和类内容配置提取、准备并经事件处理 autodoc 文档字符串 | Uses:sphinx/ext/autodoc/_property_types.py, sphinx/ext/autodoc/importer.py, sphinx/pycode/__init__.py, sphinx/util/docstrings.py, sphinx/util/inspect.py | API:- | Constraints:空但存在的 docstring 必须形成空列表以允许 autodoc-process-docstring 注入内容，None 则不得发事件；事件可就地改写每份行列表，非空末行后补空行；类可按 class/init/both 合并自身与 __init__/__new__ 文档且过滤 object 默认文档，别名类不展示类 docstring；源码 #: 属性注释优先运行时 docstring，重新定位类定义时可改用声明模块分析器；属性不得继承值或非数据描述符的误导 docstring，__slots__ 文档单独读取且非法 slots 只警告；未初始化和无注释运行时实例属性分别保留无文档语义，先前因签名解析处理过的 docstring 必须复用避免丢失事件改写\n_documenters.py[8 D X E S]: Role:声明 autodoc 各对象类型的 Documenter 元数据、属性模型类型和指令选项规格，供扩展注册与生成流程分派 | Uses:sphinx/ext/autodoc/_directive_options.py, sphinx/ext/autodoc/_property_types.py | API:Documenter、ModuleDocumenter、FunctionDocumenter、DecoratorDocumenter、ClassDocumenter、ExceptionDocumenter、DataDocumenter、MethodDocumenter、AttributeDocumenter、PropertyDocumenter、TypeAliasDocumenter | Constraints:当前可见实现只定义 objtype、directivetype、titles_allowed、props 与 option_spec，不实现对象装载、成员选择或输出生命周期；Module/Class 各自限定可接受选项，Data/Attribute 扩展 annotation 与 no-value，TypeAlias 不接受兼容 noindex\n_event_listeners.py[7 U X E S]: Role:提供按对象类型裁剪行或按正则标记保留/排除区段的 autodoc-process-docstring 监听器工厂 | Uses:- | API:cut_lines(pre,post=0,what=None)、between(marker,what=None,keepempty=False,exclude=False) | Constraints:两个工厂返回就地修改 lines 的事件回调；what 为空处理全部类型，cut_lines 对字符串 what 兼容为单一类型；cut_lines 去尾行前先移除一个现有尾空行，再裁剪 post；between 以 re.match 切换区段且标记行本身不保留，结果为空而 keepempty 为假时恢复原文；非空结果末尾必须补空行\n_generate.py[9 C X E M]: Role:编排 autodoc 对象及成员的源码分析、文档字符串处理、指令渲染、别名说明和依赖登记，递归生成带来源位置的 reStructuredText | Uses:sphinx/ext/autodoc/_docstrings.py, sphinx/ext/autodoc/_member_finder.py, sphinx/ext/autodoc/_renderer.py, sphinx/ext/autodoc/mock.py, sphinx/pycode/__init__.py | API:_generate_directives()（测试也调用） | Constraints:类必须按对象 __module__ 选择分析器，其他对象可沿用 real_modname；源码分析失败不得阻止运行时对象文档生成，但应尽量登记模块来源依赖；隐式模块成员默认以 __module__ 排除导入对象，显式 imported-members 放开；输出必须先有空行并保留每行 source/line，附加指令正文位于 docstring 后；成员生成沿同一 options 递归；GenericAlias、NewType、TypeVar 和按属性记录的类别名各有独立 alias 文本规则\n_member_finder.py[9 C X E L]: Role:发现模块与类的可记录成员，合并运行时、源码注释、注解、slots、枚举和继承信息，执行筛选、对象类型选择与排序 | Uses:sphinx/ext/autodoc/importer.py, sphinx/ext/autodoc/_property_types.py, sphinx/ext/autodoc/_directive_options.py, sphinx/pycode/__init__.py, sphinx/events.py | API:ObjectMember、special_member_re | Constraints:模块在未忽略 __all__ 时以其限制全成员，类默认只取本类成员，inherited-members 才放开继承集合；显式 members 缺失须警告，mock 且无属性文档的成员跳过；源码属性注释和仅注解属性须作为成员，slots 文档、实例属性与 MRO 阴影关系不得丢失，私有名反混淆不得把父类私有成员误归子类；autodoc-skip-member 的首个非 None 返回值可覆盖内置筛选，筛选异常只警告并跳过；对象类型按 exception、class/NewType/TypeVar、property、attribute、method、function/decorator、type alias、module data 的优先级选择且不自动文档化子模块；bysource 优先 __all__ 顺序，否则分析器顺序，groupwise 按固定组后按全名，alphabetical 按全名；成员全部预先装载后再排序以避免排序间触发循环导入；完成后必须清空 current_document 的 autodoc 模块和类上下文\n_property_types.py[7 D X P S]: Role:以分类型属性记录统一承载 autodoc 发现的模块、类、函数、赋值和类型别名元数据及排序信息 | Uses:sphinx/ext/autodoc/_sentinels.py | API:_ItemProperties、_ModuleProperties、_ClassDefProperties、_FunctionDefProperties、_AssignStatementProperties、_TypeStatementProperties | Constraints:模块没有 parts 且 full_name 等于模块名；运行期实例属性与未初始化属性不产生 object_name；类的规范名优先对象 __module__ 和 __qualname__，局部类或信息不足时返回空；groupwise 顺序固定为异常10、类20、函数30、数据40、类/静态/普通方法48/49/50、属性或 attribute60、类型别名70\n_renderer.py[8 U X E S]: Role:把对象属性与 autodoc 选项渲染为 Python 域指令头、签名行、类型/值/修饰选项及带来源缩进的正文 | Uses:sphinx/ext/autodoc/_property_types.py, sphinx/ext/autodoc/_sentinels.py | API:- | Constraints:多签名后续行须与首行名称列对齐；嵌套对象显式写 module；no-index/no-index-entry、async/class/static/abstract/final/canonical 等选项须按对象类型发出；类型提示为 none 时不写自动 type；模拟对象、哨兵、描述符、泛型别名、hide-value 或 no-value 情形不得泄露不适用的运行时值；空正文行不得附缩进且每行来源位置必须保留\n_sentinels.py[7 U X V S]: Role:定义 autodoc 在成员选择、属性探测、值抑制和初始化状态中使用的唯一哨兵对象 | Uses:- | API:ALL、EMPTY、INSTANCE_ATTR、RUNTIME_INSTANCE_ATTRIBUTE、SLOTS_ATTR、SUPPRESS、UNINITIALIZED_ATTR | Constraints:哨兵名称即 repr，实例创建后不可改属性且不可 pickle；ALL 的包含判断恒真且 append 无操作，EMPTY 的包含判断恒假；与类型表达式使用竖线时须构造 typing.Union，运行时对象与 TYPE_CHECKING 替身语义需对应\ndirective.py[9 I X E S]: Role:实现所有 auto* 指令的统一调度器，解析已注册 Documenter 选项、装载对象、生成 reStructuredText、登记源码依赖并转回 Docutils 节点 | Uses:sphinx/ext/autodoc/_directive_options.py, sphinx/ext/autodoc/_generate.py, sphinx/ext/autodoc/importer.py, sphinx/util/docutils.py, sphinx/util/parsing.py | API:AutodocDirective、parse_generated_content() | Constraints:对象类型由指令名去除 auto 前缀并从注册表选择；未知或非法选项记录定位错误并返回空节点，不继续装载；自定义 attr getter 按注册顺序匹配首个 isinstance 类型，否则走 safe_getattr，getter 适配器不可变；装载或生成无结果时返回空；生成内容必须在切换源码输入的上下文中解析，titles_allowed 为假时禁止标题并返回临时段落的子节点；全部分析到的文件加入 Docutils record_dependencies\nimporter.py[9 C X E V L]: Role:导入并解析 autodoc 目标，构造分类型对象属性，恢复声明型属性与类型注释，并从运行时、docstring、overload 和事件生成签名 | Uses:sphinx/ext/autodoc/_property_types.py, sphinx/ext/autodoc/_docstrings.py, sphinx/ext/autodoc/mock.py, sphinx/ext/autodoc/type_comment.py, sphinx/pycode/__init__.py | API:import_module()、import_object()、py_ext_sig_re | Constraints:导入会真实执行模块副作用；非 ImportError 的 BaseException 包括 SystemExit 必须包装为保留回溯的 ImportError，属性链失败在此前子模块导入失败时恢复原 ImportError 诊断；原生扩展或 pyx 旁存在同名 pyi 时默认以 stub loader 执行并使 __file__/spec.origin 指向 pyi，SPHINX_AUTODOC_IGNORE_NATIVE_MODULE_TYPE_STUBS 非空可禁用；可选重载模式临时令 typing.TYPE_CHECKING=True 重载本次新增的非 pyi 模块并最终恢复 False。名称支持 module::path、当前 autodoc/py 模块与类上下文，automodule 禁止参数和返回注解；装载失败须警告、note_reread 并返回 None，但 data/attribute 先回退仅注解、运行期实例和未初始化属性；无效 __all__ 警告后忽略。类型注释会就地补入模块及类 __annotations__ 并以弱集合避免重复；签名优先显式指令、docstring、运行时内省，再经 autodoc-process-signature 首个结果覆盖，重载和 singledispatch 可生成多签名；类签名按显式 __signature__、元类 __call__、__new__、__init__、对象回退顺序，NewType/TypeVar 抑制类签名，普通方法隐藏绑定首参；autodoc-before-process-signature 与 process-bases 必须在相应阶段发出。必须保持原生模块同名 .pyi 被优先装载且文件与 spec 来源均指向真实 stub（test_import_native_module_stubs）\nmock.py[8 I X E S]: Role:为 autodoc_mock_imports 提供临时元路径查找器、惰性模拟模块和对象及模拟装饰器解包判定 | Uses:sphinx/util/inspect.py | API:mock()、ismock()、ismockmodule()、undecorate()、MockFinder、MockLoader | Constraints:只模拟精确模块名及其点号后代，模拟模块以 os.devnull 为文件且 __all__/__path__ 为空；上下文必须把 finder 置于 sys.meta_path 首位，并在退出时移除 finder 及本次创建的全部 sys.modules 项；模拟对象允许任意属性、下标、调用、继承和装饰器链而保持可辨识显示名，但容器语义固定为空；ismock 须区分模拟模块、对象与绑定方法且不得仅凭任意真值属性误判；undecorate 只在模拟调用保存了装饰器参数时返回首个原对象\npreserve_defaults.py[7 I X E S]: Role:实现 autodoc_preserve_defaults 扩展，从源码 AST 恢复函数默认参数的原始表达式文本并写入运行时签名 | Uses:sphinx/pycode/ast.py, sphinx/util/inspect.py, sphinx/application.py | API:setup(app)、DefaultValue、get_function_def()（Sphinx 9 弃用） | Constraints:功能仅在配置开启且可取得源码与 ast.arguments 时生效；单行默认值按源码切片保留精确拼写，多行或无位置值回退 AST unparse；位置、普通与仅关键字默认值须按运行时 Signature 参数顺序配对，绑定方法必要时从 __func__ 取得签名；DefaultValue 的 repr 必须原样返回源码表达式以阻止求值；lambda 多行取源导致的 SyntaxError 静默跳过，其他取参语法错误由回调捕获后返回，无法设置 __signature__ 或内建类型失败不报错，AST 不支持只警告；get_function_def 每次调用发 RemovedInSphinx90Warning\ntype_comment.py[7 I X E S]: Role:解析函数源码中的 PEP 484 类型注释并在签名处理前补充缺失的运行时 __annotations__ | Uses:sphinx/pycode/ast.py, sphinx/util/inspect.py, sphinx/application.py | API:setup(app)、get_type_comment()、signature_from_ast() | Constraints:autodoc_use_type_comments 关闭时不得修改对象；已有参数或返回注解优先，类型注释只补缺失项并就地改变 __annotations__；绑定方法移除首参，省略号单一参数注释表示抑制而不得覆盖逐参数注释；源码不可取或语法无法解析时返回 None，参数名不匹配和 AST 反解析失败只警告；位置专用、普通、变长、仅关键字和关键字变长参数种类必须保留\ntypehints.py[8 I X E S]: Role:在签名事件中记录运行时类型提示，并在 Python 对象描述转换时按配置把参数和返回类型合并进文档字段列表 | Uses:sphinx/addnodes.py, sphinx/util/inspect.py, sphinx/application.py | API:setup(app)、record_typehints()、merge_typehints() | Constraints:仅 Python 域且 autodoc_typehints 为 both 或 description 时改写正文；记录以对象全名存入当前文档状态，签名不可取时静默跳过，类型名格式和短 Literal 服从配置；缺字段列表时须在首个嵌套 desc 前插入，否则追加；description_target=all 为所有注解补 param/type，类返回 None 可抑制 rtype，documented_params 只给已有说明项补类型并可强制非 None 返回类型，其他模式不强制返回类型；已有 param/type/return/rtype 不得重复，*args 与 **kwargs 名称须与现有说明匹配\n\n===/testbed/sphinx/ext/autosummary/===\n__init__.py[9 C X E L]: Role:实现 autosummary 指令与 autolink 角色，导入对象并复用 autodoc 生成签名和摘要表、隐藏目录树及构建期存根生成接线 | Uses:sphinx/ext/autodoc/, sphinx/ext/autosummary/generate.py, sphinx/pycode/__init__.py, sphinx/util/parsing.py, sphinx/addnodes.py | API:Autosummary、AutoLink、autosummary_toc、autosummary_table、import_by_name()、import_ivar_by_name()、mangle_signature()、extract_summary()、limited_join()、process_generate_options()、setup(app) | Constraints:signatures 只接受 none/short/long，旧 nosignatures 映射 none；~ 仅缩短显示名，摘要先经 autodoc docstring 事件且只取首段首个不破坏 RST 的句子，已知缩写不得误断句，尾随 :: 改为句点；toctree 路径相对当前文档，缺失与被排除存根分别警告，caption 无 toctree 时忽略并警告；表格首列 HTML 空格改为不换行字符，LaTeX 列规格固定等宽。导入按当前类、模块、裸名顺序尝试并聚合底层异常，实例属性可从源码注释或注解回退；autolink 导入失败必须退化为保持类名的 emphasis 而非坏链接。构建期生成只选择支持 reStructuredText 的首个后缀，generate=True 扫全部源，列表项补首后缀并剔除缺失文件；默认加载 autodoc，生成开关默认真且 overwrite 默认真。必须保持签名压缩、摘要边界、对象导入元组、表格/目录树节点和生成存根内容及递归、文件名映射、覆盖、mock、__all__ 行为（test_ext_autosummary.py）\ngenerate.py[9 C X E L]: Role:扫描源文件与 docstring 中的 autosummary 条目，导入并分类对象成员，通过沙箱模板递归生成存根，并实现 sphinx-autogen 命令 | Uses:sphinx/ext/autosummary/__init__.py, sphinx/ext/autodoc/, sphinx/pycode/__init__.py, sphinx/util/template.py, sphinx/config.py | API:sphinx-autogen；main()、AutosummaryEntry、AutosummaryRenderer、generate_autosummary_content()、generate_autosummary_docs()、find_autosummary_in_files()、find_autosummary_in_docstring()、find_autosummary_in_lines()、members_of() | Constraints:独立 CLI 使用最小应用并显式注册十类 Documenter；模板查找优先用户路径，名称缺失时依次尝试 autosummary/<objtype>.rst 与 base.rst，Jinja 必须沙箱化并以 RST escape 为 e/escape；模块成员是否服从 __all__ 由 ignore_module_all 反向控制，显式空 __all__ 必须产生空成员集；递归包只生成可导入且非 mock 的子模块，被包命名空间中非模块对象覆盖的名字须跳过，公开子模块可受 __all__ 限制。生成文件名先应用 filename_map；现存同内容不重写，内容变化仅 overwrite 时写，新增文件递归扫描且返回新旧全部路径；导入失败记录去重提示并跳过。源码扫描维护 currentmodule/automodule 上下文，toctree 路径相对源文件目录，~ 从对象名剥除，automodule 还递归扫描模块 docstring。CLI suffix 自动补点，--remove-old 只删除输出目录内未生成的同后缀文件，删除失败警告。必须保持生成上下文分类、递归文件集合、模板内容、覆盖与 remove-old 语义（test_ext_autosummary.py）\n\n===/testbed/sphinx/ext/autosummary/templates/autosummary/===\nbase.rst[7 D X E T]: Role:作为 autosummary 通用存根模板，为任意对象生成带标题、currentmodule 上下文和对应 auto 指令的页面 | Uses:sphinx/ext/autosummary/generate.py, sphinx/ext/autodoc/ | API:- | Constraints:标题使用转义后的完整限定名；auto 指令类型由 objtype 选择，目标名使用当前模块下的 objname\nclass.rst[7 D X E T]: Role:作为 autosummary 类存根模板，生成类文档、构造器以及按条件列出的本类方法和属性摘要 | Uses:sphinx/ext/autosummary/generate.py, sphinx/ext/autodoc/, sphinx/ext/autosummary/templates/autosummary/base.rst | API:Jinja 块 methods、attributes 供主题或项目模板覆写 | Constraints:方法和属性摘要使用 ~name.member 缩短显示；仅在相应集合非空时输出栏目，构造器始终通过 automethod __init__ 展示\nmodule.rst[7 D X E T]: Role:作为 autosummary 模块存根模板，按属性、函数、类、异常和子模块分类生成递归 API 摘要 | Uses:sphinx/ext/autosummary/generate.py, sphinx/ext/autodoc/, sphinx/ext/autosummary/templates/autosummary/base.rst | API:Jinja 块 attributes、functions、classes、exceptions、modules 供主题或项目模板覆写 | Constraints:对象栏目仅在集合非空时出现；子模块摘要启用空 toctree 与 recursive 以继续生成层级存根；其余对象在 automodule 指令内容中渲染\n\n===/testbed/sphinx/ext/intersphinx/===\n__init__.py[8 C X E T]: Role:汇总并公开 Intersphinx 的清单装载、外部角色与引用解析接口，并把配置和生命周期回调接入 Sphinx | Uses:sphinx/ext/intersphinx/_load.py, sphinx/ext/intersphinx/_resolve.py, sphinx/ext/intersphinx/_shared.py, sphinx/application.py | API:IntersphinxDispatcher、IntersphinxRole、IntersphinxRoleResolver、InventoryAdapter、fetch_inventory()、inspect_main()、install_dispatcher()、inventory_exists()、load_mappings()、missing_reference()、resolve_reference_any_inventory()、resolve_reference_detect_inventory()、resolve_reference_in_inventory()、validate_intersphinx_mapping()、setup(app) | Constraints:intersphinx_mapping 与 resolve_self 变化触发 env 重建，cache_limit 与 timeout 不直接触发；默认禁用普通回退解析 std:doc，但显式 external 角色和命名 inventory 不服从该禁用；扩展环境数据版本为 1且声明并行读取安全；旧 normalize_intersphinx_mapping 仅经模块属性访问发 Sphinx 10 弃用警告\n__main__.py[3 E X C T]: Role:提供 python -m sphinx.ext.intersphinx 清单检查命令入口 | Uses:sphinx/ext/intersphinx/_cli.py | API:python -m sphinx.ext.intersphinx <inventory path-or-URL> | Constraints:初始化标准日志后以 inspect_main 返回码退出\n_cli.py[5 E X C T]: Role:实现 intersphinx 对象清单检查 CLI，读取本地或远程 inventory 并按对象类型和名称排序打印 | Uses:sphinx/ext/intersphinx/_load.py | API:inspect_main(argv) | Constraints:缺少参数打印固定帮助和错误到 stderr 并返回 1；成功时按类型、对象名排序，显示名为 - 时打印空白并返回 0；已知 ValueError 使用其格式化消息，其他异常以 Unknown error repr 输出到 stderr 并返回 1。必须保持本地文件与 HTTP URL 输出以 c:function 开头且无 stderr（test_ext_intersphinx.py）\n_load.py[8 C X E A L]: Role:校验并正规化 intersphinx_mapping，并发读取、缓存和合并本地或远程 objects.inv | Uses:sphinx/ext/intersphinx/_shared.py, sphinx/util/inventory.py, sphinx/util/requests.py, sphinx/builders/html/__init__.py, sphinx/config.py | API:validate_intersphinx_mapping()、load_mappings()、fetch_inventory() | Constraints:项目名和目标 URI必须为唯一非空字符串，值须为二元组，inventory 位置正规化为仅含 None 或非空字符串的 tuple；校验聚合全部错误后以单复数 ConfigError 失败。所有项目并发加载，同项目位置按顺序尝试，部分失败仅 info、全部失败 warning；本地清单每次读取，远程清单按天缓存，负 cache_limit 永不过期，doctree 缓存目录为不稳定内部细节；配置删除项目或更改目标 URI 时丢弃旧缓存，合并按 name/expiry 排序以稳定遮蔽顺序；远程请求应用 timeout、User-Agent 和 TLS 设置，日志 URL 隐藏密码，生成链接 URI剥离全部 basic auth；仅当 inventory 地址的重定向与链接基址相同或为其目录时同步移动链接基址。必须保持重定向、fallback、缓存期限、URL 斜杠、精确映射诊断与凭据剥离语义（test_ext_intersphinx.py、test_ext_intersphinx_cache.py） | Keys:inventory:objects.inv(消费者)\n_resolve.py[9 C X E P L]: Role:把缺失域引用和 external/external+inventory 角色解析为远程 inventory 链接，并在解析前安装动态角色分派器 | Uses:sphinx/ext/intersphinx/_shared.py, sphinx/domains/__init__.py, sphinx/transforms/post_transforms/__init__.py, sphinx/util/docutils.py, sphinx/addnodes.py | API:inventory_exists()、resolve_reference_in_inventory()、resolve_reference_any_inventory()、resolve_reference_detect_inventory()、missing_reference()、IntersphinxDispatcher、IntersphinxRole、IntersphinxRoleResolver、install_dispatcher() | Constraints:普通缺失引用先查合并库存，再把首个冒号前缀当命名库存；resolve_self 命中时剥前缀交还本地解析并标记节点；命名 inventory 与显式 external 角色不受 disabled_reftypes，普通回退支持 *、domain:* 与 domain:type 禁用；any 按排序域搜索，std cmdoption 兼容 option，py attribute 兼容 method；std label/term 唯一大小写不敏感匹配可解析，多个不同目标告警；相对清单 URI按 refdoc 深度回退，数字版本标题加 v，文本版本不加；隐式标题优先 inventory display_name，显式标题原样保留，display_name=- 时剥命名库存前缀；external 角色可指定 inventory、domain、role，缺库存/域/角色或目标均给定类告警并降为无链接正文。必须保持 Python/标准/JS/C++ 上下文限定、相对 URI、禁用矩阵、external 角色诊断和 HTML 链接文本（test_ext_intersphinx.py）\n_shared.py[7 D X E S]: Role:定义 Intersphinx 项目值对象、环境库存适配器及跨装载和解析模块共享的类型与日志器 | Uses:sphinx/environment/__init__.py, sphinx/util/logging.py | API:InventoryAdapter | Constraints:_IntersphinxProject 要求非空字符串 name/target_uri 和非空 tuple locations，位置只允许 None 或非空字符串，构造后不可赋值或删除属性；InventoryAdapter 首次使用时同时初始化 cache、主库存和命名库存，clear 只清两类解析库存而保留下载缓存\n\n===/testbed/sphinx/ext/napoleon/===\n__init__.py[8 I X E L]: Role:作为 Napoleon 扩展入口注册 Google/NumPy docstring 转换、成员纳入策略、配置项，并扩展 Python 域关键字参数字段 | Uses:sphinx/ext/napoleon/docstring.py, sphinx/ext/autodoc/__init__.py, sphinx/domains/python/_object.py, sphinx/application.py | API:setup(app)、Config、GoogleDocstring、NumpyDocstring | Constraints:真实 Sphinx 应用加载时先补丁 Python 域：parameter 字段别名加入 arg/argument，并追加可折叠 keyword 字段及 kwarg/kwparam、paramtype/kwtype 名；非 Sphinx 对象调用 setup 只返回版本与并行安全元数据，不注册或补丁。docstring 处理在 NumPy 开关开启时先转 NumpyDocstring，再在 Google 开关开启时处理所得行，并原位替换 lines；两者均关闭则保持原文。init/private/special 纳入只对模块或由当前类真实拥有、有 docstring 且非 __weakref__ 的成员覆盖 autodoc 跳过决定，继承成员不得误判为本类拥有，解析 owner 失败返回 None。十五项 napoleon 配置均影响 env，Config 辅助对象先载默认值再允许传入设置覆盖；singular Note 的具体转换与各章节语法由 docstring.py 执行\ndocstring.py[8 C X E P L]: Role:将 Google 与 NumPy 风格 docstring 的章节、字段、类型规范、交叉引用及缩进结构解析并转换为可供 Docutils/autodoc 消费的 reStructuredText | Uses:sphinx/ext/napoleon/__init__.py, sphinx/util/typing.py, sphinx/util/logging.py, sphinx/locale/__init__.py | API:GoogleDocstring、NumpyDocstring；_convert_type_spec、_recombine_set_tokens、_token_type、_tokenize_type_spec（测试也调用） | Constraints:输入可为字符串或行列表，输出由 lines() 返回并由 __str__ 以换行拼接；Google 章节以冒号与后续缩进识别，NumPy 章节要求至少两个合法标点组成的下划线；属性/data/property 走内联类型解析，类或模块属性缺省类型可从 PEP 526 注解解析；napoleon_use_param/use_keyword/use_rtype、use_ivar、admonition、custom_sections、preprocess_types、type_aliases 与 attr_annotations 分别控制字段布局、章节渲染和类型解析；类型预处理保持既有显式角色，值集合及字符串/数值写为字面量，optional/default 斜体，普通对象生成 py:class，None/True/False/Ellipsis 生成 py:obj，畸形括号或引号必须发出带 docstring 位置的警告；字段中的角色、代码、meta 与显式链接内冒号不得误作分隔符，参数星号须转义且 strip_signature_backslash 时尾随下划线转义；NumPy See Also 优先生成带别名翻译的对象链接，无法按 numpydoc 项格式解析时退化为 seealso admonition。必须保持两种方言对参数、关键字、返回、yield/receive、raises、属性、方法、列表/定义列表、admonition、自定义章节与多行缩进的精确 RST 输出，以及 no-index、PEP 526、类型别名和 autodoc typehints 组合行为（TestGoogleDocstring、TestNumpyDocstring、TestInlineAttribute、TestNamedtupleSubclass、test_napoleon_and_autodoc_typehints_description_all、test_napoleon_and_autodoc_typehints_description_documented_params）\n\n===/testbed/sphinx/templates/apidoc/===\nmodule.rst.jinja[5 D X E T]: Role:把单个 Python 模块的 apidoc 上下文渲染为可选标题和 automodule 指令 | Uses:sphinx/ext/apidoc/_generate.py | API:Jinja 上下文 basename、qualname、show_headings、automodule_options；输出 reStructuredText 模块页 | Constraints:标题仅在 show_headings 为真时生成并对名称转义；每个 automodule 选项输出为空值的指令选项行\npackage.rst.jinja[7 D X E T]: Role:把 Python 包或命名空间的 apidoc 上下文渲染为包正文、子包与子模块目录 | Uses:sphinx/ext/apidoc/_generate.py | API:Jinja 上下文 pkgname、is_namespace、modulefirst、subpackages、submodules、separatemodules、show_headings、automodule_options、maxdepth；输出 reStructuredText 包页 | Constraints:命名空间输出 py:module 而不输出包 automodule；普通包内容依 modulefirst 置于目录前或后；子模块仅在 separatemodules 时进入 toctree，否则原页逐项嵌入 automodule；标题文本与层级必须保持\ntoc.rst.jinja[5 D X E T]: Role:把 apidoc 顶层文档列表渲染为带标题和深度限制的 toctree 页面 | Uses:sphinx/ext/apidoc/_generate.py | API:Jinja 上下文 header、maxdepth、docnames；输出 reStructuredText 目录页 | Constraints:header 通过 heading 过滤器生成标题；docnames 按传入顺序逐行进入 toctree\n\n===/testbed/sphinx/templates/graphviz/===\ngraphviz.css[5 D X E H T]: Role:为 Graphviz 扩展生成的 HTML 图像与对象提供无边框和响应式宽度样式 | Uses:sphinx/ext/graphviz.py | API:CSS 选择器 img.graphviz、object.graphviz | Constraints:两类图形最大宽度均为 100%，仅 img 明确清除边框\n\n===/testbed/sphinx/templates/imgmath/===\npreview.tex.jinja[7 D X E H T]: Role:把数学公式及排版参数渲染为借助 preview 包裁剪边界的独立 LaTeX 文档 | Uses:sphinx/ext/imgmath.py | API:模板变量 preamble、tightpage、fontsize、baselineskip、math；输出 imgmath 预览 TeX 源 | Constraints:模板使用 <%=...%> 分隔符；用户 preamble 位于基础数学包之后；preview 包必须以 active 加 tightpage 参数加载，公式置于 preview 环境并以指定字号与基线距排版\ntemplate.tex.jinja[7 D X E H T]: Role:把数学公式及排版参数渲染为不依赖 preview 裁剪的独立 LaTeX 文档 | Uses:sphinx/ext/imgmath.py | API:模板变量 preamble、fontsize、baselineskip、math；输出 imgmath TeX 源 | Constraints:模板使用 <%=...%> 分隔符；用户 preamble 位于基础数学包之后；文档无页眉页脚，公式以指定字号与基线距直接置于 document 中\n\n## 对账报告\n- 对齐 2017, 观察 0, 忽略 3, 已清除 0\n\n纲要与代码已对齐。\n\n以上是模块 X 的纲要。能据此回答的问题直接回答，不重复读源码；具体事实没写或出现冲突时读对应文件核实；别的模块的问题再按模块取。纲要与需求、源码、测试或实际运行结果冲突时，读取对应源码与测试核实，并修正不准确的纲要；状态对齐不证明代码正确或语义完整。"
        }
      ],
      "structured_content": null
    },
    "error": null,
    "status": "completed"
  },
  "call_ref": "item_6"
}
```

## 12. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_8",
    "type": "command_execution",
    "command": "/bin/bash -lc 'rg -n -C 8 \"is_allowed_version|allowed_version\" sphinx tests'",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 13. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc 'rg -n -C 8 \"is_allowed_version|allowed_version\" sphinx tests'"
  },
  "call_ref": "item_8"
}
```

## 14. tool / tool_output

```
{
  "output": {
    "output": "/bin/bash: line 1: rg: command not found\n",
    "exit_code": 127,
    "status": "failed"
  },
  "call_ref": "item_8"
}
```

## 15. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_10",
    "type": "command_execution",
    "command": "/bin/bash -lc \"grep -RIn -C 8 --exclude-dir=.git -e 'is_allowed_version' -e 'allowed_version' sphinx tests 2>/dev/null\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 16. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"grep -RIn -C 8 --exclude-dir=.git -e 'is_allowed_version' -e 'allowed_version' sphinx tests 2>/dev/null\""
  },
  "call_ref": "item_10"
}
```

## 17. tool / tool_output

```
{
  "output": {
    "output": "",
    "exit_code": 1,
    "status": "failed"
  },
  "call_ref": "item_10"
}
```

## 18. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_12",
    "type": "command_execution",
    "command": "/bin/bash -lc \"sed -n '1,260p' sphinx/ext/doctest.py\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 19. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"sed -n '1,260p' sphinx/ext/doctest.py\""
  },
  "call_ref": "item_12"
}
```

## 20. tool / tool_output

```
{
  "output": {
    "output": "\"\"\"Mimic doctest in Sphinx.\n\nThe extension automatically execute code snippets and checks their results.\n\"\"\"\n\nfrom __future__ import annotations\n\nimport doctest\nimport os.path\nimport re\nimport sys\nimport time\nfrom io import StringIO\nfrom typing import TYPE_CHECKING\n\nfrom docutils import nodes\nfrom docutils.parsers.rst import directives\nfrom packaging.specifiers import InvalidSpecifier, SpecifierSet\nfrom packaging.version import Version\n\nimport sphinx\nfrom sphinx._cli.util.colour import bold\nfrom sphinx.builders import Builder\nfrom sphinx.locale import __\nfrom sphinx.util import logging\nfrom sphinx.util.docutils import SphinxDirective\nfrom sphinx.util.osutil import relpath\n\nif TYPE_CHECKING:\n    from collections.abc import Callable, Set\n    from typing import Any, ClassVar\n\n    from docutils.nodes import Element, Node, TextElement\n\n    from sphinx.application import Sphinx\n    from sphinx.util.typing import ExtensionMetadata, OptionSpec\n\n\nlogger = logging.getLogger(__name__)\n\nblankline_re = re.compile(r'^\\s*<BLANKLINE>', re.MULTILINE)\ndoctestopt_re = re.compile(r'[ \\t]*#\\s*doctest:.+$', re.MULTILINE)\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n# set up the necessary directives\n\n\nclass TestDirective(SphinxDirective):\n    \"\"\"Base class for doctest-related directives.\"\"\"\n\n    has_content = True\n    required_arguments = 0\n    optional_arguments = 1\n    final_argument_whitespace = True\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\nclass TestsetupDirective(TestDirective):\n    option_spec: ClassVar[OptionSpec] = {\n        'skipif': directives.unchanged_required,\n    }\n\n\nclass TestcleanupDirective(TestDirective):\n    option_spec: ClassVar[OptionSpec] = {\n        'skipif': directives.unchanged_required,\n    }\n\n\nclass DoctestDirective(TestDirective):\n    option_spec: ClassVar[OptionSpec] = {\n        'hide': directives.flag,\n        'no-trim-doctest-flags': directives.flag,\n        'options': directives.unchanged,\n        'pyversion': directives.unchanged_required,\n        'skipif': directives.unchanged_required,\n        'trim-doctest-flags': directives.flag,\n    }\n\n\nclass TestcodeDirective(TestDirective):\n    option_spec: ClassVar[OptionSpec] = {\n        'hide': directives.flag,\n        'no-trim-doctest-flags': directives.flag,\n        'pyversion': directives.unchanged_required,\n        'skipif': directives.unchanged_required,\n        'trim-doctest-flags': directives.flag,\n    }\n\n\nclass TestoutputDirective(TestDirective):\n    option_spec: ClassVar[OptionSpec] = {\n        'hide': directives.flag,\n        'no-trim-doctest-flags': directives.flag,\n        'options': directives.unchanged,\n        'pyversion': directives.unchanged_required,\n        'skipif': directives.unchanged_required,\n        'trim-doctest-flags': directives.flag,\n    }\n\n\nparser = doctest.DocTestParser()\n\n\n# helper classes\n\n\nclass TestGroup:\n    def __init__(self, name: str) -> None:\n        self.name = name\n        self.setup: list[TestCode] = []\n        self.tests: list[list[TestCode] | tuple[TestCode, None]] = []\n        self.cleanup: list[TestCode] = []\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n    def __repr__(self) -> str:\n        return (\n            f'TestGroup(name={self.name!r}, setup={self.setup!r}, '\n            f'cleanup={self.cleanup!r}, tests={self.tests!r})'\n        )\n\n\nclass TestCode:\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n    def __repr__(self) -> str:\n        return (\n            f'TestCode({self.code!r}, {self.type!r}, filename={self.filename!r}, '\n            f'lineno={self.lineno!r}, options={self.options!r})'\n        )\n\n\nclass SphinxDocTestRunner(doctest.DocTestRunner):\n    pass\n\n\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_12"
}
```

## 21. assistant / message

```
源码显示该辅助函数整段缺失，但所需 `packaging` 类型已经在目标模块导入。接下来我会核对现有 doctest 测试结构和依赖版本的实际 PEP 440 行为，确保预发布版的默认过滤、复合约束与异常传播都由同一标准实现承担。
```

## 22. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_15",
    "type": "command_execution",
    "command": "/bin/bash -lc \"find tests -type f -iname '*doctest*' -o -type f -path '*doctest*' | sort\npython - <<'PY'\nimport packaging\nfrom packaging.specifiers import SpecifierSet\nfrom packaging.version import Version\nprint(packaging.__version__)\nfor spec, version in [\n    ('<=3.5','3.3'), ('<=3.2','3.3'), ('>3.2,<4.0','3.3'),\n    ('>=2.7,\"'!=3.0.*,!=3.1.*'\"','2.7.18'), ('~=3.7.0','3.7.9'),\n    ('~=3.7.0','3.8.0'), ('>=1.0','1.1a1'), ('>=1.0a1','1.1a1'),\n]:\n    print(spec, version, Version(version) in SpecifierSet(spec))\nPY\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 23. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"find tests -type f -iname '*doctest*' -o -type f -path '*doctest*' | sort\npython - <<'PY'\nimport packaging\nfrom packaging.specifiers import SpecifierSet\nfrom packaging.version import Version\nprint(packaging.__version__)\nfor spec, version in [\n    ('<=3.5','3.3'), ('<=3.2','3.3'), ('>3.2,<4.0','3.3'),\n    ('>=2.7,\"'!=3.0.*,!=3.1.*'\"','2.7.18'), ('~=3.7.0','3.7.9'),\n    ('~=3.7.0','3.8.0'), ('>=1.0','1.1a1'), ('>=1.0a1','1.1a1'),\n]:\n    print(spec, version, Version(version) in SpecifierSet(spec))\nPY\""
  },
  "call_ref": "item_15"
}
```

## 24. tool / tool_output

```
{
  "output": {
    "output": "tests/roots/test-ext-doctest-fail-fast/conf.py\ntests/roots/test-ext-doctest-fail-fast/fail-fast.txt\ntests/roots/test-ext-doctest-skipif/conf.py\ntests/roots/test-ext-doctest-skipif/skipif.txt\ntests/roots/test-ext-doctest-with-autodoc/conf.py\ntests/roots/test-ext-doctest-with-autodoc/dir/__init__.py\ntests/roots/test-ext-doctest-with-autodoc/dir/bar.py\ntests/roots/test-ext-doctest-with-autodoc/dir/inner.rst\ntests/roots/test-ext-doctest-with-autodoc/foo.py\ntests/roots/test-ext-doctest-with-autodoc/index.rst\ntests/roots/test-ext-doctest/conf.py\ntests/roots/test-ext-doctest/doctest.txt\ntests/roots/test-trim_doctest_flags/conf.py\ntests/roots/test-trim_doctest_flags/index.rst\n25.0\n<=3.5 3.3 True\n<=3.2 3.3 False\n>3.2,<4.0 3.3 True\n>=2.7,!=3.0.*,!=3.1.* 2.7.18 True\n~=3.7.0 3.7.9 True\n~=3.7.0 3.8.0 False\n>=1.0 1.1a1 False\n>=1.0a1 1.1a1 True\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_15"
}
```

## 25. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_17",
    "type": "command_execution",
    "command": "/bin/bash -lc \"find tests -type f | grep -E 'doctest|trim_doctest' | sort\nfind tests -maxdepth 2 -type f -name '*.py' | sort | grep -E 'ext|doctest' | head -200\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 26. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"find tests -type f | grep -E 'doctest|trim_doctest' | sort\nfind tests -maxdepth 2 -type f -name '*.py' | sort | grep -E 'ext|doctest' | head -200\""
  },
  "call_ref": "item_17"
}
```

## 27. tool / tool_output

```
{
  "output": {
    "output": "tests/roots/test-ext-doctest-fail-fast/conf.py\ntests/roots/test-ext-doctest-fail-fast/fail-fast.txt\ntests/roots/test-ext-doctest-skipif/conf.py\ntests/roots/test-ext-doctest-skipif/skipif.txt\ntests/roots/test-ext-doctest-with-autodoc/conf.py\ntests/roots/test-ext-doctest-with-autodoc/dir/__init__.py\ntests/roots/test-ext-doctest-with-autodoc/dir/bar.py\ntests/roots/test-ext-doctest-with-autodoc/dir/inner.rst\ntests/roots/test-ext-doctest-with-autodoc/foo.py\ntests/roots/test-ext-doctest-with-autodoc/index.rst\ntests/roots/test-ext-doctest/conf.py\ntests/roots/test-ext-doctest/doctest.txt\ntests/roots/test-trim_doctest_flags/conf.py\ntests/roots/test-trim_doctest_flags/index.rst\ntests/test_builders/test_build_gettext.py\ntests/test_builders/test_build_text.py\ntests/test_ext_autodoc/__init__.py\ntests/test_ext_autodoc/autodoc_util.py\ntests/test_ext_autodoc/test_ext_autodoc.py\ntests/test_ext_autodoc/test_ext_autodoc_autoattribute.py\ntests/test_ext_autodoc/test_ext_autodoc_autoclass.py\ntests/test_ext_autodoc/test_ext_autodoc_autodata.py\ntests/test_ext_autodoc/test_ext_autodoc_autofunction.py\ntests/test_ext_autodoc/test_ext_autodoc_automodule.py\ntests/test_ext_autodoc/test_ext_autodoc_autoproperty.py\ntests/test_ext_autodoc/test_ext_autodoc_configs.py\ntests/test_ext_autodoc/test_ext_autodoc_events.py\ntests/test_ext_autodoc/test_ext_autodoc_importer.py\ntests/test_ext_autodoc/test_ext_autodoc_mock.py\ntests/test_ext_autodoc/test_ext_autodoc_preserve_defaults.py\ntests/test_ext_autodoc/test_ext_autodoc_private_members.py\ntests/test_ext_autodoc/test_ext_autodoc_type_alias_nitpicky.py\ntests/test_ext_autosummary/__init__.py\ntests/test_ext_autosummary/test_ext_autosummary.py\ntests/test_ext_autosummary/test_ext_autosummary_imports.py\ntests/test_ext_imgconverter/__init__.py\ntests/test_ext_imgconverter/test_ext_imgconverter.py\ntests/test_ext_imgconverter/test_ext_imgmockconverter.py\ntests/test_ext_intersphinx/__init__.py\ntests/test_ext_intersphinx/test_ext_intersphinx.py\ntests/test_ext_intersphinx/test_ext_intersphinx_cache.py\ntests/test_ext_napoleon/__init__.py\ntests/test_ext_napoleon/pep526_data_google.py\ntests/test_ext_napoleon/pep526_data_numpy.py\ntests/test_ext_napoleon/test_ext_napoleon.py\ntests/test_ext_napoleon/test_ext_napoleon_docstring.py\ntests/test_extensions/__init__.py\ntests/test_extensions/test_ext_apidoc.py\ntests/test_extensions/test_ext_autosectionlabel.py\ntests/test_extensions/test_ext_coverage.py\ntests/test_extensions/test_ext_duration.py\ntests/test_extensions/test_ext_extlinks.py\ntests/test_extensions/test_ext_githubpages.py\ntests/test_extensions/test_ext_graphviz.py\ntests/test_extensions/test_ext_ifconfig.py\ntests/test_extensions/test_ext_inheritance_diagram.py\ntests/test_extensions/test_ext_math.py\ntests/test_extensions/test_ext_todo.py\ntests/test_extensions/test_ext_viewcode.py\ntests/test_extensions/test_extension.py\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_17"
}
```

## 28. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_19",
    "type": "command_execution",
    "command": "/bin/bash -lc \"grep -n 'InvalidSpecifier\\\\|SpecifierSet\\\\|Version' sphinx/ext/doctest.py\ngit status --short -- sphinx/ext/doctest.py\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 29. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"grep -n 'InvalidSpecifier\\\\|SpecifierSet\\\\|Version' sphinx/ext/doctest.py\ngit status --short -- sphinx/ext/doctest.py\""
  },
  "call_ref": "item_19"
}
```

## 30. tool / tool_output

```
{
  "output": {
    "output": "18:from packaging.specifiers import InvalidSpecifier, SpecifierSet\n19:from packaging.version import Version\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_19"
}
```

## 31. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_21",
    "type": "file_change",
    "changes": [
      {
        "path": "/testbed/sphinx/ext/doctest.py",
        "kind": "update"
      }
    ],
    "status": "in_progress"
  }
}
```

## 32. tool / event

```
{
  "name": "filechange",
  "output": {
    "id": "item_21",
    "type": "file_change",
    "changes": [
      {
        "path": "/testbed/sphinx/ext/doctest.py",
        "kind": "update"
      }
    ],
    "status": "completed"
  },
  "message_ref": "item_21"
}
```

## 33. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_23",
    "type": "mcp_tool_call",
    "server": "ortg",
    "tool": "ortg_update",
    "arguments": {
      "path": "sphinx/ext/doctest.py",
      "outline": "doctest.py[8 C X E P L]: Role:提供执行文档代码示例并比较输出的 doctest Builder 与 testsetup、testcleanup、doctest、testcode、testoutput 指令，并按 PEP 440 判断版本约束 | Uses:sphinx/builders/__init__.py, sphinx/util/docutils.py | API:is_allowed_version(spec, version)（测试也调用）、TestDirective、TestsetupDirective、TestcleanupDirective、DoctestDirective、TestcodeDirective、TestoutputDirective、TestGroup、TestCode、SphinxDocTestRunner、DocTestBuilder、setup(app)；builder 名 doctest；五个同名指令 | Constraints:is_allowed_version 以 packaging 的 SpecifierSet 与 Version 解析并匹配完整 PEP 440 约束，复合约束、排除、兼容发布及 pre/post/dev 语义均由其处理，非法 spec 与 version 分别传播 InvalidSpecifier 与 InvalidVersion；当前源码的指令 run、TestGroup/TestCode 初始化及 Builder 执行、统计、报告主体被遮罩，具体实现未知，不得据接口补造；可见初始化会把 doctest.compile 全局替换为 Builder.compile、把 doctest_path 前插 sys.path、打开 UTF-8 output.txt并写带当前时间的标题，所有发现文档均视为过期且目标 URI 为空；公开文档规定同一文档各组先执行全部 setup、再按出现顺序执行测试、最后 cleanup，空组名为 default而 * 归入所有组，skipif 真值使对应指令不参与，testcode 整块执行且由 testoutput 给预期输出；默认 flags 为 DONT_ACCEPT_TRUE_FOR_1、ELLIPSIS、IGNORE_EXCEPTION_DETAIL，doctest_fail_fast 默认假，成功展示默认真，扩展只声明并行读取安全；pyversion、hide、trim/no-trim 和 options 的可见选项由各指令分别限制。遮罩区域中的异常处理、命名空间共享、失败计数、状态码、output.txt 其余格式及 fail-fast 细节未知"
    },
    "result": null,
    "error": null,
    "status": "in_progress"
  }
}
```

## 34. assistant / tool_call

```
{
  "name": "ortg_update",
  "server": "ortg",
  "arguments": {
    "path": "sphinx/ext/doctest.py",
    "outline": "doctest.py[8 C X E P L]: Role:提供执行文档代码示例并比较输出的 doctest Builder 与 testsetup、testcleanup、doctest、testcode、testoutput 指令，并按 PEP 440 判断版本约束 | Uses:sphinx/builders/__init__.py, sphinx/util/docutils.py | API:is_allowed_version(spec, version)（测试也调用）、TestDirective、TestsetupDirective、TestcleanupDirective、DoctestDirective、TestcodeDirective、TestoutputDirective、TestGroup、TestCode、SphinxDocTestRunner、DocTestBuilder、setup(app)；builder 名 doctest；五个同名指令 | Constraints:is_allowed_version 以 packaging 的 SpecifierSet 与 Version 解析并匹配完整 PEP 440 约束，复合约束、排除、兼容发布及 pre/post/dev 语义均由其处理，非法 spec 与 version 分别传播 InvalidSpecifier 与 InvalidVersion；当前源码的指令 run、TestGroup/TestCode 初始化及 Builder 执行、统计、报告主体被遮罩，具体实现未知，不得据接口补造；可见初始化会把 doctest.compile 全局替换为 Builder.compile、把 doctest_path 前插 sys.path、打开 UTF-8 output.txt并写带当前时间的标题，所有发现文档均视为过期且目标 URI 为空；公开文档规定同一文档各组先执行全部 setup、再按出现顺序执行测试、最后 cleanup，空组名为 default而 * 归入所有组，skipif 真值使对应指令不参与，testcode 整块执行且由 testoutput 给预期输出；默认 flags 为 DONT_ACCEPT_TRUE_FOR_1、ELLIPSIS、IGNORE_EXCEPTION_DETAIL，doctest_fail_fast 默认假，成功展示默认真，扩展只声明并行读取安全；pyversion、hide、trim/no-trim 和 options 的可见选项由各指令分别限制。遮罩区域中的异常处理、命名空间共享、失败计数、状态码、output.txt 其余格式及 fail-fast 细节未知"
  },
  "call_ref": "item_23"
}
```

## 35. tool / tool_output

```
{
  "output": {
    "result": {
      "content": [
        {
          "type": "text",
          "text": "已提交 sphinx/ext/doctest.py 的纲要，指纹已前移，状态：对齐"
        }
      ],
      "structured_content": null
    },
    "error": null,
    "status": "completed"
  },
  "call_ref": "item_23"
}
```

## 36. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_25",
    "type": "command_execution",
    "command": "/bin/bash -lc \"find tests -type f -name '*.py' | grep -E 'doctest|test_build' | sort | head -200\npython - <<'PY'\nfrom packaging.specifiers import InvalidSpecifier\nfrom packaging.version import InvalidVersion\nfrom sphinx.ext.doctest import is_allowed_version\n\ncases = [\n    ('<=3.5', '3.3', True),\n    ('<=3.2', '3.3', False),\n    ('>3.2, <4.0', '3.3', True),\n    ('>=2.7, \"'!=3.0.*, !=3.1.*'\"', '2.7.18', True),\n    ('>=2.7, \"'!=3.0.*, !=3.1.*'\"', '3.1.9', False),\n    ('==3.8.*', '3.8.12', True),\n    ('~=3.7.0', '3.7.9.post1', True),\n    ('~=3.7.0', '3.8.0', False),\n    ('>=1.0', '1.1a1', False),\n    ('>=1.0a1', '1.1a1', True),\n    ('>=1.0.dev1', '1.0.dev2', True),\n    ('==1.0', '1.0+local', True),\n]\nfor spec, version, expected in cases:\n    actual = is_allowed_version(spec, version)\n    assert actual is expected, (spec, version, actual, expected)\n\nfor spec, version, error in [\n    ('not a specifier', '1.0', InvalidSpecifier),\n    ('>=1.0', 'not a version', InvalidVersion),\n]:\n    try:\n        is_allowed_version(spec, version)\n    except error:\n        pass\n    else:\n        raise AssertionError(f'{error.__name__} not raised')\nprint(f'{len(cases) + 2} predicate checks passed')\nPY\npython -m compileall -q sphinx/ext/doctest.py\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 37. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"find tests -type f -name '*.py' | grep -E 'doctest|test_build' | sort | head -200\npython - <<'PY'\nfrom packaging.specifiers import InvalidSpecifier\nfrom packaging.version import InvalidVersion\nfrom sphinx.ext.doctest import is_allowed_version\n\ncases = [\n    ('<=3.5', '3.3', True),\n    ('<=3.2', '3.3', False),\n    ('>3.2, <4.0', '3.3', True),\n    ('>=2.7, \"'!=3.0.*, !=3.1.*'\"', '2.7.18', True),\n    ('>=2.7, \"'!=3.0.*, !=3.1.*'\"', '3.1.9', False),\n    ('==3.8.*', '3.8.12', True),\n    ('~=3.7.0', '3.7.9.post1', True),\n    ('~=3.7.0', '3.8.0', False),\n    ('>=1.0', '1.1a1', False),\n    ('>=1.0a1', '1.1a1', True),\n    ('>=1.0.dev1', '1.0.dev2', True),\n    ('==1.0', '1.0+local', True),\n]\nfor spec, version, expected in cases:\n    actual = is_allowed_version(spec, version)\n    assert actual is expected, (spec, version, actual, expected)\n\nfor spec, version, error in [\n    ('not a specifier', '1.0', InvalidSpecifier),\n    ('>=1.0', 'not a version', InvalidVersion),\n]:\n    try:\n        is_allowed_version(spec, version)\n    except error:\n        pass\n    else:\n        raise AssertionError(f'{error.__name__} not raised')\nprint(f'{len(cases) + 2} predicate checks passed')\nPY\npython -m compileall -q sphinx/ext/doctest.py\""
  },
  "call_ref": "item_25"
}
```

## 38. tool / tool_output

```
{
  "output": {
    "output": "tests/roots/test-ext-doctest-fail-fast/conf.py\ntests/roots/test-ext-doctest-skipif/conf.py\ntests/roots/test-ext-doctest-with-autodoc/conf.py\ntests/roots/test-ext-doctest-with-autodoc/dir/__init__.py\ntests/roots/test-ext-doctest-with-autodoc/dir/bar.py\ntests/roots/test-ext-doctest-with-autodoc/foo.py\ntests/roots/test-ext-doctest/conf.py\ntests/roots/test-trim_doctest_flags/conf.py\ntests/test_builders/__init__.py\ntests/test_builders/conftest.py\ntests/test_builders/test_build.py\ntests/test_builders/test_build_all.py\ntests/test_builders/test_build_changes.py\ntests/test_builders/test_build_dirhtml.py\ntests/test_builders/test_build_epub.py\ntests/test_builders/test_build_gettext.py\ntests/test_builders/test_build_html.py\ntests/test_builders/test_build_html_5_output.py\ntests/test_builders/test_build_html_assets.py\ntests/test_builders/test_build_html_code.py\ntests/test_builders/test_build_html_copyright.py\ntests/test_builders/test_build_html_download.py\ntests/test_builders/test_build_html_highlight.py\ntests/test_builders/test_build_html_image.py\ntests/test_builders/test_build_html_maths.py\ntests/test_builders/test_build_html_numfig.py\ntests/test_builders/test_build_html_tocdepth.py\ntests/test_builders/test_build_html_toctree.py\ntests/test_builders/test_build_latex.py\ntests/test_builders/test_build_linkcheck.py\ntests/test_builders/test_build_manpage.py\ntests/test_builders/test_build_texinfo.py\ntests/test_builders/test_build_text.py\ntests/test_builders/test_build_warnings.py\ntests/test_builders/test_incremental_reading.py\ntests/test_builders/xpath_data.py\ntests/test_builders/xpath_html_util.py\ntests/test_builders/xpath_util.py\n14 predicate checks passed\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_25"
}
```

## 39. assistant / message

```
函数现已恢复，14 个覆盖比较、通配排除、兼容发布、pre/post/dev/local 版本及两类非法输入的直接检查均通过。由于这份工作树刻意遮罩了 doctest 扩展的其他实现，我只对该公开谓词做独立验收，并再检查差异与静态规则，避免触碰任务外代码。
```

## 40. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_28",
    "type": "command_execution",
    "command": "/bin/bash -lc 'git diff --check\ngit diff -- sphinx/ext/doctest.py\nruff check sphinx/ext/doctest.py'",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 41. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc 'git diff --check\ngit diff -- sphinx/ext/doctest.py\nruff check sphinx/ext/doctest.py'"
  },
  "call_ref": "item_28"
}
```

## 42. tool / tool_output

```
{
  "output": {
    "output": "diff --git a/sphinx/ext/doctest.py b/sphinx/ext/doctest.py\nindex 1133da0..0f94da2 100644\n--- a/sphinx/ext/doctest.py\n+++ b/sphinx/ext/doctest.py\n@@ -42,6 +42,13 @@\n doctestopt_re = re.compile(r'[ \\t]*#\\s*doctest:.+$', re.MULTILINE)\n \n \n+def is_allowed_version(spec: str, version: str) -> bool:\n+    \"\"\"Return whether *version* satisfies the PEP 440 *spec*.\"\"\"\n+    specifier = SpecifierSet(spec)\n+    parsed_version = Version(version)\n+    return parsed_version in specifier\n+\n+\n \n \n \n@@ -654,4 +661,3 @@ def setup(app: Sphinx) -> ExtensionMetadata:\n \n \n \n-\n/bin/bash: line 3: ruff: command not found\n",
    "exit_code": 127,
    "status": "failed"
  },
  "call_ref": "item_28"
}
```

## 43. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_30",
    "type": "command_execution",
    "command": "/bin/bash -lc 'tail -n 12 sphinx/ext/doctest.py | nl -ba\ngit show HEAD:sphinx/ext/doctest.py | tail -n 12 | nl -ba'",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 44. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc 'tail -n 12 sphinx/ext/doctest.py | nl -ba\ngit show HEAD:sphinx/ext/doctest.py | tail -n 12 | nl -ba'"
  },
  "call_ref": "item_30"
}
```

## 45. tool / tool_output

```
{
  "output": {
    "output": "     1\t        | doctest.IGNORE_EXCEPTION_DETAIL,\n     2\t        '',\n     3\t        types=frozenset({int}),\n     4\t    )\n     5\t    app.add_config_value('doctest_fail_fast', False, '', types=frozenset({bool}))\n     6\t    return {\n     7\t        'version': sphinx.__display_version__,\n     8\t        'parallel_read_safe': True,\n     9\t    }\n    10\t\n    11\t\n    12\t\n     1\t        '',\n     2\t        types=frozenset({int}),\n     3\t    )\n     4\t    app.add_config_value('doctest_fail_fast', False, '', types=frozenset({bool}))\n     5\t    return {\n     6\t        'version': sphinx.__display_version__,\n     7\t        'parallel_read_safe': True,\n     8\t    }\n     9\t\n    10\t\n    11\t\n    12\t\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_30"
}
```

## 46. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_32",
    "type": "file_change",
    "changes": [
      {
        "path": "/testbed/sphinx/ext/doctest.py",
        "kind": "update"
      }
    ],
    "status": "in_progress"
  }
}
```

## 47. tool / event

```
{
  "name": "filechange",
  "output": {
    "id": "item_32",
    "type": "file_change",
    "changes": [
      {
        "path": "/testbed/sphinx/ext/doctest.py",
        "kind": "update"
      }
    ],
    "status": "completed"
  },
  "message_ref": "item_32"
}
```

## 48. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_33",
    "type": "mcp_tool_call",
    "server": "ortg",
    "tool": "ortg_update",
    "arguments": {
      "path": "sphinx/ext/doctest.py",
      "outline": "doctest.py[8 C X E P L]: Role:提供执行文档代码示例并比较输出的 doctest Builder 与 testsetup、testcleanup、doctest、testcode、testoutput 指令，并按 PEP 440 判断版本约束 | Uses:sphinx/builders/__init__.py, sphinx/util/docutils.py | API:is_allowed_version(spec, version)（测试也调用）、TestDirective、TestsetupDirective、TestcleanupDirective、DoctestDirective、TestcodeDirective、TestoutputDirective、TestGroup、TestCode、SphinxDocTestRunner、DocTestBuilder、setup(app)；builder 名 doctest；五个同名指令 | Constraints:is_allowed_version 以 packaging 的 SpecifierSet 与 Version 解析并匹配完整 PEP 440 约束，复合约束、排除、兼容发布及 pre/post/dev 语义均由其处理，非法 spec 与 version 分别传播 InvalidSpecifier 与 InvalidVersion；当前源码的指令 run、TestGroup/TestCode 初始化及 Builder 执行、统计、报告主体被遮罩，具体实现未知，不得据接口补造；可见初始化会把 doctest.compile 全局替换为 Builder.compile、把 doctest_path 前插 sys.path、打开 UTF-8 output.txt并写带当前时间的标题，所有发现文档均视为过期且目标 URI 为空；公开文档规定同一文档各组先执行全部 setup、再按出现顺序执行测试、最后 cleanup，空组名为 default而 * 归入所有组，skipif 真值使对应指令不参与，testcode 整块执行且由 testoutput 给预期输出；默认 flags 为 DONT_ACCEPT_TRUE_FOR_1、ELLIPSIS、IGNORE_EXCEPTION_DETAIL，doctest_fail_fast 默认假，成功展示默认真，扩展只声明并行读取安全；pyversion、hide、trim/no-trim 和 options 的可见选项由各指令分别限制。遮罩区域中的异常处理、命名空间共享、失败计数、状态码、output.txt 其余格式及 fail-fast 细节未知"
    },
    "result": null,
    "error": null,
    "status": "in_progress"
  }
}
```

## 49. assistant / tool_call

```
{
  "name": "ortg_update",
  "server": "ortg",
  "arguments": {
    "path": "sphinx/ext/doctest.py",
    "outline": "doctest.py[8 C X E P L]: Role:提供执行文档代码示例并比较输出的 doctest Builder 与 testsetup、testcleanup、doctest、testcode、testoutput 指令，并按 PEP 440 判断版本约束 | Uses:sphinx/builders/__init__.py, sphinx/util/docutils.py | API:is_allowed_version(spec, version)（测试也调用）、TestDirective、TestsetupDirective、TestcleanupDirective、DoctestDirective、TestcodeDirective、TestoutputDirective、TestGroup、TestCode、SphinxDocTestRunner、DocTestBuilder、setup(app)；builder 名 doctest；五个同名指令 | Constraints:is_allowed_version 以 packaging 的 SpecifierSet 与 Version 解析并匹配完整 PEP 440 约束，复合约束、排除、兼容发布及 pre/post/dev 语义均由其处理，非法 spec 与 version 分别传播 InvalidSpecifier 与 InvalidVersion；当前源码的指令 run、TestGroup/TestCode 初始化及 Builder 执行、统计、报告主体被遮罩，具体实现未知，不得据接口补造；可见初始化会把 doctest.compile 全局替换为 Builder.compile、把 doctest_path 前插 sys.path、打开 UTF-8 output.txt并写带当前时间的标题，所有发现文档均视为过期且目标 URI 为空；公开文档规定同一文档各组先执行全部 setup、再按出现顺序执行测试、最后 cleanup，空组名为 default而 * 归入所有组，skipif 真值使对应指令不参与，testcode 整块执行且由 testoutput 给预期输出；默认 flags 为 DONT_ACCEPT_TRUE_FOR_1、ELLIPSIS、IGNORE_EXCEPTION_DETAIL，doctest_fail_fast 默认假，成功展示默认真，扩展只声明并行读取安全；pyversion、hide、trim/no-trim 和 options 的可见选项由各指令分别限制。遮罩区域中的异常处理、命名空间共享、失败计数、状态码、output.txt 其余格式及 fail-fast 细节未知"
  },
  "call_ref": "item_33"
}
```

## 50. tool / tool_output

```
{
  "output": {
    "result": {
      "content": [
        {
          "type": "text",
          "text": "已提交 sphinx/ext/doctest.py 的纲要，指纹已前移，状态：对齐"
        }
      ],
      "structured_content": null
    },
    "error": null,
    "status": "completed"
  },
  "call_ref": "item_33"
}
```

## 51. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_35",
    "type": "command_execution",
    "command": "/bin/bash -lc \"grep -RIn --include='*.py' -e 'test-ext-doctest' -e 'doctest_fail_fast' -e 'doctest_skipif' tests 2>/dev/null | head -200\ngit diff --check\ngit diff --stat\ngit status --short\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 52. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"grep -RIn --include='*.py' -e 'test-ext-doctest' -e 'doctest_fail_fast' -e 'doctest_skipif' tests 2>/dev/null | head -200\ngit diff --check\ngit diff --stat\ngit status --short\""
  },
  "call_ref": "item_35"
}
```

## 53. tool / tool_output

```
{
  "output": {
    "output": "tests/roots/test-ext-doctest-fail-fast/conf.py:11:# doctest_fail_fast = ...\n sphinx/ext/doctest.py | 8 +++++++-\n 1 file changed, 7 insertions(+), 1 deletion(-)\n M sphinx/ext/doctest.py\n?? ortg.tsv\n?? ortg.tsv.bak\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_35"
}
```

## 54. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_37",
    "type": "command_execution",
    "command": "/bin/bash -lc 'git diff -- sphinx/ext/doctest.py'",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 55. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc 'git diff -- sphinx/ext/doctest.py'"
  },
  "call_ref": "item_37"
}
```

## 56. tool / tool_output

```
{
  "output": {
    "output": "diff --git a/sphinx/ext/doctest.py b/sphinx/ext/doctest.py\nindex 1133da0..0f94da2 100644\n--- a/sphinx/ext/doctest.py\n+++ b/sphinx/ext/doctest.py\n@@ -42,6 +42,13 @@\n doctestopt_re = re.compile(r'[ \\t]*#\\s*doctest:.+$', re.MULTILINE)\n \n \n+def is_allowed_version(spec: str, version: str) -> bool:\n+    \"\"\"Return whether *version* satisfies the PEP 440 *spec*.\"\"\"\n+    specifier = SpecifierSet(spec)\n+    parsed_version = Version(version)\n+    return parsed_version in specifier\n+\n+\n \n \n \n@@ -654,4 +661,3 @@ def setup(app: Sphinx) -> ExtensionMetadata:\n \n \n \n-\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_37"
}
```

## 57. tool / event

```
{
  "name": "item.started",
  "output": {
    "id": "item_40",
    "type": "command_execution",
    "command": "/bin/bash -lc \"nl -ba sphinx/ext/doctest.py | sed -n '38,56p'\npython - <<'PY'\nfrom sphinx.ext.doctest import is_allowed_version\nassert is_allowed_version('>=2.7, \"'!=3.0.*, !=3.1.*, <4'\"', '3.8.19')\nassert not is_allowed_version('~=3.7.0', '3.8.0')\nprint('final smoke test passed')\nPY\"",
    "aggregated_output": "",
    "exit_code": null,
    "status": "in_progress"
  }
}
```

## 58. assistant / tool_call

```
{
  "name": "command_execution",
  "arguments": {
    "command": "/bin/bash -lc \"nl -ba sphinx/ext/doctest.py | sed -n '38,56p'\npython - <<'PY'\nfrom sphinx.ext.doctest import is_allowed_version\nassert is_allowed_version('>=2.7, \"'!=3.0.*, !=3.1.*, <4'\"', '3.8.19')\nassert not is_allowed_version('~=3.7.0', '3.8.0')\nprint('final smoke test passed')\nPY\""
  },
  "call_ref": "item_40"
}
```

## 59. tool / tool_output

```
{
  "output": {
    "output": "    38\t\n    39\tlogger = logging.getLogger(__name__)\n    40\t\n    41\tblankline_re = re.compile(r'^\\s*<BLANKLINE>', re.MULTILINE)\n    42\tdoctestopt_re = re.compile(r'[ \\t]*#\\s*doctest:.+$', re.MULTILINE)\n    43\t\n    44\t\n    45\tdef is_allowed_version(spec: str, version: str) -> bool:\n    46\t    \"\"\"Return whether *version* satisfies the PEP 440 *spec*.\"\"\"\n    47\t    specifier = SpecifierSet(spec)\n    48\t    parsed_version = Version(version)\n    49\t    return parsed_version in specifier\n    50\t\n    51\t\n    52\t\n    53\t\n    54\t\n    55\t\n    56\t\nfinal smoke test passed\n",
    "exit_code": 0,
    "status": "completed"
  },
  "call_ref": "item_40"
}
```

## 60. assistant / message

```
Implemented `is_allowed_version` in [sphinx/ext/doctest.py](/testbed/sphinx/ext/doctest.py:45).

It now:

- Uses `packaging` for full PEP 440 semantics.
- Supports compound constraints, exclusions, compatible releases, and pre/post/dev versions.
- Propagates `InvalidSpecifier` and `InvalidVersion`.
- Passes compilation and 14 focused predicate checks.
```

## 61. tool / event

```
{
  "name": "turn.completed",
  "output": {
    "type": "turn.completed",
    "usage": {
      "input_tokens": 810668,
      "cached_input_tokens": 763776,
      "cache_write_input_tokens": 0,
      "output_tokens": 6260,
      "reasoning_output_tokens": 2697
    }
  }
}
```
