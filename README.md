# AntDesign

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
