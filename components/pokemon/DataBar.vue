<template>
    <div class="progress-label-bar">
        <div class="label">
            <label :for="name">{{ name }}</label>
        </div>
        <div class="progress-bar">
            <progress :id="name" :max="155" :value="base_stat"></progress>
            <p>{{base_stat}}</p>
        </div>
    </div>
</template>
<script>
export default {
    props: {
        base_stat: {
            default: -1,
            type: Number,
            required: true
        },
        name: {
            default: '',
            type: String,
            required: true
        }
    }
}
</script>
<style lang="scss" scoped>
    .progress-label-bar {
        display: flex;
        flex-direction: row;
        font-size: 1.4em;
        &:not(:last-of-type) {
            margin-bottom: 0.6em;
        }
    }

    label {
        text-transform: capitalize;
        margin-right: 0.5em;
    }

    .progress-bar {
        display: flex;
        flex-direction: row;
        margin-left: auto;
        & p {
            width: 25px;
            margin-left: 0.5em;
        }
    }

    progress[value] {
        /* Reset the default appearance */
        -webkit-appearance: none;
        -moz-appearance: none;
        appearance: none;
        /* Get rid of default border in Firefox. */
        border: none;
        overflow: hidden;
        height: 14px;
        background-color: #c4c4c4;
        margin: auto 0;
        text-align: right;
        &::-webkit-progress-bar {
            background: red;
        }
    }
</style>
