<template>
  <div>
    
    <b-container class="margin-top">
      <b-row>
        <b-col cols="2" lg="4"></b-col>

        <b-col cols="8" lg="4"> 
          <PiePos />
        </b-col>
        <b-col cols="2"></b-col>

      </b-row>
    </b-container>

   <b-container class="margin-top">
      <b-row>
        <b-col cols="2" style="text-align: right; margin-left:20px"> 
          <b-button variant="info" @click="Bar">Bar</b-button>          
        </b-col>
       <b-col cols="3" style="text-align: left;"> 
          <b-button variant="info" @click="Wc">WordCloud</b-button>
        </b-col>
        <b-col></b-col>
      </b-row>
    </b-container>

    <b-container class="margin-top">
      <div class="row">
      <div class="margin-top col-lg-6">
          <b-card class="card">
            <BarNounPos v-if="bar"/>
            <WcNoun v-if="wc"/>
          </b-card>
      </div>

      <div class="margin-top col-lg-6">
          <b-card class="card">
            <BarVerbPos v-if="bar"/>
            <WcVerb v-if="wc"/>
          </b-card>
        </div>

        <div class="w-100"></div>

      <div class="margin-top col-lg-6">
          <b-card class="card">
            <BarAdjPos v-if="bar" />
             <WcAdj v-if="wc"/>
          </b-card>
        </div>

      <div class="margin-top col-lg-6">
          <b-card class="card">
            <BarAdvPos v-if="bar"/>
            <WcAdv v-if="wc"/>
          </b-card>
        </div>
     </div>
    </b-container>
  </div>
</template>
<script>

import PiePos from "@/components/commonpage/PiePos";
import BarNounPos from "@/components/commonpage/BarNounPos";
import BarVerbPos from "@/components/commonpage/BarVerbPos";
import BarAdjPos from "@/components/commonpage/BarAdjPos";
import BarAdvPos from "@/components/commonpage/BarAdvPos";

import WcNoun from "@/components/commonpage/WcNoun";
import WcVerb from "@/components/commonpage/WcVerb";
import WcAdv from "@/components/commonpage/WcAdv";
import WcAdj from "@/components/commonpage/WcAdj";
export default {
    data:()=>({
        bar : true,
        wc : false

    }) ,
    methods:{
        Wc(){
            this.bar = false;
            this.wc = true
            
        },
           Bar(){
            this.bar = true;
            this.wc = false
            
        }
    }
    ,
  components: {
   
    PiePos,

    BarNounPos,
    BarVerbPos,
    BarAdjPos,
    BarAdvPos,
    WcNoun,
    WcVerb,
    WcAdv,
    WcAdj
  },
};
</script>
<style  scoped>
.margin-top {
  margin-top: 20px;
}
.card {
  background-color: white;
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  border-radius: 20px;
}
</style>