# 婚前辅导多表单（本地网页）

同一站点选择不同问卷填写与双方对照。数据仅存本机浏览器。

## 启动

```bash
cd web
python -m http.server 8765
```

打开：`http://127.0.0.1:8765/`

## 表单列表

| ID | 名称 | 对照 |
|---|---|---|
| assessment | 婚前关系评估 | 量表色标 |
| intake | 约谈问卷 | 开放题并排 |
| expectations | 期待 + 婚姻观 | 开放题并排 |
| family | 原生家庭 | 开放题并排 |
| knowyou | 知己知彼与沟通 | 开放题并排 |
| roles | 夫妻角色 | 量表色标 |
| sex | 性观念 | 选择题色标 |

## 用法

1. 首页点选表单 → 填丈夫 / 填妻子  
2. 点「对照」看差异（有分数的表）或开放题并排  
3. **每个表单**可「导出本表 / 导入本表」；顶部还可「导出全部 / 导入」  
4. 单表文件：`premarital-<formId>.json`；全部：`premarital-forms-all.json`  
5. **双机填写**：丈夫手机只填丈夫 → 导出全部；妻子手机导入后只填妻子 → 再导出给丈夫导入。导入默认 **按人合并**（空的一方不会覆盖本地已填）。

## 测试

```bash
node scripts/test_import_export.mjs
```

覆盖：导出全部往返、双机 merge、replace 会擦掉空侧、单表导入、表单过滤。

链接格式：

- 填写：`fill.html?form=roles&person=a`
- 对照：`compare.html?form=roles`

## 隐私

- 不上云；清浏览器会丢数据  
- 导出文件含敏感内容，自行保管  

## 重新生成题库

```bash
python scripts/build_assessment_json.py   # 评估
python scripts/build_other_forms.py       # 其余表单
```

注册表：`web/data/forms.json`（增表单改这里 + 加 `web/data/forms/<id>.json`）。
