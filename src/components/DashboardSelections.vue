<template>
    <div class="selections">
        <p class="select_country">{{ $t("home.wemast_select_region") }}</p>
        <!-- <select name="" id="region_selection">
            <option value=""></option>
        </select> -->
        <div id="region_selection" v-if="region_selection">
          <CustomSelect2
       />
        </div>
       

      

        <p  class="select_cause">{{ $t("home.wemast_select_indicator") }}</p>
        <div id="cause_selection"  @click="clickedMe">
          <CustomSelectIndicator />
        </div>

        <p class="select_sub-indicator" v-if="storeUserSelections.selected_indicator !='Basin Vulnerability Index'">{{ $t("home.wemast_select_subindicator") }}</p>
        <div class="sub_indicator_selection" v-if="storeUserSelections.selected_indicator !='Basin Vulnerability Index'">
            <CustomSelectSubIndicator />
        </div>

        <p  v-if="storeUserSelections.selected_sub_indicator !== 'Undulation'" :class="{'select_year2':(storeUserSelections.selected_sub_indicator === 'Water Quality' ||
        storeUserSelections.selected_sub_indicator === 'Wetland Inventory' || storeUserSelections.selected_sub_indicator === 'Vegetation Cover'), 
        'select_year3':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status' ),
         'select_year':(storeUserSelections.selected_sub_indicator !== 'Water Quality')} ">{{ $t("home.wemast_select_year") }}</p>
        <div v-if="storeUserSelections.selected_sub_indicator !== 'Undulation'" :class="{'year_selection2':(storeUserSelections.selected_sub_indicator === 'Water Quality' ||
        storeUserSelections.selected_sub_indicator === 'Wetland Inventory' || storeUserSelections.selected_sub_indicator === 'Vegetation Cover'),
        'year_selection3':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status' ), 
     
         'year_selection':(storeUserSelections.selected_sub_indicator !== 'Water Quality')}  ">
            <CustomSelectYear />
        </div>

        <p :class="{'select_season_satellite ':storeUserSelections.selected_sub_indicator === 'Vegetation Cover', 
        'select_year2':(storeUserSelections.selected_sub_indicator === 'Precipitation Index' 
        // || storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'
        || storeUserSelections.selected_sub_indicator === 'Soil Moisure Index' ), 
        'season_status':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status'),
        'satellite_none':(storeUserSelections.selected_sub_indicator === 'Land Cover'),
        'satellite_none':(storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'),
       
        'bvi_label':(storeUserSelections.selected_indicator ==='Basin Vulnerability Index')
        
        }" 
        v-if="storeUserSelections.selected_sub_indicator === 'Precipitation Index' 
        // || storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'
         || storeUserSelections.selected_sub_indicator === 'Vegetation Cover' 
         || storeUserSelections.selected_sub_indicator === 'Soil Moisure Index'
        || storeUserSelections.selected_parameter === 'Wetland Status'
        || storeUserSelections.selected_indicator ==='Basin Vulnerability Index' ">{{ $t("home.wemast_select_season") }}</p>

        <div :class="{'season_satellite_selection ':storeUserSelections.selected_sub_indicator === 'Vegetation Cover', 
        'year_selection2':(storeUserSelections.selected_sub_indicator === 'Precipitation Index'
        //  || storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'
         || storeUserSelections.selected_sub_indicator === 'Soil Moisure Index'),
        'season_status_selection':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status'),
        'bvi_select':(storeUserSelections.selected_indicator ==='Basin Vulnerability Index'),
        'satellite_none':(storeUserSelections.selected_sub_indicator === 'Land Cover'),
        'satellite_none':(storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'),}" 
          v-if="storeUserSelections.selected_sub_indicator === 'Precipitation Index' 
          // || storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'
          || storeUserSelections.selected_sub_indicator === 'Soil Moisure Index'
          || storeUserSelections.selected_sub_indicator === 'Vegetation Cover' 
          || storeUserSelections.selected_parameter === 'Wetland Status'
          || storeUserSelections.selected_indicator ==='Basin Vulnerability Index'">
          <CustomSelectSeason />
        </div>


        <p class="select_parameter" 
        :class="{'satellite_none':(storeUserSelections.selected_indicator ==='Basin Vulnerability Index')}"
        v-if="storeUserSelections.selected_sub_indicator === 'Water Quality' ||
        storeUserSelections.selected_sub_indicator === 'Wetland Inventory'">{{ $t("home.wemast_select_parameter") }}</p>
        <div id="parameter_selection"
        :class="{'satellite_none':(storeUserSelections.selected_indicator ==='Basin Vulnerability Index')}"
         v-if="storeUserSelections.selected_sub_indicator === 'Water Quality' || storeUserSelections.selected_sub_indicator === 'Wetland Inventory'">
          <CustomSelectParameter />
        </div>

        <p :class="{'select_year':(storeUserSelections.selected_sub_indicator === 'Vegetation Cover'),
          'satellite_none':(storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'),
         'select_year2':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status'),
         'satellite_none':(storeUserSelections.selected_sub_indicator === 'Land Cover' ),
       
         'satellite_none':(storeUserSelections.selected_indicator ==='Basin Vulnerability Index' || storeUserSelections.selected_sub_indicator ==='Undulation'),

         'satellite_none':(storeUserSelections.selected_sub_indicator === 'Precipitation Index' || storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS')}"
         v-if="storeUserSelections.selected_sub_indicator === 'Vegetation Cover' || storeUserSelections.selected_parameter === 'Wetland Status' ">{{ $t("home.wemast_select_satellite") }}</p>
        <div :class="{'year_selection':(storeUserSelections.selected_sub_indicator === 'Vegetation Cover'), 
         'satellite_none':(storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS'),
        'year_selection2':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status'),
        'satellite_none':(storeUserSelections.selected_sub_indicator === 'Land Cover' ),
       
        'satellite_none':(storeUserSelections.selected_indicator ==='Basin Vulnerability Index' ||storeUserSelections.selected_sub_indicator ==='Undulation'),
        'satellite_none':(storeUserSelections.selected_indicator ==='Undulation'),

        'satellite_none':(storeUserSelections.selected_sub_indicator === 'Precipitation Index' ||storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS' )}" 
        v-if="storeUserSelections.selected_sub_indicator === 'Vegetation Cover' || storeUserSelections.selected_parameter === 'Wetland Status' ">
            <CustomSelectSatellite />
        </div> 
        



        <button id="request_layers" :class="{'request':(storeUserSelections.selected_sub_indicator === 'Precipitation Index' 
        ),
         'request_satellite':(storeUserSelections.selected_sub_indicator === 'Vegetation Cover'),
         'burnt_request':(    
          storeUserSelections.selected_sub_indicator === 'Soil Moisure Index'),
         'request_status':(storeUserSelections.selected_sub_indicator === 'Wetland Inventory' && storeUserSelections.selected_parameter === 'Wetland Status'),
        'request2':(storeUserSelections.selected_sub_indicator === 'Water Quality' || storeUserSelections.selected_sub_indicator === 'Vegetation Cover' ||
        storeUserSelections.selected_sub_indicator === 'Wetland Inventory'),
         'request1':( storeUserSelections.selected_sub_indicator === '' || storeUserSelections.selected_sub_indicator === 'Land Cover' ||
         storeUserSelections.selected_sub_indicator === 'Burnt Area MODIS' ||storeUserSelections.selected_sub_indicator === 'Burnt Area FIRMS' ),
         
         'flood_request':(storeUserSelections.selected_sub_indicator === 'Undulation')
         } " type="button" @click="$emit('fetchData')">{{ $t("home.request") }}</button>

         <p class="search_location" v-if="storeUserSelections.selected_basin != ''">{{ $t("home.search") }}</p>
         <div id="location_search">
          
         </div>

        <!-- <button type="button">Upload Shapefile</button> "$emit('increment-btn', 1)" storeUserSelections.selected_sub_indicator !== 'Precipitation Index' || --> 
        

    </div>
   
  
</template>

<script setup>
  import { onMounted, ref } from 'vue';
import CustomSelect from './CustomSelect.vue';
import {useCounterStore } from '../stores/counter';
import CustomSelect2 from './CustomSelect2.vue';
import CustomSelectIndicator from './CustomSelectIndicator.vue';
import CustomSelectSubIndicator from './CustomSelectSubIndicator.vue'
import CustomSelectYear from './CustomSelectYear.vue'
import CustomSelectSeason from './CustomSelectSeason.vue';
import CustomSelectParameter from './CustomSelectParameter.vue';
import CustomSelectSatellite from './CustomSelectSatellite.vue';

//refs
let region_selection = ref(true)
let indicator_selection = ref(true)
let year_selection = ref(true)

const storeUserSelections = useCounterStore()



// onMounted( ()=> {
  // let counties = ref(['Limpopo', 'Cuvelai', 'Okavango', 'Zambezi'])



// const fetchData = () => {
//   console.log('fetch!')

// }
const fetchRegion = () => {
  console.log('fetched region')
}
// })

const clickedMe = () => {
  console.log('clicked indicator select')


}

</script>

<style scoped>
    .selections{
        background-color: #f6f6f6;
        position: absolute; width: 89vw;
          height: 50px; padding: 15px; top: 12vh; left: 15vw;
           border-radius: 35px; padding-bottom: 20px;
    }
    .select_country{ 
  position: absolute;
  top: 0.1vh;
  left: 1.3vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}
#region_selection{ 
  position: absolute;
  top: 4vh;
  left: 0.8vw;
  height: 35px;
  width: 120px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}

.select_cause{ 
  position: absolute;
  top: 0.1vh;
  left: 9.5vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}

#cause_selection{ 
  position: absolute;
  top: 4vh;
  left: 10.5vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
  
}

.select_sub-indicator{ 
  position: absolute;
  top: 0.1vh;
  left: 18vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}

.sub_indicator_selection{
  position: absolute;
  top: 4vh;
  left: 18vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}



.bvi_label{
  position: absolute;
  top: 0.1vh;
  left: 20vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}
.bvi_select{
  position: absolute;
  top: 4vh;
  left: 20vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}


.select_year{ 
  position: absolute;
  top: 0.1vh;
  left: 29vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}

.flood_request{
  position: absolute;
  top: 4vh;
  left: 29vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;


}

.year_selection{
  position: absolute;
  top: 4vh;
  left: 29vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}
.select_season{
  position: absolute;
  top: 0.1vh;
  left: 38vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;

}
#season_selection{
  position: absolute;
  top: 4vh;
  left: 38vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}

