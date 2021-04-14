<template>
  <CCard>
        <CCardHeader>
        <strong>Normal</strong> Form
        </CCardHeader>
            <CForm novalidate @submit.prevent="handleSubmit">
                    <CCardBody>
                        <CInput
                        label="Title"
                        type="text"
                        placeholder="Enter title"
                        required
                        was-validated
                        v-model="title"
                        />
                        <CInput
                        type="text"
                        label="Name"
                        placeholder="Enter Name"
                        required
                        was-validated
                        v-model="name"
                        />
                        <label>Content</label>
                        <CTextarea
                        placeholder="Content here"
                        horizontal
                        rows="9"
                        v-model="content"
                        />
                        <CSelect
                            type="checkbox"
                            horizontal
                            :options="selectOptions"
                            :value.sync="selectOptions_id"
                            placeholder="Please select"
                        />
                    </CCardBody>
                    <CCardFooter>
                        <CButton type="submit" size="sm" color="primary"><CIcon name="cil-check-circle"/> Submit</CButton>
                        <CButton type="reset" size="sm" color="danger"><CIcon name="cil-ban"/> Reset</CButton>
                    </CCardFooter>
                </CForm>
            </CCard>
</template>

<script>

import axios from 'axios'

export default {
    name: 'Normalform',
    data () {
        return {
            selectOptions: [],
            selectOptions_id : null,
            isActive: 0,
            name: '',
            title: '',
            content: '',
            token: ''
        }
    },
    created () {
        axios.get("http://localhost:3000/getall").then(res => {
            if ( res.data.data.length > 0) {
                for ( var i = 0; i < res.data.data.length; i++) {
                    this.selectOptions.push({
                        value:  res.data.data[i].id,
                        label: res.data.data[i].account
                    })
                }
            }
        }).catch(err => {
            console.log(err)
        }),
        console.log(this.selectOptions)
    },
    methods: {
        handleSubmit () {
            this.submitted = false
            let token = "Bearer " + localStorage.getItem('Token')
            let config = {
                headers: {
                    Authorization: token
                }
            }
            axios.post("http://localhost:3000/addnoti", {
                name : this.name,
                title : this.title,
                content : this.content,
                id_user : this.selectOptions_id
            }, config).then(res => {
                this.$router.push('/')
            }).catch(err => {
                console.log(err)
            })
        }
    }
}
</script>

<style>

</style>