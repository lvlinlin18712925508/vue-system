<template>
    <div>
      <a-form layout="horizontal" :form='form'>
        <a-form-item
          label="付款账户"
          :label-col="formItemLayout.labelCol"
          :wrapper-col="formItemLayout.wrapperCol"
        >
          <a-input v-decorator="['payAccount', {
            initialValue: step.payAccount, rules: [{required: true, message: '请输入支付账号'}]
          }]" placeholder="请输入支付账号"></a-input>
        </a-form-item>
        <a-form-item>
          <a-button type="primary" @click="handleSubmit"></a-button>
        </a-form-item>
      </a-form>
    </div>
</template>

<script>
    export default {
      name: "Step1",
      data() {
        this.form = this.$form.createForm(this)
        return {
          formItemLayout: {
            labelCol: {span: 4},
            wrapperCol: {span: 14}
          }
        }
      },
      computed: {
        step() {
          console.log('11', this.$store)
          return this.$store.state.form.step;
        }
      },
      methods: {
        handleSubmit() {
          const {form, $router, $store} = this;
          form.validateField((err,values) => {
            if(!err) {
              $store.commit({
                type: 'form/saveStepFormData',
                payload: values,
              })
              $router.push('/form/step-form/confirm')
            }
          })
        }
      }
    }
</script>

<style scoped>

</style>
