<template>
    <div>
        <select v-model="prov">
            <option v-for="option in arr" :value="option.name">
                {{ option.name }}
            </option>
        </select>
        <select v-model="city">
            <option v-for="option in cityArr" :value="option.name">
                {{ option.name }}
            </option>
        </select>
        <select v-model="district" v-if="district">
            <option v-for="option in districtArr" :value="option.name">
                {{ option.name }}
            </option>
        </select>
    </div>
</template>

<script type="text/javascript">
let arrAll = [
            {name: "选择省份", sub: [{name: "请选择"}], type: 1},
            {
                name: "北京",
                sub: [
                    {name: "请选择", sub: []},
                    {
                        name: "北京",
                        sub: [{name: "请选择"}, {name: "东城区"}, {name: "西城区"}, {name: "崇文区"}, {name: "宣武区"}, {name: "朝阳区"}, {name: "海淀区"}, {name: "丰台区"}, {name: "石景山区"}, {name: "房山区"}, {name: "通州区"}, {name: "顺义区"}, {name: "昌平区"}, {name: "大兴区"}, {name: "怀柔区"}, {name: "平谷区"}, {name: "门头沟区"}, {name: "密云县"}, {name: "延庆县"}, {name: "其他"}],
                        type: 0
                    }], type: 1
            },
]
export default {
    data() {
        return {
            arr: arrAll,
            prov: '北京',
            city: '北京',
            district: '东城区',
            cityArr: [],
            districtArr: []   
        }
    },
    methods: {
        updateCity: function () {
            for (var i in this.arr) {
                var obj = this.arr[i];
                if (obj.name == this.prov) {
                    this.cityArr = obj.sub;
                    break;
                }
            }
            this.city = this.cityArr[1].name;
        },
        updateDistrict: function () {
            for (var i in this.cityArr) {
                var obj = this.cityArr[i];
                if (obj.name == this.city) {
                    this.districtArr = obj.sub;
                    break;
                }
            }
            if(this.districtArr && this.districtArr.length > 0 && this.districtArr[1].name) {
                this.district = this.districtArr[1].name;
            } else {
                this.district = '';
            }
        }
    },
    beforeMount: function () {
        this.updateCity();
        this.updateDistrict();
    },
    watch: {
        prov: function () {
            this.updateCity();
            this.updateDistrict();
        },
        city: function () {
            this.updateDistrict();
        }
    }
}
</script>