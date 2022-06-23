<template>
  <!--
    0: 有理数加法
    1: 有理数减法
    2: 有理数乘法
    3: 有理数除法
    4: 有理数加减乘除混合
  -->
  <div class="form">
    <el-form :model="form" :inline="true">
      <el-form-item label="id">
        <el-select v-model="form.id" placeholder="id">
          <el-option label="有理数加法" value="0" />
          <el-option label="有理数减法" value="1" />
          <el-option label="有理数乘法" value="2" />
          <el-option label="有理数除法" value="3" />
          <el-option label="有理数加减乘除混合" value="4" />
        </el-select>
      </el-form-item>

      <el-input v-model="form.maxNumber" placeholder="最大值" />
      <el-input v-model="form.number" placeholder="数量" />

      <el-form-item>
        <el-button type="primary" @click="onSubmit">Create</el-button>
        <el-button @click="onClear">clear</el-button>
      </el-form-item>
    </el-form>
  </div>

  <p v-for="item in result" :key="item">{{ item }}</p>
</template>

<script setup>
import { reactive, ref } from 'vue'

// do not use same name with ref
const form = reactive({
  id: '0',
  maxNumber: 100,
  number: ''
})

const result = ref([])

const onSubmit = () => {
  for (let index = 0; index < form.number; index++) {
    let x = Math.floor(Math.random() * form.maxNumber) + 1
    let y = Math.floor(Math.random() * form.maxNumber) + 1

    const upper = Math.floor(Math.random() * 2)
    const under = Math.floor(Math.random() * 2)

    if (upper === 0) {
      x = '(-' + x + ')'
    }

    if (under === 0) {
      y = '(-' + y + ')'
    }

    const arr = ['+', '-', '×', '÷']

    // if (form.id === '0') {
    //   temp = x + '+' + y
    // } else if (form.id === '1') {
    //   temp = x + '-' + y
    // } else if (form.id === '2') {
    //   temp = x + '*' + y
    // } else if (form.id === '3') {
    //   temp = x + '/' + y
    // } else if (form.id === '4') {
    //   temp = x + '-' + y
    // }

    result.value.push(x + arr[form.id] + y)
  }
}

const onClear = () => {
  result.value = []
}
</script>

<style lang="less" scoped>
.form {
  width: 30vw;
  margin: 0 auto;
}

p {
  text-align: center;
}

@media screen and (max-width: 1200px) {
  .form {
    width: 70vw !important;
  }
}
</style>
