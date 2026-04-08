# CSV 测试数据目录

此目录用于存放 JMeter 测试脚本的参数化数据文件。

## 文件格式

- 格式：CSV（逗号分隔）
- 编码：UTF-8 with BOM（支持中文）
- 第一行：列标题（变量名）

## 示例

### 用户数据 (user_data.csv)
```csv
username,password,email
testuser1,Pass123,user1@example.com
testuser2,Pass456,user2@example.com
testuser3,Pass789,user3@example.com
```

### 商品数据 (product_data.csv)
```csv
productId,productName,price,category
1001,iPhone 15,7999,手机
1002,MacBook Pro,14999,电脑
1003,iPad Air,4799,平板
```

## 注意事项

1. 使用相对路径引用 CSV 文件
2. 在 JMeter 中设置 `recycle=true` 以重用数据
3. 使用 `shareMode.all` 确保线程安全
4. 测试前验证数据格式正确性
