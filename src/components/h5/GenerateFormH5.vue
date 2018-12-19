<template>
  <div>
    <!-- <el-form ref="generateForm" :model="models" :rules="rules" :label-position="data.config.labelPosition" :label-width="data.config.labelWidth + 'px'">
      <template v-for="item in data.list">
    
        <template v-if="item.type == 'grid'">
          <el-row
            :key="item.key"
            type="flex"
            :gutter="item.options.gutter ? item.options.gutter : 0"
            :justify="item.options.justify"
            :align="item.options.align"
          >
            <el-col v-for="(col, colIndex) in item.columns" :key="colIndex" :span="col.span">
              
    
              <template v-for="citem in col.list" >
                <el-form-item v-if="citem.type=='blank'" :label="citem.name" :prop="citem.model" :key="citem.key">
                  <slot :name="citem.model" :model="models"></slot>
                </el-form-item>
                <genetate-form-item-h5 v-else :key="citem.key" :models.sync="models" :remote="remote" :rules="rules" :widget="citem"></genetate-form-item-h5>
              </template>
            </el-col>
          </el-row>
        </template>
    
        <template v-else-if="item.type == 'blank'">
          <el-form-item :label="item.name" :prop="item.model" :key="item.key">
            <slot :name="item.model" :model="models"></slot>
          </el-form-item>
        </template>
    
        <template v-else>
          <genetate-form-item-h5 :key="item.key" :models.sync="models" :rules="rules" :widget="item" :remote="remote"></genetate-form-item-h5>
        </template>
        
      </template>
    </el-form> -->

    <el-form ref="generateForm" :model="models" :rules="rules" :label-position="data.config.labelPosition" :label-width="data.config.labelWidth + 'px'">
      <template v-for="item in data.list">
        
        <!-- grid为栅格布局，移动端不用做栅格布局，直接遍历columns中的list即可.blank为自定义区域也不需要 -->
        <template v-if="item.type == 'grid'">
          <template v-for="(col, colIndex) in item.columns" >
              
    
              <template v-for="citem in col.list" >
                
                <genetate-form-item-h5 :key="citem.key" :models.sync="models" :remote="remote" :rules="rules" :widget="citem"></genetate-form-item-h5>
              </template>
            </template>
          
        </template>
    
        <template v-else>
          <genetate-form-item-h5 :key="item.key" :models.sync="models" :rules="rules" :widget="item" :remote="remote"></genetate-form-item-h5>
        </template>
        
      </template>
    </el-form>
  </div>
</template>

<script>
import GenetateFormItemH5 from './GenerateFormItemH5'

/*渲染模板fm-generate-form-h5组件注册*/
export default {
  name: 'fm-generate-form-h5',
  components: {
    GenetateFormItemH5
  },
  props: ['data', 'remote', 'value'],
  data () {
    return {
      models: {},
      rules: {}
    }
  },
  created () {
    this.generateModle(this.data.list)
  },
  methods: {
    generateModle (genList) {
      for (let i = 0; i < genList.length; i++) {
        if (genList[i].type === 'grid') {
          genList[i].columns.forEach(item => {
            this.generateModle(item.list)
          })
        } else { 
          if (Object.keys(this.value).indexOf(genList[i].model) >= 0) {
            this.models[genList[i].model] = this.value[genList[i].model]
          } else {
            if (genList[i].type === 'blank') {
              this.models[genList[i].model] = genList[i].options.defaultType === 'String' ? '' : (genList[i].options.defaultType === 'Object' ? {} : [])
            } else {
              this.models[genList[i].model] = genList[i].options.defaultValue
            }
            
          }
          
          if (this.rules[genList[i].model]) { 
            this.rules[genList[i].model] = [...this.rules[genList[i].model], ...genList[i].rules]
          } else {
            this.rules[genList[i].model] = [...genList[i].rules]
          }
          
        }
      }

      console.log('全部校验规则：',this.rules)
    },
    getData () {
      return new Promise((resolve, reject) => {
        this.$refs.generateForm.validate(valid => {
          if (valid) {
            resolve(this.models)
          } else {
            reject(new Error('表单数据校验失败').message)
          }
        })
      })
    },
    getData2 () {
      return this.models
    },
    refresh () {
      
    }
  },
  watch: {
    value: {
      deep: true,
      handler (val) {
        console.log(JSON.stringify(val))
        this.models = {...this.models, ...val}
      }
    }
  }
}
</script>
