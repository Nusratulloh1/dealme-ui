<template>
    <div class="default-main">
        <el-row :gutter="20">
            <el-col class="lg-mb-20" :xs="24" :sm="24" :md="24" :lg="10">
                <div class="admin-info">
                    <el-upload class="avatar-uploader" action="https://jsonplaceholder.typicode.com/posts/" :show-file-list="false">
                        <img src="~assets/images/avatar.png" class="avatar" />
                    </el-upload>
                    <div class="admin-info-base">
                        <div class="admin-nickname">{{ $t('noTitle') }}</div>
                        <div class="admin-other">
                            <div>上次登录于 2022-01-23 25:21</div>
                        </div>
                    </div>
                    <div class="admin-info-form">
                        <el-form label-position="top" :rules="rules" ref="formRef" :model="state.adminInfo">
                            <el-form-item label="用户名">
                                <el-input disabled v-model="state.adminInfo.username"></el-input>
                            </el-form-item>
                            <el-form-item label="用户昵称" prop="nickname">
                                <el-input placeholder="请输入昵称" v-model="state.adminInfo.nickname"></el-input>
                            </el-form-item>
                            <el-form-item label="邮箱地址" prop="email">
                                <el-input placeholder="请输入邮箱地址" v-model="state.adminInfo.email"></el-input>
                            </el-form-item>
                            <el-form-item label="手机号码" prop="mobile">
                                <el-input placeholder="请输入手机号码" v-model="state.adminInfo.mobile"></el-input>
                            </el-form-item>
                            <el-form-item label="签名">
                                <el-input placeholder="这家伙很懒，什么也没写" type="textarea" v-model="state.adminInfo.motto"></el-input>
                            </el-form-item>
                            <el-form-item label="新密码" prop="password">
                                <el-input type="password" placeholder="不修改请留空" v-model="state.adminInfo.password"></el-input>
                            </el-form-item>
                            <el-form-item>
                                <el-button type="primary" @click="onSubmit">保存修改</el-button>
                                <el-button @click="onResetForm">重置</el-button>
                            </el-form-item>
                        </el-form>
                    </div>
                </div>
            </el-col>
            <el-col :xs="24" :sm="24" :md="24" :lg="14">
                <el-card header="操作日志" shadow="never">
                    <el-timeline>
                        <el-timeline-item type="primary" icon="el-icon-Plus" size="large" timestamp="2018-04-12 20:46">这里是内容</el-timeline-item>
                        <el-timeline-item type="primary" icon="el-icon-Delete" size="large" timestamp="2018-04-12 20:46">这里是内容</el-timeline-item>
                        <el-timeline-item type="warning" icon="el-icon-Edit" size="large" timestamp="2018-04-12 20:46">这里是内容</el-timeline-item>
                    </el-timeline>
                </el-card>
            </el-col>
        </el-row>
    </div>
</template>

<script setup lang="ts">
import { ref, reactive } from 'vue'
import { useI18n } from 'vue-i18n'

const { t } = useI18n()
const formRef = ref()

const state: {
    adminInfo: any
} = reactive({
    adminInfo: {
        avatar: '',
        username: '',
        nickname: '',
        email: '',
        mobile: '',
        motto: '',
        password: '',
    },
})

const rules: any = reactive({
    nickname: [
        {
            required: true,
            message: t('adminLogin.Please enter an account'),
            trigger: 'blur',
        },
        {
            min: 3,
            message: t('adminLogin.Account length must be greater than 3 digits'),
            trigger: 'blur',
        },
    ],
    email: [
        {
            type: 'email',
            message: '请输入正确的邮箱地址',
            trigger: 'blur',
        },
    ],
    mobile: [
        {
            type: 'email',
            message: '请输入正确的手机号码',
            trigger: 'blur',
        },
    ],
    password: [
        {
            required: true,
            message: t('adminLogin.Please input a password'),
            trigger: 'blur',
        },
        {
            min: 6,
            max: 32,
            message: t('adminLogin.Password length must be between 6 and 32 bits'),
            trigger: 'blur',
        },
    ],
})

const onSubmit = () => {}

const onResetForm = () => {}
</script>

<style scoped lang="scss">
.admin-info {
    background-color: #fff;
    border-radius: var(--el-border-radius-base);
    border-top: 3px solid #d63c31;
    .avatar-uploader {
        display: flex;
        align-items: center;
        justify-content: center;
        position: relative;
        margin: 60px auto 10px auto;
        border-radius: 50%;
        box-shadow: var(--el-box-shadow-light);
        border: 1px dashed var(--color-sub-1);
        cursor: pointer;
        overflow: hidden;
        width: 110px;
        height: 110px;
    }
    .avatar-uploader:hover {
        border-color: var(--color-primary);
    }
    .avatar {
        width: 110px;
        height: 110px;
        display: block;
    }
    .admin-info-base {
        .admin-nickname {
            font-size: 22px;
            color: var(--color-text-primary);
            text-align: center;
            padding: 8px 0;
        }
        .admin-other {
            color: var(--color-regular);
            font-size: 14px;
            text-align: center;
            line-height: 20px;
        }
    }
    .admin-info-form {
        padding: 30px;
    }
}
.el-card :deep(.el-timeline-item__icon) {
    font-size: 10px;
}
@media screen and (max-width: 1200px) {
    .lg-mb-20 {
        margin-bottom: 20px;
    }
}
</style>
