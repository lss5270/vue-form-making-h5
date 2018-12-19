<template>
  <div class="lss-form-item">
    <van-cell-group>
      <!-- 普通输入框 Field输入框支持框下错误提示-->
      <template v-if="widget.type == 'input'" >
        <van-field
          v-model="dataModel"
          :required="widget.options.required"
          :label="widget.name"
          :placeholder="widget.options.placeholder"
          :clearable="clearable"
          :is-link="isLink"
          :input-align="inputAlign"

        />
      </template>
      <!-- 计步器 -->
      <template v-if="widget.type == 'number'" >
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <van-stepper class="slot_button"
            v-model.number="dataModel"
            integer
            :min="widget.options.min"
            :max="widget.options.max"
            :step="widget.options.step"
          />
        </van-cell>
        <!-- <van-field
          :required="widget.options.required"
          :label="widget.name"
          :is-link="isLink"
          disabled
        >
          <van-stepper slot="button" class="slot_button"
            v-model.number="dataModel"
            integer
            :min="widget.options.min"
            :max="widget.options.max"
            :step="widget.options.step"
          />
        </van-field> -->
      </template>
      
      <!-- 文本域 Field输入框支持框下错误提示-->
      <template v-if="widget.type == 'textarea'">
        <van-field
          type="textarea"
          v-model="dataModel"
          :required="widget.options.required"
          :label="widget.name"
          :placeholder="widget.options.placeholder"
          :clearable="clearable"
          :is-link="isLink"
          :input-align="inputAlign"
          rows="1"
          autosize
        />
      </template>

      <!-- 单选 -->
      <template v-if="widget.type == 'radio'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <van-radio-group v-model="dataModel">
            <template v-for="(item, index) in (widget.options.remote ? widget.options.remoteOptions : widget.options.options)">
              <van-radio :name="item.value">{{item.label}}</van-radio>
            </template>
            <!-- <van-radio name="2">单选框 2</van-radio> -->
          </van-radio-group>
        </van-cell>

      </template>
      <!-- 多选 -->
      <template v-if="widget.type == 'checkbox'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <van-checkbox-group v-model="dataModel">
            <van-checkbox
              v-for="(item, index) in (widget.options.remote ? widget.options.remoteOptions : widget.options.options)"
              :key="index"
              :name="item.value"
            >
              {{item.label}}
            </van-checkbox>
          </van-checkbox-group>
        </van-cell>

      </template>

      <!-- 开关 -->
      <template v-if="widget.type == 'switch'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <van-switch v-model="dataModel" :disabled="widget.options.disabled" size="24px" />
        </van-cell>
      </template>
      
      <!-- 日期 年月日 -->
      <template v-if="widget.type == 'date'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <div @click="dateShow = true">&nbsp;{{dataModel | parseTime('{y}-{m}-{d}')}}</div>
        </van-cell>

        <van-popup 
          v-model="dateShow" 
          position="bottom"
          
          >
            <van-datetime-picker
              :title="widget.name"
              v-model="dataModel"
              type="date"
              :show-toolbar="true"
              :formatter="formatter"
              @confirm="dateConfirmClick"
              @cancel="dateShow = false"
            />
              
          </van-popup>
      </template>

      <!-- 时间 时分 -->
      <template v-if="widget.type == 'time'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <div @click="dateShow = true">&nbsp;{{dataModel}}</div>
        </van-cell>

        <van-popup 
          v-model="dateShow" 
          position="bottom"
          
          >
            <van-datetime-picker
              :title="widget.name"
              v-model="dataModel"
              type="time"
              :show-toolbar="true"
              @confirm="dateShow = false"
              @cancel="dateShow = false"
            />
              
          </van-popup>
      </template>
      
      <!-- 评分 -->
      <template v-if="widget.type == 'rate'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        >
          <van-rate
            v-model="dataModel"
            :size="24"
            :count="widget.options.max"
            
          />
        </van-cell>
      </template>

      <!-- 滑块 -->
      <template v-if="widget.type == 'slider'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        > 
          <div style="padding:11px;">
            <van-slider v-model="dataModel" :min="widget.options.min" :max="widget.options.max" :step="widget.options.step" />
          </div>
          
        </van-cell>
      </template>

      <!-- 图片上传 (涉及到文件上传的服务器，)-->
      <template v-if="widget.type == 'imgupload'">
        <van-cell 
          :required="widget.options.required"
          :title="widget.name"
          :is-link="isLink"
          disabled
        > 
          
          <van-uploader :after-read="onReadFile" accept="image/gif, image/jpeg" multiple style="width:100%;font-size:20px;vertical-align:middle;">
            <van-icon name="photograph" />
          </van-uploader>
       
        </van-cell>
      </template>
    </van-cell-group>


    

    <!-- <template v-if="widget.type == 'textarea'">
      <el-input type="textarea" :rows="5"
        v-model="dataModel"
        :placeholder="widget.options.placeholder"
        :style="{width: widget.options.width}"
      ></el-input>
    </template>
    
    <template v-if="widget.type == 'number'">
      <el-input-number 
        v-model="widget.options.defaultValue" 
        :style="{width: widget.options.width}"
        :step="widget.options.step"
        controls-position="right"
      ></el-input-number>
    </template>
    
    <template v-if="widget.type == 'radio'">
      <el-radio-group v-model="dataModel"
        :style="{width: widget.options.width}"
      >
        <el-radio
          :style="{display: widget.options.inline ? 'inline-block' : 'block'}"
          :label="item.value" v-for="(item, index) in (widget.options.remote ? widget.options.remoteOptions : widget.options.options)" :key="index"
        >
          <template v-if="widget.options.remote">{{item.label}}</template>
          <template v-else>{{widget.options.showLabel ? item.label : item.value}}</template>
        </el-radio>
      </el-radio-group>
    </template>
    
    <template v-if="widget.type == 'checkbox'">
      <el-checkbox-group v-model="dataModel"
        :style="{width: widget.options.width}"
      >
        <el-checkbox
          
          :style="{display: widget.options.inline ? 'inline-block' : 'block'}"
          :label="item.value" v-for="(item, index) in (widget.options.remote ? widget.options.remoteOptions : widget.options.options)" :key="index"
        >
          <template v-if="widget.options.remote">{{item.label}}</template>
          <template v-else>{{widget.options.showLabel ? item.label : item.value}}</template>
        </el-checkbox>
      </el-checkbox-group>
    </template>
    
    <template v-if="widget.type == 'time'">
      <el-time-picker 
        v-model="dataModel"
        :is-range="widget.options.isRange"
        :placeholder="widget.options.placeholder"
        :start-placeholder="widget.options.startPlaceholder"
        :end-placeholder="widget.options.endPlaceholder"
        :readonly="widget.options.readonly"
        :disabled="widget.options.disabled"
        :editable="widget.options.editable"
        :clearable="widget.options.clearable"
        :arrowControl="widget.options.arrowControl"
        :value-format="widget.options.format"
        :style="{width: widget.options.width}"
      >
      </el-time-picker>
    </template>
    
    <template v-if="widget.type=='date'">
      <el-date-picker
        v-model="dataModel"
        :type="widget.options.type"
        :placeholder="widget.options.placeholder"
        :start-placeholder="widget.options.startPlaceholder"
        :end-placeholder="widget.options.endPlaceholder"
        :readonly="widget.options.readonly"
        :disabled="widget.options.disabled"
        :editable="widget.options.editable"
        :clearable="widget.options.clearable"
        :value-format="widget.options.timestamp ? 'timestamp' : widget.options.format"
        :format="widget.options.format"
        :style="{width: widget.options.width}"
      >
      </el-date-picker>
    </template>
    
    <template v-if="widget.type =='rate'">
      <el-rate v-model="dataModel"
        :max="widget.options.max"
        :disabled="widget.options.disabled"
        :allow-half="widget.options.allowHalf"
      ></el-rate>
    </template>
    
    <template v-if="widget.type == 'color'">
      <el-color-picker 
        v-model="dataModel"
        :disabled="widget.options.disabled"
        :show-alpha="widget.options.showAlpha"
      ></el-color-picker>
    </template>
    
    <template v-if="widget.type == 'select'">
      <el-select
        v-model="dataModel"
        :disabled="widget.options.disabled"
        :multiple="widget.options.multiple"
        :clearable="widget.options.clearable"
        :placeholder="widget.options.placeholder"
        :style="{width: widget.options.width}"
      >
        <el-option v-for="item in (widget.options.remote ? widget.options.remoteOptions : widget.options.options)" :key="item.value" :value="item.value" :label="widget.options.showLabel || widget.options.remote?item.label:item.value"></el-option>
      </el-select>
    </template>
    
    <template v-if="widget.type=='switch'">
      <el-switch
        v-model="dataModel"
        :disabled="widget.options.disabled"
      >
      </el-switch>
    </template>
    
    <template v-if="widget.type=='slider'">
      <el-slider 
        v-model="dataModel"
        :min="widget.options.min"
        :max="widget.options.max"
        :disabled="widget.options.disabled"
        :step="widget.options.step"
        :show-input="widget.options.showInput"
        :range="widget.options.range"
        :style="{width: widget.options.width}"
      ></el-slider>
    </template>
    
    <template v-if="widget.type=='imgupload'">
      <fm-upload
        v-model="dataModel"
        :disabled="widget.options.disabled"
        :style="{'width': widget.options.width}"
        :width="widget.options.size.width"
        :height="widget.options.size.height"
        :token="widget.options.token"
        :domain="widget.options.domain"
      >
      </fm-upload>
    </template> -->
  </div>
