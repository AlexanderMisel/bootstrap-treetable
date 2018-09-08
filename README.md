# bootstrap-treetable

#### 项目介绍
这个东西最初出现在guns项目，基于jquery.treegrid.js实现的树。但在实际应用过程中这个方案数据量过大会有性能问题，遂抛掉了jquery.treegrid重新实现了相关功能。

用法跟bootstrap-table差不多，这里就不多写了，当然也可以参考guns项目或ruoyi项目。


### 2018-09-08 更新内容

> * 列参数增加align、valign、visible三项
> * 优化css样式

### 2018-08-31 更新内容

> * 优化appendData方法，不再刷新整个表格，如果添加数据id重复，将以最后一条为准
> * 由于选择数据问题得已解决，因此去掉 code 设置、 parentCode 变更为 parentId、rootCodeValue 变更为 rootIdValue，简化配置

### 2018-08-23 更新内容

> * 优化收缩子行显示，收缩后再展开保留子行的展开记录
> * 优化getSelections方法，getSelections返回的数据不再是显示列的数据，而是直接返回原数据
> * 新增appendData方法，为啥是appendData而不是appendChildNode？因为可以添加任意数据到表格（数据格式与原数据一样），目前还是刷新整个表格⊙﹏⊙

#### DEMO 1

```

<table id="demo"></table>
var treeTable = $('#demo').bootstrapTreeTable({
    columns: [{
        title: '菜单名称',
        field: 'menuName',
        width: '20%',
        formatter: function(value,row, index) {
            if (row.icon == null || row == "") {
                return row.menuName;
            } else {
                return '<i class="' + row.icon + '"></i> <span class="nav-label">' + row.menuName + '</span>';
            }
        }
    }],
    data:[{
        "id": 1,
        "menuName": "系统管理",
        "parentId": 0,
        "icon": "glyphicon glyphicon-thumbs-up"
    }, {
        "id": 2,
        "menuName": "系统监控",
        "parentId": 0,
        "icon": "glyphicon glyphicon-thumbs-up"
    }, {
        "id": 100,
        "menuName": "用户管理",
        "parentId": 1,
        "icon": "#"
    }, {
        "id": 101,
        "menuName": "角色管理",
        "parentId": 1,
        "icon": "#"
    }]
});
```

#### DEMO 2
```
<div id="demo-toolbar" class="btn-group" role="group">
  <button type="button" class="btn btn-default">新增</button>
  <button type="button" class="btn btn-default">编辑</button>
  <button type="button" class="btn btn-default">删除</button>
</div>
<table id="demo"></table>
var treeTable = $('#demo').bootstrapTreeTable({
    type: 'get',                   // 请求方式（*）
    url: "./data.json",            // 请求后台的URL（*）
    ajaxParams : {},               // 请求数据的ajax的data属性
    toolbar: "#demo-toolbar",      //顶部工具条
    expandColumn : 1,              // 在哪一列上面显示展开按钮
    columns: [{
        field: 'selectItem',
        checkbox: true
     },{
        title: '菜单名称',
        field: 'menuName',
        width: '20%',
        formatter: function(value,row, index) {
            if (row.icon == null || row == "") {
                return row.menuName;
            } else {
                return '<i class="' + row.icon + '"></i> <span class="nav-label">' + row.menuName + '</span>';
            }
        }
    }]
});
```
#### 所有表格参数

```
rootIdValue: null,            // 设置根节点id值----可指定根节点，默认为null,"",0,"0"
id : "id",                      // 选取记录返回的值,用于设置父子关系
parentId : "parentId",        // 用于设置父子关系
type: 'get',                    // 请求方式（*）
url: "./data.json",             // 请求后台的URL（*）
ajaxParams : {},                // 请求数据的ajax的data属性
expandColumn : 0,               // 在哪一列上面显示展开按钮
expandAll : false,              // 是否全部展开
expandFirst : true,             // 是否默认第一级展开--expandAll为false时生效
toolbar: null,                  // 顶部工具条
height: 0,                      // 表格高度
expanderExpandedClass : 'glyphicon glyphicon-chevron-down',// 展开的按钮的图标
expanderCollapsedClass : 'glyphicon glyphicon-chevron-right',// 缩起的按钮的图标
```

#### 所有列参数

```

title      String  undefined   表头要显示的文本
field      String  undefined   要显示数据的字段名称，可以理解为json对象里的key
checkbox   Boolean false   设置为True的时候 则显示一列checkbox组件，该列的宽度为固定宽度
radio      Boolean false   设置为True的时候 则显示一列radio组件，该列的宽度为固定宽度
align      String  undefined   设置单元格数据的左右对齐方式， 可选择的值有：’left’, ‘right’, ‘center’
valign     String  undefined   设置单元格数据的上下对齐方式， 可选择的值有：’top’, ‘middle’, ‘bottom’
width      Number {Pixels or Percentage}   undefined    设置单元格列宽度。可以使用’%’百分比的方式，也可以设置要显示的像素值
visible    Boolean true    显示或隐藏该列， 默认显示， False为隐藏
formatter  Function    undefined   单元格格式化函数，有三个参数：value： 该列的字段值；row： 这一行的数据对象；index： 行号，第几行，从0开始计算
例子：formatter : function(value, row, index){ return value + row.id + index; }

```
#### 方法
```
//刷新
$('#demo').bootstrapTreeTable('refresh');
```

```
//带参刷新
var params = {
    searchKey:"haha"
};
$('#demo').bootstrapTreeTable('refresh',params);
```

```
//获取所选数据
var selected = $('#demo').bootstrapTreeTable('getSelections');
//为了兼容bootstrap-table的写法，统一返回数组
```

```
//任意添加数据到表格（数据格式与原数据一样）
//注：重复数据将以最后一条为准
var data = [{
        "searchValue": null,
        "createBy": "admin",
        "createTime": "2018-03-16 11:33:00",
        "updateBy": null,
        "updateTime": null,
        "remark": null,
        "params": null,
        "id": 1038,
        "menuName": "在线查询",
        "parentName": null,
        "parentId": 109,
        "orderNum": "1",
        "url": "#",
        "menuType": "F",
        "visible": 0,
        "perms": "monitor:online:list",
        "icon": "#"
    },{...}];
$('#demo').bootstrapTreeTable('appendData',data);
```

![输入图片说明](https://images.gitee.com/uploads/images/2018/0730/143841_6391c64a_405607.png "demo.png")
![输入图片说明](https://images.gitee.com/uploads/images/2018/0730/153142_6dc6ff87_405607.png "demo2.png")