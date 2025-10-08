<template>
  <q-page class="q-pa-md">

    <q-form
      ref="basicForm"
      @submit="onSubmit"
      @reset="onReset"
      class="q-gutter-md"
    >
      <!-- ชื่อ -->
      <q-input
        v-model="form.name"
        label="Name"
        outlined
        :rules="[
          val => !!val || 'Name is required',
          val => val.length >= 3 || 'Name must be at least 3 chars'
        ]"
      />

      <!-- อีเมล -->
      <q-input
        v-model="form.email"
        label="Email"
        outlined
        :rules="[
          val => !!val || 'Email is required',
          val => /.+@.+\..+/.test(val) || 'Email must be valid'
        ]"
      />

      <!-- รหัสผ่าน -->
      <q-input
        v-model="form.password"
        label="Password"
        type="password"
        outlined
        :rules="[
          val => !!val || 'Password is required',
          val => val.length >= 6 || 'Password must be ≥ 6 chars'
        ]"
      />

      <div class="row q-gutter-sm">
        <q-btn label="Submit" type="submit" color="primary" />
        <q-btn label="Reset" type="reset" color="secondary" flat />
      </div>
    </q-form>

  </q-page>
</template>

<script setup>
import { ref } from 'vue'

const basicForm = ref(null)

const form = ref({
  name: '',
  email: '',
  password: ''
})

function onSubmit () {
  // ฟอร์ม validate สำเร็จแล้ว
  // basicForm.value.validate() ถูกเรียกอัตโนมัติก่อนเข้ามา onSubmit
  console.log('Submit form:', form.value)
  // คุณอาจส่งค่าขึ้น server หรือแสดงข้อความสำเร็จ
}

function onReset () {
  // รีเซ็ตค่าฟอร์ม
  form.value.name = ''
  form.value.email = ''
  form.value.password = ''

  // รีเซ็ต validation (ซ่อน error)
  basicForm.value.resetValidation()
}
</script>

<style scoped>
/* ถ้าต้องการตกแต่งเพิ่มเติม */
</style>