</template>

<script>
import FmUpload from '../Upload'

export default {
  props: ['widget', 'models', 'rules', 'remote'],
  components: {
    FmUpload
  },
  data () {
    return {
      dataModel: this.models[this.widget.model],
      clearable: true,
      isLink: true,
      inputAlign: 'right',
      dateShow: false,
    }
  },
  created () {
    if (this.widget.options.remote && this.remote[this.widget.options.remoteFunc]) {
      this.remote[this.widget.options.remoteFunc]((data) => {
        this.widget.options.remoteOptions = data.map(item => {
          return {
            value: item[this.widget.options.props.value],
            label: item[this.widget.options.props.label]
          }
        })
      })
    }

    if (this.widget.type === 'imgupload') {
      //先注释
      /*this.remote[this.widget.options.tokenFunc]((data) => {
        this.widget.options.token = data
      })*/
    }
  },
  watch: {
    dataModel: {
      deep: true,
      handler (val) {
        this.models[this.widget.model] = val
        this.$emit('update:models', {
          ...this.models,
          [this.widget.model]: val
        })
      }
    },
    models: {
      deep: true,
      handler (val) {
        /*console.log('--------')*/
        this.dataModel = val[this.widget.model]
      }
    }
  },
  methods:{
    formatter(type, value) {
      if (type === 'year') {
        return `${value}年`;
      } else if (type === 'month') {
        return `${value}月`
      } else if (type === 'day') {
        return `${value}日`
      }
      return value;
    },
    dateConfirmClick(v) {
      let vm = this
      console.log('选中的日期为：',v)
      vm.dateShow = false
      /*if(new Date(v)){
        alert('日期')
      }*/
    },
    onReadFile(file) {
      console.log('文件选中:',file)
    }
  }
}
</script>

<style>
  .van-cell__title{
    width: 100px !important;
  }
  .van-cell__value{
    flex: 2.5 !important;
  }
</style>