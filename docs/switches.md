# Переключатели
Нексту манфу, говорит нам писатель статьи о свичах.

Будем считать, что дорогой читатель уже ознакомился с разделом в FAQ, рассказывающим об [основных типах переключателей](https://rumech.guide/#/FAQ?id=%d0%9a%d0%b0%d0%ba%d0%b8%d0%b5-%d0%bf%d0%b5%d1%80%d0%b5%d0%ba%d0%bb%d1%8e%d1%87%d0%b0%d1%82%d0%b5%d0%bb%d0%b8-%d0%bc%d0%bd%d0%b5-%d0%bf%d0%be%d0%b4%d1%85%d0%be%d0%b4%d1%8f%d1%82) и понимает что нет свичей исключительно для гейминга, программирования или набора текста.

## Классификация
**Классическое деление по ощущению от нажатия и производимому звуку:**
* Не тактильные - линейные (linear)
* Тактильные (tactile)
  * Тихие - обычные тактильные
  * Кликающие или щёлкающие (clicky)

**По внутреннему устройству и форм-фактору:**
* Cherry MX
  * Классические полноразмерные (оригинальные Cherry MX и копии)
  * Компактные (начали разрабатываться в одно время, поэтому все **(?)** являются оригинальными разработками)
* Alps (оригинальные и копии)
* Мембранные
  * Плёночные (обычные мембранные, ножничные и "бабочка" Apple)
  * Topre (оригинальные в Realforce и HHKB, копии в клавиатурах Plum)
* Самобытные
  * IBM Buckling spring

**По типу механизма регистрации нажатий:**
* Дискретные переключатели с подпружиненным штоком
  * Замыкание металлической контактной пары
  * Срабатывание бесконтактного датчика (оптического, магнитного, емкостного)
* Мембранные (плёночные)
* Topre - емкостные, гибрид мембраны и дискретного переключателя
* Самобытные
  * IBM Buckling spring

**A basic sample4:**

  ```html
  /*vue*/
  <template>
    <div>
      <div style="margin-bottom: 10px">
        <el-row>
          <el-col :span="18">
            <el-button @click="onCreate">create 1 row</el-button>
            <el-button @click="onCreate100">create 100 row</el-button>
            <el-button @click="bulkDelete">bulk delete</el-button>
          </el-col>

          <el-col :span="6">
            <el-input placeholder="search NO." v-model="filters[0].value"></el-input>
          </el-col>
        </el-row>
      </div>

      <data-tables :data="data" :action-col="actionCol" :filters="filters" @selection-change="handleSelectionChange">
        <el-table-column type="selection" width="55">
        </el-table-column>

        <el-table-column v-for="title in titles" :prop="title.prop" :label="title.label" :key="title.prop" sortable="custom">
        </el-table-column>
      </data-tables>
    </div>
  </template>

  <script>
  export default {
    data() {
      return {
        data,
        titles,
        filters: [{
          prop: 'flow_no',
          value: ''
        }],
        actionCol: {
          props: {
            label: 'Actionssss',
          },
          buttons: [{
            props: {
              type: 'primary'
            },
            handler: row => {
              this.$message('Edit clicked')
              row.flow_no = 'hello word' + Math.random()
              row.content = Math.random() > 0.5 ? 'Water flood' : 'Lock broken'
              row.flow_type = Math.random() > 0.5 ? 'Repair' : 'Help'
            },
            label: 'Edit'
          }, {
            handler: row => {
              this.data.splice(this.data.indexOf(row), 1)
              this.$message('delete success')
            },
            label: 'delete'
          }]
        },
        selectedRow: []
      }
    },
    methods: {
      onCreate() {
        this.data.push({
          content: "new created",
          flow_no: "FW201601010003" + Math.floor(Math.random() * 100),
          flow_type: "Help",
          flow_type_code: "help"
        })
      },
      onCreate100() {
        [...new Array(100)].map(_ => {
          this.onCreate()
        })
      },
      handleSelectionChange(val) {
        this.selectedRow = val
      },
      bulkDelete() {
        this.selectedRow.map(row => {
          this.data.splice(this.data.indexOf(row), 1)
        })
        this.$message('bulk delete success')
      }
    }
  }
  </script>
  ```
