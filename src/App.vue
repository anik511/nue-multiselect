<template>
    <div id="app">
        <base-select
            class="col-md-6"
            v-model="select"
            :options="items"
        ></base-select>
    </div>
</template>

<script>
import BaseSelect from "@/components/BaseSelect.vue";
export default {
    name: "App",
    components: {
        BaseSelect,
    },
    data() {
        return {
            items: ["a", "b", "c"],
            // items: [
            //   {
            //     value: "1",
            //     label: "a",
            //   },
            //   {
            //     value: "2",
            //     label: "b",
            //   },
            //   {
            //     value: "3",
            //     label: "c",
            //   },
            // ],
            select: null,
        };
    },
};
</script>

<style>
.col-md-6 {
    margin: 20px;
}
</style>
