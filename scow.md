<details>
<summary>OpenSCOW1</summary>
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
    <summary>二级标题 - 可折叠部分1.1</summary>
    这是二级内容部分1.1。
        <details>
        <summary>三级标题 - 可折叠部分1.1.1</summary>
        这是三级内容部分1.1.1。
        </details>
    </details>
</details>



