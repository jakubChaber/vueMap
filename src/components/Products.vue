
<template>
   <div class="row"><div class="col">wojewódźtwo {{selectedVoyewodship}} </div></div>
   <div class="row">
    <div class="col" v-for="prod in products"  v-bind:key="prod">
    <div>{{prod.name}} -- {{prod.imgUrl}}</div>
    <button v-on:click="chooseProd(prod.name)">click</button>
    </div>
  </div>
</template>

<script>
import prods from './products.json'
export default {
  name: 'Products',
  props: {
    placeId: String
  },
  watch: { 
    placeId: function() { 

      for(let key in prods.products){
        let tmpArr = prods.products[key];
        
        if(tmpArr.id == this.placeId){
          this.selectedVoyewodship = tmpArr.name;
          this.products = tmpArr.products;
        }
      }
    }
  },
  data(){
    return{
      data: prods,
      selectedVoyewodship:'',
      products:[]
    }
  },
  methods:{
    chooseProd(ev){
      this.$emit('product', ev);
    }
  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.pictures > div{
  height:190px;
  min-width: 180px;
  overflow: hidden;
  background-size:80%;
  background-repeat:no-repeat;
  background-position:center;
  position:relative;
  margin:0 .5rem;
}

.pictures{
  display:flex;

  flex-flow:row;
  flex-wrap:nowrap;
  align-items: stretch;
  transition:.2s ease-in-out;
}
.screen{
  height: calc( 100% - 24px );
  background-size: 90%;
  background-position:  center ;
  background-repeat: no-repeat;
 
}
.pic footer{
  background-color: #fd0e0eeb;
  color: #ffecb0;
  font-size: 13px;
  height:24px;
  display:flex;
  align-items:center;
  position:relative;
  padding-left:.5rem;
}
.pic footer::after{
  content:'';
  position: absolute;
  bottom: 0;
  right: 0;
  width: 24px;
  height: 24px;
  background: url(/img/arrow.svg) no-repeat 0 #000;
  background-size: 15px 13px;
  background-position: 50%;
}

.control{
  position:absolute;
  top:50%;
  background: #fff;
  border: 1px solid #dee1e6;
  border-left-color: rgb(222, 225, 230);
  border-left-style: solid;
  border-left-width: 1px;
  cursor: pointer;
  display: block;
  height: 67px;
  opacity: 1;
  position: absolute;
  transition: all .3s linear;
  top: 50%;
  width: 41px;
  transform: translateY(-50%);
  margin: 0;
}
.arrowLeft{
  left:0;
  border-left: 0;
  border-radius: 0 3px 3px 0;
  left: -1px;
  opacity: 1;
}
.arrowRight{
  border-radius: 0 3px 3px 0;
  left: unset;
  right:-1px;
  opacity: 1;
}
header{
  font-weight: 400;
  color: #000;
  font-size: 24px;
  padding: 13px 0 13px 20px;
}

</style>



