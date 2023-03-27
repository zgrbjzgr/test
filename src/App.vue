<template>
  <div >
    <!-- 输入数据 -->  
    <el-row :gutter="20">
         <!-- 表单1 -->
         <el-col :span="8" :offset="0">
            <el-card class="el-card" shadow="always">
              <h1>车辆自身信息</h1>
              <el-divider></el-divider>
 
              <el-form :model="ValidateForm" ref="ValidateForm" label-width="100px" class="demo-ruleForm">
<!-- 输入车辆VIN号  -->                  
<el-form-item
  label="车辆VIN号"
  prop="VIN"
  :rules="[{ required: true, message: '车辆VIN号不能为空'},]">
  <el-input v-model="ValidateForm.VIN" autocomplete="off"  placeholder="请输入车辆VIN号"></el-input>
</el-form-item>
<!-- 以上为输入车辆VIN号 -->
<!-- 输入车型 -->
<el-form-item
  label="车型"
  prop="car1"
  :rules="[{ required: true, message: '信息不能为空'},]">
 <!--  <el-input v-model="ValidateForm.car" autocomplete="off"></el-input> -->
  <el-input v-model="ValidateForm.car1" placeholder="请输入车辆型号"></el-input>
</el-form-item>
<!-- 运营商信息 -->
<el-form-item
  label="运营商"
  prop="car2"
  :rules="[{ required: true, message: '信息不能为空'},]">
  <el-input v-model="ValidateForm.car2" placeholder="请输入运营商信息"></el-input>
</el-form-item>
<!-- 提交与重置 -->
<el-form-item>
  <el-button type="primary" @click="submitForm('ValidateForm')">提交</el-button>
  <el-button @click="resetForm('ValidateForm')">重置</el-button>
</el-form-item>
              </el-form>
            </el-card>
         </el-col>
         <!-- 表单2 -->
         <el-col :span="8" :offset="0">
            <el-card class="el-card" shadow="always">
              <h1>car box</h1>
              <el-divider></el-divider>
 
  <!-- 左边表格 -->   <el-form :model="ValidateForm2" ref="ValidateForm2" label-width="100px" class="demo-ruleForm">
<!-- 输入车辆VIN号  -->                  
<el-form-item
  label="串号信息"
  prop="chuanhao"
  :rules="[{ required: true, message: '车辆号串号信息不能为空'},]">
  <el-input v-model="ValidateForm2.chuanhao" autocomplete="off"  placeholder="请输入车辆串号信息"></el-input>
</el-form-item>
<!-- 以上为输入车辆串号信息 -->
<!-- 输入car box基本信息 -->
<!-- <el-form-item
  label="car box"
  prop="car"
  :rules="[{ required: true, message: 'car box不能为空'},]">
  <el-input v-model="ValidateForm2.car" placeholder="请输入car box号码"></el-input>
</el-form-item> -->
<!-- 提交与重置 -->
<el-form-item>
  <el-button type="primary" @click="submitForm2('ValidateForm2')">提交</el-button>
  <el-button @click="resetForm2('ValidateForm2')">重置</el-button>
</el-form-item>
              </el-form>
            </el-card>
         </el-col>
         <!-- 表单3 -->
         <el-col :span="8">
          <el-card class="el-card" shadow="always">
              <h1>绑定</h1>
             <!--  <el-divider></el-divider> -->

    <el-form :model="ValidateForm3" ref="ValidateForm3" label-width="100px" class="demo-ruleForm">
      <!-- 下拉 -->
      <el-select 
	v-model="value"
 	placeholder="请选择车辆VIN号"
 	clearable
 	filterable

 	@clear="selectClear"
   @change="selectChange"
 >
  <el-option
    v-for="(item,index) in options"
    :key="index"
    :label="item.VIN"
    :value="item.value" />
</el-select><!-- VIN下拉 -->
<el-select 
	v-model="value2"
 	placeholder="请选择车辆型号"
 	clearable
 	filterable

 	@clear="selectClear2"
   @change="selectChange2"
 >
  <el-option
    v-for="(item,index) in options2"
    :key="index"
    :label="item.car1"
    :value="item.value" />
</el-select><!-- 车型下拉 -->
<el-select 
	v-model="value3"
 	placeholder="请选择运营商"
 	clearable
 	filterable

 	@clear="selectClear3"
   @change="selectChange3"
 >
  <el-option
    v-for="(item,index) in options3"
    :key="index"
    :label="item.car2"
    :value="item.value" />
