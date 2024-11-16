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
        依赖于项目中所有包的 generate 任务
        代码生成任务，用来生成代码（可能是 gRPC 的客户端/服务端代码）。
        输入文件：包括 .proto 文件和 buf.gen.yaml 配置文件
        输出目录：generated，src/generated
        </details>
        <details>
        <summary>build</summary>
        依赖所有包的 build 任务和当前包的 generate 任务
        输出的文件夹：包含 Next.js 输出目录（.next）和项目的打包构建产物（build/**）
        </details>
        <details>
        <summary>prepareDev</summary>
        依赖于 @scow/protos 和 @scow/scheduler-adapter-protos 包的 build 任务
        输入文件夹：包含 src/pages/api/ 下的所有 TypeScript 文件
        输出目录：src/generated
        </details>
        <details>
        <summary>test</summary>
        测试的源文件和测试文件："src//.tsx", "src/**/.ts", "test//*.ts", "test//*.tsx"
        测试任务没有输出
        </details>
        <details>
        <summary>@scow/protos</summary>
        generate代码生成：输入../../../protos/**/*.proto 和 buf.gen.yaml，输出到 generated/**
        build构建任务：依赖 generate，使用生成的文件作为输入，输出到 build/**。
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
    定义了 TypeScript 编译器的选项（compilerOptions），用于控制代码编译和类型检查的行为。
    输出现代 ECMAScript 代码（ESNext）并兼容 Node.js 的 CommonJS 模块系统
    支持 .js 和 .json 文件
    开启模块解析（moduleResolution: node）和跨模块互操作性（esModuleInterop）
    严格模式（strict）提高类型安全
    跳过库检查（skipLibCheck）提高构建性能
    允许部分松散配置（noImplicitAny: false）
    支持实验性装饰器（experimentalDecorators）和元数据生成（emitDecoratorMetadata），适用于框架开发
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
        自动分组次要和修补更新。
        禁用特定文件和包的自动更新，以减少不必要的更新。
        针对特定包禁用更新，可能是由于稳定性、兼容性等原因。
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
    定义了项目 scow 的基本配置，包括依赖管理、构建、测试、开发环境等任务的 NPM 脚本，以及开发过程中所使用的工具和库。
    使用 Turbo 加速构建和任务运行。
    pnpm 用作包管理器，优化依赖管理。
    配置了 Docker 和其他开发工具（如 Husky 和 ESLint）。
    版本和发布流程也得到了支持。
        <details>
        <summary>项目基本信息</summary>
        name: "scow" — 项目的名称。
        private: true — 该项目是私有的，不会发布到 npm 注册库。
        version: "1.6.3" — 项目的版本号。
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
        @bufbuild/buf: 用于管理和生成 Protobuf 文件。
        @changesets/cli: 用于版本管理和生成变更日志。
        eslint 和 @ddadaal/eslint-config: 用于代码静态分析和检查。
        jest 和 ts-jest: 用于测试框架和 TypeScript 支持。
        typescript: TypeScript 支持。
        turbo: Turbo 工具，用于加速 monorepo 构建和任务运行。
        pnpm: 项目使用的包管理器。
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
</details>



