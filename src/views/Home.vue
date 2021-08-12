<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <a-form layout="horizontal" style="width: 600px; margin: 0 auto;">
      <a-form-item label="用户名">
        <a-input v-model:value="userName" placeholder="请输入用户名" />
      </a-form-item>
      <a-form-item label="密码">
        <a-input v-model:value="password" placeholder="请输入密码" />
      </a-form-item>
      <a-form-item>
        <a-button type="primary" @click="onSubmit">登录</a-button>
      </a-form-item>
    </a-form>
  </div>
</template>

<script lang="ts">
import axios from 'axios'
import { defineComponent, reactive, toRefs } from 'vue'
import { Button, Form, Input } from 'ant-design-vue'

interface FormState {
  userName: string,
  password: string
}

export default defineComponent({
  components: {
    [Button.name]: Button,
    [Form.name]: Form,
    [Form.Item.name]: Form.Item,
    [Input.name]: Input
  },
  setup () {
    const formState: FormState = reactive({
      userName: 'admin',
      password: '123456'
    })
    const onSubmit = () => {
      axios.request({
        url: '/api/login',
        params: formState
      }).then(res => {
        console.log(res.data, 'res----')
      })
    }
    return {
      ...toRefs(formState),
      onSubmit
    }
  }
})
</script>