</el-select><!-- 运营商下拉 -->
<el-select 
	v-model="value4"
 	placeholder="请选择串号号码"
 	clearable
 	filterable

 	@clear="selectClear4"
   @change="selectChange4"
 >
  <el-option
    v-for="(item,index) in options4"
    :key="index"
    :label="item.chuanhao"
    :value="item.value" />
</el-select><!-- 串号下拉 -->

<!-- 绑定选项 -->
<el-form-item>
  <el-button type="primary" @click="submitForm3('ValidateForm3')">提交</el-button>
  <el-button @click="resetForm3('ValidateForm3')">重置</el-button>
</el-form-item>
              </el-form>
            </el-card>
         </el-col>
      </el-row>
      <!-- 添加数据的表格 -->
    <el-row :gutter="20">
      <!-- 表格1 -->
      <el-col :span="8" :offset="0">
         <el-table
      :data="tableData"
      style="width: 100%"
      ><!-- @delete-row="deleteRow" -->
      <!-- 给表格添加索引 -->
      <el-table-column
      label="序号"
      type="index"
      width="50">
     <!--  <template slot-scope="scope">
        {{ scope.$index + 1 }}
      </template> -->
      </el-table-column>
      <!-- 表格内输入的参数 -->
      <el-table-column
        prop="VIN"
        label="车辆vin号"
        width="180">
      </el-table-column><!-- 表格内填入的VIN -->
      <el-table-column
        prop="car1"
        label="车型"
        width="100">
      </el-table-column><!-- 表格内填入的车型 -->
      <el-table-column
        prop="car2"
        label="运营商"
        width="100">
      </el-table-column><!-- 表格内填入的运营商 -->
      <el-table-column
        prop="xiugai"
        label="控制键"
        width="180">
        <template slot-scope="scope"><!-- 删除和详情 -->
        <el-button type="danger" icon="el-icon-delete" @click="shanchu(scope.$index)" circle></el-button>      
        <!-- 抽屉 -->
          <el-button type="info" icon="el-icon-message" circle @click="table = true"></el-button>
          <el-drawer
  title='详情'
  :visible.sync="table"
  direction="rtl"
  size="50%">
   <el-table :data="gridData">
      <el-table-column property="shichang" label="在线时长" width="150"></el-table-column>
      <el-table-column property="shujuliang" label="上传数据量" width="200"></el-table-column>
    </el-table>
           </el-drawer>
          </template>
        <!-- <el-button type="info" icon="el-icon-message" circle @click="table = true"></el-button> -->
        <!-- <el-button type="text" @click="table = true">打开嵌套表格的 Drawer</el-button> -->
      </el-table-column>
         </el-table>
      </el-col>
      <!-- 表格2 -->
      <el-col :span="8" :offset="0">
         <el-table
      :data="tableData2"
      style="width: 100%"
      ><!-- @delete-row="deleteRow" -->
      <!-- 给表格添加索引 -->
      <el-table-column
      label="序号"
      type="index"
      width="50">
     <!--  <template slot-scope="scope">
        {{ scope.$index + 1 }}
      </template> -->
      </el-table-column>
      <!-- 表格内输入的参数 -->
      <el-table-column
        prop="chuanhao"
        label="车辆串号信息"
        width="180">
      </el-table-column><!-- 表格内填入的串号信息 -->
      <!-- <el-table-column
        prop="car"
        label="car box"
        width="100">
      </el-table-column> --><!-- 表格内填入的car box -->
      <el-table-column
        prop="xiugai2"
        label="控制键"
        width="180">
        <template slot-scope="scope"><!-- 删除和详情 -->
        <el-button type="danger" icon="el-icon-delete" @click="shanchu2(scope.$index)" circle></el-button>      
        <!-- 抽屉 -->
          <el-button type="info" icon="el-icon-message" circle @click="table = true"></el-button>
          <el-drawer
  title='详情'
  :visible.sync="table"
  direction="rtl"
  size="50%">
   <el-table :data="gridData">
      <el-table-column property="shichang" label="在线时长" width="150"></el-table-column>
      <el-table-column property="shujuliang" label="上传数据量" width="200"></el-table-column>
    </el-table>
           </el-drawer>
          </template>
        <!-- <el-button type="info" icon="el-icon-message" circle @click="table = true"></el-button> -->
        <!-- <el-button type="text" @click="table = true">打开嵌套表格的 Drawer</el-button> -->
      </el-table-column>
         </el-table>
      </el-col>
      <!-- 表格3 -->
      <el-col :span="8" :offset="0">
         <el-table
      :data="tableData3"
      style="width: 100%"
      ><!--  @delete-row="deleteRow"-->
      <!-- 给表格添加索引 -->
      <el-table-column
      label="序号"
      type="index"
      width="50">
     <!--  <template slot-scope="scope">
        {{ scope.$index + 1 }}
      </template> -->
      </el-table-column>
      <!-- 表格内输入的参数 -->
      <el-table-column
        prop="VIN"
        label="车辆vin号"
        width="180">
      </el-table-column><!-- 表格内填入的VIN -->
      <el-table-column
        prop="car1"
        label="车型"
        width="100">
      </el-table-column><!-- 表格内填入的车型 -->
      <el-table-column
        prop="car2"
        label="运营商"
        width="100">
      </el-table-column><!-- 表格内填入的运营商 -->
      <el-table-column
        prop="chuanhao"
        label="串号信息"
        width="100">
      </el-table-column><!-- 表格内填入的串号信息 -->

      <el-table-column
        prop="xiugai"
        label="控制键"
        width="180">
        <template slot-scope="scope"><!-- 删除和详情 -->
        <el-button type="danger" icon="el-icon-delete" @click="shanchu3(scope.$index)" circle></el-button>      
        <!-- 抽屉 -->
          <el-button type="info" icon="el-icon-message" circle @click="table = true"></el-button>
          <el-drawer
  title='详情'
  :visible.sync="table"
  direction="rtl"
  size="50%">
   <el-table :data="gridData">
      <el-table-column property="shichang" label="在线时长" width="150"></el-table-column>
      <el-table-column property="shujuliang" label="上传数据量" width="200"></el-table-column>
    </el-table>
           </el-drawer>
          </template>
        <!-- <el-button type="info" icon="el-icon-message" circle @click="table = true"></el-button> -->
        <!-- <el-button type="text" @click="table = true">打开嵌套表格的 Drawer</el-button> -->
      </el-table-column><!-- 操作 -->
         </el-table>
      </el-col>
    </el-row>
    <!-- 上传 -->
    <el-row>
  <el-col :span="8" :offset="8">
                <el-upload
              class="upload-demo"
              action="https://jsonplaceholder.typicode.com/posts/"
              :on-preview="handlePreview"
              :on-remove="handleRemove"
              :before-remove="beforeRemove"
              multiple
              :limit="5"
              :on-exceed="handleExceed"
              :file-list="fileList">
              <el-button size="small" type="primary">点击上传</el-button>
            </el-upload>
  </el-col>
    </el-row>
  </div>
