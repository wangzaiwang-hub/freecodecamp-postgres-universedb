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
```

## 项目结构 🗂️
```
.
├── sql/
│   ├── init_tables.sql       # 表结构定义
│   ├── sample_data.sql       # 示例数据
│   ├── queries/              # 示例查询
│   └── maintenance/          # 维护脚本
├── docs/
│   └── database_design.md    # 数据库设计文档
├── tests/                    # 查询测试案例
└── LICENSE
```

## 数据模型示例 🪐
```sql
CREATE TABLE celestial_bodies (
    body_id SERIAL PRIMARY KEY,
    name VARCHAR(100) UNIQUE NOT NULL,
    type VARCHAR(50) CHECK (type IN ('star', 'planet', 'moon', 'galaxy')),
    mass_kg NUMERIC, 
    diameter_km INT,
    discovery_date DATE,
    coordinates GEOMETRY(PointZ, 4326)
);

CREATE TABLE planetary_systems (
    system_id SERIAL PRIMARY KEY,
    host_star INT REFERENCES celestial_bodies(body_id),
    planets JSONB   # 存储行星轨道参数
);
```

## 示例查询 🔭
查找类地行星：
```sql
SELECT name, mass_kg, diameter_km 
FROM celestial_bodies
WHERE type = 'planet' 
  AND mass_kg BETWEEN 0.3e24 AND 5e24
  AND diameter_km BETWEEN 8000 AND 15000;
```

统计星系类型：
```sql
SELECT 
  CASE 
    WHEN mass_kg > 1e42 THEN 'Elliptical'
    WHEN mass_kg BETWEEN 1e40 AND 1e42 THEN 'Spiral'
    ELSE 'Dwarf'
  END AS galaxy_class,
  COUNT(*) AS quantity
FROM celestial_bodies
WHERE type = 'galaxy'
GROUP BY galaxy_class;
```

## 维护工具 🛠️
1. 备份数据库：
```bash
pg_dump -U postgres universedb > backup/$(date +%Y%m%d).sql
```

2. 重建索引：
```sql
psql -U postgres -d universedb -c "REINDEX DATABASE universedb;"
```

## 开发指南 👨🚀
### 数据规范
- 天体命名遵循IAU命名规范
- 坐标使用WGS84坐标系（经度, 纬度, 距离）
- 质量单位统一使用千克(kg)

### 贡献流程
1. 创建新分支进行开发
2. 所有SQL修改需包含对应的回滚脚本
3. 提交前执行基础验证：
```bash
./validate_scripts.sh
```

## 许可证 📜
[GPL-3.0 License](LICENSE)

---

🌠 关联freeCodeCamp课程：https://www.freecodecamp.org/learn/relational-database/
```

如果需要调整技术细节或补充特定功能说明，请告诉我具体需求！
