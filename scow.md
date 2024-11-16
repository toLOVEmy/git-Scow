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
</details>



