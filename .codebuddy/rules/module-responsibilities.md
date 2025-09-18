# 模块职责划分规范

## 分层架构职责

### 1. Interfaces层 (表现层)
**职责**: 处理HTTP请求和响应
- 接收外部请求
- 参数验证和格式化
- 返回统一的响应格式
- 身份验证和授权

**允许依赖**: Application层
**禁止依赖**: Domain层, Infrastructure层

### 2. Application层 (应用层)
**职责**: 协调领域逻辑和基础设施
- 业务流程编排
- 事务管理
- 领域服务调用协调
- DTO转换

**允许依赖**: Domain层
**禁止依赖**: Infrastructure层, Interfaces层

### 3. Domain层 (领域层)
**职责**: 核心业务逻辑
- 领域模型定义
- 业务规则实现
- 领域服务
- 值对象和实体

**允许依赖**: 无其他层（纯领域逻辑）
**禁止依赖**: 任何其他层

### 4. Infrastructure层 (基础设施层)
**职责**: 技术实现细节
- 数据库访问 (Repository实现)
- 外部API调用
- 消息队列
- 文件存储

**允许依赖**: Domain层
**禁止依赖**: Interfaces层, Application层

## 具体模块职责示例

### 股票数据模块
- **Interfaces**: `StockController` - 提供RESTful API
- **Application**: `StockApplicationService` - 协调数据获取和业务逻辑
- **Domain**: `Stock`, `StockPrice` - 领域模型和业务规则
- **Infrastructure**: `JpaStockRepository` - 数据库访问实现

### 分析报告模块
- **Interfaces**: `ReportController` - 报告生成和下载API
- **Application**: `ReportApplicationService` - 报告生成流程协调
- **Domain**: `AnalysisReport`, `ReportGenerator` - 报告生成逻辑
- **Infrastructure**: `PdfReportExporter` - PDF导出实现

## 跨层交互规则
1. Interfaces → Application: 通过Application Service接口
2. Application → Domain: 直接调用领域服务或聚合根
3. Application → Infrastructure: 通过接口依赖，由IoC容器注入实现
4. Infrastructure → Domain: 实现Domain定义的Repository接口