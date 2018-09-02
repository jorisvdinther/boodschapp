<template>

  <div>
    <div class="header">
      <h1>BoodschApp</h1>
    </div>

    <div class="invoer">
      <form >
        <input class="nieuwProduct" v-model="newBoodschap.product" type="text" placeholder="Nieuw product" />
        <input class="aantalProduct" v-model="newBoodschap.aantal" type="text" placeholder="Aantal" />
        <v-btn v-on:click="addProduct">Toevoegen</v-btn>
      </form>
      <hr />
    </div>

    <div class="boodschappenlijst">
      <div class="lijstHeader">Boodschappenlijst</div>
      <div class="boodschap" v-for="boodschap in boodschappenSorted" :class="{afgestreept: boodschap.afgestreept}">
        <div  class="boodschap totaal" v-on:click="afstrepen(boodschap)">
          <div  class="lijstAantal">
            <input type="text" :class="{afgestreept: boodschap.afgestreept}" class="lijstAantal" v-model="boodschap.aantal" />
          </div>
          <div :class="{afgestreept: boodschap.afgestreept}" class="lijstProduct" >{{boodschap.product}}</div>
        </div>
        <v-btn class="btndelete" v-on:click="deleteProduct(boodschap)">
          <v-icon dark right>delete_outline</v-icon>
        </v-btn>
        <hr />
      </div>
     
    </div>
    <div class="bottom">
      <v-btn v-on:click="sortAantal()">Sorteer op #</v-btn>
        <v-btn v-on:click="sortProduct()">Sorteer op naam</v-btn>
    </div>
  </div>

</template>
<script>

  export default {
  name: 'boodschapp',

  data() {
  return{
  sort: 'product',
  sortOrder: 'asc',
  newBoodschap:{},
  boodschappen: [
    
  ]
  }
  },
  methods: {
  addProduct: function(e) {
  this.boodschappen.push({
  product: this.newBoodschap.product,
  aantal: this.newBoodschap.aantal,
  afgestreept: false
  });
  e.preventDefault();
  },
  deleteProduct: function(boodschap){
        this.boodschappen.splice(this.boodschappen.indexOf(boodschap), 1);
  },
  afstrepen: function(boodschap){

  if(boodschap.afgestreept == true){
  boodschap.afgestreept = false;
  }else{
  boodschap.afgestreept = true;
  }
  },
  sortAantal: function(){
  let sort = this.sort;
  let sortOrder = this.sortOrder;
  if(sort === 'aantal')
  {
  if(sortOrder === 'asc')
  {
  this.sortOrder = 'desc';
  }else{
  this.sortOrder = 'asc';
  }
  }
  this.sort = 'aantal';
  },
  sortProduct: function(){
  let sort = this.sort;
  let sortOrder = this.sortOrder;
  if(sort === 'product')
  {
  if(sortOrder === 'asc')
  {
  this.sortOrder = 'desc';
  }else{
  this.sortOrder = 'asc';
  }
  }
  this.sort = 'product';
  }
  },
  computed:{
  boodschappenSorted: function() {
  let sort = this.sort;
  let sortOrder = this.sortOrder;
  function compare(a, b) {
  if (a.afgestreept < b.afgestreept)
        return -1;
      if (a.afgestreept > b.afgestreept)
        return 1;
    if(sort === 'product')
      {
        if(sortOrder === 'asc')
        {
          if (a.product.toLowerCase() < b.product.toLowerCase())
            return -1;
          if (a.product.toLowerCase() > b.product.toLowerCase())
            return 1;
        }
        else{
          if (a.product.toLowerCase() > b.product.toLowerCase())
            return -1;
          if (a.product.toLowerCase() < b.product.toLowerCase())
            return 1;
          }
        }
    if(sort === 'aantal')
    {
      if(sortOrder === 'asc')
        {
          if (a.aantal < b.aantal)
                return -1;
          if (a.aantal > b.aantal)
            return 1;
        }
      else{
          if (a.aantal > b.aantal)
                return -1;
          if (a.aantal < b.aantal)
            return 1;
      }
      return 0;
    }
  }
    return this.boodschappen.sort(compare);
  }
  }
  }
</script>
<style scoped>
  .header{
  position: absolute;
  top: 0;
  left:0;
  height:5em;
  width: 100%;
  background: #7b7d7f;
  text-align:center;
  color:#ffffff;
  }
  .invoer{
  position:relative;
  top:2em;
  left:0;

  }
  .aantalProduct{
  width:3em;
  border:1px solid;
  height:2em;
  }
  .boodschappenlijst{
  position:relative;
  margin:auto;
  margin-top:2.5em;
  border: 1px solid #81a0d1;
  width: 80%;
  min-width:20em;
  max-width: 30em;
  }
  .lijstHeader{

  background:#81a0d1;
  }
  .boodschap{
  text-align: left;
  border:0;
  }
  .lijstProduct{
  postion: relative;
  margin-left: 1em;
  display: inline-block;
  border-left:0;
  }
  .lijstAantal{
  display: inline-block;
  margin-left:0.2em;
  width: 1.5em;
  border:0;

  }
  .afgestreept{
  background:#7b7d7f;
  text-decoration: line-through;

  }
  .btndelete{
  position:relative;
  display: inline-block;
  margin-right:0em;
  height: 1.8em;
  }
  .totaal{
  
  display:inline-block;
  height: 2em;
  width: calc(70% - 1.2em);
  border:1 px red solid;
  }
  .nieuwProduct{
  border: 1px solid;
  height:2em;
  }
</style>
