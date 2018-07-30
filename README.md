# bootstrap-treetable

#### 项目介绍
这个东西最初出现在guns项目，基于jquery.treegrid.js实现的树。但在实际应用过程中这个方案数据量过大会有性能问题，遂抛掉了jquery.treegrid重新实现了相关功能。

用法跟bootstrap-table差不多，这里就不多写了，当然也可以参考guns项目或ruoyi项目。

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
    url: "./data.json",             // 请求后台的URL（*）
    ajaxParams : {},               // 请求数据的ajax的data属性
    toolbar: "#demo-toolbar",//顶部工具条
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
    }]
});
```
#### 所有参数

```
rootCodeValue: null,            // 设置根节点code值----可指定根节点，默认为null,"",0,"0"
id : "id",                      // 选取记录返回的值
code : "id",                    // 用于设置父子关系
parentCode : "parentId",        // 用于设置父子关系
type: 'get',                    // 请求方式（*）
url: "./data.json",             // 请求后台的URL（*）
ajaxParams : {},                // 请求数据的ajax的data属性
expandColumn : 0,             // 在哪一列上面显示展开按钮
expandAll : false,              // 是否全部展开
expandFirst : true,             // 是否默认第一级展开--expandAll为false时生效
toolbar: null,                  // 顶部工具条
height: 0,                      // 表格高度
expanderExpandedClass : 'glyphicon glyphicon-chevron-down',// 展开的按钮的图标
expanderCollapsedClass : 'glyphicon glyphicon-chevron-right',// 缩起的按钮的图标
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
//刷新
var selected = $('#demo').bootstrapTreeTable('getSelections');
//为了兼容bootstrap-table的写法，统一返回数组，这里返回了指定的id及表格显示列的数据
```

![输入图片说明](https://images.gitee.com/uploads/images/2018/0730/143841_6391c64a_405607.png "demo.png")
