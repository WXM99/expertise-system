<template>
    <div>
        <navi></navi>
        <div style="margin-top: 10px">
            <el-form  label-width="100px">
                <el-row :gutter="20">
                    <el-col :span="6">
                        <el-form-item label="姓名">
                            <el-input v-model="name" ></el-input>
                        </el-form-item>
                    </el-col>
                    <el-col :span="6">
                        <el-form-item label="证件号">
                            <el-input v-model="id" ></el-input>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4">
                        <el-form-item label="是否机密">
                            <el-select v-model="secretFlag" @change="getService" placeholder="请选择">
                                <el-option label="是" value="是"></el-option>
                                <el-option label="否" value="否"></el-option>
<!--                                <el-option label="其他" value=" "></el-option>-->
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="6">
                        <el-form-item label="密级">
                            <el-select v-model="secret" :disabled="secretshow" placeholder="请选择">
                                <el-option
                                        v-for="item in secretoptions"
                                        :key="item.value"
                                        :label="item.label"
                                        :value="item.value">
                                </el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="6" style="align-items: end">
                        <el-form-item label="电话">
                            <el-input v-model="phone" ></el-input>
                        </el-form-item>
                    </el-col>
                    <el-col :span="6" style="align-items: end">
                        <el-form-item label="类型">
                            <el-select v-model="type" clearable placeholder="请选择">
                                <el-option label="专业" value="专业"></el-option>
                                <el-option label="财务" value="财务"></el-option>
                                <el-option label="其他" value="其他"></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="4">
                        <el-form-item label="性别">
                            <el-select v-model="gender" clearable placeholder="请选择">
                                <el-option label="男" value="男"></el-option>
                                <el-option label="女" value="女"></el-option>
                                <el-option label="其他" value=" "></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                </el-row>
                <el-form-item label="单位">
                    <el-input v-model="company" ></el-input>
                </el-form-item>
                <el-row :gutter="20">
                    <el-col :span="6">
                        <el-form-item label="出生日期">
                            <el-date-picker
                                    v-model="birth"
                                    type="date"
                                    placeholder="选择日期">
                            </el-date-picker>
                        </el-form-item>
                    </el-col>
                    <el-col :span="6">
                        <el-form-item label="主领域">
                            <el-select v-model="firstArea" filterable placeholder="请选择">
                                <el-option label="集成电路" value="集成电路"></el-option>
                                <el-option label="人工智能" value="人工智能"></el-option>
                                <el-option label="生物医药" value="生物医药"></el-option>
                                <el-option label="网络空间" value="网络空间"></el-option>
                                <el-option label="新能源" value="新能源"></el-option>
                                <el-option label="核能" value="核能"></el-option>
                                <el-option label="航天" value="航天"></el-option>
                                <el-option label="航空" value="航空"></el-option>
                                <el-option label="船舶（含海洋工程）" value="船舶（含海洋工程）"></el-option>
                                <el-option label="电子信息" value="电子信息"></el-option>
                                <el-option label="新材料" value="新材料"></el-option>
                                <el-option label="智能装备" value="智能装备"></el-option>
                                <el-option label="应急" value="应急"></el-option>
                                <el-option label="空间信息（含北斗导航）" value="空间信息（含北斗导航）"></el-option>
                                <el-option label="其他（含财务）" value="其他（含财务）"></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="6">
                        <el-form-item label="副领域">
                            <el-select v-model="secondaryArea" filterable multiple placeholder="请选择">
                                <el-option label="集成电路" value="集成电路"></el-option>
                                <el-option label="人工智能" value="人工智能"></el-option>
                                <el-option label="生物医药" value="生物医药"></el-option>
                                <el-option label="网络空间" value="网络空间"></el-option>
                                <el-option label="新能源" value="新能源"></el-option>
                                <el-option label="核能" value="核能"></el-option>
                                <el-option label="航天" value="航天"></el-option>
                                <el-option label="航空" value="航空"></el-option>
                                <el-option label="船舶（含海洋工程）" value="船舶（含海洋工程）"></el-option>
                                <el-option label="电子信息" value="电子信息"></el-option>
                                <el-option label="新材料" value="新材料"></el-option>
                                <el-option label="智能装备" value="智能装备"></el-option>
                                <el-option label="应急" value="应急"></el-option>
                                <el-option label="空间信息（含北斗导航）" value="空间信息（含北斗导航）"></el-option>
                                <el-option label="其他（含财务）" value="其他（含财务）"></el-option>
                            </el-select>
                        </el-form-item>
                    </el-col>
                    <el-col :span="9">
                        <el-form-item label="简介">
                            <el-input v-model="introduction" ></el-input>
                        </el-form-item>
<!--                        <p>{{firstArea+secondaryArea}}</p>-->
                    </el-col>
                </el-row>
                <el-form-item>
                    <el-button type="primary" @click="submitForm()">立即创建</el-button>
                    <el-button @click="resetForm()">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
    import navi from "../../components/navi";
    export default {
        name: "edit",
        components: {navi},
        data(){
            return{
                id:'',
                name:'',
                phone:'',
                gender:'',
                secret:'',
                company:'',
                type:'',
                area:'',
                firstArea:'',
                secondaryArea:'',
                introduction:'',
                birth:'',
                secretoptions: [{
                    value: '一般',
                    label: '一般'
                }, {
                    value: '重要',
                    label: '重要'
                }],
                value: '',
                secretFlag:'',
                secretshow:''
            }
        },
        methods:{
            getService(){
                // this.secretFlag=!this.secretFlag;
                if (this.secretFlag==='是') this.secretshow=false
                else this.secretshow=true
                this.$forceUpdate()
            },
            resetForm(){
                this.birth='',
                    this.id='',
                    this.name='',
                    this.phone='',
                    this.gender='',
                    this.secret='',
                    this.secretFlag='',
                    this.secretshow='',
                    this.company='',
                    this.type='',
                    this.area='',
                    this.firstArea='',
                    this.secondaryArea='',
                    this.introduction='',
                    this.birth=''
            },
            submitForm(){
                // let that = this
                this.area=this.firstArea+','+this.secondaryArea
               let data = {
                   id:this.id,
                    name: this.name,
                    phone: this.phone,
                   gender: this.gender,
                   secret: this.secret,
                   company:this.company,
                   type: this.type,
                   area:this.area,
                   introduction:this.introduction,
                   birth: this.birth
                }
                var url = 'http://localhost:8080/expert/insert/'
                this.$http({
                    method: 'post',
                    url: url,
                    headers: {
                        'Access-Control-Allow-Credentials': true,
                        'Access-Control-Allow-Origin': true,
                        'Content-Type': 'application/json'
                    },
                    data: JSON.stringify(data)
                })
                    .then(response => {
                        console.log(response.data)
                        console.log('get response')
                        //redirect
                        this.$router.push({path: '/expert'})
                    })
                    .catch(error => {
                        JSON.stringify(error)
                        console.log(error)
                    })
            }
        }
    }
</script>

<style scoped>

</style>