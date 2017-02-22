<template>
  <div id="app">
  <el-row type="flex" class="row-bg">
    <el-col :span=24>
      <el-form ref="form" :model="form" >
        <el-form-item label="用户名：" placeholder="请输入您的姓名">
          <el-input v-model="form.userName"></el-input>
        </el-form-item>
        <el-form-item label="年龄：" placeholder="请输入您的年龄">
          <el-input v-model="form.userAge"></el-input>
        </el-form-item>
        <el-button 
          type="primary"
          size="small"
          @click="add">添加</el-button>
        <el-button type="danger" size="small" native-type="reset">重置</el-button>
    </el-form>
    <hr>
    <el-table
     :data="tableData"
      border
      empty-text="暂无数据……"
      style="widht:100%">
        <el-table-column 
          label="序号"
          type="index"
          align="center">
        </el-table-column>
        <el-table-column
          label="用户名"
          prop="userName"          
          align="center">
        </el-table-column>
        <el-table-column
          label="年龄"
          prop="userAge"
          align="center">
        </el-table-column>
        <el-table-column
          label="操作"
          :content="_self"
          inline-template
          align="center">
        <div>
          <el-button 
            size="small"
            @click="deleteLog($index,row)"
            type="danger">删除</el-button>
        </div>
        </el-table-column> 
      </el-table> 
      <el-col :span=24 class="table-bottom">
        <el-button type="danger" @click="deleteAll">
          删除全部
        </el-button> 
      </el-col> 
    </el-col>
  </el-row>
    
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          userName: '',
          userAge: ''
        }, 
        tableData:[
            {
              userName:'haha',
              userAge:'50'
            },
            {
              userName:'gz',
              userAge:'10'
            }
        ]
      }
    },
    methods: {
      add(){ 
        var _this=this 
        var userName=_this.form.userName
        var userAge=_this.form.userAge
        if(userName==''||userAge=='')
        {
          return
        }
        _this.tableData.push({
          userName:userName,
          userAge:userAge,
        })
        _this.form.userName=''
        _this.form.userAge=''
      },
      deleteLog(index,row){ 
        this.$confirm('此操作将删除此记录，是否继续？','提示',{
          confirmButtonText:'确定',
          cancelButtonText:'取消',
          type:'warning'
        }).then(()=>{
        this.tableData.splice(index,1)
          this.$message({
            type:'success',
            message:'删除成功！'
          });
        }).catch(()=>{
          this.$message({
            type:'info',
            message:'已取消删除'
          })
        })
      },
      deleteAll(){
        this.$confirm('此操作将删除全部记录，是否继续？','提示',{
          confirmButtonText:'确定',
          cancelButtonText:'取消',
          type:'warning'
        }).then(()=>{
        this.tableData=[]
          this.$message({
            type:'success',
            message:'删除成功！'
          });
        }).catch(()=>{
          this.$message({
            type:'info',
            message:'已取消删除'
          })
        })
      }
    }
  }
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale; 
  color: #2c3e50; 
}
.table-bottom{
  margin-top: 10px;
  text-align: right;
}
</style>
