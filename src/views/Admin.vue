<template>
  <v-container>
    <div class="admin">
      <h1>Phishing test statuses</h1>
    </div>
    <div></div>
    <v-data-table
        :headers="headers"
        :items="items"
        :items-per-page="20"
        class="elevation-1 mt-6"
        :loading="items.length===0"
    ></v-data-table>
  </v-container>

</template>
<script>
export default {
  name: 'Admin',
  data:()=> ({
    headers: [
        {text: 'Email', align: 'start', sortable: true, value:'email'},
        {text: 'Status',  value:'status'}
      ],
    items:[]

  }),
  mounted() {
    this.items = this.getData()
  },
  methods:{
    getData(){
      return [
        {email: 'a@cy.com', status:'opened'},
        {email: 'b@cy.com', status:'received'}
      ]
    }
  }

}
</script>
