<template>
    <div class="select-input":style="{width: typeof width === 'number'? width+'px': width}">
        <input
                class="input-inner"
                type="text"
                ref="input"
                @click="showList"
                :value="selectVal"
                :placeholder="placeholder"
                readonly
        >
        <i class="icon" @click="showList"></i>
        <scrollbar :style="{height:height}" class='dropdown' v-if="isShow">
            <ul>
                <li class="dropdown-item"
                    :class="[selectOption == option ? 'lightheight' : '',i+1 != options.length ? 'drapdown-item-line':''] "
                    v-for="(option,i) in options"
                    :key="typeof option === 'object' ? option[selectKey] : option"
                    @click="handleSelectOption(option)"
                >{{typeof option === 'object' ? option[selectName] : option}}</li>
            </ul>
        </scrollbar>


    </div>
</template>

<script>
    import scrollbar from 'vue-scrollbar_gaoshuai/dist/vue-scrollbar.min';
    export default {
        name:'VSelect',
        props: {
            value: [String,Number],
            options: Array,
            placeholder: String,
            selectKey: String,
            selectName: String,
            width: {type:[String,Number],default:'200px'},
            height: {type:[String,Number],default:'200px'}
        },
        data () {
            return {
                isShow: false,
                selectOption: null
            }
        },
        components: {scrollbar},
        computed: {
            selectVal () {
                if (!this.selectOption) {
                    return null
                }
                return typeof this.selectOption ==='object' ? this.selectOption[this.selectName] :this.selectOption
            }
        },
        created () {
            this.getSelectOption(this.value)
        },
        watch: {
            value: function () {
                this.getSelectOption(this.value)
            },
            options: function () {
                this.getSelectOption(this.value)
            }
        },
        methods: {
            handleSelectOption: function (option){
                this.selectOption = option
                this.isShow ? this.isShow = false : this.isShow = true
                this.$emit('input', typeof this.selectOption ==='object' ? this.selectOption[this.selectKey] :this.selectOption)
                this.$emit('change')
            },
            showList: function(){
                this.isShow ? this.isShow = false : this.isShow = true
                document.addEventListener('click', this.clickOutside, false)
            },
            clickOutside: function(event){
                if(this.$el && !this.$el. contains(event.target)) {
                    this.isShow = false
                }
            },
            getSelectOption: function (value) {
                if(!value){
                    this.selectOption =null;
                    return
                }
                for(var i = 0; i < this.options.length; i++){
                    if(value === this.options[i][this.selectKey]){
                        this.selectOption = this.options[i];
                        break;
                    }
                }
            }
        }
    }
</script>

<style scoped>
    ul,ul li{
        list-style: none;
        margin: 0;
        padding: 0;
    }
    .select-input{
        position: relative;
        height: 2.8rem;
    }
    .input-inner{
        color: #606266;
        display: inline-block;
        width: 100%;
        height: 100%;
        box-sizing: border-box;
        border: 0.1rem solid #b8e8ff;
        border-radius: 2rem;
        padding: 0 1.5rem;
        font-weight: bold;
        outline: none;
        font-size: 12px;
    }
    .icon{
        width: 1.5rem;
        height: 100%;
        line-height: 3rem;
        position: absolute;
        right: 8px;
        top:0;
        background: url(./select-icon.png) center no-repeat;
    }
    .dropdown{
        width: 100%;
        position: absolute;
        top: 2.8rem;
        background: #fff;
        z-index: 100;
        border: 1px solid #fff;
        border-radius:  5px;
        box-shadow:2px 3px 5px rgba(167, 142, 142, 0.1);
    }

    .dropdown-item{

        height: 40px;
        line-height: 40px;
        padding: 0 20px;
        overflow: hidden;
        white-space: normal;
        text-overflow: ellipsis;
    }
    .dropdown-item.drapdown-item-line:after{
        content: '';
        display: block;
        width: 100%;
        height: 0;
        background: #fff;
        /*border-bottom: 1px solid #e5e5e5;*/
    }
    .dropdown-item.lightheight{
        color:#109eff;
    }
    .dropdown-item:hover{
        background: #f5f7fa;
    }
</style>
