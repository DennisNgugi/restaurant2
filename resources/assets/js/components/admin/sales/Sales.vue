<template lang="html">

<div>

  <div class="table-responsive">
  <table class="table table-hover table-striped">
    <thead>
      <tr>
        <th>#</th>
        <th>Date</th>
        <th>Ref</th>
          <th>Served by</th>
          <th>Total items</th>
          <th>Total Price</th>
          <th>Action</th>

      </tr>
    </thead>
    <tbody>

      <tr v-for="(p,index) in posts" @key="index">
        <td>{{index+1}}</td>
        <td>{{p.created_at | date}}</td>
        <td>{{p.reference_code}}</td>
        <td>{{p.waiters_name | capitalize}}</td>
        <td>{{p.total_quantity}}</td>
        <td>Ksh. {{p.grand_total}}</td>
        <td><router-link :to="{name: 'sales_view', params: { id: p.id }}" class="btn btn-info btn-sm">View</router-link></td>

      <!-- <td>{{p.waiters_name}}</td> -->
        <!-- <td>{{p.checkout_total}}</td>
        <!-- <td>{{p.quantity}} </td> -->


      </tr>
      <!-- <pagination :data="posts" @pagination-change-page="getResults"></pagination> -->
    </tbody>
  </table>
  </div>
</div>
</template>


<script>
export default {

    data() {
        return {
            posts: {},

        }
    },

    mounted: function() {
        // this.getResults();
        this.fetchData();
    },
    methods: {
        fetchData: function() {
            console.log('Fetching data....');

            this.axios.get('/api/checkout').then((response) => {
                //  console.log(response.data);
                this.posts = response.data;
            }).catch((error) => {
                console.log(error);
            })
        },
    //     getResults(page = 1) {
    //         this.axios.get('/api/checkout?page=' + page)
    //             .then(response => {
    //                 this.posts = response.data;
    //             });
    //     }
   },


}
</script>

<style lang="css" scoped>
</style>
