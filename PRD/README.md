# 产品需求文档



产品需求可以集思广益，有空的同学，或者在做这一块的同学，可以根据现在的产品做一些功能迭代，提供prd文档。



# 需求说明

## 目前已完成的需求

![1565234927724](1565234927724.png)

## 后续需求规划

下面是我按照B2B2C的电商功能整理的部分需要，目前只写了平台功能的商品和交易管理部分，稍后我会把会员管理，促销、积分商城、分销、统计、结算、搜索
卖家模块、买家模块的功能完善了。至少希望到用Spring Cloud Alibaba 重构的时候能把这个电商平台变成B2B2C的。

平台功能
一、商品管理
1. 品牌管理

功能描述

维护平台所有卖的所有品牌。

具体操作

查询、添加、编辑、删除

2.规格管理

功能描述

管理比如颜色、尺码等此类数据的管理。

具体操作

查询、添加、编辑、删除

3. 类型管理

功能描述

关联品牌、规格，并可以录入查询属性和自定义属性，查询属性在列表页方便用户动态筛选，自定义属性需要商家在录入商品的时候录入对应的数据。

具体操作

查询、添加、编辑、删除

4. 分类管理

功能描述

商城的三级分类，关联类型，在此处录入佣金，根据佣金比例，平台和商家结算时扣除对应的佣金。

具体操作

查询、添加、编辑、删除



品牌、规格、类型、分类构成商品的基本属性，类型又关联商品的查询属性、自定义属性，这样每一个分类下面的商品属性都是动态可配置的。
5. 待审核的品牌

功能描述

平台录入的品牌不满足商家要求时，商家可以提交品牌给平台进行审核，平台审核通过之后，进入到品牌库中。

具体操作

查询、审核


6. 商家分类申请

功能描述

刚审核通过的商家是不能在分类下面上传商品，商家想在平台哪个三级分类下面上传商品，需要提交平台进行审核，平台根据商家的资质进行审核，审核通过之后商家才能在此分类下面上传商品。

具体操作

查询、审核通过、审核失败


7. 待售商品

功能描述

显示商家提交审核的全部商品，管理员可以审核通过、审核驳回、也可以直接删除商品。

具体操作

查询、商品详情、审核通过、审核驳回、删除商品

8. 在售商品

功能描述

显示全部在销售的商品，并可以对已经销售的商品进行下架、删除操作，也可以对单个商品设置三级分销的佣金。

具体操作

查询、删除商品、下架商品、设置佣金 

9. 已删除的商品

功能描述

采用标记删除，删除之后是不可逆的，已经删除的商品，在用户前端是可以查看的，不过显示此产品已经下架。

具体操作

查询


共有7个状态来控制商品的上架流程分别是：刚创建、提交审核、审核通过、申请驳回、商品删除、上架、下架，只有处于已上架状态的产品，用户才可能看到商品，各个细节形成一个完整的闭环

二、交易管理
1. 全部订单

功能描述

查看所有的订单，并可以打印订单详情，查看订单具体内容，货到付款的订单可以设置为已经收款。

具体操作

查询、打印、订单详情、确认收款 

2. 未付订单

功能描述

显示未付款的订单。

具体操作

查询、打印

3. 待确认订单

功能描述

货到付款的订单是待确认的订单，商家确认操作之后到待发货的订单。

具体操作

查询、打印

4. 待发货订单

功能描述

待发货的订单是付完款和待确认的订单确认之后显示。

具体操作

查询、打印

5. 已发货订单

功能描述

待发货的订单发货之后到已发货的订单。

具体操作

查询、打印、确认收款

6. 已完成订单

功能描述

完成以下2个操作之一，从已发货的订单变成已完成的订单：
1、用户点击确认收货；
2、用户不点击确认收货15个自然日系统定时器由已发货的订单修改为已完成的订单

具体操作

查询、打印、确认收款

6. 已取消订单

功能描述

完成以下2个操作之一，可以变成已取消的订单：
1、用户点击取消；
2、用户未付款24小时系统定时器从未付款的订单变成已取消的订单

具体操作

查询


订单共有6种基本状态分别是：1、未付款的订单；2、待确认的订单；3、待发货的订单；4、已发货的订单；5、已完成的订单；6、取消的订单。
订单关于库存的处理：
1、加入购物车判断库存，不减库存；
2、提交订单判断库存数量；
3、下单成功减库存；
4、订单取消库存回滚；

7. 退货管理

功能描述

已确认收货的订单可以在15个工作日之内进行退货操作，最终由平台完成退款的操作，具体操作流程：买家申请退货—>商家审核通过或者不予处理—>商家审核通过买家发货—>商家收货收货—>平台退款—>退货完成

具体操作

查询、退款


8. 换货管理

功能描述

换货是商家和用户之间的关联，平台只是查看所有的换货信息，换货的流程是：买家提交换货申请—>卖家审核通过或者不予处理—>卖家审核通过用户发回退件—>卖家收到退件判断是否符合退货申请—>商家发出换件或者原件退还—>不处理—>换货结束

具体操作

查询

9. 投诉管理

功能描述

假如商家不给用户退货换，用户可以提交平台进行申诉，商家也可以提交申诉，最终由平台进行裁决。具体的操作流程是：买家提交投诉申请—>平台审核买家投诉是否通过审核—>平台审核通过之后卖家提交申诉—>平台最终裁定买家申诉通过还是不通过—>卖家申诉不通过强制卖家处理退货换—>卖家申诉通过不处理—>申诉结束

具体操作

查询、处理、重置


退货换完全按照京东和天猫的方式来做的，审核通过之后商家会录入收货地址，买家邮寄商品也会选择快递公司并输入快递单号









