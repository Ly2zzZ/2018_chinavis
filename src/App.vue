 <template>
  <div id="app">
    <div id="main_view">
      <my_main  @nodeselect="nodeselect"></my_main>
    </div>
    <div id="wordcloud">
      <wordcloud ref="wordcloud"></wordcloud>
    </div>
    <div id="Inf_view1">
        <punch ref="punch"></punch>  
    </div>
    <div id="timeline">
      <pxzb ref="pxzb"></pxzb>
    </div>
  </div>
</template>

<script>
/*  import * as d3 from 'd3v4'*/

  import timeline from './components/timeline'
  import my_main from './components/main'
  import wordcloud from './components/wordcloud'
  import punch from './components/punch'
  import pxzb from './components/pxzb'

  export default {
    name: 'App',
    data(){
      return {

      }
    },
    components:{
      timeline,
      "my_main":my_main,
      wordcloud,
      punch,
      pxzb
    },
    methods:{
      nodeselect(node){
        this.$refs.wordcloud.drawwordcloud(node) 
        this.$refs.punch.drawpunch(node) 
        this.$refs.pxzb.drawpxzb(node) 
      }
    },
    beforeCreate(){
/*    document.body.style.cursor="wait";
      this.$ajax.get('/api/getArticles')
      .then((response)=>{
        console.log(response)
      document.body.style.cursor="pointer";
      })
      .catch(function (error) {
        console.log(error);
      });*/
    },
    mounted(){
          var that=this;
          d3.json("../../static/Email_person/Email_person.json",function(email){
            that.$store.dispatch('getEmail_personAction',email);
          })
        d3.json("../../static/Check_person/Check_person.json",function(check){
             that.$store.dispatch('Check_person_personAction',check);
          })
        d3.json("../static/Web_depart.json",function(Web_depart){
             that.$store.dispatch('Web_person_personAction',Web_depart);
          })
    }
  }
</script>

<style>
body{
  background-color: #303243;
}
*{
  margin: 0px;
  padding: 0px;
}
#app{
/*  width: 1688px;
height: 1000px;*/
width: 99%;
height: 800px;
}
#main_view{
  box-sizing: border-box;
  width: 40%;
  height: 70%;
  border: 1px solid  #9A2EFE;
  float:left;
}
#Inf_view1{
  box-sizing: border-box;
  width: 30%;
  height: 70%;
  border: 1px solid  #9A2EFE;
  float:right;
}

#wordcloud{
  box-sizing: border-box;
  width: 30%;
  height: 70%;
  border: 1px solid  #9A2EFE;
  float:left;
}

#timeline{
  box-sizing: border-box;
  clear:both;
  width: 100%;
  height: 45%;
  border: 1px solid  #9A2EFE;
}
</style>