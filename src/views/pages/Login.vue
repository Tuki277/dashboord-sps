<template>
  <div v-if=" this.a === null">
    <div class="c-app flex-row align-items-center">
      <CContainer>
        <CRow class="justify-content-center">
          <CCol md="8">
            <CCardGroup>
              <CCard class="p-4">
                <CCardBody>
                  <CForm @submit.prevent="handleSubmit">
                    <h1>Login</h1>
                    <p class="text-muted">Sign In to your account</p>
                    <CInput
                      placeholder="Username"
                      autocomplete="username email"
                      v-model="username"
                    >
                      <template #prepend-content><CIcon name="cil-user"/></template>
                    </CInput>
                    <CInput
                      placeholder="Password"
                      type="password"
                      autocomplete="curent-password"
                      v-model="password"
                    >
                      <template #prepend-content><CIcon name="cil-lock-locked"/></template>
                    </CInput>
                    <CRow>
                      <CCol col="6" class="text-left">
                        <CButton type="submit" color="primary" class="px-4">Login</CButton>
                      </CCol>
                      <CCol col="6" class="text-right">
                        <CButton color="link" class="px-0">Forgot password?</CButton>
                        <CButton color="link" class="d-lg-none">Register now!</CButton>
                      </CCol>
                    </CRow>
                  </CForm>
                </CCardBody>
              </CCard>
              <CCard
                color="primary"
                text-color="white"
                class="text-center py-5 d-md-down-none"
                body-wrapper
              >
                <CCardBody>
                  <h2>Sign up</h2>
                  <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.</p>
                  <CButton
                    color="light"
                    variant="outline"
                    size="lg"
                  >
                    Register Now!
                  </CButton>
                </CCardBody>
              </CCard>
            </CCardGroup>
          </CCol>
        </CRow>
      </CContainer>
    </div>
  </div>
  <div v-else-if=" this.a !== null">
    <CContainer>
        <CRow class="justify-content-center">
          <CCol md="8">
            <CCardGroup>
              <CCard class="p-4">
                <CCardBody>
                  <h1>Ban da login, hay dang xuat de dang nhap lai</h1>
                </CCardBody>
              </CCard>
              
            </CCardGroup>
          </CCol>
        </CRow>
      </CContainer>
  </div>
</template>

<script>

import axios from 'axios'

export default {
  name: 'Login',
  data () {
    return {
      username : '',
      password : '',
      a : ''
    }
  },
  created () {
    const checkID = localStorage.getItem('id')
    this.a = checkID
  },
  methods: {
        handleSubmit () {
            this.submitted = false
            axios.post('http://localhost:3000/getlogin', {
              username : this.username,
              password: this.password
            }).then((res) => {
              if (res) {
                localStorage.setItem('Token', res.data.token)
                localStorage.setItem('id', res.data.rows[0].id)
                localStorage.setItem('username', res.data.rows[0].account)
                this.$router.push('/')
              } else {
                alert("login fail")
              }
            }).catch((err) => {
              console.log({ err })
            })
        }
    }
}
</script>
