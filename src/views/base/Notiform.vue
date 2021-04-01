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
            selectOptions: [{}],
            selectOptions_id : null,
            isActive: 0,
            name: '',
            title: '',
            content: ''
        }
    },
    created () {
        axios.get("http://localhost:3000/userstatus").then(res => {
            console.log(res.data.data.length)
            for (var i = 0; i<res.data.data.length; i++) {
                this.selectOptions.push(res.data.data[i].id)
            }
            console.log(this.selectOptions)
        }).catch(err => {
            console.log(err)
        }),
        console.log(this.selectOptions)
    },
    methods: {
        handleSubmit () {
            this.submitted = false
            console.log(this.selectOptions_id)
            localStorage.setItem("id", JSON.stringify(this.selectOptions_id))
            axios.post("http://localhost:3000/addnoti", {
                name : this.name,
                title : this.title,
                content : this.content,
                selectOptions_id : this.selectOptions_id
            }).then(res => {
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