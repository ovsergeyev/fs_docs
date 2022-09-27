<template>
    <div v-if="hideAfterSearch" class="block">
        Content
    </div>
</template>

<script>

export default {
    components: {
    },
    props: {
        content: {},
        hidden_search: {
            type: Boolean,
            default: false
        },
        title: {
            type: String,
            default: null
        }
    },
    data() {
        return {
            hideAfterSearch: true,
        }
    },
    async mounted() {
        this.setBlockParams()
        //Скрытие блока после поиска (если настройка включена в geoCMS)
        if(this.hidden_search){
            eventBus.$on('searchComplite', ()=>{
                this.hideAfterSearch = true
            })
        }
    },
    methods: {
        setBlockParams(){
            try{
                let content = {}
                try { content =  JSON.parse(this.content) }catch (e){}
                console.log('content', content)

            } catch (e) {
                console.log('Ошибка в методе setBlockParams', e)
            }
        },
    },
}
</script>

<style scoped lang="scss">
@import "../../../../sass/colors";


</style>
