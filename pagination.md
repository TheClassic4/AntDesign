[antd pagination 文档](https://ant.design/components/pagination-cn/#header)
```
                 pagination={{
                   total:rowCount,
                   current:pageNumber,
                   showQuickJumper:true,
                   showSizeChanger:true,
                   onChange:this.paginationChange,
                   onShowSizeChange:this.pageShowSizeChange,
                   showTotal:total => intl('item_total_number', {"rowCount": rowCount}, true),
                 }}                
```
total:数据总数
current:当前的页数

```
  paginationChange=(page, pageSize)=>{
    this.setState({
      pageSize:pageSize,
      pageNumber:page,
    })
  }
```

当页面跳转，或者每个页面可以选择展示的pageSize改变的时候刷新获取默认展示参数的list

如果需要跳转回page 1 只需在相应的借口后面设置setState让current = 1
