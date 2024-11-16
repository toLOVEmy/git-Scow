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
    </details>
</details>



