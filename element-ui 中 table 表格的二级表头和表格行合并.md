# element-ui 中 table 表格的二级表头和表格行合并

#### 一、二级表头

> 只需要在 el-table-column 里面嵌套 el-table-column，就可以实现多级表头。

```vue
<template>
    <div>
        <el-table
            :data="tableData"
            border
            style="width: 100%"
            align="center"
            size="mini"
        >
            <el-table-column
                prop="on"
                label="序号"
                align="center"
                width="60"
                fixed
            >
            </el-table-column>
            <el-table-column
                prop="title"
                label="系统名称"
                header-align="center"
                width="160"
                fixed
            >
            </el-table-column>
            <el-table-column
                prop="type"
                label="系统级别"
                align="center"
                width="100"
            >
            </el-table-column>
            <el-table-column label="主要问题" align="center">
                <el-table-column
                    prop="reportGrade"
                    label="等级"
                    align="center"
                    width="70"
                >
                    <template slot-scope="scope">
                        <span
                            style="color: #f04134;"
                            v-if="scope.row.reportGrade == 1"
                        >
                            高
                        </span>
                        <span
                            style="color: #ffbf00;"
                            v-else-if="scope.row.reportGrade == 2"
                        >
                            中
                        </span>
                        <span
                            style="color: #00a854;"
                            v-else-if="scope.row.reportGrade == 3"
                        >
                            低
                        </span>
                        <span v-else>暂无</span>
                    </template>
                </el-table-column>
                <el-table-column
                    prop="reportComments"
                    label="问题描述"
                    header-align="center"
                    min-width="200"
                >
                    <template slot-scope="scope">
                        <span v-if="scope.row.reportComments !== ''">
                            {{ scope.row.reportComments }}
                        </span>
                        <div style="text-align: center;" v-else>暂无</div>
                    </template>
                </el-table-column>
                <el-table-column label="操作" align="center" width="50">
                    <template slot-scope="scope">
                        <el-button
                            type="text"
                            size="mini"
                            style="color:red;"
                            @click="remove(scope.row, scope.$index)"
                        >
                            删除
                        </el-button>
                    </template>
                </el-table-column>
            </el-table-column>
        </el-table>
    </div>
</template>
```

#### 二、表格合并

> 通过给 table 传入 span-method 方法可以实现合并行或列，方法的参数是一个对象，里面包含当前行 row、当前列 column、当前行号 rowIndex、当前列号 columnIndex 四个属性。该函数可以返回一个包含两个元素的数组，第一个元素代表 rowspan，第二个元素代表 colspan。 也可以返回一个键名为 rowspan 和 colspan 的对象。

