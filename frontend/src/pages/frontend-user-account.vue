<template>
    <div class="main wrap clearfix">
        <div class="main-left">
            <div class="home-feeds cards-wrap">
                <div class="settings-main card">
                    <div class="settings-main-content">
                        <a-input title="User name">
                            <input type="text" v-model="form.username" placeholder="User name" class="base-input" name="username">
                            <span class="input-info error">Please input username</span>
                        </a-input>
                        <a-input title="Email">
                            <input type="text" v-model="form.email" placeholder="Email" class="base-input" name="email">
                            <span class="input-info error">Please input email</span>
                        </a-input>
                    </div>
                    <!-- <div class="settings-footer clearfix">
                        <a href="javascript:;" class="btn btn-blue">Save</a>
                    </div> -->
                </div>
            </div>
        </div>
        <div class="main-right">
            <account></account>
        </div>
    </div>
</template>

<script lang="babel">
import api from '~api'
import account from '../components/aside-account.vue'
import aInput from '../components/_input.vue'
export default {
    data() {
        return {
            form: {
                username: '',
                email: ''
            }
        }
    },
    components: {
        account,
        aInput
    },
    methods: {
        async getUser() {
            const { data: { code, data} } = await api.get('frontend/user/account')
            if (code === 200) {
                this.form.username = data.username
                this.form.email = data.email
            }
        }
    },
    mounted() {
        this.getUser()
    },
    metaInfo () {
        return {
            title: 'Blog',
            meta: [{ vmid: 'description', name: 'description', content: 'Blog by Vue' }]
        }
    }
}
</script>
