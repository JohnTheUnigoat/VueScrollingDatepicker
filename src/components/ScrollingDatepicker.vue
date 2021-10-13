<template>
    <div class="scrolling-datepicker">
        <div class="datepicker" @scroll="onScroll" ref="container">
            <div
                v-for="(value, i) in values"
                :key="value"
                class="value"
                ref="value"
                :class="{ selected: selectedIndex === i }"
            >
                {{ value }}
            </div>
        </div>

        <pre class="logs">{{ log }}</pre>
    </div>
</template>

<script>
import _ from 'lodash';

export default {
    data() {
        return {
            values: _.range(1, 10).map(n => `Value ${n}`),
            selectedIndex: 0,
            valueHeight: null,

            log: null,
        };
    },
    watch: {
        selectedIndex(val) {
        },
    },
    methods: {
        onScroll(e) {
            this.log =
`${JSON.stringify({
    scrollTop: e.target.scrollTop,
    scrollHeight: e.target.scrollHeight,
}, null, 2)}`;

            setTimeout(() => {
                console.log('setting updated scroll');
                this.$refs.container.scroll({
                    top: Math.round(e.target.scrollTop / this.valueHeight) * this.valueHeight,
                    behavior: 'smooth',
                });
            }, 100);
        },
    },
    mounted() {
        this.valueHeight = this.$refs.value[0].scrollHeight;

        console.log(this.valueHeight);

        this.$refs.container.style.height = `${this.valueHeight * 3}px`;

        console.log(this.$refs.container.style.height, this.$refs.container.scrollHeight);
    },
};
</script>

<style scoped>
    .datepicker {
        border: 1px solid #000;
        width: fit-content;
        overflow-y: scroll;
        font-size: 2rem;
    }
    .value {
        color: #555;
        font-weight: 600;
        height: 45px;
        display: flex;
        align-items: center;
    }

    .value.selected {
        color: rgb(44, 117, 148);
    }

    .value:first-child {
        margin-top: 45px;
    }

    .value:last-child {
        padding-bottom: 45px;
    }

    .value::-webkit-scrollbar {
        display: none;
    }
</style>