<template>
  <div class="app-container">
    <!-- 筛选栏 -->
    <div class="filter-container my-container">
      <!-- 第一行 -->
      <el-row :align="middle">
        <el-col :span="8">
          <el-col :span="6">
            <div style="line-height: 40px">
              设备名称:
            </div>
          </el-col>
          <!-- 输入框 -->
          <el-col :span="18">
            <el-input v-model="listQuery.groupName" placeholder="请输入设备名称" style="width: 160px;" class="filter-item" @keyup.enter.native="handleFilter" />
            <el-button class="my-icon-button" icon="el-icon-search" />
          </el-col>
        </el-col>
        <el-col :span="8">
          <el-col :span="6">
            <div style="line-height: 40px">
              所属机构:
            </div>
          </el-col>
          <!-- 下拉框 -->
          <el-col :span="18">
            <el-select v-model="listQuery.group" placeholder="请选择所属机构" clearable style="width: 200px" class="filter-item">
              <el-option v-for="item in importanceOptions" :key="item" :label="item" :value="item" />
            </el-select>
          </el-col>
        </el-col>
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              所属分组:
            </div>
          </el-col>
          <!-- 下拉框 -->
          <el-col :span="18">
            <el-select v-model="listQuery.group" placeholder="请选择所属分组" clearable style="width: 200px" class="filter-item">
              <el-option v-for="item in importanceOptions" :key="item" :label="item" :value="item" />
            </el-select>
          </el-col>
        </el-col>
      </el-row>
      <!-- 第二行 -->
      <el-row type="flex" justify="space-around">
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              MAC地址:
            </div>
          </el-col>
          <!-- 输入框 -->
          <el-col :span="18">
            <el-input v-model="listQuery.groupName" placeholder="请输入MAC地址" style="width: 160px;" class="filter-item" @keyup.enter.native="handleFilter" />
            <el-button class="my-icon-button" icon="el-icon-search" />
          </el-col>
        </el-col>
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              分辨率:
            </div>
          </el-col>
          <!-- 下拉框 -->
          <el-col :span="18">
            <el-input v-model="listQuery.groupName" placeholder="请输入分辨率" style="width: 160px;" class="filter-item" @keyup.enter.native="handleFilter" />
            <el-button class="my-icon-button" icon="el-icon-search" />
          </el-col>
        </el-col>
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              设备状态:
            </div>
          </el-col>
          <!-- 下拉框 -->
          <el-col :span="18">
            <el-select v-model="listQuery.sort" style="width: 200px" class="filter-item" @change="handleFilter">
              <el-option v-for="item in sortOptions" :key="item.key" :label="item.label" :value="item.key" />
            </el-select>
          </el-col>
        </el-col>
      </el-row>
      <!-- 第三行 -->
      <el-row type="flex" justify="space-around">
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              系统版本:
            </div>
          </el-col>
          <!-- 输入框 -->
          <el-col :span="18">
            <el-select v-model="listQuery.sort" style="width: 200px" class="filter-item" @change="handleFilter">
              <el-option v-for="item in sortOptions" :key="item.key" :label="item.label" :value="item.key" />
            </el-select>
          </el-col>
        </el-col>
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              当前计划:
            </div>
          </el-col>
          <!-- 下拉框 -->
          <el-col :span="18">
            <el-select v-model="listQuery.group" placeholder="请选择当前计划" clearable style="width: 200px" class="filter-item">
              <el-option v-for="item in importanceOptions" :key="item" :label="item" :value="item" />
            </el-select>
          </el-col>
        </el-col>
        <el-col :span="8">
          <el-col el-col :span="6">
            <div style="line-height: 40px">
              SN:
            </div>
          </el-col>
          <!-- 下拉框 -->
          <el-col :span="18">
            <el-input v-model="listQuery.groupName" placeholder="请输入SN号" style="width: 160px;" class="filter-item" @keyup.enter.native="handleFilter" />
            <el-button class="my-icon-button" icon="el-icon-search" />
          </el-col>
        </el-col>
      </el-row>
      <el-row type="flex" justify="end">
        <el-col :span="2.5">
          <!-- 重置按钮 -->
          <el-button class="filter-item" style="margin-left: 10px;" type="primary" icon="el-icon-refresh" @click="handleFilter">
            重置
          </el-button>
          <!-- 查询按钮 -->
          <el-button v-waves class="filter-item" type="primary" icon="el-icon-search" @click="handleFilter">
            查询
          </el-button>
        </el-col>
      </el-row>
    </div>

    <div class="new-group my-container">
      <el-row type="flex" justify="end">
        <el-col :span="2.5">
          <div class="new-group">
            <!-- 新建分组按钮 -->
            <el-button v-waves class="filter-item" type="primary" icon="el-icon-document-copy" @click="handleMoreInfo">
              批量导入
            </el-button>
            <el-button v-waves class="filter-item" type="primary" icon="el-icon-download" @click="handleCreate">
              模板下载
            </el-button>
            <el-button v-waves class="filter-item" type="primary" icon="el-icon-delete" @click="handleCreate">
              批量删除
            </el-button>
            <el-button v-waves class="filter-item" type="primary" icon="el-icon-connection" @click="handleCreate">
              批量控制
            </el-button>
            <el-button v-waves class="filter-item" type="primary" icon="el-icon-upload2" @click="handleCreate">
              数据导出
            </el-button>
          </div>
        </el-col>
      </el-row>
    </div>

    <!-- 表单 v-loading="listLoading" -->
    <el-table
      :key="tableKey"
      :data="list"
      fit
      highlight-current-row
      style="width: 100%;"
      @sort-change="sortChange"
    >
      <el-table-column type="selection" width="25px" />
      <el-table-column label="设备名称" prop="id" align="center" width="120px" :class-name="getSortClass('id')">
        <template slot-scope="{row}">
          <span>{{ row.id }}</span>
        </template>
      </el-table-column>
      <el-table-column label="所属机构" width="120px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.group }}</span>
        </template>
      </el-table-column>
      <el-table-column label="所属分组" width="120px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="MAC地址" width="150px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="分辨率" width="150px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="设备状态" width="120px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="系统升级" width="120px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="当前计划" width="120px" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
      <el-table-column label="操作" align="center">
        <template slot-scope="{row}">
          <span>{{ row.author }}</span>
        </template>
      </el-table-column>
    </el-table>

    <!-- 分页 -->
    <pagination v-show="total>0" :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList" />

    <!-- 添加 对话框 -->
    <el-dialog :title="textMap[dialogStatus]" :visible.sync="dialogFormVisible" width="30%">
      <el-form ref="dataForm" :rules="rules" :model="temp" label-position="left" label-width="90px" style="width: 300px; margin-left:50px;">
        <el-form-item label="设备名称" prop="groupName">
          <el-input v-model="temp.groupName" placeholder="请输入设备名称" />
        </el-form-item>
        <el-form-item label="所属分组" prop="group">
          <el-select v-model="temp.group" class="filter-item" placeholder="请选择所属分组">
            <el-option v-for="item in calendarTypeOptions" :key="item.key" :label="item.display_name" :value="item.key" />
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">
          取消
        </el-button>
        <el-button type="primary" @click="dialogStatus==='create'?createData():updateData()">
          保存
        </el-button>
      </div>
    </el-dialog>

    <el-dialog :visible.sync="dialogTableVisible" width="40%" title="设备详情">
      <template>
        <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
          <el-tab-pane label="设备信息" name="first">
            <!-- 第一行 -->
            <el-row>
              <el-col :span="12">
                <el-col :span="6">
                  设备型号:
                </el-col>
                <el-col :span="18">
                  HiDPTAndroid Hi3751V553
                </el-col>
              </el-col>
              <el-col :span="12">
                <el-col :span="6">
                  系统版本:
                </el-col>
                <el-col :span="18">
                  BOE_iGallery32_V13103_V5.2.0
                </el-col>
              </el-col>
            </el-row>
            <!-- 第二行 -->
            <el-row>
              <el-col :span="12">
                <el-col :span="6">

                </el-col>
                <el-col :span="18">

                </el-col>
              </el-col>
              <el-col :span="12">
                <el-col :span="6">
                  
                </el-col>
                <el-col :span="18">
                  
                </el-col>
              </el-col>
            </el-row>
          </el-tab-pane>
          <el-tab-pane label="安装信息" name="second">
            <!-- 第一行 -->
            <el-row>
              <el-col :span="12">
                <el-col :span="6">
                  设备名称:
                </el-col>
                <el-col :span="18">
                  test
                </el-col>
              </el-col>
              <el-col :span="12">
                <el-col :span="6">
                  注册时间:
                </el-col>
                <el-col :span="18">
                  2022-06-27 14:31:14
                </el-col>
              </el-col>
            </el-row>
          </el-tab-pane>
          <el-tab-pane label="状态信息" name="third">
            <!-- 第一行 -->
            <el-row>
              <el-col :span="12">
                <el-col :span="6">
                  设备状态:
                </el-col>
                <el-col :span="18">
                  离线
                </el-col>
              </el-col>
              <el-col :span="12">
                <el-col :span="6">
                  当前计划:
                </el-col>
                <el-col :span="18">
                  --
                </el-col>
              </el-col>
            </el-row>
          </el-tab-pane>
        </el-tabs>
      </template>
      <!-- <el-table :data="pvData" border fit highlight-current-row style="width: 75%">
        <el-table-column prop="key" label="Channel" />
        <el-table-column prop="pv" label="Pv" />
      </el-table> -->
      <span slot="footer" class="dialog-footer">
        <el-button type="primary" @click="dialogTableVisible = false">返回</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
