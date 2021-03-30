<template>
  <CRow>
    <CCol col>
      <CCard>
        <CCardHeader>
          <h1>Hello world</h1>
        </CCardHeader>
      </CCard>
    </CCol>
  </CRow>
</template>

<script>
export default {
  name: 'Helloworld'
}
</script>

<style>
  .breadcrumb-item + .font-xl.breadcrumb-item::before {
    color: rgb(140, 195, 38);
    content: '>>';
    padding: 0px 10px;

  }
</style>