</template>
<style scoped>
.el-row {
  margin-bottom: 20px;
 
}
.el-col {
  border-radius: 4px;
}
.el-card{
  border-radius: 30px;
  width: 380px;
  display: flex;
  justify-content: center;
  background: #fcfafa;
}
</style>
<script>
export default {
  data() {
    return {
      value:'',
      value2:'',
      value3:'',
      value4:'',

      ValidateForm: {
        VIN: '',
        car1:'',
        car2:''
      },
      ValidateForm2:{
        chuanhao:'',
      },
      ValidateForm3: {
       
      },
     /* 表单3绑定部分 */
     options: [
		{value: '无保留意见', VIN: '无保留意见'},
		{value: '保留意见', VIN: '保留意见' }
 	],/* VIN */
   options2: [
		{value: '无保留意见', car1: '无保留意见'},
		{value: '保留意见', car1: '保留意见' }
 	],/* 型号 */
   options3: [
		{value: '无保留意见', car2: '无保留意见'},
		{value: '保留意见', car2: '保留意见' }
 	],/* 运营商 */
   options4: [
		{value: '无保留意见', car3: '无保留意见'},
		{value: '保留意见', car3: '保留意见' }
 	],/* 串号 */


      /* 表内数据 */
      tableData: [{
            VIN: 'che1',
            car1: '汽车',
            car2: '问界'
          }, {
            VIN: 'che2',
            car1: '京B',
            car2:'问界'
          }],
      tableData2: [{
            chuanhao: '123',
          }, {
            chuanhao: '456',
          }],
      tableData3: [{
            VIN: 'che1',
            car1: '汽车',
            car2: '问界',
            chuanhao:'12'
          }, {
            VIN: 'che2',
            car1: '京B',
            car2:'问界',
            chuanhao:'89'
          }],
          index:0,
          table:false,
         /* 抽屉嵌套数据 */
        gridData: [{
        shichang: '10' + 'min',
        shujuliang: '100'+'M',
      }],
      /* 上传 */
      fileList: [{name: '文件1.txt'}],
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('输入的VIN号是:'+this.ValidateForm.VIN +'\n'+'车型为:'+this.ValidateForm.car1 + '\n'+'运营商是:'+this.ValidateForm.car2);
          /* this.tableData.push(this.ValidateForm); */
          var a= JSON.parse(JSON.stringify(this.ValidateForm));
          /* console.log(a); */
          this.tableData.push(a);
          this.options.push({value:a.VIN,VIN:a.VIN});
          this.options2.push({value:a.car1,car1:a.car1});
          this.options3.push({value:a.car2,car2:a.car2});
          /* console.log(this.ValidateForm); */
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
      /* this.tableData.push(this.ValidateForm); */
    },
    /* 删除一组数据 */
    shanchu(index){
      this.$confirm('确认删除？')
          .then(_ => {
            this.tableData.splice(index,1);
            console.log(this);
          })
          .catch(_ => {});    
    },
    /* 表单2提交验证 */
    submitForm2(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert('输入的car box串号信息是:'+this.ValidateForm2.chuanhao/*  +'\n'+'车型为:'+this.ValidateForm.car1 + '\n'+'运营商是:'+this.ValidateForm.car2 */);
          /* this.tableData.push(this.ValidateForm); */
          var a= JSON.parse(JSON.stringify(this.ValidateForm2));
          /* console.log(a); */
          this.tableData2.push(a);
          this.options4.push({value:a.chuanhao,chuanhao:a.chuanhao});
          /* console.log(this.ValidateForm); */
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    /* 表单2重置 */
    resetForm2(formName) {
      this.$refs[formName].resetFields();
      /* this.tableData.push(this.ValidateForm); */
    },
    /* 表格2删除 */
    shanchu2(index){
      this.$confirm('确认删除？')
          .then(_ => {
            this.tableData2.splice(index,1);
            console.log(this);
          })
          .catch(_ => {});    
    },


  /* 表单3提交验证 */
    submitForm3(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert( '以下为绑定的信息' + '\n' +'VIN号:'+this.value +'\n'+'车型为:'+this.value2 + '\n'+'运营商是:'+this.value3 +'\n'+'串号信息:'+this.value4);
          /* this.tableData.push(this.ValidateForm); */
          /* console.log(a); */
          this.tableData3.push({VIN:this.value,car1:this.value2,car2:this.value3,chuanhao:this.value4});
          /* console.log(this.value);
          console.log(this.value2);
          console.log(this.value3);
          console.log(this.value4); */



          // var a= JSON.parse(JSON.stringify(this.ValidateForm3));


          /* console.log(a); */
          // this.tableData3.push(a);
          
          /* console.log(this.ValidateForm); */
        } else {
          console.log('error submit!!');
          return false;
        }
      });
    },
    /* 表单2重置 */
    resetForm3(formName) {
      this.$refs[formName].resetFields();
      /* this.tableData.push(this.ValidateForm); */
    },
    /* 表格2删除 */
    shanchu3(index){
      this.$confirm('确认删除？')
          .then(_ => {
            this.tableData3.splice(index,1);
            console.log(this);
          })
          .catch(_ => {});    
    },


    /* 表单3设置VIN */
   selectClear() {
    this.value = '';
    console.log(this);
    this.$forceUpdate();
  },
  selectChange(val) {
    this.value = val;
    this.$forceUpdate();
  },
  /* 表单3设置car1 */
  selectClear2() {
    this.value2 = '';
    console.log(this);
    this.$forceUpdate();
  },
  selectChange2(val) {
    this.value2 = val;
    this.$forceUpdate();
  },
  /* 表单3设置car2 */
  selectClear3() {
    this.value3 = '';
    console.log(this);
    this.$forceUpdate();
  },
  selectChange3(val) {
    this.value3 = val;
    this.$forceUpdate();
  },
    /* 表单3设置chuanhao */
    selectClear4() {
    this.value4 = '';
    console.log(this);
    this.$forceUpdate();
  },
  selectChange4(val) {
    this.value4 = val;
    this.$forceUpdate();
  },


  /* 上传 */
  handleRemove(file, fileList) {
        console.log(file, fileList);
      },
      handlePreview(file) {
        console.log(file);
      },
      handleExceed(files, fileList) {
        this.$message.warning(`当前限制选择 5 个文件，本次选择了 ${files.length} 个文件，共选择了 ${files.length + fileList.length} 个文件`);
      },
      beforeRemove(file, fileList) {
        return this.$confirm(`确定移除 ${ file.name }？`);
      }

  },
}
</script>
