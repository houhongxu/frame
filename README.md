# frame

仅包含项目初始化所需的前后端骨架。

- 前端：React 19.3.0、Vite 8.3.2、TypeScript 6.0.3
- 后端：Java 21、Spring Boot 4.1.1、Maven 3.9.16（Wrapper）
- 前端为空白页面；后端只有启动类和应用上下文测试

## 目录

```text
frame/
├── frontend/                 # React + Vite + TypeScript
│   ├── src/
│   ├── package.json
│   └── package-lock.json
├── backend/                  # Spring Boot
│   ├── .mvn/wrapper/
│   ├── src/main/
│   ├── src/test/
│   ├── pom.xml
│   ├── mvnw
│   └── mvnw.cmd
├── .editorconfig
├── .gitignore
├── .nvmrc
└── README.md
```

## 环境要求

- Node.js 24 LTS，推荐使用 `.nvmrc` 指定的 24.19.0；npm 11.9.0
- JDK 21，确保 `java` 和 `javac` 可用，`JAVA_HOME` 指向 JDK
- 首次安装需联网下载 npm 和 Maven 依赖；无需全局安装 Maven

## 本地启动

在仓库根目录打开终端。如果使用 nvm，可先运行 `nvm install` 和 `nvm use`。

前端：

```bash
cd frontend
npm ci
npm run dev
```

默认访问 http://localhost:5173。页面保持空白，可从 `frontend/src/App.tsx` 开始开发。

另开一个终端启动后端：

```bash
cd backend
./mvnw spring-boot:run
```

Windows PowerShell 使用 `./mvnw.cmd spring-boot:run`。

后端默认监听 8080 端口，日志出现 `Started FrameApplication` 即启动成功。当前没有业务接口，访问根路径返回 404 是预期行为。

## 检查与构建

前端：

```bash
cd frontend
npm ci
npm run lint
npm run build
```

`build` 会先进行 TypeScript 检查，再输出静态文件到 `frontend/dist/`。可运行 `npm run preview` 本地预览构建结果。

后端：

```bash
cd backend
./mvnw clean verify
java -jar target/frame-backend-0.0.1-SNAPSHOT.jar
```

`verify` 会运行应用上下文测试并打包。Windows 使用 `./mvnw.cmd clean verify`。

前端依赖使用精确版本与 `package-lock.json` 锁定；Spring Boot 版本在 `backend/pom.xml` 中锁定，Maven 版本由 Wrapper 固定。升级依赖时同步更新相关版本文件和锁文件。
