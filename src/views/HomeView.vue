<script>

import axios from "axios";

export default {
    name: 'restAPI',
    data() {
        return {
            accounts: [],
            eventResult: {},
        }
    },
    methods: {
        async getMain() {
            const config = {
                headers: {
                    "Content-Type": "application/json"
                }, params: {},
            };

            const result = await axios.get('http://localhost:21010/client/v1/display/get-main-menu?cache=true', config)
            console.log(result.data.mainMenu.accounts);
            this.accounts = result.data.mainMenu.accounts;
        },
        async getEvent(eventNo) {
            const config = {
                headers: {
                    "Content-Type": "application/json"
                }, params: {
                    order: 'ADMIN_SETTING',
                    soldout: true
                },
            };

            const result = await axios.get(`http://localhost:21010/client/v1/display/get-main-menu/product/${eventNo}`, config)
            console.log(result.data);
            this.eventResult = result.data;
        },

    },
    created() {
        this.getMain().then(() => {
            this.accounts.forEach(account => account.banners.forEach(
                banner => {
                    this.getEvent(banner.landingUrl);
                }
            ))
        });


    }
}
</script>

<template>
    <main>
        <div v-for="account in accounts" :key="account.name">
            {{ account.accountName }}
        </div>

        <div v-for="event in eventResult" :key="event.section">
            {{event.section}}
        </div>
    </main>
</template>
