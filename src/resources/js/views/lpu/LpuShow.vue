<template>
    <main-layout>
        <a href="/lpu/create" style="text-decoration: none;">новая версия</a>
        <a :href="'/api/v1/lpu/' + this.$route.params.id + '/download'" style="text-decoration: none; margin-left: 10px; color: #0b2e13">скачать</a>


        <lpu-form :file="file" :version="version" @save="saveEvent($event)"></lpu-form>
    </main-layout>
</template>

<script>
import MainLayout from "../layouts/MainLayout";
import LpuForm from "../../components/lpu/LpuForm";
import ButtonGreen from "../../components/UI/ButtonGreen";

export default {
    name: "LpuShow",
    components: {ButtonGreen, LpuForm, MainLayout},
    data() {
        return {
            lpu: [],
            file: null,
            version: '',
        }
    },
    methods: {
        async fileRequest() {
            return await axios.get('/api/v1/lpu/' + this.$route.params.id);
        },
        getFile() {
            this.fileRequest().then(response => {
                if (response.data.success === true) {
                    this.file = response.data.data.file;
                    this.version = response.data.data.version;
                }
            })
        },
        saveEvent($event) {
            this.lpu = $event.lpu;
            this.version = $event.version;
            this.lpuUpdate();
        },
        async lpuUpdateRequest() {
            return axios.put('/api/v1/lpu/' + this.$route.params.id + '/update', {lpu: this.lpu, version:this.version});
        },
        lpuUpdate() {
            this.lpuUpdateRequest().then(response => {
                if (response.data.success === true) {
                    if (Number(this.$route.params.id) !== Number(response.data.data.id)) {
                        window.location.href = '/lpu/' + response.data.data.id;
                    } else {
                        alert('Сохранено!')
                    }
                } else {
                    console.log('LpuShow error lpu update ', response.data)
                }
            })
        }
    },
    mounted() {
        let token = document.head.querySelector('meta[name="csrf-token"]');
        if (token) {
            window.axios.defaults.headers.common['X-CSRF-TOKEN'] = token.content;
        }
        this.getFile();
    }
}
</script>

<style scoped>

</style>
