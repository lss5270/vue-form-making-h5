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
        data() {
        	return {
	          	jsonData: {"list":[{"type":"input","name":"名字","icon":"regular/keyboard","options":{"width":"100%","defaultValue":"lss","required":true,"dataType":"string","pattern":"","placeholder":"","remoteFunc":"func_1544779961000_15273"},"key":"1544779961000_15273","model":"name","rules":[{"type":"string","message":"名字格式不正确"},{"required":true,"message":"性别必须填写"}]},{"type":"number","name":"计数器","icon":"sort-numeric-up","options":{"width":"","required":false,"defaultValue":0,"min":0,"max":11,"step":1,"disabled":false,"controlsPosition":"","remoteFunc":"func_1545031700000_44134"},"key":"1545031700000_44134","model":"number_1545031700000_44134","rules":[]},{"type":"radio","name":"性别","icon":"regular/dot-circle","options":{"inline":true,"defaultValue":"man","showLabel":true,"options":[{"value":"man","label":"男"},{"value":"woman","label":"女"}],"required":true,"width":"","remote":false,"remoteOptions":[],"props":{"value":"value","label":"label"},"remoteFunc":"func_1544779976000_87453"},"key":"1544779976000_87453","model":"sex","rules":[{"required":true,"message":"性别必须填写"}]},{"type":"checkbox","name":"兴趣爱好","icon":"regular/check-square","options":{"inline":true,"defaultValue":["eat"],"showLabel":true,"options":[{"value":"eat","label":"吃饭"},{"value":"sleep","label":"睡觉"},{"value":"hit","label":"打豆豆"}],"required":false,"width":"","remote":false,"remoteOptions":[],"props":{"value":"value","label":"label"},"remoteFunc":"func_1545036930000_10021"},"key":"1545036930000_10021","model":"checkbox_1545036930000_10021","rules":[]},{"type":"switch","name":"是否管理员","icon":"toggle-off","options":{"defaultValue":true,"required":false,"disabled":false,"remoteFunc":"func_1545030546000_14547"},"key":"1545030546000_14547","model":"switch_1545030546000_14547","rules":[]},{"type":"textarea","name":"多行文本","icon":"regular/keyboard","options":{"width":"100%","defaultValue":"多行文本默认内容","required":false,"pattern":"","placeholder":"","remoteFunc":"func_1545030842000_38061"},"key":"1545030842000_38061","model":"textarea_1545030842000_38061","rules":[]},{"type":"grid","name":"栅格布局","icon":"th","columns":[{"span":12,"list":[{"type":"input","name":"栅格左布局","icon":"regular/keyboard","options":{"width":"100%","defaultValue":"左布局默认内容","required":false,"dataType":"string","pattern":"","placeholder":"","remoteFunc":"func_1545030578000_13235"},"key":"1545030578000_13235","model":"input_1545030578000_13235","rules":[{"type":"string","message":"栅格左布局格式不正确"}]}]},{"span":12,"list":[]}],"options":{"gutter":0,"justify":"start","align":"top","remoteFunc":"func_1545030574000_16644"},"key":"1545030574000_16644","model":"grid_1545030574000_16644","rules":[]},{"type":"blank","name":"自定义","icon":"chalkboard","options":{"defaultType":"String","remoteFunc":"func_1545031064000_63022"},"key":"1545031064000_63022","model":"blank_1545031064000_63022","rules":[]}],"config":{"labelWidth":100,"labelPosition":"top"}},
          		editData: {},
		        remoteFuncs: {}
	        }
        },
        methods: {
          handleSubmit () {
            this.$refs.generateForm.getData().then(data => {
              // 数据校验成功
              // data 为获取的表单数据
            }).catch(e => {
              // 数据校验失败
            })
          }
        }
}
</script>
