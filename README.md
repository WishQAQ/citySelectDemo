# 城市三级联动选择，省市区demo

>Vue + element 三级联动，可高度定制


#### 选择框代码
```
 <div class="city">
     <el-select v-model="province" placeholder="选择省份" @change="getCity(province)">
       <el-option
           v-for="(item,index) in provinceData"
           :key="index"
           :label="item.name"
           :value="item.id">
       </el-option>
     </el-select>
 
     <el-select v-model="city" placeholder="选择城市" @change="getDistrict(city)">
       <el-option
           v-for="(item,index) in cityData"
           :key="index"
           :label="item.name"
           :value="item.id">
       </el-option>
     </el-select>
 
     <el-select v-model="district" placeholder="选择区县">
       <el-option
           v-for="(item,index) in districtData"
           :key="index"
           :label="item.name"
           :value="item.id">
       </el-option>
     </el-select>
   </div>
```
#### 功能代码
```
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
```