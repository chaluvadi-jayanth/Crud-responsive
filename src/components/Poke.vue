<template>



    <div class='table-container'>
    <h1 class="heading">Pokemon</h1>
    <div class='input-group input'> 
   <input id='name' type="text" autofocus placeholder="Name"> &nbsp;&nbsp;&nbsp;
  <input id='url' type="text" placeholder="Url">&nbsp;&nbsp;
  <button @click='add' class="btn btn-primary">Add</button>
  
</div>
    <table class='table'>
        <thead>
            <tr>
                <th>Name</th>
                <th>Url</th>
                <th>Actions</th>
                
            </tr>
        </thead>
        <tbody>
            <tr :key='poke.name' v-for='(poke,index) in pokemonarray'>
                <td  data-labe="Name" class='Bold' v-if="poke.editing"><input type="text" v-model='name'></td>
                <td v-else data-labe="Name">{{poke.name}}</td>
                <td  data-labe="Url" class='Bold' v-if="poke.editing"><input type="text" v-model='url'></td>
                <td v-else data-labe="Url">{{poke.url}}</td>
                <td data-labe="Actions"> <a href="#" style='background-color:#007bff' class='btn' @click="updatePoke(poke)">{{ poke.editing ? 'Update':'Edit'}}</a> <a href="#" @click="del(index)" class='btn'>Delete</a> </td>
                
            </tr>
        </tbody>
    </table>
</div>

</template>

<script>
import {mapGetters} from 'vuex'

export default {
  data(){
    return{
     name:'',
     url:''
      // editing: false
    }
  },

methods:{
  updatePoke(poke) {
    
    poke.editing=!poke.editing
      console.log(poke.editing)
        // this.editing = this.editing == true ? false : true;
      if (!poke.editing) {
        console.log(poke.editing)
        if (this.name)
        {
          poke.name=this.name
          this.name=''
        }
        if (this.url)
        {
          poke.url=this.url
          this.url=''
        }
        
      } 
    },

del(index){
  console.log(index)
this.$store.commit('deletepoke',index)
},
add(){
   let name=document.querySelector('#name').value
   let url=document.querySelector('#url').value
   this.pokemonarray.unshift({
     name,
     url
   })
   document.querySelector('#name').value=''
   document.querySelector('#url').value=''
  }
},
//with the help of getters we are accessing the state data,we can also
//acess the state data directly.
computed: mapGetters(['pokemonarray']),
 //Calls the poke function in actions when vue is created. 
  created(){
    console.log("created")
    this.$store.dispatch('poke')
  }

}
</script>


<style>
*{
            margin:0;
            padding:0;
            box-sizing:border-box;
        }
        body{
            background-color: #32312f;
            font-family: sans-serif;
        }
.table-container{
    padding:0 10%;
    margin: 40px auto 0;
}
.heading{
    font-size: 40px;
    text-align: center;
    /* color:#f1f1f1; */
    margin-bottom: 40px;
}
.table{
    width:100%;
    border-collapse: collapse;
}
.table thead{
    background-color:#1aff1a;
}
.table thead tr th {
    font-size:14px;
    font-weight: 600;
    letter-spacing: 0.35px;
    color:#FFFFFF;
    opacity:1;
    padding:12px;
    vertical-align: top;
    border:1px solid #dee2e685;
}
.table tbody tr td{
font-size: 14px;
letter-spacing: 0.35px;
font-weight: normal;
color:#f1f1f1;
background-color: #595959;
padding:8px;
text-align: center;
border:1px solid #dee2e685;
overflow: hidden;
}
.table tbody tr td .btn{
    width:130px;
    text-decoration: none;
    line-height: 35px;
    display: inline-block;
    background-color: #FF1046;
    font-weight: medium;
    color:#FFFFFF;
    text-align:center;
    vertical-align: middle;
    /* user-select:none; */
    border:1px solid transparent;
    font-size:14px;
    opacity:1;
}
@media (max-width:768px){
   td input{
width:100px;
    }
    .table thead{
        display: none;

    }
    .table, .table tbody,.table tr,.table td{
        display: block;
        width:100%;

    }
.table tr{
    margin-bottom: 15px;
}
.table tbody tr td .btn{
    width:100px;
    height:40px;
    text-align: center;
}
.table tbody tr td{
    text-align: right;
    padding-left:50%;
    position: relative;
    min-height:50px;
}
.table td:before{
    content:attr(data-labe);
    position: absolute;
    left:0;
    width:50%;
    padding-left:15px;
    font-weight: 600;
    font-size: 14px;
    text-align:left;
}
}

</style>