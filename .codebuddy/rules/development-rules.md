# 开发规则规范

## 代码风格规范
- **语言**: Java 17+
- **缩进**: 4个空格
- **命名约定**:
  - 类名: PascalCase (如 `StockService`)
  - 方法名: camelCase (如 `calculatePrice`)
  - 变量名: camelCase (如 `stockPrice`)
  - 常量: UPPER_SNAKE_CASE (如 `MAX_RETRY_COUNT`)
- **包结构**: 遵循分层架构模式

## 架构约束
- **严格分层**: 各层之间单向依赖
- **依赖方向**: Interfaces → Application → Domain ← Infrastructure
- **禁止跨层调用**: Infrastructure层不能直接调用Interfaces层

## 测试要求
- 单元测试覆盖率 ≥ 80%
- 每个公共方法都必须有对应的测试
- 使用Given-When-Then模式编写测试

## 提交规范
- 提交信息遵循Conventional Commits格式
- 功能提交: `feat: 添加股票数据查询功能`
- 修复提交: `fix: 修复价格计算逻辑错误`
- 文档提交: `docs: 更新API文档`

## 安全规范
- 禁止硬编码敏感信息
- 所有API端点必须进行身份验证
- 数据库查询使用参数化查询防止SQL注入