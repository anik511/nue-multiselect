<template>
    <div style="display: flex">
        <!-- <label class="product_label" v-if="label">{{ label }}</label> -->
        <!-- {{ title }}{{ typeof value == "object" }} -->
        <select
            class="form-control form-select-lg mb-3"
            style="float: left"
            :value="
                title != null ? title : typeof value == 'object' ? value : title
            "
            @input="updateValue"
        >
            <option :selected="value == null">Open this select menu</option>
            <option
                v-for="option in options"
                :key="option.label"
                :selected="option === value"
            >
                {{ label != "" ? option[label] : option }}
            </option>
        </select>
        <span class="ddd" @click="cancleValue">{{
            value != null ? (value != "Open this select menu" ? "x" : " ") : " "
        }}</span>
    </div>
</template>

<script>
export default {
    props: {
        options: {
            type: Array,
            required: true,
        },
        label: {
            type: String,
            default: "",
        },
        track_data: {
            type: String,
            default: "",
        },
        value: {
            type: [String, Number, Object],
            default: null,
        },
    },
    data() {
        return {
            title: "Open this select menu",
        };
    },
    methods: {
        updateValue(event) {
            console.log("11" + event.target.value + "11");
            if (event.target.value != "") {
                if (this.label != "") {
                    let vald = this.options.find(
                        (option) => option[this.label] === event.target.value
                    );
                    console.log(vald[this.track_data]);
                    this.title = vald[this.label];
                    this.$emit("input", vald[this.track_data]);
                } else {
                    this.title = event.target.value;
                    this.$emit("input", event.target.value);
                }
            } else {
                this.title = "Open this select menu";
                this.$emit("input", null);
            }

            //   this.$emit("input", event.target.value);
        },
        cancleValue() {
            this.title = "Open this select menu";
            this.$emit("input", null);
        },
    },
};
</script>

<style>
/* imoprt bootstrap 5 cdn for vue */
.form-control,
.dataTable-input {
    line-height: 1.5 !important;
}
.form-control {
    padding: 10px 9px;
    background-color: #fff;
    border: 1px solid #ced4da;
    margin-bottom: 12px;
    border-radius: 0.25rem;
    border-right-width: 0px;
    border-bottom-right-radius: 0rem;
    border-top-right-radius: 0rem;
}
.product_label {
    padding: 7px 0;
    font-weight: 600;
    font-size: 16px;
}
.ddd {
    float: left;
    width: 10px;
    background-color: #fff;
    border: 1px solid #ced4da;
    border-left-width: 0px;
    margin-bottom: 12px;
    border-bottom-right-radius: 0.25rem;
    border-top-right-radius: 0.25rem;
    cursor: pointer;
    font-weight: normal;
    display: block;
    white-space: nowrap;
    min-height: 1.2em;
    padding: 8px 6px 1px;
}
.form-control:focus {
    color: #212529;
    background-color: #fff;
    border-color: #ced4da;
    outline: 0;
    box-shadow: 0 0 0 0.25rem rgb(13 110 253 / 0%);
}
</style>
