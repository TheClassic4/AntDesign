 ### Table
 ```
 /**
 * 修复react中数据需要加key
 * @param arr
 * @param name
 * @returns {Array}
 * @example
 *     dataSource = fixArrKey(dataSource, 'id');
 */
export function fixArrKey(arr = [], name = 'id') {
    return arr.map((item, index) => {
      if (item.key) return item;
      item.key = item[name] || index;
      return item;
    });
}
 
 onSelectChange = selectedRowKeys =>{
 // 此处rowKey若不规定则为默认选择行id 1,2,3 指定后则为dataSoure中对应的'id'
  this.setState({ selectedRowKeys });
 }
 render(){
      const rowSelection = {
      selectedRowKeys,
      onChange: this.onSelectChange
    }
     let columns = [
        {
          title: '',
          width: 300,
          dataIndex: 'description',
          key: 'description'
        },
        {
          title: '',
          width: 300,
          dataIndex: 'hotTopicContext',
        },
        {
          title: '',
          width: 300,
          dataIndex: 'channel',
        },
        {
          title: ,
          width: 300,
          dataIndex: 'count',
        },
        {
          title:'',
          render :(id,item) => {
            return <span>
              <span onClick={this.similarQuestionModal.bind(this,'edit',item)} className='editButton'></span>
          }
        }
    ];
 return(   
   <Table
    rowKey='id'
    columns={columns}
    rowSelection={rowSelection}
    dataSource={fixArrKey(dataSource)}
    pagination={{}}
  />
  )
}
 ```
