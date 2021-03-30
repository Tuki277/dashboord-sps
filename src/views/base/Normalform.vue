<template>
  <CCard>
        <CCardHeader>
        <strong>Normal</strong> Form
        </CCardHeader>
            <CForm novalidate @submit.prevent="handleSubmit">
                    <CCardBody>
                        <CInput
                        label="Name"
                        type="text"
                        placeholder="Enter Name"
                        required
                        was-validated
                        v-model="name"
                        />
                        <CInput
                        type="text"
                        label="Address"
                        placeholder="Enter your address"
                        required
                        was-validated
                        v-model="address"
                        />
                        <CInput
                        type="text"
                        label="Phone number"
                        placeholder="Enter your phone number"
                        required
                        was-validated
                        v-model="phone"
                        />
                        <CInput
                        type="email"
                        description="Please enter your email."
                        autocomplete="email"
                        label="Email"
                        placeholder="Enter Email..."
                        required
                        was-validated
                        v-model="email"
                        />
                        <label>Sex</label>
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
export default {
    name: 'Normalform',
    data () {
        return {
            selectOptions: [
                { value: 1, label: 'nam'},
                { value: 2, label: 'nu'},
                { value: 3, label: 'bede'}
            ],
            selectOptions_id : null,
            name: '',
            address: '',
            phone: '',
            email: '',
            submitted: false
        }
    },
    methods: {
        handleSubmit () {
            this.submitted = false
            console.log(this.name)
            console.log(this.address)
            console.log(this.phone)
            console.log(this.email)
            console.log(this.selectOptions_id)
        }
    }
}
</script>

<style>

</style>