import { fetchList, createArticle, updateArticle } from '@/api/article'
import waves from '@/directive/waves' // waves directive
import { parseTime } from '@/utils'
import Pagination from '@/components/Pagination' // secondary package based on el-pagination
// import InputSearch from '@/components/InputSearch'

const calendarTypeOptions = [
  { key: 'CN', display_name: 'China' },
  { key: 'US', display_name: 'USA' },
  { key: 'JP', display_name: 'Japan' },
  { key: 'EU', display_name: 'Eurozone' }
]

// arr to obj, such as { CN : "China", US : "USA" }
const calendarTypeKeyValue = calendarTypeOptions.reduce((acc, cur) => {
  acc[cur.key] = cur.display_name
  return acc
}, {})

export default {
  name: 'ComplexTable',
  components: {
    Pagination
    // InputSearch
  },
  directives: { waves },
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'info',
        deleted: 'danger'
      }
      return statusMap[status]
    },
    typeFilter(type) {
      return calendarTypeKeyValue[type]
    }
  },
  data() {
    return {
      activeName: 'first',
      tableKey: 0,
      list: null,
      total: 0,
      listLoading: true,
      listQuery: {
        page: 1,
        limit: 20,
        importance: undefined,
        title: undefined,
        type: undefined,
        sort: '+id'
      },
      importanceOptions: [1, 2, 3],
      calendarTypeOptions,
      sortOptions: [{ label: 'ID Ascending', key: '+id' }, { label: 'ID Descending', key: '-id' }],
      statusOptions: ['published', 'draft', 'deleted'],
      showReviewer: false,
      temp: {
        id: undefined,
        importance: 1,
        remark: '',
        timestamp: new Date(),
        title: '',
        type: '',
        status: 'published'
      },
      dialogFormVisible: false,
      dialogStatus: '',
      textMap: {
        update: '设备详情',
        create: '编辑设备'
      },
      dialogTableVisible: false,
      pvData: [],
      rules: {
        groupName: [{ required: true, message: 'groupName is required', trigger: 'change' }],
        timestamp: [{ type: 'date', required: true, message: 'timestamp is required', trigger: 'change' }],
        title: [{ required: true, message: 'title is required', trigger: 'blur' }]
      },
      downloadLoading: false
    }
  },
  created() {
    // this.getList()
  },
  methods: {
    // 获得数据
    getList() { // 404报错处
      this.listLoading = true
      fetchList(this.listQuery).then(response => {
        this.list = response.data.items
        this.total = response.data.total

        // 模拟请求的时间
        setTimeout(() => {
          this.listLoading = false
        }, 1.5 * 1000)
      })
    },
    // 筛选
    handleFilter() {
      this.listQuery.page = 1
      // this.getList()
    },
    handleModifyStatus(row, status) {
      this.$message({
        message: '操作Success',
        type: 'success'
      })
      row.status = status
    },
    sortChange(data) {
      const { prop, order } = data
      if (prop === 'id') {
        this.sortByID(order)
      }
    },
    sortByID(order) {
      if (order === 'ascending') {
        this.listQuery.sort = '+id'
      } else {
        this.listQuery.sort = '-id'
      }
      this.handleFilter()
    },
    resetTemp() {
      this.temp = {
        id: undefined,
        importance: 1,
        remark: '',
        timestamp: new Date(),
        title: '',
        status: 'published',
        type: ''
      }
    },
    // 新增
    handleCreate() {
      this.resetTemp()
      this.dialogStatus = 'create'
      this.dialogFormVisible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].clearValidate()
      })
    },
    createData() {
      this.$refs['dataForm'].validate((valid) => {
        if (valid) {
          this.temp.id = parseInt(Math.random() * 100) + 1024 // mock a id
          this.temp.author = 'vue-element-admin'
          createArticle(this.temp).then(() => {
            this.list.unshift(this.temp)
            this.dialogFormVisible = false
            this.$notify({
              title: 'Success',
              message: 'Created Successfully',
              type: 'success',
              duration: 2000
            })
          })
        }
      })
    },
    handleUpdate(row) {
      this.temp = Object.assign({}, row) // copy obj
      this.temp.timestamp = new Date(this.temp.timestamp)
      this.dialogStatus = 'update'
      this.dialogFormVisible = true
      this.$nextTick(() => {
        this.$refs['dataForm'].clearValidate()
      })
    },
    updateData() {
      this.$refs['dataForm'].validate((valid) => {
        if (valid) {
          const tempData = Object.assign({}, this.temp)
          tempData.timestamp = +new Date(tempData.timestamp) // change Thu Nov 30 2017 16:41:05 GMT+0800 (CST) to 1512031311464
          updateArticle(tempData).then(() => {
            const index = this.list.findIndex(v => v.id === this.temp.id)
            this.list.splice(index, 1, this.temp)
            this.dialogFormVisible = false
            this.$notify({
              title: 'Success',
              message: 'Update Successfully',
              type: 'success',
              duration: 2000
            })
          })
        }
      })
    },
    handleDelete(row, index) {
      this.$notify({
        title: 'Success',
        message: 'Delete Successfully',
        type: 'success',
        duration: 2000
      })
      this.list.splice(index, 1)
    },
    handleMoreInfo() {
      this.dialogTableVisible = true
      // fetchPv(pv).then(response => {
      //   this.pvData = response.data.pvData
      //   this.dialogTableVisible = true
      // })
    },
    // 导出
    handleDownload() {
      this.downloadLoading = true
      import('@/vendor/Export2Excel').then(excel => {
        const tHeader = ['timestamp', 'title', 'type', 'importance', 'status']
        const filterVal = ['timestamp', 'title', 'type', 'importance', 'status']
        const data = this.formatJson(filterVal)
        excel.export_json_to_excel({
          header: tHeader,
          data,
          filename: 'table-list'
        })
        this.downloadLoading = false
      })
    },
    formatJson(filterVal) {
      return this.list.map(v => filterVal.map(j => {
        if (j === 'timestamp') {
          return parseTime(v[j])
        } else {
          return v[j]
        }
      }))
    },
    getSortClass: function(key) {
      const sort = this.listQuery.sort
      return sort === `+${key}` ? 'ascending' : 'descending'
    }
  }
}
</script>

<style lang="scss">
@import '@/styles/public-styles.scss';
</style>
