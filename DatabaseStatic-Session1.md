# Hbabies 数据库临时数据 - 第一阶段用


### /account/list

```
name:TQ工行 account:622202360205446442 bank:工商银行 balance:32000 note:TQ国内工行
name:宅杰招商 account:622202360205446443 bank:招商银行 balance:124000 note:宅杰国内招商
name:Vien汇丰 account:622202360205446444 bank:汇丰银行 balance:46000 note:Vien香港汇丰
name:Vien渣打 account:622202360205446445 bank:渣打银行 balance:14000 note:Vien香港渣打
```

### /staff/list

```
name:TQ account:622202360205446442 password:tq123 phone:13580493109 email:tqtan@qq.com
name:Vien account:622202360205446444 password:vien123 phone:18814864859 email:vienluk@qq.com
name:宅杰 account:622202360205446443 password:zhai123 phone:18028615055 email:zhaijie@qq.com
```

### /tag/list

```
name:red
name:yellow
name:orange
name:green
name:blue
name:dark
name:white
```

### /type/list

```
name:围巾
name:鞋子
name:手袋
name:衣服
name:裤子
name:外套
name:手表
name:香水
```

### /form/prefillInfo

// 录入商品预拉上面员工、tag、type、account 的所有字段，相当于一个合并请求

```
data: {
	accounts: [],
	staff: [],
	tag: [],
	type: []
}
```