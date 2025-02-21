# 宇宙数据库 🌌

一个为freeCodeCamp PostgreSQL课程设计的太空天体数据库系统，包含恒星、行星及宇宙现象的数据管理与分析功能。

## 功能亮点 🚀
- **天体数据管理**
  - 恒星/行星/卫星分类存储
  - 天体物理属性记录（质量、轨道参数等）
- **高级查询**
  - 星系结构分析
  - 天体类型统计
  - 空间坐标范围搜索
- **数据维护**
  - 批量数据导入/导出
  - 数据库备份脚本
  - 数据完整性校验

## 快速入门 ▶️
### 环境准备
- PostgreSQL 12+
- pgAdmin 4（可选）
- PostGIS 3.0（空间扩展）

### 安装步骤
```bash
git clone https://github.com/wangzaiwang-hub/freecodecamp-postgres-universedb.git
cd freecodecamp-postgres-universedb

# 创建数据库
psql -U postgres -c "CREATE DATABASE universedb;"

# 初始化表结构
psql -U postgres -d universedb -f sql/init_tables.sql

# 导入示例数据
psql -U postgres -d universedb -f sql/sample_data.sql
