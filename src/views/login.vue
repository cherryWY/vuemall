<template>
<div class="login-wrap">
    <el-form class="login-form" label-position="top" label-width="80px">
        <h2>用户登录</h2>
        <el-form-item label="用户名">
            <el-input v-model="formdata.username"></el-input>
        </el-form-item>
        <el-form-item label="密码">
            <el-input v-model="formdata.password"></el-input>
        </el-form-item>
        <el-button @click="handlelogin()" class="login-button" type="primary">登陆</el-button>
    </el-form>
</div>
</template>

<script>
export default {
    data() {
        return {
            formdata: {
                username: '',
                password: ''
            }
        }
    },
    methods: {
        async handlelogin() {
            const res = await this.$http.post('login', this.formdata)

            const {
                meta
            } = res.data

            if (meta.status === 200) {

              console.log(res);
              

                const token = res.data.data.token
                sessionStorage.setItem('token', token)
                this.$message.success(meta.msg);
                this.$router.push({
                    name: 'home'
                })
            } else {
                this.$message.error(meta.msg);
            }

            // .then((res) => {
            //     console.log(res);
            //     const {
            //         meta
            //     } = res.data

            //     if (meta.status === 200) {
            //         this.$message.success(meta.msg);
            //         this.$router.push({
            //             name: 'home'
            //         })
            //     } else {
            //         this.$message.error(meta.msg);
            //     }
            // })
        }
    }
}
</script>

<style>
.login-wrap {
    background-color: #324152;
    height: 100%;
    display: flex;
    justify-content: center;
    align-items: center;
}

.login-wrap .login-form {
    background-color: #fff;
    width: 400px;
    padding: 30px;
    border-radius: 5px;
}

.login-wrap .login-form .login-button {
    width: 100%;
}
</style>
