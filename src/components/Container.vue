<template>
 <div class="container">
      <div class="row" >
        <div class="col-lg-6 col-md-8 col-sm-12" v-for="(item, index) in setData" :key="index">
          <div class="card">
            <div class="card-body">
              <h5 class="card-title">{{item.title}}</h5>
              <h6 class="card-subtitle mb-2 text-muted">{{item.date.day}}.{{item.date.month}}.{{item.date.year}}</h6>
              <p class="card-text">
                {{item.text}}
              </p>
            </div>
          </div>
        </div>
      </div>
    </div>
    
</template>

<script>

import NewItem from './NewItem.vue';
export default {
  props:['setData'],
components:{
  NewItem,
}
}
</script>

<style scoped>
.card-title{
  
  font-weight: 700;
  margin-bottom: 20px;
}
</style>

