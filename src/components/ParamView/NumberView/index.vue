<template>
    <div class="number-view">
        <div class="param">
            <div class="state">
                <div class="label">{{ label }}:</div>
                <input
                    type="text"
                    class="value"
                    v-bind:value="value"
                    v-on:input="handleChange"
                    :data-pname="pname"
                />
            </div>

            <div class="block">
                <input
                    type="range"
                    class="range"
                    :min="min"
                    :max="max"
                    :step="step"
                    v-bind:value="value"
                    v-on:input="handleChange"
                    :data-pname="pname"
                />
                <!-- <el-slider
                    v-bind:value="value"
                    class="range"
                    :min="min"
                    :max="max"
                    :step="step"
                    @change="handleSlide"
                    :data-pname="pname"
                ></el-slider> -->
                <i
                    class="el-icon-s-tools setting"
                    @click="configVisible = !configVisible"
                ></i>
            </div>

            <div class="config" v-if="configVisible">
                <div class="row">
                    <div class="label">最小值:</div>
                    <input
                        type="text"
                        class="value"
                        v-bind:value="min"
                        v-on:input="handleSetting"
                        data-pname="min"
                    />
                </div>

                <div class="row">
                    <div class="label">最大值:</div>
                    <input
                        type="text"
                        class="value"
                        v-bind:value="max"
                        v-on:input="handleSetting"
                        data-pname="max"
                    />
                </div>

                <div class="row">
                    <div class="label">步长:</div>
                    <input
                        type="text"
                        class="value"
                        v-bind:value="step"
                        v-on:input="handleSetting"
                        data-pname="step"
                    />
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import GameEvent from "@/core/event/index";

export default {
    data() {
        return {
            configVisible: false,
            min: 0,
            max: 2,
            step: 0.01
        };
    },
    props: ["label", "value", "pname"],
    computed: {},

    mounted() {},

    methods: {
        handleChange(e) {
            // console.log(this.pname + " == " + e.target.value);
            this.$emit("change", this.pname, e.target.value);
        },
        handleSlide(n) {
            this.$emit("change", this.pname, n);
        },
        handleSetting(e) {
            let key = e.target.dataset.pname;
            this[key] = e.target.value;
        }
    }
};
</script>

<style lang="less" scoped>
@import "./index.less";
</style>
