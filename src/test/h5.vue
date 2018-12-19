<template>
  <!-- <fm-making-form  preview generate-code generate-json>
    <template slot="action">
    </template>
  </fm-making-form> -->
  <div>
  	<h2>h5测试页……</h2>
  	<fm-generate-form-h5 :data="jsonData" :remote="remoteFuncs" :value="editData" ref="generateForm">
  	        
  	</fm-generate-form-h5>
  	<!-- <el-button type="primary" @click="handleSubmit">提交</el-button> -->
	<p>
		<van-button type="default" @click="handleSubmit" size="large">提交</van-button>
	</p>
  </div>
</template>

<script>
export default {
        name: '',
        //props: ['rules'],
        data() {
        	return {
	          jsonData: {"list":[{"type":"input","name":"名字","icon":"regular/keyboard","options":{"width":"100%","defaultValue":"lss","required":true,"dataType":"string","pattern":"","placeholder":"","remoteFunc":"func_1544779961000_15273"},"key":"1544779961000_15273","model":"name","rules":[{"type":"string","message":"名字格式不正确"},{"required":true,"message":"评分必须填写"}]},{"type":"input","name":"电话号码","icon":"icon-input","options":{"width":"100%","defaultValue":"","required":true,"dataType":"string","pattern":"/^[1][3,4,5,7,8][0-9]{9}$/","placeholder":"","remoteFunc":"func_1545211048000_67897"},"key":"1545211048000_67897","model":"input_1545211048000_67897","rules":[{"type":"string","message":"名字格式不正确"},{"required":true,"message":"电话号码必须填写"},{"pattern":"/^[1][3,4,5,7,8][0-9]{9}$/","message":"电话号码格式不匹配"}]},{"type":"number","name":"计数器","icon":"sort-numeric-up","options":{"width":"","required":false,"defaultValue":0,"min":0,"max":11,"step":1,"disabled":false,"controlsPosition":"","remoteFunc":"func_1545031700000_44134"},"key":"1545031700000_44134","model":"number_1545031700000_44134","rules":[]},{"type":"radio","name":"性别","icon":"regular/dot-circle","options":{"inline":true,"defaultValue":"man","showLabel":true,"options":[{"value":"man","label":"男"},{"value":"woman","label":"女"}],"required":true,"width":"","remote":false,"remoteOptions":[],"props":{"value":"value","label":"label"},"remoteFunc":"func_1544779976000_87453"},"key":"1544779976000_87453","model":"sex","rules":[{"required":true,"message":"性别必须填写"}]},{"type":"checkbox","name":"兴趣爱好","icon":"regular/check-square","options":{"inline":true,"defaultValue":["eat"],"showLabel":true,"options":[{"value":"eat","label":"吃饭"},{"value":"sleep","label":"睡觉"},{"value":"hit","label":"打豆豆"}],"required":false,"width":"","remote":false,"remoteOptions":[],"props":{"value":"value","label":"label"},"remoteFunc":"func_1545036930000_10021"},"key":"1545036930000_10021","model":"checkbox_1545036930000_10021","rules":[]},{"type":"switch","name":"是否管理员","icon":"toggle-off","options":{"defaultValue":true,"required":false,"disabled":false,"remoteFunc":"func_1545030546000_14547"},"key":"1545030546000_14547","model":"switch_1545030546000_14547","rules":[]},{"type":"textarea","name":"多行文本","icon":"regular/keyboard","options":{"width":"100%","defaultValue":"多行文本默认内容","required":false,"pattern":"","placeholder":"","remoteFunc":"func_1545030842000_38061"},"key":"1545030842000_38061","model":"textarea_1545030842000_38061","rules":[]},{"type":"grid","name":"栅格布局","icon":"th","columns":[{"span":12,"list":[{"type":"input","name":"栅格左布局","icon":"regular/keyboard","options":{"width":"100%","defaultValue":"左布局默认内容","required":false,"dataType":"string","pattern":"","placeholder":"","remoteFunc":"func_1545030578000_13235"},"key":"1545030578000_13235","model":"input_1545030578000_13235","rules":[{"type":"string","message":"栅格左布局格式不正确"}]}]},{"span":12,"list":[]}],"options":{"gutter":0,"justify":"start","align":"top","remoteFunc":"func_1545030574000_16644"},"key":"1545030574000_16644","model":"grid_1545030574000_16644","rules":[]},{"type":"blank","name":"自定义","icon":"chalkboard","options":{"defaultType":"String","remoteFunc":"func_1545031064000_63022"},"key":"1545031064000_63022","model":"blank_1545031064000_63022","rules":[]},{"type":"time","name":"时间选择器","icon":"icon-time","options":{"defaultValue":"","readonly":false,"disabled":false,"editable":true,"clearable":true,"placeholder":"","startPlaceholder":"","endPlaceholder":"","isRange":false,"arrowControl":true,"format":"HH:mm:ss","required":false,"width":"","remoteFunc":"func_1545102093000_71754"},"key":"1545102093000_71754","model":"time_1545102093000_71754","rules":[]},{"type":"date","name":"日期选择器","icon":"icon-date","options":{"defaultValue":"","readonly":false,"disabled":false,"editable":true,"clearable":true,"placeholder":"","startPlaceholder":"","endPlaceholder":"","type":"date","format":"yyyy-MM-dd","timestamp":true,"required":true,"width":"","remoteFunc":"func_1545102098000_23837"},"key":"1545102098000_23837","model":"date_1545102098000_23837","rules":[{"required":true,"message":"日期选择器必须填写"}]},{"type":"rate","name":"评分","icon":"icon-icon-test","options":{"defaultValue":4,"max":6,"disabled":false,"allowHalf":false,"required":true,"remoteFunc":"func_1545116997000_18496"},"key":"1545116997000_18496","model":"rate_1545116997000_18496","rules":[{"required":true,"message":"评分必须填写"}]},{"type":"slider","name":"滑块","icon":"icon-slider","options":{"defaultValue":0,"disabled":false,"required":true,"min":0,"max":100,"step":1,"showInput":false,"range":false,"width":"","remoteFunc":"func_1545117001000_3762"},"key":"1545117001000_3762","model":"slider_1545117001000_3762","rules":[{"required":true,"message":"滑块必须填写"}]},{"type":"imgupload","name":"图片","icon":"icon-tupian","options":{"defaultValue":[],"size":{"width":100,"height":100},"width":"","tokenFunc":"funcGetToken","token":"odaWpqNvohuJr1UrGQgOixj4Kw05b1stVq2-YjKh:kz-ioN8UPyYd_YUoWHemPaKYlVQ=:eyJkZWxldGVBZnRlckRheXMiOjEsInJldHVybkJvZHkiOiJ7XCJrZXlcIjpcIiQoa2V5KVwiLFwiaGFzaFwiOlwiJChldGFnKVwiLFwiZnNpemVcIjokKGZzaXplKSxcImJ1Y2tldFwiOlwiJChidWNrZXQpXCIsXCJuYW1lXCI6XCIkKHg6bmFtZSlcIn0iLCJzY29wZSI6ImZvcm0tbWFraW5nIiwiZGVhZGxpbmUiOjE1NDUyMTQ2OTB9","domain":"http://pfp81ptt6.bkt.clouddn.com/","disabled":false,"length":8,"multiple":true,"remoteFunc":"func_1545118136000_2992"},"key":"1545118136000_2992","model":"imgupload_1545118136000_2992","rules":[]}],"config":{"labelWidth":100,"labelPosition":"top"}},
            editData: {},
		        remoteFuncs: {}
	        }
        },
        methods: {
          handleSubmit () {
            /*this.$refs.generateForm.getData().then(data => {
              // 数据校验成功 
              // data 为获取的表单数据
              console.log('校验通过的表单数据为:',data)
            }).catch(e => {
              // 数据校验失败
            })*/
            
            /*移动端大多数表单元素不支持框下错误提示，故只能改成弹窗提示*/
            let _rules = this.$refs.generateForm.rules
            let _dataJson = this.$refs.generateForm.getData2()
            console.log('校验规则',_rules)
            console.log('表单数据',_dataJson)

            for (let key of Object.keys(_rules)) {
              if(_rules[key].length > 0){
                console.log(key + ': ' + JSON.stringify(_rules[key]) )
                for (let item of _rules[key]){
                  //必填项校验
                  if(item.required && !_dataJson[key]){
                    this.$toast(item.message)
                    return false
                  }
                  //数据类型校验

                  //正则校验
                  if(item.pattern && item.pattern !==''){
                    if( !eval(item.pattern).test(_dataJson[key]) ){
                      this.$toast(item.message)
                      return false
                    }
                    
                  }
                }
              }
            }

            console.log('数据校验通过：',_dataJson)
          }
        }
}
</script>
