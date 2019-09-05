# AntDesign

## Form

```
<template>
  <a-form @submit="handleOk" :form="form">
    // :form="form" 必须优先注册
    <!-- 客户姓名 -->
    <a-form-item
        :labelCol="labelCol" // 排列样式
        :wrapperCol="wrapperCol"
        label='客户姓名：'
      >
      <a-input
        v-decorator="[
          'name', // 给表单赋值或拉取表单时，该input对应的key
          {rules: [{ required: true, message: '请输入客户名称!' }]}
        ]"
        placeholder="请输入客户名称"/>
    </a-form-item>
  </a-form>
</template>

export default {
  data() {
    return {
      form: this.$form.createForm(this), // 只有这样注册后，才能通过表单拉取数据
    }
  }
}

```
通过`validateFields`的方法，能够校验必填项是否有值，若无，则页面会给出警告！
```
this.form.validateFields((err, values) => {
  if (err) {
    // 这里做逻辑处理
    console.log(values) // { name: '' }
  }
}
```
### 清空表单的方法
执行`this.form.resetFields()`，则会将表单清空。
### 给表单赋值
值得一提的是，`setFieldsValue`只有通过这种方式给表单赋值，拉取表单的时候才能拉取到值，其他设置默认值的方式，拉取表单时都无法获取到默认值。
```
 this.form.setFieldsValue({
   name: '设置值'
 })
 ```
 `components层`
 ```
 
 import {Form, Input, Icon, Select, Row, Col, Button, Modal, DatePicker, Radio, Tooltip} from 'antd';
 const FormItem = Form.Item;
 
 class SimilarQuestionModalForm extends Component {

    componentWillMount() {
        const { hotQuestionConfig } = this.props;
        let newList = [];
        try {
            if (hotQuestionConfig && hotQuestionConfig.length > 0) {
                newList = hotQuestionConfig
            }
        } catch (e) {
            console.log("similar question context error");
            console.log(e);
        }
        this.state = {
            similarQuestionList: newList,
        }
    }

    componentWillReceiveProps(nextProps, nextContext) {
        const { hotQuestionConfig } = nextProps;
        let newList = [];
        try {
            if (hotQuestionConfig && hotQuestionConfig.length > 0) {
                //newList = JSON.parse(similarQuestionConfigs);
                newList = hotQuestionConfig
            }
        } catch (error) {
            console.log("similar question context error")
            console.log(error)
        }

        this.setState({
            similarQuestionList: newList
        })
    }

    onModalOK = () => {
           this.props.updateSimilarQuestion();
    }



    render() {
        const {getFieldDecorator, getFieldValue} = this.props.form;
        const formItemLayout = {
            labelCol: {span: 5},
            wrapperCol: {span: 15}
        };
        return(
            <Modal
                title={intl('route_similarQuestionMng_add_button', true)}
                visible={this.props.modalVisible}
                style={{position: 'fixed', top: 0, right: 0}}
                onOk={this.onModalOK.bind(this)}
                onCancel={this.props.cancelUpdateSimilarQuestion}
            >
                <Form>
                    <FormItem {...formItemLayout} label={(
                        <span>
                          {'标题'}&nbsp;
                            <Tooltip title={intl('route_hotTopicsMng_column_description', true)}>
                            <Icon type="question-circle-o"/>
                          </Tooltip>
                        </span>
                    )}>
                        {getFieldDecorator('description', {
                            // validateTrigger: 'onBlur',
                            // rules: [
                            //     {required: true, message: ''},
                            //     {transform: val => val && val.trim()},
                            //     {max: 10, message: ''}
                            //     {validator: this._checkData,}
                            // ]
                        })(
                            <Input/>
                        )}

                    </FormItem>
                    <FormItem {...formItemLayout} label={(
                        <span>
                          {''}&nbsp;
                            <Tooltip title={intl('route_similarQuestionMng_column_hotTopicContext', true)}>
                            <Icon type="question-circle-o"/>
                          </Tooltip>
                        </span>
                    )}>
                        {getFieldDecorator('hotTopicContext', {
                            rules: [
                                {required: true, message: ''},
                            ]
                        })(
                            <Input/>
                        )}

                    </FormItem>
                    <FormItem {...formItemLayout} label={(
                        <span>
                          {intl('route_similarQuestionMng_column_channel', true)}&nbsp;
                            <Tooltip title={''}>
                            <Icon type="question-circle-o"/>
                          </Tooltip>
                        </span>
                    )}>
                        {getFieldDecorator('channel', {
                            rules: [
                                {required: true, message: ''},
                            ]
                        })(
                            <Input/>
                        )}

                    </FormItem>
                    <FormItem {...formItemLayout} label={(
                        <span>
                          {intl('route_similarQuestionMng_column_count', true)}&nbsp;
                            <Tooltip title={''}>
                            <Icon type="question-circle-o"/>
                          </Tooltip>
                        </span>
                    )}>
                        {getFieldDecorator('count', {
                            rules: [
                                {required: true, message: '')},
                            ]
                        })(
                            <Input/>
                        )}

                    </FormItem>
                </Form>
            </Modal>
        )
    }
}

const SimilarQuestionModal = Form.create({
    mapPropsToFields(props) {
        const {hotQuestionConfig} = props;
        return {
            description: {value: hotQuestionConfig && hotQuestionConfig.description || ''},
            hotTopicContext: {value: hotQuestionConfig && hotQuestionConfig.hotTopicContext || ''},
            channel: {value: hotQuestionConfig && hotQuestionConfig.channel || null},
            count: {value: hotQuestionConfig && hotQuestionConfig.count || null},
            id: {value: hotQuestionConfig && hotQuestionConfig.id || null},
        }
    }
})(SimilarQuestionModalForm);

export default SimilarQuestionModal
 ```
 `routes层引用`
 ```
 <SimilarQuestionModal/>
 ```
 

 