```vue
<template>
    <div>
        <el-table
            :data="tableData"
            border
            style="width: 100%"
            align="center"
            size="mini"
            :span-method="objectSpanMethod"
        >
            <el-table-column
                prop="on"
                label="序号"
                align="center"
                width="60"
                fixed
            >
            </el-table-column>
            <el-table-column
                prop="title"
                label="系统名称"
                header-align="center"
                width="160"
                fixed
            >
            </el-table-column>
            <el-table-column
                prop="type"
                label="系统级别"
                align="center"
                width="100"
            >
            </el-table-column>
            <el-table-column
                prop="number"
                label="备案编号"
                align="center"
                width="140"
            >
                <template slot-scope="scope">
                    <span v-if="scope.row.number">
                        {{ scope.row.number }}
                    </span>
                    <span v-else>暂无</span>
                </template>
            </el-table-column>
            <el-table-column
                prop="reportnumber"
                label="报告编号"
                align="center"
                width="220"
            >
                <template slot-scope="scope">
                    <span v-if="scope.row.reportnumber">
                        {{ scope.row.reportnumber }}
                    </span>
                    <span v-else>暂无</span>
                </template>
            </el-table-column>
            <el-table-column
                prop="reportauthotr"
                label="编制人"
                align="center"
                width="60"
            >
                <template slot-scope="scope">
                    <span v-if="scope.row.reportauthotr">
                        {{ scope.row.reportauthotr }}
                    </span>
                    <span v-else>暂无</span>
                </template>
            </el-table-column>
            <el-table-column
                prop="reporttime"
                label="时间"
                align="center"
                width="140"
            >
                <template slot-scope="scope">
                    <span v-if="scope.row.reporttime">
                        {{ scope.row.reporttime }}
                    </span>
                    <span v-else>暂无</span>
                </template>
            </el-table-column>
            <el-table-column prop="grade" label="测评结论" align="center">
                <template slot-scope="scope">
                    <span style="color: #00a854;" v-if="scope.row.grade == 1"
                        >优</span
                    >
                    <span
                        style="color: #0e77d1;"
                        v-else-if="scope.row.grade == 2"
                        >良</span
                    >
                    <span
                        style="color: #ffbf00;"
                        v-else-if="scope.row.grade == 3"
                        >中</span
                    >
                    <span
                        style="color: #f04134;"
                        v-else-if="scope.row.grade == 4"
                        >差</span
                    >
                    <span v-else>暂无</span>
                </template>
            </el-table-column>
            <el-table-column
                prop="score"
                label="测评得分"
                align="center"
                width="70"
            >
                <template slot-scope="scope">
                    <span v-if="scope.row.score > 0">{{
                        scope.row.score
                    }}</span>
                    <span v-else>暂无</span>
                </template>
            </el-table-column>
            <el-table-column label="主要问题" align="center">
                <el-table-column
                    prop="reportGrade"
                    label="风险等级"
                    align="center"
                    width="70"
                >
                    <template slot-scope="scope">
                        <span
                            style="color: #f04134;"
                            v-if="scope.row.reportGrade == 1"
                            >高</span
                        >
                        <span
                            style="color: #ffbf00;"
                            v-else-if="scope.row.reportGrade == 2"
                            >中</span
                        >
                        <span
                            style="color: #00a854;"
                            v-else-if="scope.row.reportGrade == 3"
                            >低</span
                        >
                        <span v-else>暂无</span>
                    </template>
                </el-table-column>
                <el-table-column
                    prop="reportComments"
                    label="问题描述"
                    header-align="center"
                    min-width="200"
                >
                    <template slot-scope="scope">
                        <span v-if="scope.row.reportComments !== ''">{{
                            scope.row.reportComments
                        }}</span>
                        <div style="text-align: center;" v-else>暂无</div>
                    </template>
                </el-table-column>
                <el-table-column label="操作" align="center" width="50">
                    <template slot-scope="scope">
                        <el-button
                            type="text"
                            size="mini"
                            style="color:red;"
                            @click="remove(scope.row, scope.$index)"
                        >
                            删除
                        </el-button>
                    </template>
                </el-table-column>
            </el-table-column>
            <el-table-column label="操作" align="center" width="80">
                <template slot-scope="scope">
                    <el-button
                        type="text"
                        size="mini"
                        @click="editSystem(scope.row)"
                        >编辑系统</el-button
                    >
                </template>
            </el-table-column>
        </el-table>
    </div>
</template>

<script>
import { getSystemList } from "@/api/project";
export default {
    data() {
        return {
            tableData: [],
        };
    },
    mounted() {
        this.getList();
    },
    methods: {
        getList() {
            getSystemList(this.$route.query.id).then((res) => {
                this.options = res.data;
                // 格式化数据
                this.tableData = this.formatData(res.data);
            });
        },
        // 表格合并函数
        objectSpanMethod({ row, columnIndex }) {
            // 合并前 9 行和第 12 行
            if (columnIndex < 9 || columnIndex == 12) {
                if (row.reportLength > 0) {
                    return {
                        rowspan: row.reportLength,
                        colspan: row.reportLength > 0 ? 1 : 0,
                    };
                } else {
                    return {
                        rowspan: 0,
                        colspan: 0,
                    };
                }
            }
        },
        // 数据格式化
        formatData(data) {
            let arr = [];
            let on = 0; // 表格序号
            for (let i = 0; i < data.length; i++) {
                if (data[i].reporttime) {
                    // 格式化时间为: 2020-11-12 14:07:01
                    data[i].reporttime = this.dataTime(
                        data[i].reporttime * 1000
                    );
                }
                let dataChildren = data[i].report;
                on++;
                if (dataChildren.length) {
                    for (let j = 0; j < dataChildren.length; j++) {
                        let obj = {
                            on: on,
                            grade: data[i].grade,
                            id: data[i].id,
                            number: data[i].number,
                            reportauthotr: data[i].reportauthotr,
                            reportnumber: data[i].reportnumber,
                            reporttime: data[i].reporttime,
                            score: data[i].score,
                            title: data[i].title,
                            type: data[i].type,
                            // 当表格需要合并时，表格需要合并的行就是 dataChildren 的长度
                            reportLength: j === 0 ? dataChildren.length : 0,
                            reportId: dataChildren[j].id,
                            reportGrade: dataChildren[j].grade,
                            reportComments: dataChildren[j].comments,
                        };
                        arr.push(obj);
                    }
                } else {
                    let obj = {
                        on: on,
                        grade: data[i].grade,
                        id: data[i].id,
                        number: data[i].number,
                        reportauthotr: data[i].reportauthotr,
                        reportnumber: data[i].reportnumber,
                        reporttime: data[i].reporttime,
                        score: data[i].score,
                        title: data[i].title,
                        type: data[i].type,
                        // 当表格没有需要合并的行时，表格需要独占一行，reportLength 不能设为 0，reportLength 设为 0 时，表格中的行会出现错乱的情况
                        reportLength: 1,
                        reportId: "",
                        reportGrade: "",
                        reportComments: "",
                    };
                    arr.push(obj);
                }
            }
            return arr;
        },
        // 时间格式化函数
        dataTime(time) {
            let date = new Date(+time + 8 * 3600 * 1000);
            return date
                .toJSON()
                .substr(0, 19)
                .replace("T", " ")
                .replace(/-/g, "-");
        },
    },
};
</script>
```
