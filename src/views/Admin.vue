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
      const users = []
      fetch('http://localhost:3000/list')
          .then(res => {
            if (res.status ===200){
              const data = res.json()
              data.then(response => {
                console.log('response: ', response)
                response['statusList'].forEach(item => users.push({email: item['userId'], status:'link clicked'}))
              }).catch(err => console.log('not valid: ',err))
            }
          })
      return users

    }
  }

}
</script>
