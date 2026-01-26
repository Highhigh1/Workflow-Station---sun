# Low-Code Workflow Platform

Enterprise low-code workflow platform for HSBC, providing visual process design, workflow automation, and business process management capabilities.

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                        API Gateway                               │
│                    (Spring Cloud Gateway)                        │
└─────────────────────────┬───────────────────────────────────────┘
                          │
    ┌─────────────────────┼─────────────────────┐
    │                     │                     │
    ▼                     ▼                     ▼
┌─────────┐        ┌─────────────┐       ┌──────────┐
│ Admin   │        │  Workflow   │       │  User    │
│ Center  │        │   Engine    │       │  Portal  │
└────┬────┘        └──────┬──────┘       └────┬─────┘
     │                    │                   │
     └────────────────────┼───────────────────┘
                          │
              ┌───────────┴───────────┐
              │                       │
         ┌────▼────┐            ┌─────▼─────┐
         │ Kafka   │            │  Redis    │
         │ (Async) │            │  (Cache)  │
         └─────────┘            └───────────┘
                          │
                    ┌─────▼─────┐
                    │PostgreSQL │
                    │   16.5    │
                    └───────────┘
```

## Tech Stack

| Layer | Technology |
|-------|------------|
| Backend | Java 17, Spring Boot 3.2, Spring Cloud Gateway |
| Frontend | Vue 3, TypeScript, Element Plus |
| Database | PostgreSQL 16.5 |
| Cache | Redis 7.2 |
| Messaging | Apache Kafka |
| Workflow | Flowable 7.0.0 |
| Container | Docker, Kubernetes, Helm |

## Modules

### Backend Services
- `api-gateway` - API Gateway with rate limiting and authentication
- `workflow-engine-core` - Flowable-based workflow engine
- `admin-center` - User, role, and permission management
- `developer-workstation` - Visual process and form designer
- `user-portal` - Task inbox and process initiation

### Shared Libraries
- `platform-common` - Shared DTOs, exceptions, utilities
- `platform-security` - JWT authentication, encryption
- `platform-cache` - Redis cache service
- `platform-messaging` - Kafka event publishing

### Frontend Applications
- `frontend/admin-center` - Admin management UI
- `frontend/developer-workstation` - Developer tools UI
- `frontend/user-portal` - End user portal UI

## Quick Start

### Prerequisites
- Java 17+
- Node.js 20+
- Docker & Docker Compose
- Maven 3.9+

### Local Development

1. Start infrastructure services:
```bash
docker-compose up -d postgres redis kafka zookeeper
```

2. Build backend:
```bash
mvn clean install -DskipTests
```

3. Run services:
```bash
# Terminal 1 - API Gateway
cd backend/api-gateway && mvn spring-boot:run

# Terminal 2 - Workflow Engine
cd backend/workflow-engine-core && mvn spring-boot:run
```

4. Start frontend:
```bash
cd frontend/user-portal && npm install && npm run dev
```

### Full Stack with Docker
```bash
docker-compose --profile full up -d
```

## Configuration

Environment variables:
| Variable | Description | Default |
|----------|-------------|---------|
| `POSTGRES_PASSWORD` | Database password | `platform_dev_password` |
| `REDIS_PASSWORD` | Redis password | `redis_dev_password` |
| `JWT_SECRET` | JWT signing key | (dev key) |
| `ENCRYPTION_SECRET_KEY` | AES-256 encryption key | (dev key) |

## API Documentation

API documentation available at:
- Gateway: `http://localhost:8080/swagger-ui.html`
- Workflow Engine: `http://localhost:8081/swagger-ui.html`

## Testing

```bash
# Run all tests
mvn test

# Run with coverage
mvn test jacoco:report
```

## Deployment

### Kubernetes
```bash
kubectl apply -f deploy/kubernetes/
```

### Helm
```bash
helm install workflow-platform ./deploy/helm/platform -f values-production.yaml
```

## Documentation

- [Requirements](docs/requirements-full/)
- [Architecture Spec](.kiro/specs/platform-architecture/)

## License

Proprietary - HSBC Internal Use Only

你正在分析的是一个【已经规范好的代码结构】。

请根据你当前能看到的：
- 文件夹结构
- 文件命名方式
- 代码风格
- 抽象层级
- 错误处理方式
- 依赖边界
- 注释与文档习惯

执行以下任务（按顺序）：

1. 总结这个项目【隐含的工程规范和设计约定】，而不是常见的通用规范。
   - 重点关注：作者“刻意在坚持什么”
   - 忽略偶然出现的例外

2. 抽象出一份【Steering / Coding Rules 文档】：
   - 用“必须 / 不允许 / 建议”的语气
   - 每条规则要短、可执行
   - 假设这份文档是给 AI 和新成员用的

3. 给出这份 Steering 的【适用边界】：
   - 哪些规则是全局的
   - 哪些只适用于某些目录或层

4. 输出为 Markdown，结构如下：

# Project Steering

## Architecture Rules
- 

## Code Style Rules
- 

## Dependency Rules
- 

## Error Handling Rules
- 

## Naming & Structure Rules
- 

## Things This Project Explicitly Avoids
- 

不要复述代码，不要解释基础概念，只输出你总结出的规则。
如果某些规则你无法确定，请明确标注为「推断规则」。

4. 将这份 Steering 改写成【AI Follow Rules】风格：
   - 假设这是 system-level 指令
   - 用 "Always / Never / Only if" 开头
   - 不要解释原因
