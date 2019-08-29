<template>
  <div class="city">

    <el-select v-model="province" placeholder="请选择" @change="getCity(province)">
      <el-option
          v-for="(item,index) in provinceData"
          :key="index"
          :label="item.name"
          :value="item.id">
      </el-option>
    </el-select>

    <el-select v-model="city" placeholder="请选择" @change="getDistrict(city)">
      <el-option
          v-for="(item,index) in cityData"
          :key="index"
          :label="item.name"
          :value="item.id">
      </el-option>
    </el-select>

    <el-select v-model="district" placeholder="请选择" @change="">
      <el-option
          v-for="(item,index) in districtData"
          :key="index"
          :label="item.name"
          :value="item.id">
      </el-option>
    </el-select>

  </div>
</template>

<script>
  export default {
    name: "cityDemo",
    data(){
      return {
        province: '',  // 省份
        provinceData: '', // 省份列表

        city: '',  // 城市
        cityData: '',  // 城市列表

        district: '', // 区县
        districtData: '', // 区县列表

      }
    },
    created(){
      this.getProvinceData()
    },
    methods:{
      getProvinceData(){
        this.$axios.get('/static/mock/city.json')
            .then(res =>{
              this.provinceData = res.data
            })
      },

      // 获取城市
      getCity(val){
        this.city = ''
        this.district = ''
        this.provinceData.forEach(res =>{
          if(res.id === val){
            this.cityData = res.child
          }
        })
      },

      // 获取区县
      getDistrict(val){
        this.district = ''
        this.cityData.forEach(res =>{
          if(res.id === val){
            this.districtData = res.child
          }
        })
      },
    }
  }
</script>

<style scoped>

</style>