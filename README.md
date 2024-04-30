# 模拟股票交易系统运行

## 数据库
/BACKEND/app/settings.py 保存着数据库设置
```
'mysql+pymysql://root:root@127.0.0.1:3306/exchange_system'  # 数据库配置连接
```
创建用户为root,密码为root的mysql连接，也可以修改以上配置

需创建名为‘exchange_system’的数据库，

使用exchange_system.sql在数据库查询中，初始化数据库

## 后端

### 创建虚拟环境
conda create -n stock python=3.9

conda activate stock
### 安装依赖项
cd /BACKEND
pip install -r requirements.txt

### 运行 
python app\run.py

## 前端
前端采用Vue框架

### 下载依赖包
```
npm install
```

### 编译开发

```
npm run serve
```

### 上线部署

```
npm run build