<details>
<summary>OpenSCOW</summary>    
    <details>
    <summary>turbo.json</summary>
    用于定义任务调度和依赖关系。Turbo 是一个现代化的构建工具，支持任务缓存、并行执行和智能依赖追踪。
        <details>
        <summary>dev</summary>
        持久任务，任务的结果不会被缓存。
        </details>
        <details>
        <summary>generate</summary>
        <br>依赖于项目中所有包的 generate 任务
        <br>代码生成任务，用来生成代码（可能是 gRPC 的客户端/服务端代码）。
        <br>输入文件：包括 .proto 文件和 buf.gen.yaml 配置文件
        <br>输出目录：generated，src/generated
        </details>
        <details>
        <summary>build</summary>
        <br>依赖所有包的 build 任务和当前包的 generate 任务
        <br>输出的文件夹：包含 Next.js 输出目录（.next）和项目的打包构建产物（build/**）
        </details>
        <details>
        <summary>prepareDev</summary>
        <br>依赖于 @scow/protos 和 @scow/scheduler-adapter-protos 包的 build 任务
        <br>输入文件夹：包含 src/pages/api/ 下的所有 TypeScript 文件
        <br>输出目录：src/generated
        </details>
        <details>
        <summary>test</summary>
        <br>测试的源文件和测试文件："src//.tsx", "src/**/.ts", "test//*.ts", "test//*.tsx"
        <br>测试任务没有输出
        </details>
        <details>
        <summary>@scow/protos</summary>
        <br>generate代码生成：输入../../../protos/**/*.proto 和 buf.gen.yaml，输出到 generated/**
        <br>build构建任务：依赖 generate，使用生成的文件作为输入，输出到 build/**。
        </details>
        <details>
        <summary>@scow/scheduler-adapter-protos</summary>
        与 @scow/protos 类似，但处理 @scow/scheduler-adapter 相关的 proto 文件。
        </details>
        <details>
        <summary>lint</summary>
        输入："/.proto", "**/.tsx", "/*.ts"
        </details>
    </details>
    <details>
    <summary>tsconfig.json</summary>
    <br>定义了 TypeScript 编译器的选项（compilerOptions），用于控制代码编译和类型检查的行为。
    <br>输出现代 ECMAScript 代码（ESNext）并兼容 Node.js 的 CommonJS 模块系统
    <br>支持 .js 和 .json 文件
    <br>开启模块解析（moduleResolution: node）和跨模块互操作性（esModuleInterop）
    <br>严格模式（strict）提高类型安全
    <br>跳过库检查（skipLibCheck）提高构建性能
    <br>允许部分松散配置（noImplicitAny: false）
    <br>支持实验性装饰器（experimentalDecorators）和元数据生成（emitDecoratorMetadata），适用于框架开发
        <details>
        <summary>target</summary>
        指定编译后代码的目标 ECMAScript 版本
        </details>
        <details>
        <summary>allowJs</summary>
        允许编译器处理 .js 文件
        </details>
        <details>
        <summary>skipLibCheck</summary>
        跳过对声明文件（*.d.ts）的类型检查，加快编译速度，避免因外部库的类型定义错误导致构建失败。
        </details>
        <details>
        <summary>strict</summary>
        启用 TypeScript 的严格模式
        </details>
        <details>
        <summary>forceConsistentCasingInFileNames</summary>
        强制在文件引用中使用一致的大小写
        </details>
        <details>
        <summary>experimentalDecorators</summary>
        启用对装饰器语法的支持
        </details>
        <details>
        <summary>emitDecoratorMetadata</summary>
        在编译输出中生成与装饰器相关的元数据
        </details>
        <details>
        <summary>noImplicitAny</summary>
        允许隐式的 any 类型
        </details>
        <details>
        <summary>esModuleInterop</summary>
        启用对 CommonJS 和 ES 模块的兼容性支持
        </details>
        <details>
        <summary>module</summary>
        指定模块的输出格式为 CommonJS
        </details>
        <details>
        <summary>moduleResolution</summary>
        指定模块解析策略为 Node.js 风格
        </details>
        <details>
        <summary>resolveJsonModule</summary>
        允许导入 JSON 文件
        </details>
        <details>
        <summary>isolatedModules</summary>
        强制每个文件独立编译
        </details>
    </details>
    <details>
    <summary>renovate.json</summary>
    用于配置自动化的依赖更新工具 Renovate。Renovate 通过自动提交 pull requests 来更新依赖库，使得项目保持最新和安全。
        <details>
        <summary>extends</summary>
        该配置继承了 Renovate 的基本配置（config:base）
        </details>
        <details>
        <summary>ignorePaths</summary>
        指定 Renovate 忽略的文件或路径："docker-compose.dev.yml"，"dev/ldap/Dockerfile"，".devcontainer/**"
        </details>
        <details>
        <summary>timezone</summary>
        设置 Renovate 的时区为上海时间（Asia/Shanghai），这会影响 Renovate 的任务调度时间，确保按照该时区的时间进行操作。
        </details>
        <details>
        <summary>schedule</summary>
        every sunday 表示每周日执行一次依赖更新任务
        </details>
        <details>
        <summary>packageRules</summary>
        <br>自动分组次要和修补更新。
        <br>禁用特定文件和包的自动更新，以减少不必要的更新。
        <br>针对特定包禁用更新，可能是由于稳定性、兼容性等原因。
        </details>
    </details>
    <details>
    <summary>pnpm-workspace.yaml</summary>
    指定了项目中的特定文件和目录路径，以便选择或排除某些内容。它通常用于指定在构建、测试、发布等过程中需要关注的文件和目录，或者是用于管理依赖、模块、文档等。
        <details>
        <summary>代码库和应用程序</summary>
        libs/** 和 apps/**
        </details>
        <details>
        <summary>文档目录</summary>
        docs
        </details>
        <details>
        <summary>排除 Next.js 构建产物</summary>
        !**/.next
        </details>
        <details>
        <summary>协议定义文件</summary>
        protos
        </details>
        <details>
        <summary>部署和开发相关的文件</summary>
        deploy/** 和 dev/**
        </details>
    </details>
    <details>
    <summary>package.json</summary>
    <br>定义了项目 scow 的基本配置，包括依赖管理、构建、测试、开发环境等任务的 NPM 脚本，以及开发过程中所使用的工具和库。
    <br>使用 Turbo 加速构建和任务运行。
    <br>pnpm 用作包管理器，优化依赖管理。
    <br>配置了 Docker 和其他开发工具（如 Husky 和 ESLint）。
    <br>版本和发布流程也得到了支持。
        <details>
        <summary>项目基本信息</summary>
        <br>name: "scow" — 项目的名称。
        <br>private: true — 该项目是私有的，不会发布到 npm 注册库。
        <br>version: "1.6.3" — 项目的版本号。
        </details>
        <details>
        <summary>scripts</summary>
        <br>build: turbo run build — 使用 Turbo 工具来构建整个项目。
        <br>build:libs: turbo run build --filter "./libs/**" — 只构建 libs 目录下的库。
        <br>build:images: docker build -f docker/Dockerfile.scow -t scow . — 使用 Docker 构建镜像。
        <br>build:protos: turbo run build --filter "./libs/protos/**" — 只构建 libs/protos 目录下的 Protobuf 文件。
        <br>prepareDev: pnpm build:libs && turbo run prepareDev — 先构建库，然后运行 prepareDev。
        <br>prune: pnpm clean --yes && pnpm bootstrap --ci -- --production — 清理并在 CI 环境中以生产模式重建项目。
        <br>dev:libs: turbo run dev --concurrency 100% --filter "./libs/**" — 在开发模式下，针对 libs 目录下的所有库运行脚本。
        <br>devenv: docker compose --env-file dev/.env.dev -f dev/docker-compose.dev.yml up -d — 使用 Docker Compose 启动开发环境。
        <br>devenv:stop: docker compose --env-file dev/.env.dev -f dev/docker-compose.dev.yml down — 停止开发环境中的 Docker 容器。
        <br>test: turbo run test — 使用 Turbo 工具运行测试。
        <br>test:ci: pnpm run -r test --ci --coverage --runInBand — 在 CI 环境中运行测试，并生成测试覆盖率报告。
        <br>prepare: 用于初始化 Husky（Git 钩子管理工具），确保所有的 Git 钩子正确配置。
        <br>lint: turbo run lint --continue — 使用 Turbo 工具运行代码检查，并且在发现错误时继续运行。
        <br>ci:version: node scripts/version.mjs — 生成项目版本信息。
        <br>ci:publish: pnpm publish -r — 发布项目。
        <br>api:breaking: 运行 Protobuf 文件的版本断裂检测，确保 API 兼容性。
        </details>
        <details>
        <summary>devDependencies</summary>
        <br>@bufbuild/buf: 用于管理和生成 Protobuf 文件。
        <br>@changesets/cli: 用于版本管理和生成变更日志。
        <br>eslint 和 @ddadaal/eslint-config: 用于代码静态分析和检查。
        <br>jest 和 ts-jest: 用于测试框架和 TypeScript 支持。
        <br>typescript: TypeScript 支持。
        <br>turbo: Turbo 工具，用于加速 monorepo 构建和任务运行。
        <br>pnpm: 项目使用的包管理器。
        </details>
        <details>
        <summary>volta</summary>
        node: "20.15.0" — 指定该项目使用的 Node.js 版本为 20.15.0。
        </details>
        <details>
        <summary>packageManager</summary>
        pnpm@9.4.0 — 项目使用 pnpm 作为包管理器，并指定了其版本。
        </details>
        <details>
        <summary>pnpm</summary>
        patchedDependencies: 为 react-typed-i18n 和 next 两个包提供了补丁文件，用于修复某些问题或调整特性。
        </details>
    </details>
    <details>
    <summary>eslint.config.js</summary>
    <br>一个 ESLint 配置文件，主要用于 JavaScript/TypeScript 项目的代码质量检查和自动化处理。它配置了多个规则，插件以及自定义的设置。
    <br>忽略了一些常见的文件夹和文件。
    <br>定义了较为宽松的 TypeScript 规则，避免了严格的类型检查和异步函数使用要求。
    <br>强制要求每个文件包含版权头。
    <br>基于扩展的方式引入了外部配置（@ddadaal/eslint-config），实现了配置的复用和统一管理。
    </details>
    <details>
    <summary>codecov.yml</summary>
    <br>某个工具（如代码质量管理工具、CI/CD 配置文件等）中的一部分配置，专注于代码覆盖率的报告和状态显示。它配置了项目的覆盖率状态，具体来说是针对 project 和 patch 两个级别的报告。
    <br>不论是整个项目的覆盖率，还是每个补丁的覆盖率，都将被标记为“信息性”，即它们只会作为信息提示显示，不会影响构建状态或标记为失败。这种配置通常用于持续集成/持续部署（CI/CD）流程中，提供代码覆盖率的透明性，而不强制要求一定的覆盖率水平。
    </details>
    <details>
    <summary>scripts</summary>
        <details>
        <summary>scripts/copyDist.mjs</summary>
        <br>将指定的应用程序及其依赖库的必要文件复制到 dist 文件夹中，通常用于构建或部署过程中。
        <br>假设你有一个名为 mis-server 的应用位于 apps 目录中，并且你希望将它的必要文件复制到 dist 目录，你可以运行：
        <br>node scripts/copyDist.mjs apps/mis-server
        <br>这会将 mis-server 应用的必要文件以及任何相关的 @scow/ 库文件复制到 dist 目录中。
            <details>
            <summary>默认复制的源路径，默认复制到的目标路径，总是需要复制的根目录文件，默认复制的文件</summary>
                <br>APPS_BASE_PATH: 应用程序（apps）所在的基本路径，默认为 "apps"。
                <br>DIST_BASE_PATH: 文件将被复制到的目标文件夹，默认为 "dist"。
                <br>ROOT_ITEMS: 总是需要复制的根目录文件（如 package.json、pnpm-lock.yaml）。
                <br>DEFAULT_COPY_ITEMS: 默认复制的文件，当应用的 package.json 中没有指定文件时。
            </details> 
            <details>
            <summary>pnpm-lock.yaml</summary>
                <br>脚本读取根目录下的 pnpm-lock.yaml 文件，识别应用程序的依赖项。如果找不到锁文件，脚本会抛出错误。
            </details> 
            <details>
            <summary>默认复制的目录</summary>
                <br>如果没有传递任何目录，脚本会使用一个默认的应用目录列表（如 portal-web、portal-server 等）
            </details> 
            <details>
            <summary>复制的处理过程</summary>
                <br>对于每个应用，脚本会读取 package.json 文件，查找 "files" 字段中列出的文件。
                <br>脚本会排除 TypeScript 文件（!**/*.ts）。
                <br>最终返回一个文件列表，包含了默认的文件（如 package.json）和 package.json 中 "files" 字段指定的文件。
            </details> 
            <details>
            <summary>复制过程</summary>
                <br>创建 dist 文件夹: 如果 dist 文件夹不存在，脚本会创建它。
                <br>复制根目录文件: 将 ROOT_ITEMS 中列出的根目录文件复制到 dist 文件夹。
                <br>复制应用程序文件: 对于每个应用目录，脚本会将需要的文件复制到 dist 中相应的目录。
                <br>复制库依赖文件: 对于每个应用，脚本会检查其依赖项（从 pnpm-lock.yaml 文件中获取）。如果依赖项以 @scow/ 开头且尚未复制过，脚本会将该库的文件复制到 dist 中。
            </details> 
            <details>
            <summary>依赖项处理</summary>
                <br>依赖项通过 copiedLibs 集合进行追踪，确保每个库只被复制一次。
                <br>对于每个依赖项，脚本会检查它是否以 @scow/ 开头，如果是且尚未复制，脚本会复制该库的文件。
            </details> 
            <details>
            <summary>错误处理</summary>
                <br>如果找不到 pnpm-lock.yaml 文件，脚本会抛出错误（No lockfile found）。
                <br>如果应用的 package.json 没有指定 "files" 字段，脚本会抛出错误（No files specified in package.json）。
            </details> 
        </details>
        <details>
        <summary>scripts/createVersionFile.mjs</summary>
        <br>生成一个 JSON 文件，记录当前 Git 仓库的提交哈希值和当前分支的标签信息。
        <br>具体操作流程：
        <br>读取命令行参数：获取输出文件路径。
        <br>调用 Git 命令：获取当前提交关联的标签。获取当前提交的哈希值。
        <br>生成 JSON 文件：创建包含 tag 和 commit 的对象。将对象写入指定路径的 JSON 文件。
        <br>使用示例：
        <br>node scripts/createVersionFile.mjs version.json
        <br>如果未提供文件路径，则默认生成的文件名为 version.json。
            <details>
            <summary>具体处理：需要提供生成的文件名及路径</summary>
                <br>let outputFile = process.argv[2] || "version.json";
                <br>process.argv[2]：表示用户运行脚本时提供的第一个参数，指定生成的 JSON 文件路径。
                <br>如果用户未提供参数，脚本默认将文件生成在当前目录下，文件名为 version.json。
            </details> 
            <details>
            <summary>辅助函数 exec，用于从 Git 仓库中获取所需的版本信息</summary>
                <br>调用 Node.js 的 execSync 函数执行同步命令，并以 UTF-8 编码返回结果。
            </details> 
            <details>
            <summary>获取 Git 标签和提交哈希</summary>
                <br>git tag --points-at HEAD：获取当前提交（HEAD）指向的所有 Git 标签。结果通过 split("\n") 转换为数组。
                <br>git rev-parse HEAD：获取当前提交（HEAD）的完整哈希值。trim() 用于去除返回值中的多余空白字符。
            </details> 
            <details>
            <summary>构建版本对象</summary>
                <br>如果存在标签，取第一个标签（tags[0]）。
                <br>如果没有标签，设为 undefined。
                <br>当前提交的完整哈希值。
            </details> 
            <details>
            <summary>写入 JSON 文件</summary>
                <br>调用 writeFileSync 将 versionObject 写入文件：
                <br>outputFile：文件的输出路径。
                <br>JSON.stringify(versionObject)：将 versionObject 转换为 JSON 格式字符串。
            </details> 
        </details>
        <details>
        <summary>scripts/tag.mjs</summary>
        <br>检查两个 package.json 文件的版本信息是否有更新（当前版本与上一次提交中的版本对比）。如果版本发生变化，脚本会在 Git 仓库中创建相应的标签并将标签推送到远程仓库。
        <br>具体功能流程：
        <br>对比当前版本与上一次提交版本（HEAD^1）：检查根目录的 package.json 文件版本。检查 protos/package.json 文件版本。
        <br>如果发现版本发生变化：为根目录版本创建标签（如 v1.0.0）。为 SCOW API 版本创建标签（如 api-v1.0.0）。推送所有创建的标签到远程仓库。
        <br>使用方法：
        <br>普通模式：node scripts/tag.mjs ————脚本会根据版本变化实际执行创建和推送标签的操作。
        <br>模拟模式（--dry-run）：node scripts/tag.mjs --dry-run ————脚本只会输出将要执行的命令，但不会真的执行。
        </details>
        <details>
        <summary>scripts/version.mjs</summary>
        <br>对当前项目的代码和版本变更进行汇总、处理，并生成更新日志（changelog），得到的是github上release里面的内容
        <br>具体功能：
        <br>版本管理：自动更新版本号，无需手动修改。
        <br>变更可追溯性：每次代码更新都记录到变更日志，便于开发团队和用户查看改动。
        <br>统一变更格式：根据变更类型生成规范化日志，清晰表达更新的重要性。
        <br>使用流程：
        <br>假设：.changeset 包含以下文件：001.md：对 portal-web 进行了一次小型更新。002.md：对 scheduler-adapter-protos 进行了一次重大更新。当前 portal-web 的版本从 1.0.0 升级到 1.1.0。
        <br>运行脚本：
        <br>node scripts/your-script.mjs
        <br>![image](https://github.com/user-attachments/assets/c99e4af6-c55b-4e7d-8f69-d15f0d4e0ea1)
        <br>![image](https://github.com/user-attachments/assets/c44e6676-3420-487f-b7dd-ee2798218703)
        </details>
    </details>
    <details>
    <summary>protos</summary>
        <details>
        <summary>protos/package.json</summary>
        <br>描述了一个 npm 包的基本信息和配置信息
        <br>描述和配置 SCOW 项目的 gRPC API 模块
        <br>作为 @scow 命名空间下的一个子模块，提供 gRPC 接口定义相关功能。
        <br>使用 version 字段跟踪当前接口的版本号，便于发布和更新。
        <br>lint 脚本通过 buf lint 保证 protobuf 文件的质量。
        <br>breaking 脚本使用 buf breaking 验证接口定义的变更是否会破坏与旧版本的兼容性。
        <br>包含了清晰的描述、作者、许可证信息及代码仓库地址。
            <details>
            <summary>scripts</summary>
                <br>lint:命令为 buf lint。使用 Buf 工具对 protobuf 文件进行 lint（语法检查），确保接口定义符合规范。
                <br>breaking:命令为 buf breaking --against '../.git#subdir=protos'。用于检查当前 protobuf 文件的接口是否与以前版本不兼容。参数 --against '../.git#subdir=protos'：指定将当前代码与 git 历史中 protos 子目录的代码进行对比。
            </details> 
            <details>
            <summary>基本信息</summary>
                <br>脚本读取根目录下的 pnpm-lock.yaml 文件，识别应用程序的依赖项。如果找不到锁文件，脚本会抛出错误。
                <br>name:包名称为 @scow/grpc-api。@scow 是命名空间，表明这是一个属于 SCOW 项目的子包。
                <br>private:设置为 false，表示此包不是私有包，可以发布到 npm 公共仓库（尽管这里似乎没有实际计划发布）。
                <br>version:当前版本为 1.12.0，使用语义化版本（Semantic Versioning）。
                <br>description:描述为 “The gRPC API for SCOW”，表明这个包定义了 SCOW 项目的 gRPC 接口。
                <br>main:主入口文件为 index.js。暗示此包可能包含或导出 JavaScript 文件（虽然 gRPC 通常与 protobuf 相关）。
                <br>author:作者为 PKUHPC，链接到其 GitHub 主页。
                <br>license:使用的是 “Mulan PSL v2”（木兰开源协议 2.0），表明该项目遵循中国的开源协议。
                <br>repository:项目代码的版本库地址，存放于 GitHub。
            </details> 
        </details>
        <details>
        <summary>protos/buf.yaml</summary>
        <br>一个配置文件，可能与 Buf 工具相关，用于管理和验证 gRPC 的 protobuf 文件
        <br>具体操作流程：
        <br>版本控制：通过 version: v1 维护配置文件的语义化版本管理。
        <br>接口兼容性检查：使用 breaking 检测修改是否破坏兼容性，保护已有系统或客户端的正常运行。
        <br>代码规范检查：lint 确保 protobuf 文件的书写符合行业或项目的约定。排除部分规则以适应具体的项目需求。
        </details>
        <details>
        <summary>protos/CHANGELOG.md</summary>
        <br>@scow/grpc-api的版本更新的日志，讲了每次更新了哪些问题
        </details>
        <details>
        <summary>protos/audit</summary>
            <details>
            <summary>protos/audit/operation_log.proto</summary>
            <br>全面定义了 SCOW 系统的 gRPC 消息协议，是服务端和客户端进行通信的基础。
            <br>具体功能：
            <br>用户登录与登出，作业管理（SubmitJob+EndJob），创建远程桌面会话，删除远程桌面会话。创建、删除文件和目录，文件分片上传与合并。文件移动和复制，添加/移除用户到账户，设置/取消账户管理员权限，用户封禁/解封，创建租户，设置/取消租户管理员，财务权限设置，设置/取消平台管理员权限
            <br>设置平台计费规则，为账户设置消费限制，处理充值。设置租户的计费规则。UNKNOWN = 0; // 未知SUCCESS = 1; // 成功FAIL = 2;    // 失败
            <br>管理数据集。管理算法版本。账户的创建、充值、消费记录导出。租户的账户列表、消费记录管理。设置/移除租户管理员。用户租户的变更操作。操作日志导出。自定义类型的事件支持，允许用户通过 name 和 content 自定义事件内容。
            </details>
            <details>
            <summary>protos/audit/statistic.proto</summary>
            <br>一个围绕系统使用和活动统计的服务。
            <br>具体功能：
            <br>GetActiveUserCount用于统计某个时间范围内的活跃用户数。支持按时区调整统计基准。
            <br>GetPortalUsageCount 和 GetMisUsageCount统计系统中不同操作类型的使用情况。响应中包含多个操作类型及其对应的使用计数。
            <br>![image](https://github.com/user-attachments/assets/ce3ab6a7-4ea0-4756-a8ac-32447050a8ae)
            <br>![image](https://github.com/user-attachments/assets/b0be60a6-1ee2-4462-b48f-c513358c8253)
            </details>
        </details>
        <details>
        <summary>protos/common</summary>
            <details>
            <summary>protos/common/config.proto</summary>
            <br>获取集群配置GetClusterConfig: 按集群 ID 查询其具体配置，返回调度器名称及分区信息。
            <br>获取用户可用分区GetAvailablePartitionsForCluster: 根据用户账户和 ID 获取用户可用的分区信息。
            <br>获取集群配置文件GetClusterConfigFiles: 返回 SCOW 部署中所有集群的配置文件内容。
            <br>获取 API 版本GetApiVersion: 提供 SCOW API 的版本信息，便于其他服务接入。
            <br>![image](https://github.com/user-attachments/assets/7abec485-11dd-444d-9405-a00bad92c9ec)
            <br>![image](https://github.com/user-attachments/assets/b3ea5a57-683b-4c0d-a9fd-c108eb371fc6)
            <br>![image](https://github.com/user-attachments/assets/93aecdaf-af61-4ba3-9dfd-656b128b6e08)
            </details>
            <details>
            <summary>protos/common/ended_job.proto</summary>
            <br>这个 proto 文件定义了 JobInfo 消息，表示一个作业的详细信息，主要用于记录作业的提交、执行和资源使用情况。
            <br>具体功能：
            <br>基本作业信息
                <br>bi_job_index：作业的唯一标识符，通常是数据库中的主键或内部生成的 ID。
                <br>id_job：作业 ID，可能是作业调度系统（如 Slurm）的标识符。
                <br>account：提交作业的账户。
                <br>user：提交作业的用户。
                <br>partition：作业运行的分区名。
                <br>nodelist：作业分配的节点列表。
            <br>作业的时间信息
                <br>time_submit：作业提交时间。
                <br>time_start：作业开始执行时间。
                <br>time_end：作业结束时间。
                <br>record_time：作业信息记录的时间。
            <br>资源请求与分配
                <br>gpu：请求的 GPU 数量。
                <br>cpus_req：请求的 CPU 数量。
                <br>mem_req：请求的内存（MB）。
                <br>nodes_req：请求的节点数。
                <br>cpus_alloc：实际分配的 CPU 数量。
                <br>mem_alloc：实际分配的内存（MB）。
                <br>nodes_alloc：实际分配的节点数。
            <br>作业运行时限和实际使用
                <br>timelimit：作业的时间限制（秒）。
                <br>time_used：作业实际使用的时间（秒）。
                <br>time_wait：作业在队列中等待的时间（秒）。
            <br>作业的质量服务和费用信息
                <br>qos：作业的服务质量（Quality of Service）标识。
                <br>tenant_price：租户层级的费用。
                <br>account_price：账户层级的费用。
            </details>
            <details>
            <summary>protos/common/i18n.proto</summary>
            <br>该 proto 文件定义了用于国际化（i18n）处理的消息类型，主要用于支持多语言环境下的文本显示。
            <br>I18nObject:I18nObject 包含一个嵌套消息 I18n，用于描述多语言的文本信息。该消息支持三种语言：default：默认语言文本。en：英文文本（可选）。zh_cn：简体中文文本（可选）。
            <br>I18nStringProtoType:I18nStringProtoType 采用 oneof 来表示两种可能的值：direct_string：直接的字符串（适用于没有多语言需求的场景）。i18n_object：包含多语言支持的 I18nObject，适用于需要多语言支持的场景。
            </details>
            <details>
            <summary>protos/common/job.proto</summary>
            <br>这个 proto 文件定义了一个名为 RunningJob 的消息类型，表示正在运行的作业的详细信息。
            <br>job_id (string)：作业的唯一标识符。partition (string)：作业所属的分区。name (string)：作业名称。user (string)：提交作业的用户。state (string)：当前作业的状态。running_time (string)：作业的运行时间。nodes (string)：作业使用的计算节点列表。
            <br>nodes_or_reason (string)：如果作业没有分配到节点，则可能包含作业未分配原因。account (string)：提交作业的账户名。cores (string)：作业请求的核心数。gpus (string)：作业请求的 GPU 数量。qos (string)：作业的质量等级（Quality of Service）。
            <br>submission_time (string)：作业提交的时间。time_limit (string)：作业的时间限制，格式为 days-hours:minutes:seconds，可以是 "NOT_SET" 或 "UNLIMITED"。working_dir (string)：作业的工作目录。
            </details>
            <details>
            <summary>protos/common/money.proto</summary>
            <br>这个 Money 消息在 proto3 语法中用于表示货币金额。
            <br>positive (bool)该字段表示货币值是正数还是负数。它可以用于表示信用（正数）和借记（负数），或处理退款和支付等场景。
            <br>yuan (uint64)该字段存储货币的整数部分，假设是以人民币（元）为单位。使用 uint64 类型表示，可以处理较大的金额。
            <br>decimal_place (uint32)该字段表示货币的精确小数部分，最多可保留四位小数。它通常用于表示“分”的值（人民币单位的百分之一）。比如 12.3456 元就会在这里使用 12 和 3456 分别存储整数和小数部分。
            </details>
            <details>
            <summary>protos/common/sort_order.proto</summary>
            <br>这是一个简单的 proto3 消息定义，定义了一个名为 SortOrder 的枚举类型，用于表示排序顺序。
            <br>枚举定义 SortOrderASCEND (值 0): 表示升序排序。DESCEND (值 1): 表示降序排序。
            </details>
        </details>
        <details>
        <summary>protos/google</summary>
            <details>
            <summary>protos/google/type</summary>
                <details>
                <summary>protos/google/type/date.proto</summary>
                <br>这是一个描述日期的 proto3 消息定义，定义了一个 Date 类型，用于表示一个完整的或部分的日历日期。它的主要用途是表示像生日、纪念日、信用卡到期日期等日期信息。该消息支持不同的日期粒度，可以只包含年份、月份，或者是完整的日期。
                <br>year (字段编号 1)：表示年份，取值范围是 1 到 9999，或者为 0 用于表示没有年份的日期（例如只包含月份和日期的情况）。
                <br>month (字段编号 2)：表示月份，取值范围是 1 到 12，或者为 0 用于表示没有月份和日期的年份（例如只有年份的日期）。
                <br>day (字段编号 3)：表示日期，取值范围是 1 到 31，且必须是该年份和月份有效的日期，或者为 0 用于表示只包含年份和月份的日期（例如只包含年和月而不关心具体日期的场景）。
                </details>
            </details>
        </details>
        <details>
        <summary>protos/hook</summary>
            <details>
            <summary>protos/hook/hook.proto</summary>
            <br>这是一个定义了多个消息类型和事件钩子的 Protobuf 文件，主要用于处理与账户、用户、支付、作业等相关的事件。这些消息类型涵盖了不同的事件场景，如账户的创建、冻结、解冻、用户的添加、作业的保存、账户或租户的支付等。
            <br>AccountBlocked：表示账户被冻结。包含 account_name 和 tenant_name，分别表示账户名称和租户名称。
            <br>AccountUnblocked：表示账户解冻。包含 account_name 和 tenant_name。
            <br>AccountCreated：表示账户的创建。包含 account_name、tenant_name、owner_id 和 comment（可选字段，用于备注）。
            <br>UserBlockedInAccount：表示账户内的某个用户被冻结。包含 user_id 和 account_name。
            <br>UserUnblockedInAccount：表示账户内的某个用户解冻。包含 user_id 和 account_name。
            <br>UserCreated：表示用户的创建。包含 user_id 和 tenant_name。
            <br>UserAdded：表示用户被添加到租户中。包含 user_id 和 tenant_name。
            <br>AccountPaid：表示账户支付了某笔费用。包含 account_name、amount（使用 Money 类型表示）、type（支付类型）、comment（支付的备注）。
            <br>TenantPaid：表示租户支付了某笔费用。包含 tenant_name、amount（使用 Money 类型表示）、type（支付类型）、comment（支付的备注）。
            <br>JobsSaved：表示作业已保存。包含一个 repeated common.JobInfo jobs，用于保存多个作业的信息。
            <br>OnEventRequest：请求消息类型，包含事件的元数据（Metadata），以及实际的事件类型（例如账户冻结、账户支付等）。
            <br>OnEventResponse：响应消息类型，暂时为空（可以用于扩展）。
            </details>
        </details>
        <details>
        <summary>protos/portal</summary>
            <details>
            <summary>protos/portal/app.proto</summary>
            <br>一个基于 gRPC 的协议文件，用于定义和描述与应用程序会话管理相关的服务接口及其数据结构，主要用于一个分布式计算环境的应用门户中
            <br>多语言支持：通过国际化字符串实现不同语言环境的适配。
            <br>资源管理：支持灵活的资源分配配置（如 CPU、GPU、内存等），适用于高性能计算和多用户环境。
            <br>会话管理：提供对应用会话的全面操作，包括创建、查询和连接。
            <br>自定义属性：支持动态定义用户界面字段和选项，满足不同应用的需求。
            <br>用户友好性：通过查询最后一次提交的信息和可用应用列表，简化用户操作。
            <br>提供了应用会话的创建、连接和管理能力，并支持复杂的资源配置和多语言环境。
                <details>
                <summary> 数据结构</summary>
                <br>I18nStringProtoType：支持国际化字符串表示，允许直接字符串或包含多语言对象。
                <br>ConnectToAppRequest 和 ConnectToAppResponse：定义了连接到应用程序的请求和响应：请求包含用户 ID、集群名称和会话 ID。响应包含主机地址、端口、密码及应用程序的连接参数（Web 应用或 VNC）。
                <br>CreateAppSessionRequest 和 CreateAppSessionResponse：定义了创建应用程序会话的请求和响应：请求支持指定用户、集群、应用 ID、账户、资源分配（核心数、节点数、GPU、内存、最大时间等）、自定义属性等。响应返回作业 ID 和会话 ID。
                <br>ListAppSessionsRequest 和 ListAppSessionsResponse：定义列出现有应用会话的请求和响应：请求指定用户和集群。响应返回一组应用会话对象，每个对象包含会话 ID、作业 ID、提交时间、应用状态等信息。
                <br>GetAppMetadataRequest 和 GetAppMetadataResponse：获取应用的元数据信息：请求包含应用 ID 和集群名称。响应返回应用名称、自定义属性（如输入字段类型和选项）、评论等。
                <br>ListAvailableAppsRequest 和 ListAvailableAppsResponse：获取当前可用应用的列表：请求只需要指定集群。响应返回应用的 ID、名称和图标路径。
                <br>GetAppLastSubmissionRequest 和 GetAppLastSubmissionResponse：查询某个用户最近一次提交的信息：请求包含用户 ID、集群和应用 ID。响应返回最后一次提交的作业信息（包括提交时间、资源配置等）。
                </details>
                <details>
                <summary> 核心服务接口</summary>
                <br>I18nStringProtoType：ConnectToApp：用于连接到已存在的应用会话。
                <br>CreateAppSession：创建新的应用程序会话，并指定所需的资源和自定义参数。
                <br>ListAppSessions：列出现有的应用程序会话，便于用户查看和管理。
                <br>GetAppMetadata：获取指定应用的元数据信息，包括属性、名称和说明。
                <br>ListAvailableApps：获取当前集群支持的所有可用应用列表。
                <br>GetAppLastSubmission：获取指定应用的最后一次提交信息，用于快速复用配置。
                </details>
            </details>
            <details>
            <summary>protos/portal/config.proto</summary>
            <br>一个 gRPC 协议，用于获取集群和节点的资源状态信息。主要功能集中在计算集群中各个分区和节点的资源使用率监控、状态查询以及相关信息的服务接口。
            <br>资源监控：提供集群分区和节点的详细资源分配与使用情况，包括 CPU、内存、GPU 的分配、空闲状态。
            <br>状态查询：支持实时查询集群运行状态（例如分区是否可用，节点是空闲还是运行中）。
            <br>灵活性：支持按分区或节点维度查询，满足多样化的监控需求。
            <br>高效管理：管理员可通过接口快速定位资源瓶颈或分区异常，优化资源调度。
                <details>
                <summary> 数据结构</summary>
                <br>PartitionInfo（分区信息）：描述计算集群分区的运行状态，包括：分区名称（partition_name）。节点和 CPU、GPU 的总数、运行中、空闲和不可用数量统计。作业的总数、运行中和挂起中的作业数。分区节点利用率百分比（usage_rate_percentage）。
                                            分区运行状态（PartitionStatus），分为不可用（NOT_AVAILABLE）和可用（AVAILABLE）。
                <br>NodeInfo（节点信息）：描述集群节点的运行状态，包括：节点名称（node_name）。节点所属分区列表。节点状态（NodeState），分为未知（UNKNOWN）、空闲（IDLE）、运行中（RUNNING）和不可用（NOT_AVAILABLE）。CPU 核心数和分配情况（总数、已分配、空闲）。
                                        内存容量及分配情况（总量、已分配、空闲，单位为 MB）。GPU 核心数和分配情况（总数、已分配、空闲）。
                <br>GetClusterInfoRequest 和 GetClusterInfoResponse：请求：指定要查询的集群名称。响应：返回集群名称和其所有分区的资源状态信息（PartitionInfo）。
                <br>GetClusterNodesInfoRequest 和 GetClusterNodesInfoResponse：请求：集群名称（必填）。可选指定节点名称列表（如果为空，表示查询集群所有节点信息）。响应：返回所有匹配的节点信息列表（NodeInfo）。
                </details>
                <details>
                <summary> 核心服务接口</summary>
                <br>GetClusterInfo：功能：查询指定集群的分区信息，包括分区名称、节点和资源统计信息、运行状态等。适用场景：用户希望查看某个集群的整体资源使用情况，例如空闲资源数量、分区可用性等。
                <br>GetClusterNodesInfo：功能：查询指定集群的节点信息，包括节点的运行状态、CPU、GPU 和内存资源的分配和空闲情况。适用场景：用户希望查看某些或所有节点的资源使用详细情况，例如确定空闲的节点用于作业分配。
                </details>
            </details>
            <details>
            <summary>protos/portal/dashboard.proto</summary>
            <br>一组 gRPC 服务接口，用于管理和查询用户在门户（Dashboard）中的快捷入口。快捷入口功能使用户能够快速访问常用的页面、Shell 终端或应用程序
            <br>快捷访问：用户可以通过页面快捷入口快速导航到常用的页面路径。支持集群终端（Shell）入口，方便用户快速连接到目标集群的 Shell 登录节点。提供应用入口，用于启动常用的应用程序。
            <br>自定义配置：用户可以根据需求自定义其快捷入口列表。支持页面、终端、应用三种类型的入口，满足多样化需求。
            <br>统一管理：后台服务提供接口管理所有快捷入口数据，支持快捷入口的查询和保存操作。
            <br>适配图形界面：每个入口都支持与图标库（如 Ant Design）集成，便于前端用户界面的美观与一致性。
                <details>
                <summary> 数据结构</summary>
                <br>PartitionInfo（分区信息）：PageLinkEntry（页面链接入口）：定义一个页面链接快捷入口，包含以下字段：path：页面路径。icon：页面图标的 ID（与 Ant Design 图标库对应）。
                <br>NodeInfo（节点信息）：ShellEntry（Shell 终端入口）：定义一个 Shell 终端快捷入口，包含以下字段：cluster_id：关联的集群 ID。login_node：Shell 登录节点。icon：Shell 图标的 ID（与 Ant Design 图标库对应）。
                <br>AppEntry（应用入口）：定义一个应用快捷入口，包含以下字段：app_id：应用的唯一标识。cluster_id：关联的集群 ID。
                <br>Entry（通用快捷入口）：统一定义了快捷入口的结构，包含以下字段：id：快捷入口的唯一标识。name：快捷入口的名称。entry：快捷入口的类型，支持以下三种：page_link：页面链接入口。shell：Shell 终端入口。app：应用入口。
                <br>GetQuickEntriesRequest 和 GetQuickEntriesResponse：请求：指定用户的 ID。响应：返回该用户的所有快捷入口列表。
                <br>SaveQuickEntriesRequest 和 SaveQuickEntriesResponse：请求：指定用户的 ID 和要保存的快捷入口列表。响应：确认保存操作完成，无返回具体内容。
                </details>
                <details>
                <summary> 核心服务接口</summary>
                <br>GetQuickEntries：功能：获取用户的快捷入口列表。输入：用户 ID。输出：返回该用户设置的快捷入口信息（包括页面链接、Shell 终端和应用入口）。
                <br>SaveQuickEntries：功能：保存用户的快捷入口列表。输入：用户 ID 和快捷入口列表。输出：保存成功的确认响应。
                </details>
            </details>
            <details>
            <summary>protos/portal/desktop.proto</summary>
            <br>定义了一个远程桌面管理服务，支持在高性能计算集群环境中为用户创建、连接和管理远程桌面。
            <br>远程桌面管理：提供创建、连接和关闭远程桌面的完整生命周期管理。允许用户为桌面命名并选择不同的窗口管理器（如 GNOME、KDE）。
            <br>多集群支持：支持不同集群环境的桌面管理操作。可根据登录节点分类和管理用户桌面。
            <br>灵活配置：支持查询集群支持的窗口管理器，方便用户根据需求选择。
            <br>用户友好性：提供快捷的桌面列表查询接口，方便用户查看和管理自己拥有的桌面。
                <details>
                <summary> 数据结构</summary>
                <br>PartitionInfo（分区信息）：CreateDesktopRequest：请求创建一个远程桌面，字段包括：user_id：用户标识。cluster：目标集群标识。login_node：登录节点。wm：桌面窗口管理器的名称。desktop_name：桌面的自定义名称。
                <br>CreateDesktopResponse：响应成功创建的桌面信息，字段包括：host：桌面所在主机。port：连接端口。password：连接桌面的密码。
                <br>KillDesktopRequest：请求关闭一个远程桌面，字段包括：user_id：用户标识。cluster：目标集群标识。login_node：登录节点。display_id：桌面显示 ID。
                <br>KillDesktopResponse：响应关闭操作结果（无具体返回内容）。
                <br>ConnectToDesktopRequest：请求连接到一个已创建的远程桌面，字段包括：user_id：用户标识。cluster：目标集群标识。login_node：登录节点。display_id：桌面显示 ID。
                <br>ConnectToDesktopResponse：返回连接信息，字段包括：host：桌面所在主机。port：连接端口。password：连接密码。
                <br>ListUserDesktopsRequest：请求列出用户当前拥有的远程桌面，字段包括：user_id：用户标识。cluster：目标集群标识。login_node（可选）：指定登录节点，若为空则返回该集群下所有登录节点的桌面。
                <br>Desktop：定义单个桌面信息，字段包括：display_id：桌面显示 ID。desktop_name：桌面名称。wm：窗口管理器名称。create_time：桌面创建时间。
                <br>UserDesktops：定义用户的桌面列表，字段包括：host：主机名。desktops：该主机下的桌面列表。
                <br>ListUserDesktopsResponse：响应用户桌面信息，包含：user_desktops：用户桌面信息的列表。
                <br>ListAvailableWmsRequest：请求列出集群支持的窗口管理器（WMs），字段包括：cluster：目标集群标识。
                <br>AvailableWm：定义一个窗口管理器的信息：name：窗口管理器的名称。wm：窗口管理器的标识符。
                <br>ListAvailableWmsResponse：响应支持的窗口管理器列表：wms：支持的窗口管理器信息列表。
                </details>
                <details>
                <summary> 核心服务接口</summary>
                <br>CreateDesktop：功能：创建一个远程桌面。输入：用户 ID、目标集群、登录节点、窗口管理器和桌面名称。输出：返回创建的桌面连接信息（主机、端口、密码）。
                <br>KillDesktop：功能：关闭指定的远程桌面。输入：用户 ID、目标集群、登录节点和桌面显示 ID。输出：确认关闭结果。
                <br>ConnectToDesktop：功能：获取指定远程桌面的连接信息。输入：用户 ID、目标集群、登录节点和桌面显示 ID。输出：返回桌面的主机、端口和连接密码。
                <br>ListUserDesktops：功能：列出用户当前在集群中的所有远程桌面。输入：用户 ID、目标集群以及（可选）登录节点。输出：返回用户桌面的详细信息列表。
                <br>ListAvailableWms：功能：查询集群支持的窗口管理器（WMs）。输入：目标集群标识。输出：返回支持的窗口管理器列表。
                </details>
            </details>
            <details>
            <summary>protos/portal/file.proto</summary>
            <br>定义了一套完整的文件管理与传输服务，支持在分布式集群环境中实现文件的操作、上传、下载以及跨集群传输等功能。
            <br>通过流式传输、分片管理和实时进度监控等设计，能够高效地支持大数据量的文件操作需求，同时确保文件操作的灵活性和可靠性。
            <br>集群文件管理：提供文件和目录的增删改查功能，方便用户管理集群存储资源。
            <br>大文件分片上传：通过初始化、分片上传和合并机制支持大文件的高效传输。
            <br>高性能计算中的跨集群传输：支持在不同计算集群之间快速传输文件，满足分布式计算需求。
            <br>流式下载：提供对大文件的分块下载支持，适应低带宽或大规模文件传输场景。
                <details>
                <summary> 基础文件操作</summary>
                <br>Copy：拷贝文件或目录。
                <br>CreateFile：创建新文件。
                <br>DeleteDirectory：删除目录。
                <br>DeleteFile：删除文件。
                <br>Move：移动或重命名文件/目录。
                <br>MakeDirectory：创建新目录。
                <br>Exists：检查文件或目录是否存在。
                <br>ReadDirectory：读取指定目录内容，支持返回文件信息（名称、类型、大小、修改时间等）。
                <br>GetHomeDirectory：获取用户在目标集群中的主目录路径。
                <br>GetFileMetadata：获取指定文件的元信息（大小、类型等）。
                </details>
                <details>
                <summary> 文件上传与下载</summary>
                <br>InitMultipartUpload：初始化文件分片上传，返回临时存储目录、分片大小和已上传分片信息。
                <br>Upload：逐步上传文件分片，支持流式传输。
                <br>MergeFileChunks：合并所有上传完成的文件分片，校验完整性后生成完整文件。
                <br>Download：下载文件，支持流式传输返回文件内容（以字节块形式分批返回）。
                </details>
                <details>
                <summary> 跨集群文件传输</summary>
                <br>StartFileTransfer：启动文件从一个集群到另一个集群的传输。
                <br>QueryFileTransfer：查询当前的文件传输进度，返回目标集群、路径、已传输大小、传输速度等信息。
                <br>TerminateFileTransfer：中止文件传输任务。
                <br>CheckTransferKey：校验传输任务的密钥有效性。
                </details>
                <details>
                <summary> 数据结构</summary>
                <br>文件信息（FileInfo）：字段说明：name：文件/目录名称。type：文件类型（FILE 或 DIR）。mtime：修改时间。mode：权限模式（如 UNIX 文件权限）。size：文件大小（字节）。
                <br>传输信息（TransferInfo）：字段说明：to_cluster：目标集群名称。file_path：文件路径。transfer_size_kb：已传输大小（单位：KB）。progress：传输进度（百分比）。speed_k_bps：传输速度（单位：KB/s）。
                </details>
                <details>
                <summary> 错误处理</summary>
                <br>常见错误类型及说明：NOT_FOUND：集群或路径不存在。ALREADY_EXISTS：文件或目录已存在。PERMISSION_DENIED：没有访问权限。INTERNAL：内部错误（如命令失败，具体原因存储于 stderr）。
                </details>
            </details>
            <details>
            <summary>protos/portal/job.proto</summary>
            <br>定义了一套用于高性能计算（HPC）集群环境的作业管理服务，支持从作业提交、查询到模板管理的一整套操作。
            <br>高性能计算作业管理：用户可以提交、取消、查询作业，并管理作业状态。
            <br>模板化作业配置：提供模板功能，便于重复配置常见作业需求。
            <br>多用户、多账户支持：支持按账户或用户管理不同状态的资源，灵活应对复杂的用户环境。
            <br>跨集群操作支持：支持对不同集群的作业管理，适合分布式计算环境。
                <details>
                <summary> 作业管理功能</summary>
                <br>SubmitJob：提交一个新的作业，支持指定分区、节点数、核心数、最长运行时间等配置。
                <br>SubmitFileAsJob：通过脚本文件直接提交作业。
                <br>CancelJob：取消指定作业。
                <br>ListRunningJobs：列出当前正在运行的作业信息。
                <br>ListAllJobs：查询所有作业，支持按时间范围筛选。
                <br>JobInfo（作业信息结构）：字段说明：job_id：作业编号。name：作业名称。state：作业状态（如运行中、完成、失败等）。elapsed：已运行时间。time_limit：最长运行时间。submit_time、start_time、end_time：提交、启动和结束时间。reason：作业状态的原因（如失败原因）。
                                            用途：便于用户查看作业执行的详细状态和运行历史。
                </details>
                <details>
                <summary> 作业模板管理</summary>
                <br>ListJobTemplates：列出用户的所有作业模板。
                <br>GetJobTemplate：获取指定模板的详细内容。
                <br>DeleteJobTemplate：删除指定作业模板。
                <br>RenameJobTemplate：重命名作业模板。
                <br>模板内容：
                <br>JobTemplate（作业模板结构）：字段说明：job_name：作业名称。node_count、core_count、gpu_count：节点数、核心数和 GPU 数量。max_time：最长运行时间及其单位（默认单位为分钟）。command：作业执行命令。output、error_output：输出和错误输出文件路径。
                                working_directory：工作目录。comment：模板注释。
                <br>用途：通过模板快速重复提交相似配置的作业，提高效率。
                </details>
                <details>
                <summary> 用户与账户管理</summary>
                <br>ListAccounts：列出用户在集群中的账户列表，可根据账户状态（如已阻塞、未阻塞）进行筛选。
                <br>AccountStatusFilter：ALL：返回所有账户。BLOCKED_ONLY：仅返回被阻塞的账户。UNBLOCKED_ONLY：仅返回未被阻塞的账户。
                </details>
                <details>
                <summary> 数据结构</summary>
                <br>作业时间单位（TimeUnit）类型：MINUTES（分钟）。HOURS（小时）。DAYS（天）。
                <br>作业信息（JobInfo）：包括作业的基本信息和运行状态（例如 job_id、state、elapsed、reason 等）。
                <br>作业模板信息（JobTemplateInfo）：描述模板的基本属性，如模板 ID、名称、提交时间及备注。
                </details>
                <details>
                <summary> 错误处理</summary>
                <br>NOT_FOUND：集群或作业未找到。
                <br>INTERNAL：调度器内部错误，具体错误信息可通过 details 字段查看。
                <br>BLOCKED_ACCOUNTS_ONLY/UNBLOCKED_ACCOUNTS_ONLY：账户状态限制。
                </details>
            </details>
            <details>
            <summary>protos/portal/shell.proto</summary>
            <br>定义了一种双向流式通信的服务，用于在高性能计算（HPC）环境中实现 远程交互式 Shell 会话。
            <br>远程终端访问：支持 HPC 集群用户通过远程 Shell 登录节点执行命令和操作文件。
            <br>实时交互：提供低延迟的双向通信，支持实时接收命令输出和调整窗口大小。
            <br>动态窗口调整：用户可根据终端需求随时修改窗口的大小（行数和列数）。
            <br>安全会话管理：支持基于用户 ID 和集群环境的会话隔离，确保多用户操作的安全性。
                    <details>
                    <summary> ShellRequest（请求消息）</summary>
                    <br>ShellRequest 提供用户向服务端发送的各种操作消息，包括以下几种类型：
                        <details>
                        <summary> Connect（连接会话）</summary>
                        <br>用途：启动一个远程 Shell 会话。
                        <br>字段说明：cluster：目标集群名称。login_node：指定登录节点。user_id：用户 ID。cols 和 rows：终端窗口的列数和行数（可选）。path：远程登录后的默认路径（可选）。
                        </details>
                        <details>
                        <summary> Resize（调整终端大小）</summary>
                        <br>用途：在会话中动态调整终端窗口大小。
                        <br>字段说明：cols 和 rows：新的列数和行数。
                        </details>
                        <details>
                        <summary> Data（发送数据）</summary>
                        <br>用途：向远程终端发送二进制数据（如用户输入的命令）。
                        </details>
                        <details>
                        <summary> Disconnect（断开连接）</summary>
                        <br>用途：结束当前 Shell 会话。
                        </details>
                    </details>
                    <details>
                    <summary> ShellResponse（响应消息）</summary>
                    <br>ShellResponse 用于服务端返回给客户端的消息，包含以下几种类型：
                        <details>
                        <summary> Data（数据）</summary>
                        <br>用途：将远程终端返回的二进制数据发送给客户端。
                        <br>字段说明：data：二进制数据内容。
                        </details>
                        <details>
                        <summary> Exit（退出信息）</summary>
                        <br>用途：通知客户端会话已结束，并提供退出的状态信息。
                        <br>字段说明：code（可选）：退出码。signal（可选）：退出信号信息。
                        </details>
                    </details>
                    <details>
                    <summary> ShellService</summary>
                    <br>说明：通过双向流式通信实现客户端与服务端之间的实时交互。
                        <details>
                        <summary> 流程：</summary>
                        <br>客户端通过 Connect 消息启动会话。
                        <br>会话期间，客户端可以动态发送 Data（用户输入命令）或 Resize（调整终端大小）。
                        <br>服务端通过 Data 返回终端的输出，或通过 Exit 通知客户端会话结束。
                        <br>客户端发送 Disconnect 结束会话。
                        </details>
                    </details>
            </details>
        </details>
        <details>
        <summary> protos/server</summary>
               <details>
                <summary> protos/server/account.proto</summary>
                <br>该协议定义了一套 账户管理服务，支持对租户（Tenant）下的账户进行 创建、状态管理、白名单管理、账户查询 等操作，适用于高性能计算（HPC）环境中的租户和账户控制。
                <br>资源配额与限制：通过封锁和白名单功能，确保账户资源使用符合业务需求。
                <br>财务管理：支持基于账户余额的封锁阈值动态调整，提高资源利用效率。
                <br>多租户支持：每个租户可以独立管理账户，方便在多用户环境中扩展。
                       <details>
                       <summary> 功能模块</summary>
                               <details>
                                <summary> 账户管理</summary>
                                <br>创建账户：接口：CreateAccount用途：为指定租户创建账户，指定账户所有者。参数：租户名称、账户名称、所有者 ID，以及可选的备注信息。响应：创建成功或失败（例如账户已存在、用户不存在）。
                                <br>查询账户：接口：GetAccounts用途：支持按租户名称或账户名称筛选查询账户信息，也可返回所有账户。响应：包含账户状态（正常、冻结、管理员封锁）、余额、用户数量等信息。
                                </details>
                               <details>
                                <summary> 账户状态控制</summary>
                                <br>封锁账户：接口：BlockAccount用途：手动封锁指定账户，账户无法继续使用。响应：支持返回封锁结果（如已封锁、在白名单中等）。
                                <br>解封账户：接口：UnblockAccount用途：解除账户封锁状态，使其恢复使用。响应：指示解封是否成功。
                                </details>
                               <details>
                                <summary> 账户白名单管理</summary>
                                <br>添加账户至白名单：接口：WhitelistAccount用途：将指定账户加入白名单，避免其因余额不足等被封锁。参数：支持设置备注、白名单过期时间等。响应：指示操作是否成功。
                                <br>从白名单移除账户：接口：DewhitelistAccount用途：将账户从白名单移除，使其受正常规则限制。响应：指示操作是否成功。
                                <br>获取白名单账户：接口：GetWhitelistedAccounts用途：查询租户下当前在白名单中的账户信息。响应：包含账户名、所有者信息、余额、过期时间等。
                                </details>
                               <details>
                                <summary> 阈值设置</summary>
                                <br>设置封锁阈值：接口：SetBlockThreshold用途：为账户设置自定义的余额封锁阈值。参数：阈值金额。响应：指示操作是否成功。
                                </details>
                        </details>
                       <details>
                       <summary> 数据结构</summary>
                               <details>
                                <summary> 账户信息结构：Account</summary>
                                <br>账户状态：NORMAL（正常）、FROZEN（冻结）、BLOCKED_BY_ADMIN（被管理员封锁）。
                                <br>余额信息：当前余额、封锁阈值、自定义默认阈值。
                                <br>显示状态：包括正常、冻结、管理员封锁、低于封锁阈值等。
                                </details>
                        </details>
                       <details>
                       <summary> 服务接口总结</summary>
                               <details>
                                <summary> 账户操作</summary>
                                <br>创建账户：CreateAccount
                                <br>查询账户：GetAccounts
                                </details>
                               <details>
                                <summary> 状态管理</summary>
                                <br>封锁账户：BlockAccount
                                <br>解封账户：UnblockAccount
                                </details>
                               <details>
                                <summary> 白名单管理</summary>
                                <br>添加至白名单：WhitelistAccount
                                <br>从白名单移除：DewhitelistAccount
                                <br>获取白名单账户：GetWhitelistedAccounts
                                </details>
                               <details>
                                <summary> 阈值设置</summary>
                                <br>设置封锁阈值：SetBlockThreshold
                                </details>
                        </details>
                </details>
                <details>
                <summary> protos/server/admin.proto</summary>
                <br>用于平台管理服务，包括存储配额管理、用户数据导入、集群用户查询、数据同步、以及统计信息获取等功能，适用于多租户、高性能计算平台的管理和维护。
                <br>用户和账户管理：批量管理账户与用户，支持灵活的数据导入和同步。
                <br>资源配额控制：动态调整存储配额，满足用户需求并优化资源分配。
                <br>系统维护：自动化同步账户和用户阻塞状态，确保与调度器一致性。
                <br>运营统计：提供用户、账户和租户的增长趋势，支持平台管理决策。
                <br>该协议覆盖了存储管理、账户管理、数据同步及统计分析等关键功能
                       <details>
                       <summary> 功能模块</summary>
                               <details>
                                <summary> 存储配额管理</summary>
                                <br>修改存储配额：接口：ChangeStorageQuota用途：为指定用户调整集群存储配额（增加、减少或直接设定）。参数：用户 ID、集群名称、调整模式（增加、减少、设定）、调整值。响应：返回当前存储配额。
                                <br>查询存储配额：接口：QueryStorageQuota用途：查询用户在指定集群的当前存储配额。响应：返回当前配额。
                                </details>
                               <details>
                                <summary> 用户和账户管理</summary>
                                <br>批量导入用户数据：接口：ImportUsers用途：批量导入账户和用户信息。参数：数据包含账户名、用户信息、所有者（可选）等；支持指定白名单标志。响应：返回导入的用户数、账户数，以及未提供用户名的用户数。
                                <br>查询集群用户：接口：GetClusterUsers用途：查询指定集群中的账户及其用户信息。响应：包含账户状态（已存在、新用户等）以及用户详细信息。
                                </details>
                               <details>
                                <summary> 数据同步</summary>
                                <br>获取同步信息：接口：GetFetchInfo用途：查询数据同步的状态和调度信息。响应：包括同步状态、计划信息、上次同步时间。
                                <br>设置同步状态：接口：SetFetchState用途：启用或禁用数据同步。响应：指示操作是否成功。
                                <br>同步阻塞状态：接口：SyncBlockStatus用途：同步账户及用户的阻塞状态到调度器。响应：包含同步失败的账户和用户信息。
                                <br>更新阻塞状态：接口：UpdateBlockStatus用途：更新账户及用户的阻塞状态。响应：操作结果。
                                </details>
                               <details>
                                <summary> 统计和管理信息</summary>
                                <br>获取管理员信息：接口：GetAdminInfo用途：获取平台管理员及财务人员信息。响应：包括管理员 ID 和名称、租户数、账户数、用户数等。
                                <br>获取统计信息：接口：GetStatisticInfo用途：获取指定时间段内的新增用户、账户、租户统计信息。参数：起始时间、结束时间。响应：返回新增用户数、账户数、租户数等信息。
                                </details>
                                <details>
                                <summary> 作业数据同步</summary>
                                <br>同步作业数据：接口：FetchJobs用途：同步新作业数据。响应：返回同步的作业数。
                                </details>
                        </details>
                       <details>
                       <summary> 数据结构</summary>
                               <details>
                                <summary> 存储配额调整模式：ChangeStorageQuotaMode</summary>
                                <br>枚举值：INCREASE（增加）、DECREASE（减少）、SET（直接设定）。
                                </details>
                               <details>
                                <summary> 账户和用户信息结构</summary>
                                <br>ClusterAccountInfo：包含账户名、用户列表、所有者信息、阻塞状态等。状态：已存在、新账户、新用户等。
                                <br>UserInAccount：用户 ID、用户名及阻塞状态。
                                <br>阻塞同步信息：SyncBlockStatusResponse：包含阻塞失败的账户、用户，以及未解除阻塞的账户信息。
                                </details>
                               <details>
                                <summary> 统计信息</summary>
                                <br>时间范围内的用户、账户、租户总数及新增数量。
                                </details>
                        </details>
                       <details>
                       <summary> 服务接口总结</summary>
                               <details>
                                <summary> 存储管理</summary>
                                <br>修改存储配额：ChangeStorageQuota
                                <br>查询存储配额：QueryStorageQuota
                                </details>
                               <details>
                                <summary> 用户与账户管理</summary>
                                <br>批量导入用户：ImportUsers
                                <br>查询集群用户：GetClusterUsers
                                </details>
                               <details>
                                <summary> 数据同步</summary>
                                <br>获取同步信息：GetFetchInfo
                                <br>设置同步状态：SetFetchState
                                <br>同步阻塞状态：SyncBlockStatus
                                <br>更新阻塞状态：UpdateBlockStatus
                                </details>
                               <details>
                                <summary> 统计与管理</summary>
                                <br>获取管理员信息：GetAdminInfo
                                <br>获取统计信息：GetStatisticInfo
                                </details>
                               <details>
                                <summary> 作业同步</summary>
                                <br>同步作业数据：FetchJobs
                                </details>
                        </details>
                </details>
                <details>
                <summary> protos/server/charging.proto</summary>
                <br>定义了一个关于租户和账户财务操作的系统，主要包括充值、消费、记录查询等功能。
                <br>支持多种目标类型（账户、租户或全局）。
                <br>分页与统计功能细化，便于处理大规模数据。
                <br>统一接口，支持灵活扩展（如支持元数据传递）。
                       <details>
                       <summary> 功能模块</summary>
                               <details>
                                <summary> 充值与支付</summary>
                                <br>Pay（支付）输入：支付金额、操作员ID、租户名（可选账户名）、支付类型、备注、IP地址。输出：支付前后的余额。
                                <br>Charge（充值）：输入：充值金额、租户名（可选账户名）、充值类型、备注、用户ID（可选）。输出：充值前后的余额。
                                </details>
                               <details>
                                <summary> 余额查询</summary>
                                <br>GetBalance（查询余额）输入：租户名（可选账户名）。输出：账户或租户的余额。
                                </details>
                               <details>
                                <summary> 记录管理</summary>
                                    <details>
                                    <summary> 消费记录</summary>
                                    <br>GetPaginatedChargeRecords（分页查询消费记录）：支持按用户、账户或租户查询，提供时间范围、类型过滤、分页、排序等功能。输出：记录列表。
                                    <br>GetChargeRecordsTotalCount（消费记录统计）：返回消费总金额及记录总数。
                                    </details>
                                   <details>
                                    <summary> 充值记录</summary>
                                    <br>GetPaymentRecords（查询充值记录）：支持按账户、租户或所有租户查询充值记录。输出：记录列表及总金额。
                                    </details>
                                </details>
                               <details>
                                <summary> 统计与分析</summary>
                                    <details>
                                    <summary> 每日统计</summary>
                                    <br>GetDailyCharge（每日消费统计）：按时区统计每天的消费金额。
                                    <br>GetDailyPay（每日充值统计）：按时区统计每天的充值金额。
                                    </details>
                                   <details>
                                    <summary> Top排行榜</summary>
                                    <br>GetTopChargeAccount（充值金额最多的账户）：返回充值金额排名靠前的账户及金额。
                                    <br>GetTopPayAccount（消费金额最多的账户）：返回消费金额排名靠前的账户及金额。
                                    </details>
                                </details>
                               <details>
                                <summary> 类型与支持</summary>
                                <br>GetAllPayTypes（获取支持的支付类型）：返回所有支持的支付方式。
                                </details>
                        </details>
                       <details>
                       <summary> 数据结构</summary>
                               <details>
                                <summary> 核心实体</summary>
                                <br>ChargeRecord：消费记录，包括时间、金额、备注等。
                                <br>PaymentRecord：充值记录，包括时间、金额、操作员等。
                                <br>DailyAmount：每日统计数据，包含日期和金额。
                                </details>
                               <details>
                                <summary> 查询目标</summary>
                                <br>AccountOfTenantTarget：指定租户和账户。
                                <br>AccountsOfTenantTarget：指定租户下多个账户。
                                <br>TenantTarget：指定租户。
                                <br>AllTenantsTarget：所有租户。
                                </details>
                               <details>
                                <summary> 统计信息</summary>
                                <br>时间范围内的用户、账户、租户总数及新增数量。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary> ChargingService</summary>
                                <br>提供所有充值、支付、余额查询及记录管理功能。
                                <br>标注了废弃接口（如：GetChargeRecords），并推荐使用新的分页或统计接口。
                                </details>
                        </details>
                </details>
                <details>
                <summary> protos/server/config.proto</summary>
                <br>定义了与集群管理相关的服务，包括集群的分区查询、集群激活/停用等功能。
                <br>废弃接口提醒：部分接口已被废弃，推荐使用新接口。
                <br>集群状态管理：提供集群的激活和停用管理，以及查看集群的运行时信息。
                <br>分区查询：支持根据账户、用户及集群查询可用的分区信息。
                       <details>
                        <summary> 功能模块</summary>
                               <details>
                                <summary> 集群分区查询</summary>
                                <br>GetAvailablePartitions（查询可用分区）：已废弃，原功能为查询账户下可用的集群分区。输入：账户名、用户ID。输出：包含集群和分区信息的响应。
                                </details>
                               <details>
                                <summary> 集群运行状态管理</summary>
                                <br>GetClustersRuntimeInfo（获取集群运行时信息）输入：无。输出：集群的当前运行状态（激活或停用），及最后的激活操作记录。
                                <br>ActivateCluster（激活集群）输入：集群ID、操作员ID。输出：集群是否成功激活。
                                <br>DeactivateCluster（停用集群）输入：集群ID、操作员ID、停用备注（可选）。输出：集群是否成功停用。
                                </details>
                        </details>
                        <details>
                       <summary> 数据结构</summary>
                               <details>
                                <summary> Partition（分区信息）</summary>
                                <br>包含内存、核心数、GPU 数量、节点数、QoS（服务质量）、描述等属性。
                                </details>
                               <details>
                                <summary> ClusterPartitions（集群分区）</summary>
                                <br>包含集群名称和对应的多个分区。
                                </details>
                               <details>
                                <summary> ClusterRuntimeInfo（集群运行时信息）</summary>
                                <br>包括集群ID、激活状态（激活或停用）、最后一次操作记录和更新时间。
                                </details>
                                <details>
                                <summary> LastActivationOperation（最后激活操作）</summary>
                                <br>包含操作员ID和停用备注（如果有）。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>ConfigService</summary>
                                <br>提供集群相关的操作，包括获取分区信息、查询集群状态、激活和停用集群。
                                <br>废弃的接口：GetAvailablePartitions 和 GetAvailablePartitionsForCluster 被标记为废弃，推荐使用新的集群配置接口。
                                </details>
                        </details>
                </details>
                <details>
                <summary> protos/server/export.proto</summary>
                <br>定义了与账户、用户、消费记录、充值记录相关的导出功能。
                <br>灵活的过滤条件：提供了丰富的过滤选项，支持按账户状态、时间范围、角色等多维度查询和导出数据。
                <br>数据流式导出：所有导出请求均采用流式响应，适合大数据量的导出操作。
                <br>支持多种目标：支持根据不同的目标（如账户、租户等）导出相关的记录，适应多样的业务需求。
                       <details>
                        <summary> 功能模块</summary>
                               <details>
                                <summary> 账户导出</summary>
                                <br>ExportAccountRequest（导出账户请求）：用于请求导出符合特定条件的账户信息。参数包括：账户数量、租户名称、账户名称、账户状态（封锁、欠费、冻结、正常）。
                                <br>ExportAccountResponse（账户导出响应）：返回符合条件的账户列表。
                                </details>
                               <details>
                                <summary> 用户导出</summary>
                                <br>ExportUserRequest（导出用户请求）：用于请求导出符合条件的用户信息。参数包括：用户数量、租户名称、排序字段、排序顺序、用户ID或名称、平台角色、租户角色。
                                <br>ExportUserResponse（用户导出响应）：返回符合条件的用户列表。
                                <br>ExportedUser（导出用户）：包含用户的详细信息，如用户ID、姓名、邮箱、可用账户、租户名称、创建时间、角色等。
                                </details>
                                <details>
                                <summary> 消费记录导出</summary>
                                <br>ExportChargeRecordRequest（导出消费记录请求）：用于请求导出消费记录，支持按时间范围、类型和目标（账户、租户等）筛选。参数包括：消费记录数量、开始时间、结束时间、消费类型、目标（单账户、多账户、租户等）。
                                <br>ExportChargeRecordResponse（消费记录导出响应）：返回符合条件的消费记录。
                                </details>
                                <details>
                                <summary> 充值记录导出</summary>
                                <br>ExportPayRecordRequest（导出充值记录请求）：用于请求导出充值记录，支持按时间范围、类型和目标（账户、租户等）筛选。参数包括：充值记录数量、开始时间、结束时间、充值类型、目标（单账户、多账户、租户等）。
                                <br>ExportPayRecordResponse（充值记录导出响应）：返回符合条件的充值记录。
                                </details>
                        </details>
                        <details>
                       <summary> 数据结构</summary>
                               <details>
                                <summary> Account（账户）</summary>
                                <br>账户信息结构（在导出响应中使用）。
                                </details>
                               <details>
                                <summary> TenantRole（租户角色）、PlatformRole（平台角色）</summary>
                                <br>用户角色信息。
                                </details>
                               <details>
                                <summary> ChargeRecord（消费记录）、PaymentRecord（充值记录）</summary>
                                <br>分别表示消费和充值的详细记录。
                                </details>
                                <details>
                                <summary> AccountOfTenantTarget、AccountsOfTenantTarget、TenantTarget 等</summary>
                                <br>导出记录时的目标类型，用于指定查询范围（单个账户、多个账户、租户等）。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>ExportService</summary>
                                <br>提供账户、用户、消费记录、充值记录的导出功能。
                                <br>各导出功能通过 stream 进行响应，支持数据流式传输。
                                </details>
                        </details>
                </details>
                <details>
                <summary>protos/server/init.proto</summary>
                <br>定义了与系统初始化相关的服务，包括初始化管理员设置、查询和用户验证等功能。
                <br>系统初始化管理：通过设置初始管理员和完成初始化操作，确保系统能够顺利启动并配置管理员权限。
                <br>用户管理：提供了用户是否存在的查询功能，便于后续进行权限和角色分配。
                <br>管理员角色配置：支持将用户设置为平台管理员以及租户管理员，确保系统的管理权限配置得当。
                       <details>
                        <summary> 功能模块</summary>
                               <details>
                                <summary> 查询系统初始化状态</summary>
                                <br>QuerySystemInitializedRequest（查询系统初始化请求）：用于查询系统是否已初始化。
                                <br>QuerySystemInitializedResponse（查询系统初始化响应）：返回一个布尔值，表示系统是否已经完成初始化。
                                </details>
                               <details>
                                <summary>创建初始管理员</summary>
                                <br>CreateInitAdminRequest（创建初始管理员请求）：用于创建系统初始管理员。请求参数包括用户ID、用户名、邮箱和密码。
                                <br>CreateInitAdminResponse（创建初始管理员响应）：返回一个布尔值，表示是否成功在认证系统中创建初始管理员。
                                </details>
                                <details>
                                <summary>完成系统初始化</summary>
                                <br>CompleteInitRequest（完成初始化请求）：用于请求完成系统的初始化操作。
                                <br>CompleteInitResponse（完成初始化响应）：完成初始化后的响应。
                                </details>
                                <details>
                                <summary> 设置初始管理员</summary>
                                <br>SetAsInitAdminRequest（设置为初始管理员请求）：用于将指定用户设置为平台管理员（PLATFORM_ADMIN）并且是默认租户的租户管理员（TENANT_ADMIN）。
                                <br>SetAsInitAdminResponse（设置为初始管理员响应）：对应的响应消息。
                                </details>
                                <details>
                                <summary> 取消初始管理员设置</summary>
                                <br>UnsetInitAdminRequest（取消初始管理员请求）：用于取消指定用户的初始管理员权限。
                                <br>UnsetInitAdminResponse（取消初始管理员响应）：对应的响应消息。
                                </details>
                                <details>
                                <summary> 用户存在性查询</summary>
                                <br>UserExistsRequest（查询用户是否存在请求）：用于检查指定用户ID是否存在于系统中。
                                <br>UserExistsResponse（查询用户是否存在响应）：返回一个布尔值，表示用户是否在系统中存在，同时可选地检查用户是否在认证系统中存在。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>InitService</summary>
                                <br>提供了以下服务：查询系统是否已初始化。创建初始管理员。完成系统初始化。设置或取消初始管理员角色。查询用户是否存在。
                                </details>
                        </details>
                </details>
                <details>
                <summary>protos/server/job.proto</summary>
                <br>定义了与作业（Job）管理和计费相关的服务，主要功能包括查询作业、管理作业价格、作业时间限制、取消作业以及获取作业提交和计费信息等。
                <br>作业管理：支持根据多种过滤条件查询、管理作业，如修改价格、查询时间限制等。
                <br>计费管理：提供详细的计费项目管理功能，包括新增、查询和返回历史项目。
                <br>统计与分析：支持根据时间统计作业提交情况，帮助管理员了解系统的作业分布和负载。
                       <details>
                        <summary> 功能模块</summary>
                               <details>
                                <summary> 作业查询与管理</summary>
                                <br>JobFilter（作业过滤器）：用于根据租户、用户、账户、作业ID、作业结束时间等过滤条件查询作业。
                                <br>GetJobsRequest（获取作业请求）：根据指定的过滤条件获取作业列表，可分页查询，并可根据多种字段（如ID、名称、时间等）排序。
                                <br>GetJobsResponse（获取作业响应）：返回符合条件的作业列表，包含作业总数和总计费用等信息。
                                <br>ChangeJobPriceRequest（修改作业价格请求）：用于根据过滤条件修改作业的账户价格和租户价格。
                                <br>ChangeJobPriceResponse（修改作业价格响应）：返回修改的作业数量。
                                <br>GetJobByBiJobIndexRequest（通过BI作业索引获取作业请求）：根据BI作业索引获取作业信息。
                                <br>GetJobByBiJobIndexResponse（通过BI作业索引获取作业响应）：返回作业信息。
                                <br>GetRunningJobsRequest（获取正在运行的作业请求）：根据集群、用户、账户等条件获取正在运行的作业。
                                <br>GetRunningJobsResponse（获取正在运行的作业响应）：返回当前正在运行的作业列表。
                                <br>ChangeJobTimeLimitRequest（修改作业时间限制请求）：用于修改指定作业的时间限制。
                                <br>ChangeJobTimeLimitResponse（修改作业时间限制响应）：返回修改是否成功。
                                <br>QueryJobTimeLimitRequest（查询作业时间限制请求）：查询指定作业的时间限制。
                                <br>QueryJobTimeLimitResponse（查询作业时间限制响应）：返回作业的时间限制。
                                <br>CancelJobRequest（取消作业请求）：用于取消指定的作业。
                                <br>CancelJobResponse（取消作业响应）：返回取消作业操作的结果。
                                </details>
                               <details>
                                <summary>计费与账单管理</summary>
                                <br>GetBillingItemsRequest（获取计费项目请求）：获取指定租户的计费项目，支持仅获取活跃项目或包括历史项目。
                                <br>JobBillingItem（作业计费项目）：包含计费项目的ID、路径、价格、创建时间等信息。
                                <br>GetBillingItemsResponse（获取计费项目响应）：返回活跃和历史的计费项目列表。
                                <br>AddBillingItemRequest（新增计费项目请求）：用于添加新的计费项目，可以指定租户或作为平台默认项目。
                                <br>AddBillingItemResponse（新增计费项目响应）：返回新增计费项目的结果。
                                <br>GetMissingDefaultPriceItemsRequest（获取缺失的默认价格项目请求）：查询缺少的默认价格项目。
                                <br>GetMissingDefaultPriceItemsResponse（获取缺失的默认价格项目响应）：返回缺失的默认价格项目列表。
                                </details>
                                <details>
                                <summary>作业统计与分析</summary>
                                <br>GetTopSubmitJobUsersRequest（获取提交作业最多的用户请求）：获取一定时间范围内提交作业最多的用户，默认获取前10名。
                                <br>GetTopSubmitJobUsersResponse（获取提交作业最多的用户响应）：返回提交作业最多的用户列表。
                                <br>GetUsersWithMostJobSubmissionsRequest（获取作业提交最多的用户请求）：查询在指定时间段内提交作业最多的用户，最多支持查询10个用户。
                                <br>GetUsersWithMostJobSubmissionsResponse（获取作业提交最多的用户响应）：返回作业提交最多的用户信息。
                                <br>GetNewJobCountRequest（获取新作业数量请求）：获取指定时间段内的新作业数量，支持时区设置。
                                <br>GetNewJobCountResponse（获取新作业数量响应）：返回按日期分组的新作业数量统计。
                                <br>GetJobTotalCountRequest（获取作业总数请求）：获取系统中所有作业的总数。
                                <br>GetJobTotalCountResponse（获取作业总数响应）：返回作业的总数。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>JobService</summary>
                                <br>提供了以下服务：获取作业、修改作业价格、获取运行中的作业。修改作业时间限制、取消作业。获取和添加计费项目。查询提交作业最多的用户、作业统计数据等。
                                </details>
                        </details>
                </details>
                <details>
                <summary>protos/server/job_charge_limit.proto</summary>
                <br>定义了与作业计费限额相关的服务，主要功能包括设置和取消作业的计费限额。
                <br>计费限额管理：提供了对用户作业计费限额的设置和取消功能，帮助控制作业的费用限制。
                <br>操作灵活性：支持设置限额和取消限额时，提供对限额状态（如解除封锁）的控制。
                       <details>
                        <summary> 功能模块</summary>
                               <details>
                                <summary> 作业计费限额管理</summary>
                                <br>SetJobChargeLimitRequest（设置作业计费限额请求）：用于设置指定租户、账户和用户的作业计费限额。包括租户名称、账户名称、用户ID和限额金额。
                                <br>SetJobChargeLimitResponse（设置作业计费限额响应）：返回设置操作的结果，成功时无返回数据。
                                <br>CancelJobChargeLimitRequest（取消作业计费限额请求）：用于取消指定用户的作业计费限额，允许选择是否解除封锁。包括租户名称、账户名称、用户ID和可选的unblock标志。
                                <br>CancelJobChargeLimitResponse（取消作业计费限额响应）：返回取消操作的结果，成功时无返回数据。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>JobChargeLimitService</summary>
                                <br>提供了两个主要的RPC方法：SetJobChargeLimit: 设置用户的作业计费限额。CancelJobChargeLimit: 取消用户的作业计费限额。
                                </details>
                        </details>
                </details>
                <details>
                <summary>protos/server/tenant.proto</summary>
                <br>定义了与租户管理相关的服务，涵盖了获取租户信息、创建租户以及设置默认账户封锁阈值等功能。
                <br>租户管理功能：包括租户的创建、查询和账户管理等功能。
                <br>管理员和财务人员管理：可以查询租户的管理员和财务人员信息。
                <br>灵活的账户封锁设置：允许为租户设置默认的账户封锁阈值。
                       <details>
                        <summary> 功能模块</summary>
                               <details>
                                <summary> 租户信息查询</summary>
                                <br>GetTenantInfoRequest（获取租户信息请求）：用于查询指定租户的基本信息。包括租户名称。
                                <br>GetTenantInfoResponse（获取租户信息响应）：返回租户的相关信息，包括：账户余额（balance）账户数量（account_count）用户数量（user_count）默认账户封锁阈值（default_account_block_threshold）管理员信息（admins）：包含管理员的用户ID和用户名。
                                                                           财务人员信息（financial_staff）：包含财务人员的用户ID和用户名。
                                </details>
                               <details>
                                <summary>租户列表查询</summary>
                                <br>GetTenantsRequest（获取租户列表请求）：查询所有租户。
                                <br>GetTenantsResponse（获取租户列表响应）：返回租户名称的列表。
                                </details>
                                <details>
                                <summary>租户创建</summary>
                                <br>GetAllTenantsRequest（获取所有租户请求）：查询所有租户的详细信息。
                                <br>GetAllTenantsResponse（获取所有租户响应）：返回租户的总数和每个租户的详细信息，包括：租户ID（tenant_id）租户名称（tenant_name）用户数量（user_count）账户数量（account_count）账户余额（balance）创建时间（create_time）
                                </details>
                               <details>
                                <summary>所有租户信息查询</summary>
                                <br>CreateTenantRequest（创建租户请求）：用于创建新的租户。包括租户名称、管理员的用户信息（ID、名称、邮箱、密码）。
                                <br>CreateTenantResponse（创建租户响应）：返回新创建租户的信息，包括租户ID和管理员用户ID，以及是否已在认证系统中创建。
                                <br>CreateTenantWithExistingUserAsAdminRequest（使用现有用户作为管理员创建租户请求）：用于将现有用户作为管理员创建租户。包括租户名称和管理员的用户信息（ID、名称）。
                                <br>CreateTenantWithExistingUserAsAdminResponse（使用现有用户作为管理员创建租户响应）：返回创建租户的结果，包括租户名称和管理员用户ID。
                                </details>
                               <details>
                                <summary>设置账户封锁阈值</summary>
                                <br>SetDefaultAccountBlockThresholdRequest（设置默认账户封锁阈值请求）：用于设置租户的账户封锁阈值金额。
                                <br>SetDefaultAccountBlockThresholdResponse（设置默认账户封锁阈值响应）：返回设置操作的结果，成功时无返回数据。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>TenantService</summary>
                                <br>提供了以下RPC方法：GetTenantInfo: 获取指定租户的基本信息。GetTenants: 获取所有租户名称。GetAllTenants: 获取所有租户的详细信息。CreateTenant: 创建新的租户。SetDefaultAccountBlockThreshold: 设置租户的默认账户封锁阈值。
                                                CreateTenantWithExistingUserAsAdmin: 使用现有用户创建租户并设置为管理员。
                                </details>
                        </details>
                </details>
                <details>
                <summary>protos/server/user.proto</summary>
                <br>定义了一系列与用户和租户管理相关的消息和服务，采用的是 Protocol Buffers (protobuf) 格式。它是用于描述服务端与客户端之间的通信协议，特别是用户、租户的操作和管理。
                <br>作业管理：支持根据多种过滤条件查询、管理作业，如修改价格、查询时间限制等。
                <br>计费管理：提供详细的计费项目管理功能，包括新增、查询和返回历史项目。
                <br>统计与分析：支持根据时间统计作业提交情况，帮助管理员了解系统的作业分布和负载。
                       <details>
                        <summary> 主要消息类型</summary>
                               <details>
                                <summary> 用户状态和信息</summary>
                                <br>UserStatus：定义了用户状态（如未封锁和已封锁）。
                                <br>AccountStatus：包含用户账户状态、余额、配额等信息。
                                <br>GetUserStatusRequest 和 GetUserStatusResponse：查询用户的状态信息，包括账户状态、存储配额等。
                                <br>CreateUserRequest 和 CreateUserResponse：用于创建新用户，返回用户 ID。
                                <br>GetUserInfoRequest 和 GetUserInfoResponse：获取指定用户的详细信息，包括账户隶属和角色等。
                                </details>
                               <details>
                                <summary>账户操作</summary>
                                <br>AddUserToAccountRequest 和 AddUserToAccountResponse：将用户添加到账户。
                                <br>RemoveUserFromAccountRequest 和 RemoveUserFromAccountResponse：将用户从账户中移除。
                                <br>BlockUserInAccountRequest 和 BlockUserInAccountResponse：封锁账户中的用户。
                                <br>UnblockUserInAccountRequest 和 UnblockUserInAccountResponse：解封账户中的用户。
                                </details>
                                <details>
                                <summary>角色管理</summary>
                                <br>SetAsAdminRequest 和 SetAsAdminResponse：设置用户为管理员。
                                <br>UnsetAdminRequest 和 UnsetAdminResponse：取消用户的管理员角色。
                                <br>SetPlatformRoleRequest 和 SetPlatformRoleResponse：设置用户的平台角色（如平台管理员、财务角色等）。
                                <br>UnsetPlatformRoleRequest 和 UnsetPlatformRoleResponse：取消平台角色。
                                </details>
                               <details>
                                <summary>用户和租户管理</summary>
                                <br>ChangeTenantRequest 和 ChangeTenantResponse：更改用户的租户隶属。
                                <br>GetUsersRequest 和 GetUsersResponse：查询特定租户下的所有用户。
                                <br>GetAllUsersRequest 和 GetAllUsersResponse：分页查询所有平台用户。
                                <br>GetNewUserCountRequest 和 GetNewUserCountResponse：获取指定时间段内新增用户的统计信息。
                                </details>
                        </details>
                       <details>
                       <summary> 服务定义</summary>
                               <details>
                                <summary>UserService 和 TenantService 服务</summary>
                                <br>提供了多种功能接口，如查询用户、账户管理、角色管理、创建和删除用户等。
                                </details>
                        </details>
                        <details>
                       <summary> 错误处理</summary>
                            <br>每个请求和响应消息中，错误代码（如 NOT_FOUND, ALREADY_EXISTS 等）用于处理不同的错误情况，确保客户端可以根据不同的错误做出适当的响应。
                        </details>
                </details>
        </details>
    </details>
    <details>
   <summary> apps</summary>
       <details>
        <summary>apps/ai</summary>
        <br>主要实现： next + trpc + mikro-orm + openApi。支持trpc和http 两种调用
            <details>
            <summary>apps/ai/eslint.config.js</summary>
            <br>一个 ESLint 配置文件，它将多个 ESLint 配置文件合并，并自定义了一些规则。
            <br>该配置文件在一个 React 和 TypeScript 项目中使用 ESLint 来检查代码质量，同时通过禁用一些规则来避免过于严格的检查，适应项目中的特定需求。
                <details>
                <summary>基础配置</summary>
                <br>base 引入了来自 ../../eslint.config 的基础配置。
                <br>react 引入了来自 @ddadaal/eslint-config/react 的 React 配置。
                </details>
                <details>
                <summary>规则覆盖</summary>
                <br>通过 module.exports 导出了一个配置数组，首先包含了 base 和 react 配置，随后覆盖了一些 TypeScript 相关的 ESLint 规则。
                </details>
                <details>
                <summary>禁用的规则</summary>
                <br>通过 rules 对象，禁用了以下 TypeScript 相关的规则：
                <br>@typescript-eslint/no-floating-promises: 禁用浮动的 Promise。
                <br>@typescript-eslint/no-unsafe-enum-comparison: 禁用不安全的枚举比较。
                <br>@typescript-eslint/no-misused-promises: 禁用误用 Promise 的情况。
                <br>@typescript-eslint/only-throw-error: 禁用只抛出 Error 对象的规则。
                <br>@typescript-eslint/prefer-promise-reject-errors: 禁用建议使用 Promise.reject 时必须传递 Error 对象的规则。
                </details>
            </details>
           <details>
            <summary>apps/ai/launch.sh</summary>
            <br>备份并替换 .next 目录中的某些路径，同时根据 NEXT_PUBLIC_BASE_PATH 变量的值修改内容，并启动一个 pnpm 服务。
            <br>根据 NEXT_PUBLIC_BASE_PATH 环境变量来动态修改 .next 目录中的路径配置，以便适应不同的部署环境。同时，它确保 .next 目录的备份和恢复，使得脚本在多次执行时能够安全恢复先前的状态。
                <details>
                <summary>备份和恢复 .next 目录</summary>
                <br>检查 .next.backup 目录是否存在：
                <br>如果 .next.backup 存在，删除当前的 .next 目录，并将 .next.backup 恢复为 .next 目录。
                <br>如果 .next.backup 不存在，则将当前的 .next 目录备份为 .next.backup。
                </details>
                <details>
                <summary>设置 BASE_PATH</summary>
                <br>获取环境变量 NEXT_PUBLIC_BASE_PATH 的值。
                <br>如果 BASE_PATH 为根路径 /，则将其修改为空字符串 ""，否则保持原值。
                </details>
                <details>
                <summary>路径替换</summary>
                <br>使用 find 命令遍历 .next 目录中的所有文件（-type f），并使用 sed 进行替换。
                <br>将文件中的 /@BASE_PATH@/ 替换为 /BASE_PATH/ 或 BASE_PATH（取决于 BASE_PATH 的值）。
                </details>
               <details>
                <summary>启动 Next.js 服务</summary>
                <br>最后，执行 pnpm serve:next 启动 Next.js 服务。
                </details>
            </details>
           <details>
            <summary> apps/ai/next.config.mjs</summary>
            <br>一个 Next.js 配置文件，主要功能是设置基础路径（BASE_PATH）、处理构建时的环境配置，并进行 Webpack 配置，特别是针对 .node 文件的支持和其它优化。
            <br>主要用于配置 Next.js 应用的基础路径、初始化环境配置（如 WebSocket 代理），以及扩展 Webpack 配置以支持 .node 文件。它还处理了构建过程中需要的特定操作，并对应用中的静态资源进行适当的路径配置。
                <details>
                <summary>基础路径（BASE_PATH）的配置</summary>
                <br>从环境变量中获取 NEXT_PUBLIC_BASE_PATH，如果没有则默认使用根路径 /。
                <br>该 BASE_PATH 用于设置 Next.js 应用的基础路径，影响应用中的所有路径配置。
                </details>
                <details>
                <summary>构建标识（BUILDING）</summary>
                <br>判断 process.env.BUILDING 是否为 "1"，如果是则表示当前处于构建过程。这个标识可能用于跳过一些不必要的操作，比如设置 WebSocket 代理。
                </details>
                <details>
                <summary>初始化配置（global.__CONFIG__）</summary>
                <br>将 BASE_PATH 通过 global.__CONFIG__ 全局变量存储，供应用中其他地方使用。
                </details>
                <details>
                <summary>WebSocket代理的设置</summary>
                <br> 如果当前不是构建过程中（building为false），代码会通过fetch请求调用一个setup API URL【http://localhost:>port>/api/setup】，用于初始化 WebSocket 代理服务器。
                </details>
                <details>
                <summary> Next.js 配置（nextConfig）</summary>
                <br>配置了 styled-components 编译支持。
                <br>禁用了 SWC 压缩（swcMinify: false），可能是因为需要调试或不需要额外压缩。
                <br>配置了 basePath 和 assetPrefix，这将影响资源的引用路径。
                <br>设置了 Webpack 配置：
                <br>extensionAlias：允许解析 .ts, .tsx, .js, .jsx 文件扩展名，提升开发效率。
                <br>针对 .node 文件添加了支持，使其能够在 Next.js 中正确加载。特别地，使用了 nextjs-node-loader 来处理 .node 文件。
                </details>
               <details>
                <summary> 忽略 URL 末尾的斜杠重定向（skipTrailingSlashRedirect: true）</summary>
                <br>该配置会使 Next.js 忽略 URL 末尾的斜杠，以避免不必要的重定向。
                </details>
               <details>
                <summary> 转译依赖（transpilePackages）</summary>
                <br>配置了转译 antd 和 @ant-design/icons 这两个包，确保它们在构建过程中能够被正确处理。
                </details>
            </details>
           <details>
            <summary> apps/ai/package.json</summary>
            <br>这是一个包含 @scow/ai 项目的 package.json 文件。该文件描述了项目的元数据、依赖关系、构建和运行脚本。
            <br>这个 package.json 配置了一个基于 Next.js 构建的项目，结合了前端 UI 库（如 Ant Design）和后端 ORM（MikroORM）进行数据库操作。项目包括了 TypeScript 支持、构建和部署脚本，并配置了 tRPC 用于创建类型安全的 API。
                <details>
                <summary>项目基本信息</summary>
                <br>name: @scow/ai
                <br>version: 0.2.6
                <br>private: true 表示该项目为私有项目，不会发布到 npm。
                <br>files: 指定了发布时包含的文件和目录，如 .next、public、next.config.mjs 等。
                </details>
                <details>
                <summary>脚本</summary>
                <br>dev: 启动开发模式并使用模拟数据 (NEXT_PUBLIC_USE_MOCK=1)，通过 next dev 启动 Next.js 开发服务器。
                <br>dev: 启动开发模式，但不使用模拟数据 (NEXT_PUBLIC_USE_MOCK=0)。
                <br>serve: 使用 start.mjs 启动项目。
                <br>serve: 启动 Next.js 应用。
                <br>build: 执行构建命令，先执行 build:next。
                <br>build: 清理备份并进行 Next.js 构建（next build）。
                <br>build: 编译 TypeScript 代码并创建 TypeScript 的别名。
                <br>orm: 使用 MikroORM 命令行工具连接到数据库。
                <br>ormCreate: 创建数据库迁移。
                <br>ormUp: 应用数据库迁移。
                <br>lint: 运行 ESLint 检查代码。
                </details>
                <details>
                <summary>依赖项(常用依赖)</summary>
                <br>next: 用于构建 Next.js 应用。
                <br>react 和 react-dom: React 和 React DOM 库。
                <br>@ant-design/icons, antd: Ant Design 图标和 UI 库。
                <br>@mikro-orm/core, @mikro-orm/mysql: 使用 MikroORM 进行数据库操作，支持 MySQL。
                <br>@trpc/client, @trpc/server: tRPC 客户端和服务端库，用于创建类型安全的 API。
                <br>superjson, zod: 数据验证和序列化工具。
                </details>
                <details>
                <summary>依赖项(开发依赖)</summary>
                <br> @types/*: 类型声明包，用于增强 TypeScript 开发体验。
                <br> fs-extra: 文件系统操作的扩展库。
                <br> nextjs-node-loader: 支持在 Next.js 中加载 .node 文件。
                <br> jest-environment-jsdom: Jest 的 Jsdom 环境，用于前端测试。
                <br> webpack: 打包工具。
                </details>
                <details>
                <summary> MikroORM 配置</summary>
                <br>配置了 MikroORM，使用 TypeScript 文件来加载数据库配置。
                <br>useTsNode 表示支持 TypeScript 执行。
                </details>
            </details>
           <details>
            <summary> apps/ai/start.mjs</summary>
            <br>这是一个用于处理项目构建和启动过程的脚本。
            <br>这个脚本确保了在部署或开发过程中，基础路径的替换和 .next 目录的备份恢复过程是自动化的，简化了部署操作。
            <br>备份处理：确保每次执行脚本时，.next 目录可以恢复到最新的备份状态。
            <br>环境变量替换：动态替换文件中的基础路径，以便项目在不同环境中运行时适配不同的路径。
            <br>命令执行：通过 execSync 同步执行 npm run serve:next，确保 Next.js 应用能够启动，并带上正确的环境配置。
                <details>
                <summary>备份和恢复 .next 文件夹</summary>
                <br>如果存在 .next.backup 目录（备份目录），则删除现有的 .next 目录，并将备份目录中的 .next 复制过来。
                <br>如果备份目录不存在，则将当前的 .next 目录复制到 .next.backup 作为备份。
                </details>
                <details>
                <summary>处理 BASE_PATH 环境变量</summary>
                <br>读取环境变量 NEXT_PUBLIC_BASE_PATH 来确定基础路径（BASE_PATH）。
                <br>如果 BASE_PATH 是 /，则将其更改为空字符串 ""，否则保留原值。
                </details>
                <details>
                <summary>替换 .next 目录下的文件中的 @BASE_PATH@</summary>
                <br>使用 replace-in-file 库在 .next 目录中的所有文件内查找 /@BASE_PATH@ 字符串，并将其替换为实际的 BASE_PATH 值。
                </details>
                <details>
                <summary>启动 serve:next 命令</summary>
                <br> 使用 npm run serve:next 命令启动 Next.js 应用，并传递环境变量 NEXT_PUBLIC_RUNTIME_BASE_PATH，确保应用在运行时能够使用正确的基础路径。
                </details>
            </details>
           <details>
            <summary> apps/ai/tsconfig.build.json</summary>
            <br>这是一个 TypeScript 配置文件（tsconfig.json）的扩展配置
            <br>这个配置主要用于 TypeScript 项目中，确保特定目录（如 src 和 migrations）下的 TypeScript 文件会被正确编译。
                <details>
                <summary>继承</summary>
                <br>该配置通过 extends 继承了另一个 tsconfig.json 文件的配置，使得可以重用父文件的设置。
                </details>
                <details>
                <summary>包含文件</summary>
                <br>通过 include 字段，指定了项目中需要被 TypeScript 编译器处理的文件：
                <br>所有 src 目录下的 .ts 文件（包括子目录）。
                <br>所有 migrations 目录下的 .ts 文件。
                </details>
            </details>
           <details>
            <summary> apps/ai/tsconfig.json</summary>
            <br>这是一个 TypeScript 配置文件（tsconfig.json）的内容
            <br>这个配置适用于一个 TypeScript 项目，尤其是包含 Next.js 和 Node.js 环境的项目。它启用了严格的类型检查和现代 ECMAScript 特性支持，同时还提供了路径映射和对装饰器的支持。
                <details>
                <summary>compilerOptions（编译选项）</summary>
                <br>target: 编译输出的目标 JavaScript 版本为 es2020。
                <br>lib: 引入了 dom、dom.iterable 和 esnext 库，表示代码将支持现代浏览器和最新的 ECMAScript 特性。
                <br>allowJs: 允许在项目中混合 JavaScript 文件与 TypeScript 文件。
                <br>skipLibCheck: 跳过库文件的类型检查，以提高编译性能。
                <br>strict: 启用所有严格的类型检查选项。
                <br>experimentalDecorators: 启用装饰器的实验性支持。
                <br>emitDecoratorMetadata: 在编译过程中生成装饰器的元数据，通常与 experimentalDecorators 一起使用。
                <br>forceConsistentCasingInFileNames: 强制文件名大小写一致性。
                <br>noEmit: 不生成输出文件，通常用于检查类型而不进行编译。
                <br>esModuleInterop: 启用对 ES 模块与 CommonJS 模块之间的兼容性。
                <br>module: 模块系统使用 commonjs。
                <br>moduleResolution: 使用 node 模块解析策略，这对于 Node.js 项目是常见的设置。
                <br>resolveJsonModule: 允许导入 .json 文件作为模块。
                <br>isolatedModules: 启用此选项以确保每个文件都是独立模块，这对于支持像 ts-node 这样的工具非常重要。
                <br>jsx: 让 TypeScript 保留 JSX 语法不做转换，通常用于 React 项目。
                <br>incremental: 启用增量编译，以提高后续编译的速度。
                <br>baseUrl: 设置项目的基目录，通常用来简化模块导入路径。当前设置为当前目录（.）。
                <br>plugins: 启用 next 插件，以便与 Next.js 的配置兼容。
                </details>
                <details>
                <summary>include（包含文件）</summary>
                <br>指定 TypeScript 应该包含的文件和目录：
                <br>src 目录下的所有 TypeScript 文件。
                <br>.next/types/**/*.ts 目录下的类型定义文件。
                </details>
               <details>
                <summary>exclude（排除文件）</summary>
                <br>排除了 node_modules 目录，通常用于防止将第三方依赖项纳入编译。
                </details>
               <details>
                <summary>paths（路径映射）</summary>
                <br>配置了 src/* 路径的映射，使得可以通过 src/* 直接引用 src/ 目录下的文件。
                </details>
               <details>
                <summary>ts-node（ts-node 配置）</summary>
                <br>require: 在运行时加载 tsconfig-paths/register，以支持路径映射。
                <br>preferTsExts: 优先使用 TypeScript 文件扩展名（.ts 和 .tsx）。
                </details>
            </details>
            <details>
            <summary> apps/ai/tsconfig.server.json</summary>
            <br>这是一个 TypeScript 配置文件（tsconfig.build.json），它扩展了基础的 tsconfig.json 配置，并添加了一些构建相关的设置。
            <br>这个配置文件主要用于构建过程，它继承了基础的 tsconfig.json 配置，并且对输出目录 (outDir)、是否生成文件 (noEmit)，以及路径映射（paths）进行了调整。这个配置通常用于构建 TypeScript 项目，将编译后的文件输出到 build 目录中，并允许使用简化的模块导入路径。
                <details>
                <summary>extends</summary>
                <br>extends: "./tsconfig.json": 该配置文件继承自 tsconfig.json 文件，因此会自动应用 tsconfig.json 中的所有设置，并在此基础上进行扩展和修改。
                </details>
                <details>
                <summary>compilerOptions（编译选项）</summary>
                <br>outDir: 指定编译后的输出目录为 build，即 TypeScript 编译后生成的 JavaScript 文件将存放在 build 目录中。
                <br>noEmit: 设置为 false，表示 TypeScript 会生成输出文件，而不是仅仅检查类型。通常在开发时，noEmit 为 true，用于仅进行类型检查，不生成实际的文件。设置为 false 后，编译器会生成 JavaScript 文件。
                    <details>
                    <summary>paths</summary>
                    <br>这是路径映射的配置，用来简化模块导入。
                    <br>src/* 映射到 src/*，这意味着可以通过 src/ 来访问 src 目录下的文件。
                    <br>server/* 映射到 server/*，同理，允许通过 server/ 路径访问 server 目录下的文件。
                    </details>
                </details>
            </details>
           <details>
            <summary> apps/ai/assets</summary>
                <details>
                <summary>apps/ai/assets/app</summary>
                    <details>
                    <summary>apps/ai/assets/app/server_entry.sh</summary>
                    <br>这个脚本是一个简单的 Bash 脚本，包含了一个生成密码的函数和设置环境变量的部分。
                    <br>该脚本的作用是生成随机密码，并根据传入的参数设置相关的环境变量。
                    <br>![image](https://github.com/user-attachments/assets/8e6a74c4-8ddd-4dd2-9a65-c2f6f65abed2)
                        <details>
                        <summary>get_password 函数</summary>
                        <br>该函数用于生成一个随机的密码。
                        <br>/dev/urandom：这是一个随机数源，通过它可以获取随机数据。
                        <br>tr -dc A-Za-z0-9：这条命令会过滤掉非字母和数字的字符，只保留字母（大小写）和数字。
                        <br>head -c$1：表示输出前 $1 个字符，$1 是函数的第一个参数，指定密码的长度。
                        <br>echo $password：输出生成的密码。
                        </details>
                        <details>
                        <summary> 设置环境变量</summary>
                        <br>export：该命令用于设置环境变量，使其对当前的 Shell 及其子进程可用。
                        <br>$1、$2、$3：分别表示脚本运行时传入的第一个、第二个和第三个参数，这些参数值被用来设置环境变量 PORT、HOST 和 SVCPORT。
                        </details>
                    </details>
                    <details>
                    <summary>apps/ai/assets/app/vnc_entry.sh</summary>
                    <br>这意味着，执行该脚本后，环境变量 PORT、HOST 和 SVCPORT 的值会被设为你传入的值，并且这些环境变量会在当前 shell 会话以及子进程中可用。
                    <br>设置环境变量：export PORT=$1：将脚本的第一个参数 $1 赋值给环境变量 PORT。export HOST=$2：将脚本的第二个参数 $2 赋值给环境变量 HOST。export SVCPORT=$3：将脚本的第三个参数 $3 赋值给环境变量 SVCPORT。
                    <br>![image](https://github.com/user-attachments/assets/b883ed46-beb7-4072-9352-ea5aafcb8fec)
                    </details>
                </details>
                <details>
                <summary> apps/ai/assets/icons</summary>
                <br>S的图像：192.png,512.png,favicon.ico
                </details>
               <details>
                <summary> apps/ai/assets/logo</summary>
                <br>openscow的图像：banner.dark.svg，banner.svg，logo.dark.svg，logo.svg
                </details>
            </details>
           <details>
            <summary> apps/ai/config</summary>
            <br>scow的配置文件，就是一键部署那里的配置，多了一个ai的配置文件
            </details>
           <details>
            <summary> apps/ai/env</summary>
                <details>
                <summary> apps/ai/env/.env.dev</summary>
                <br>DB_HOST=localhost    DB_NAME=scow_server    AUTH_EXTERNAL_URL="http://auth:5000"
                </details>
            </details>
           <details>
            <summary> apps/ai/src</summary>
                <details>
                <summary> apps/ai/src/app</summary>
                    <details>
                    <summary> apps/ai/src/app/auth.ts</summary>
                    <br>这段代码是一个基于 React 和 tRPC 的钩子函数（hooks）实现，用于管理用户的认证信息。
                    <br>这段代码是与前端应用中的用户认证相关的功能实现，结合了 React 钩子和 tRPC 的查询/突变（mutation）来进行数据获取和操作。
                    <br>使用方式：
                    <br>useUserQuery：用于查询用户信息，一般用于页面加载时获取当前用户状态。
                    <br>useLogoutMutation：用于登出操作，通常会在登出按钮的点击事件中调用。
                    <br>useOptionalUser：在需要获取当前用户但不强求的场景下使用（例如在一些组件中检查用户是否存在）。
                    <br>useUser：在需要保证用户已登录的场景中使用，如果没有用户数据会抛出错误，适用于需要强制认证的场景。
                        <details>
                        <summary>useUserQuery</summary>
                        <br>功能：获取用户信息。
                        <br>实现：调用 trpc.auth.getUserInfo.useQuery 来获取用户信息。staleTime: Infinity 表示该数据在客户端永远不会过期，即不会自动重新请求。
                        <br>返回：返回一个 useQuery 钩子，包含用户数据。
                        </details>
                        <details>
                        <summary>useLogoutMutation</summary>
                        <br>功能：执行登出操作。
                        <br>实现：调用 trpc.auth.logout.useMutation 来进行登出操作，通常会触发清除用户的认证信息。
                        <br>返回：返回一个 useMutation 钩子，用于执行登出请求。
                        </details>
                        <details>
                        <summary>useOptionalUser</summary>
                        <br>功能：获取当前用户信息（如果已登录），否则返回 undefined。
                        <br>实现：通过调用 useUserQuery() 获取用户数据，并从中提取 data?.user。如果没有用户数据，返回 undefined。
                        <br>返回：当前登录的用户信息或者 undefined。
                        </details>
                        <details>
                        <summary>useUser</summary>
                        <br>功能：获取当前已登录的用户信息，若未登录则抛出错误。
                        <br>实现：通过 useOptionalUser 获取用户数据，如果没有数据（即用户未登录），则抛出 Error("not logged in")。
                        <br>返回：当前登录的用户信息。
                        </details>
                    </details>
                    <details>
                    <summary> apps/ai/src/app/clientLayout.tsx</summary>
                    <br>ClientLayout 组件是一个复杂的布局容器，负责设置页面的全局配置，包括国际化、暗模式、UI 配置、样式处理和错误处理。它将多个不同的上下文和状态管理功能整合在一起，为应用提供统一的外观和行为。
                    <br>这段代码是 React 组件 ClientLayout 的实现，主要用于设置前端应用的全局布局，包括语言选择、暗模式、UI 配置和样式配置等。它将多个子组件和上下文提供程序组合在一起，并通过 tRPC 查询加载 UI 配置。
                    <br>代码执行流程：
                    <br>语言设置：在 Provider 中设置语言，默认是 zh_cn（简体中文）。
                    <br>样式和暗模式：使用 StyleProvider 和 DarkModeProvider 处理样式和暗模式。
                    <br>UI 配置加载：通过 useConfigQuery 获取 UI 配置，如果正在加载，显示 Loading 组件；否则，使用 UI 配置并渲染页面内容。
                    <br>UI 配置提供：将 UI 配置和主机名信息提供给上下文中的子组件。
                    <br>返回值：返回的组件结构是一个包含多个提供程序（Provider）的嵌套结构，所有页面内容都被包裹在这些提供程序中，确保在应用中可以访问全局配置、语言、主题、样式等信息。
                        <details>
                        <summary>国际化支持</summary>
                        <br>通过 Provider 提供初始语言设置，目前默认设置为 "zh_cn"（简体中文）。不同语言的定义存储在 languagesMap 中。
                        </details>
                        <details>
                        <summary>暗模式</summary>
                        <br>使用 DarkModeProvider 和 DarkModeCookie 来管理暗模式的状态。initialDark 可以作为初始值进行传递。
                        </details>
                        <details>
                        <summary>UI 配置加载</summary>
                        <br>使用 trpc.config.getUiConfig.useQuery 钩子从后端获取 UI 配置，并根据配置动态设置应用的主要颜色（primaryColor）。该颜色值根据当前 hostname （主机名）来决定，优先级依次为：hostnameMap 中的匹配颜色 > 默认颜色。
                        </details>
                        <details>
                        <summary>样式提供和配置</summary>
                        <br>StyleProvider 用于设置样式相关的提供者，并启用 legacyLogicalPropertiesTransformer。
                        <br>使用 StyledComponentsRegistry 和 AntdStyleRegistry 来注册样式，支持 styled-components 和 Ant Design 的样式系统。
                        </details>
                        <details>
                        <summary>页面加载与错误处理</summary>
                        <br>Loading 组件用于在 UI 配置加载时显示一个加载动画。
                        <br>ErrorBoundary 和 RootErrorContent 组件用于捕捉和处理渲染过程中可能出现的错误，确保应用在发生错误时不会崩溃。
                        </details>
                        <details>
                        <summary>UI 配置上下文</summary>
                        <br>使用 UiConfigContext.Provider 提供全局的 UI 配置信息给子组件，子组件可以通过上下文访问 UI 配置（如主机名和颜色配置）。
                        </details>
                        <details>
                        <summary>其他组件和功能</summary>
                        <br>GlobalStyle：应用全局样式。
                        <br>TopProgressBar：显示顶部进度条，用于展示页面加载进度。
                        </details>
                    </details>
                    <details>
                    <summary> apps/ai/src/app/layout.tsx</summary>
                    <br>这段代码是一个 Next.js 应用的自定义 MyApp 组件，它负责将布局容器和一些必要的环境设置提供给页面。
                    <br>MyApp 是一个 Next.js 应用的自定义入口组件，它将页面内容包裹在布局容器中，并根据用户的暗模式设置提供合适的配置。
                    <br>它通过 ServerClientProvider 和 ClientLayout 实现从服务端和客户端的 TRPC 状态管理和数据通信。通过这种方式，可以确保页面在不同环境（如服务端或客户端）以及不同配置下都能正确展示和工作。
                    <br>主要流程：
                    <br>获取暗模式设置：首先从 Cookie 中提取名为 scow-dark 的暗模式设置。如果存在，转换为 DarkModeCookie 类型。
                    <br>提供全局配置和布局：通过嵌套 ServerClientProvider 和 ClientLayout 将页面内容包裹在它们内。ClientLayout 组件负责设置语言、暗模式、样式等全局配置。
                    <br>设置页面头部信息：在 html 头部中添加一些 Meta 标签和资源，如 manifest.json 和 Favicon。
                    <br>渲染页面内容：在 ClientLayout 中渲染传入的 children（页面内容）。
                        <details>
                        <summary>导入样式</summary>
                        <br>import "antd/dist/reset.css";：导入 Ant Design 的默认样式，用于应用的基本样式。
                        <br>import { DarkModeCookie } from "@scow/lib-web/build/layouts/darkMode";：从自定义的库中导入用于管理暗模式的 Cookie。
                        </details>
                        <details>
                        <summary>从 cookies 中获取暗模式设置</summary>
                        <br>使用 next/headers 库的 cookies() 函数从 HTTP 请求的 Cookie 中获取暗模式设置（scow-dark）。如果找到了，解析它并将其转换为 DarkModeCookie 类型。
                        </details>
                        <details>
                        <summary>MyApp 组件</summary>
                        <br>它接受一个 children 属性，这个属性是页面的内容（React 组件或页面内容）。
                        <br>在 ServerClientProvider 和 ClientLayout 组件中嵌套 children。
                        <br>ClientLayout 组件会根据 initialDark 的值提供暗模式配置。
                        </details>
                        <details>
                        <summary>ServerClientProvider</summary>
                        <br>在 MyApp 组件的根容器中，嵌套了 ServerClientProvider。这个组件是为了在服务端与客户端之间共享 TRPC 客户端和服务器端状态。
                        <br>它使得从后端到前端的请求和数据通信更为高效和安全。
                        </details>
                        <details>
                        <summary>ClientLayout 组件</summary>
                        <br>ClientLayout 是一个带有布局和全局配置的组件，提供语言、样式和暗模式等全局环境。
                        <br>在 ClientLayout 中传入 initialDark 值，将根据当前用户的暗模式设置（从 Cookie 获取）来决定初始暗模式。
                        </details>
                        <details>
                        <summary>BASE_PATH</summary>
                        <br>使用 src/utils/processEnv 中的 BASE_PATH 定义应用的基础路径。它用于构建 Web 应用中的静态资源路径，如 Web Manifest 文件或 Favicon 文件。
                        <br>在 <link> 标签中将基础路径连接到 manifest.json 和 /api/icon。
                        </details>
                    </details>
                    <details>
                    <summary> apps/ai/src/app/page.tsx</summary>
                    <br>这段代码是使用 Next.js 实现的一个简单的页面重定向功能。
                    <br>该组件导入了 next/navigation 中的 redirect 函数，用于执行客户端的重定向操作。
                    <br>Page 组件在渲染时会立即调用 redirect("/dashboard")，这会导致客户端在访问该页面时自动重定向到 /dashboard 路由。
                    <br>示例使用场景：
                    <br>登录后重定向：在用户成功登录后，使用这个页面自动重定向到他们的仪表盘或其他特定页面。
                    <br>授权检查：如果你希望未认证的用户跳转到登录页面，或者已认证的用户跳转到主页面，可以使用这种方式。
                        <details>
                        <summary>重定向到 /dashboard</summary>
                        <br>当页面被渲染时，redirect 函数会被调用，触发一个客户端的重定向，自动跳转到 /dashboard 页面。
                        <br>这种做法通常用于在某些情况下自动将用户引导到另一个页面，无需用户点击链接，例如在用户登录后或者进行身份验证时。
                        </details>
                        <details>
                        <summary>Page 组件</summary>
                        <br>该 Page 组件本身不直接渲染任何内容，它的唯一作用是执行重定向。
                        </details>
                    </details>
                    <details>
                    <summary>apps/ai/src/app/trpcClient.server.tsx</summary>
                    <br>这段代码是一个 Next.js 的组件，用于提供客户端和服务器之间的通信功能，并使用了 trpc 来进行数据请求。
                    <br>代码的核心功能是通过 ServerClientProvider 组件将客户端和服务器的数据交互配置封装，并且根据不同的环境设置动态的 API 请求基础 URL。
                    <br>用途：
                    <br>动态 URL 配置：根据不同的部署环境（如 Vercel、Render 或本地开发环境），自动配置 API 的基础 URL，确保应用能够在各种环境下正常运行。
                    <br>TRPC 配置：通过 ClientProvider 提供 TRPC 客户端上下文，使得整个应用可以统一通过 TRPC 进行数据请求。
                    <br>使用场景：
                    <br>在 Next.js 项目中，通常会使用这种方式来封装服务器端与客户端的交互，特别是在涉及到 API 请求时，通过环境判断来配置正确的 URL，可以确保应用在开发、生产等不同环境下都能正常工作。
                        <details>
                        <summary>getBaseUrl 函数</summary>
                        <br>该函数用于根据不同的运行环境动态返回 API 的基础 URL。
                        <br>浏览器环境：如果是在浏览器环境下（typeof window !== "undefined"），则返回空字符串，表示 API 请求使用相对路径。
                        <br>Vercel 环境：如果在 Vercel 部署环境中，返回 https://VERCEL_URL>，这是 Vercel 提供的域名。
                        <br>Render 环境：如果在 Render 部署环境中，返回 http://RENDER_INTERNAL_HOSTNAME>:PORT>。
                        <br>本地环境：如果没有匹配以上环境的条件，假设是本地开发环境，返回 http://localhost:3000 或者根据 process.env.PORT 获取端口。
                        </details>
                        <details>
                        <summary>ServerClientProvider 组件</summary>
                        <br>这是一个高阶组件（HOC），用于为应用提供一个统一的客户端和服务器通信上下文。
                        <br>noStore()：这是 next/cache 中的一个 API，表示此组件的缓存策略不存储任何内容，确保每次都从服务器获取数据。
                        <br>ClientProvider：这是一个自定义的提供者组件，用于提供一个客户端实例，配置了 baseUrl 和 basePath，使得在应用的其他部分可以通过 TRPC 客户端与服务器进行交互。
                        </details>
                        <details>
                        <summary>传递 baseUrl 和 basePath</summary>
                        <br>baseUrl：通过 getBaseUrl() 获取。
                        <br>basePath：通过从环境变量 BASE_PATH 获取，通常用于配置应用的前缀路径。
                        </details>
                    </details>
                    <details>
                    <summary>apps/ai/src/app/trpcClient.tsx</summary>
                    <br>这段代码实现了一个基于 React 和 trpc 的客户端提供者组件 ClientProvider，用于在应用中设置全局的 TRPC 客户端和 React Query 的配置，方便管理和优化客户端与服务器之间的通信。
                    <br>用途
                    <br>API 请求统一管理：将 React Query 和 TRPC 的客户端封装为全局组件，方便在应用中复用。
                    <br>错误处理与重试策略：集中化的错误处理和重试逻辑，减少分散在代码各处的重复逻辑。
                    <br>开发体验优化：在开发环境中启用日志记录，方便调试
                        <details>
                        <summary>全局 React Query 客户端</summary>
                        <br>创建和配置 QueryClient，用于管理客户端的查询和变更。
                        <br>配置全局错误处理（如未授权、请求失败）及请求的默认行为（如重试次数、失焦重试）。
                        </details>
                        <details>
                        <summary>TRPC 客户端</summary>
                        <br>设置 TRPC 客户端以支持数据请求。
                        <br>使用 superjson 作为序列化器来支持复杂数据结构的传输。
                        </details>
                        <details>
                        <summary>错误处理</summary>
                        <br>当发生特定错误（如 UNAUTHORIZED、SFTP_ERROR 等）时，提供友好的用户提示或执行特定操作（如跳转到登录页面）。
                        </details>
                    </details>
                    <details>
                    <summary>apps/ai/src/app/uiContext.ts</summary>
                    <br>这段代码定义了一个 React 上下文 UiConfigContext 和一个用于访问上下文的自定义 Hook useUiConfig。
                    <br>它的主要功能是提供和管理用户界面配置（UiConfig）的数据共享。
                    <br>这段代码主要实现了 用户界面配置（UI 配置）上下文管理，通过上下文（React Context）和自定义 Hook 的结合，为整个应用提供共享的用户界面配置信息。
                    <br>使用场景
                    <br>跨组件共享 UI 配置：适用于需要动态调整界面主题、颜色、布局等配置的应用，例如根据用户选择切换暗/亮模式。
                    <br>全局主机信息：提供主机名（hostname）信息，方便与后端通信或界面展示。
                        <details>
                        <summary>上下文定义</summary>
                        <br>UiConfigContext 是一个全局的 React 上下文，存储了两类数据：hostname：当前主机名。uiConfig：用户界面相关的配置（UiConfig 类型，例如主题颜色、布局设置等）。
                        </details>
                        <details>
                        <summary>数据访问 Hook</summary>
                        <br>自定义 Hook useUiConfig：使用 React.useContext 提供对 UiConfigContext 数据的访问。简化了组件对上下文数据的获取过程，增强代码可读性和可维护性。
                        </details>
                        <details>
                        <summary>共享 UI 配置</summary>
                        <br>通过上下文和自定义 Hook，将 UI 配置在应用的不同组件之间共享，避免通过逐层传递 props 来共享数据。
                        </details>
                    </details>
                </details>
            </details>
        </details>
        <details>
        <summary>apps/auth</summary>
        <br>本服务提供多个HTTP API，其中/auth和/callback必须被公网可访问，其他的API都应该只对内网开放！
        </details>
    </details>
</details>


