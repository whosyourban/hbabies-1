# Hbabies 数据库表文档, 基于 Mysql8.0


```
create table user (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `name` varchar(64) DEFAULT '' COMMENT '员工名字',
    `account` varchar(64) DEFAULT '' COMMENT '账号',
    `password` varchar(64) DEFAULT '' COMMENT '加盐md5密码',
    `phone` varchar(32) DEFAULT '' COMMENT '电话号码',
    `email` varchar(64) DEFAULT '' COMMENT '邮箱',
    `is_delete` TINYINT(1) DEFAULT '0' COMMENT '是否删除状态,0:否,1:是',
    `is_active` TINYINT(1) DEFAULT '1' COMMENT '能否登录,0:否,1是',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    UNIQUE KEY `idx_account` (`account`) 
) ENGINE=InnoDB   DEFAULT CHARSET=utf8mb4 COMMENT='用户表';


create table permission (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `name` int(11)  COMMENT '权限名称',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
   UNIQUE KEY `idx_name` (`name`) 
) ENGINE=InnoDB   DEFAULT CHARSET=utf8mb4 COMMENT='权限表';


create table user_permission (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `user_id` int(11) COMMENT '用户id',
    `permission_id` int(11)  COMMENT '权限id',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    UNIQUE KEY `uniq_idx_user_permission` (`user_id`, `permission_id`)  
) ENGINE=InnoDB  DEFAULT CHARSET=utf8mb4 COMMENT='用户权限';


create table bank_account (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `name` varchar(255) DEFAULT '' COMMENT '用户名',
    `account` varchar(255) DEFAULT '' COMMENT '账号',
    `bank` varchar(511) DEFAULT '' COMMENT '银行名',
    `note` varchar(511) DEFAULT '' COMMENT '备注',
    `balance` DECIMAL(10,2) DEFAULT 0 COMMENT '余额',
    `is_delete` TINYINT(1) DEFAULT '0' COMMENT '是否删除状态,0:否,1:是',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    UNIQUE KEY `uniq_account` (`account`, `bank`) 
) ENGINE=InnoDB   DEFAULT CHARSET=utf8mb4 COMMENT='账户';


create table item_round (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `name` varchar(255) DEFAULT '' COMMENT '描述',
    `color` varchar(64) DEFAULT '' COMMENT '颜色',
    `target` varchar(255) DEFAULT '' COMMENT '目标名',
    `targetPrice` DECIMAL(10,2) DEFAULT 0 COMMENT '目标价',
    `status` TINYINT(2) DEFAULT '1' COMMENT '状态:1开放，0:结束',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间'
) ENGINE=InnoDB   DEFAULT CHARSET=utf8mb4 COMMENT='回合';


create table commodity_type (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `name` varchar(255) DEFAULT '' COMMENT '类别名',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间'
) ENGINE=InnoDB  DEFAULT CHARSET=utf8mb4 COMMENT='商品分类';


create table purchase_address (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `address` varchar(64) DEFAULT '' COMMENT '地点',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    UNIQUE KEY `uniq_address` (`address`) 
) ENGINE=InnoDB  DEFAULT CHARSET=utf8mb4 COMMENT='购买地';


create table commodity (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `round_id` int(11) COMMENT 'round_id',
    `number` varchar(255) COMMENT '商品编号',
    `name` varchar(511) DEFAULT '' COMMENT '商品名',
    `purchase_address_id` int(11) DEFAULT 0 COMMENT '购买地',
    `address` varchar(64) DEFAULT '' COMMENT '仓库所在地',
    `type_id` varchar(64) DEFAULT '' COMMENT '商品分类id',
    `size` varchar(64) DEFAULT '' COMMENT '尺码',
    `purchase_price` DECIMAL(10,2) DEFAULT 0 COMMENT '买入价格',
    `pre_sell_price` DECIMAL(10,2) DEFAULT 0 COMMENT '预估售出价格',
    `sell_price` DECIMAL(10,2) DEFAULT 0 COMMENT '实际成交价格',
    `status` int(11) DEFAULT '0' COMMENT '状态,0:无,1:付定金,2:在途,3:入库,4:出库',
    `operator` varchar(64) DEFAULT '' COMMENT '操作者账号,user.account',
    `client` varchar(64) DEFAULT '' COMMENT '售出客户名',
    `descrpition` varchar(511) COMMENT '商品描述/型号',
    `comment` varchar(511) COMMENT '备注',
    `sell_comment` varchar(511) COMMENT '售出备注',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `sell_time` TIMESTAMP COMMENT '售出时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
    KEY `idx_name` (`name`),
    KEY `idx_type_id` (`type_id`),
    KEY `idx_purchase_address_id` (`purchase_address_id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8mb4 COMMENT='商品';


create table commodity_op_account (
    `id` int(11) AUTO_INCREMENT PRIMARY KEY,
    `commodity_id` int(11) COMMENT '商品id',
    `bank_account_id` int(11) COMMENT '账户id？？？',
    `create_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
    `update_time` TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间'
) ENGINE=InnoDB  DEFAULT CHARSET=utf8mb4 COMMENT='商品操作账户, 这里需要确认下';


```