.select_parameter{
  position: absolute;
  top: 0.1vh;
  left: 28vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;

}
#parameter_selection{
  position: absolute;
  top: 4vh;
  left: 28vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}

.request{
    position: absolute;
  top: 4vh;
  left: 46vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;
}


.burnt_request{
    position: absolute;
  top: 4vh;
  left: 46vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;
}
.request1{
  position: absolute;
  top: 4vh;
  left: 38vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;

}

.select_year2{ 
  position: absolute;
  top: 0.1vh;
  left: 38vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}

.year_selection2{
  position: absolute;
  top: 4vh;
  left: 38vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}


.request2{
    position: absolute;
  top: 4vh;
  left: 48vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;
}
.select_season_satellite{
  position: absolute;
  top: 0.1vh;
  left: 47vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}
.season_satellite_selection{
  position: absolute;
  top: 4vh;
  left: 47vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}
.request_satellite{
    position: absolute;
  top: 4vh;
  left: 58vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;
}
.request_status{
    position: absolute;
  top: 4vh;
  left: 62vw;
  width: 140px;
  height: 35px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
  border-radius: 30px;
  border: none;
  color: #fff;
  background-color: steelblue;
  cursor: pointer;
}


.select_year3{ 
  position: absolute;
  top: 0.1vh;
  left: 54vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}
.year_selection3{
  position: absolute;
  top: 4vh;
  left: 54vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}
.season_status{
  position: absolute;
  top: 0.1vh;
  left: 46vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;
}
.season_status_selection{
  position: absolute;
  top: 4vh;
  left: 46vw;
  height: 35px;
  width: 140px;
  border-radius: 30px;
  cursor: pointer;
  z-index: 1200;
}
.search_location{
  position: absolute;
  top: 0.1vh;
  left: 74vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  font-weight: 500;

}
#location_search{
  position: absolute;
  top: 5vh;
  left: 74vw;
  height: 40px;
  width: 300px;
  z-index: 1000;
  /* background-color: #fff; */

}
.satellite_none{
  display: none !important;
}






</style>