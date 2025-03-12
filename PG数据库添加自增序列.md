在PostgreSQL中，若您希望在创建表时让`relate_id`字段自动递增，无需手动填写，您可以使用`SERIAL`类型或`BIGSERIAL`类型（针对`bigint`类型的自动递增）。然而，在您的DDL（数据定义语言）语句中，您已经显式地将`relate_id`定义为了`int8`（即`bigint`），并且没有使用`SERIAL`或`BIGSERIAL`。

为了修改`relate_id`以使其自动递增，您有两个选择：

1. **使用`BIGSERIAL`类型重新创建表**（如果表尚未包含重要数据，或者您可以在创建新表后迁移数据）：

```sql
CREATE TABLE "device"."zl_manual_point_relate" (
  "relate_id" BIGSERIAL NOT NULL,
  "manual_id" int8,
  "point_id" int8,
  "manual_type" varchar(200) COLLATE "pg_catalog"."default",
  "is_deleted" int2
);
```

但请注意，使用`BIGSERIAL`会自动为您创建一个名为`<table_name>_<column_name>_seq`的序列，并设置该列的默认值为`nextval`函数从该序列中获取的值。由于您已经定义了主键，因此无需再次添加主键约束，因为`BIGSERIAL`已经隐含了主键的特性（实际上，它通常与`PRIMARY KEY`一起使用，但并非严格必要，因为您可以手动指定其他列作为主键）。然而，在您的场景中，您已经有一个明确的主键定义，所以只需使用`BIGSERIAL`替换`int8`即可。

但如果您想在保持当前表结构的同时添加自动递增功能，您应该：

1. **为`relate_id`添加一个序列，并设置默认值**：

首先，创建一个序列：

```sql
CREATE SEQUENCE "device"."zl_manual_point_relate_relate_id_seq"
  START WITH 1
  INCREMENT BY 1
  NO MINVALUE
  NO MAXVALUE
  CACHE 1;
```

然后，修改表以使用此序列作为默认值：

```sql
ALTER TABLE "device"."zl_manual_point_relate"
  ALTER COLUMN "relate_id" SET DEFAULT nextval('"device"."zl_manual_point_relate_relate_id_seq"'::regclass);
```

**重要提示**：由于您已经为`relate_id`设置了主键，因此无需再次执行此操作。上述步骤仅适用于添加自动递增的主键。
