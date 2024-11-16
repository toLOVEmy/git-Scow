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
</details>



