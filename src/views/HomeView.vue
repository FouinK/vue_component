<template>
    <div>
        <h1>{{ result }}</h1>
        <form @submit.prevent="onSubmitForm">
            <input ref="answer" maxLength="4" v-model="value">
            <button type="submit">입력</button>
        </form>
        <div>시도 : {{ tries.length }}</div>
        <ul>
            <li v-for="t in tries" :key="t.try + t.result">
                <div>{{ t.try }}</div>
                <div>{{ t.result }}</div>
            </li>
        </ul>
    </div>
</template>

<script>
const getNumbers = () =>{
    const candidates = [1, 2, 3, 4, 5, 6, 7, 8, 9];
    const array = [];
    for (let i = 0; i < 4; i += 1) {
        const chosen = candidates.splice(Math.floor(Math.random() * (9 - i)), i)[0];
        array.push(chosen);
    }

    return array;
}

export default {
    data() {
        return {
            answer: getNumbers(),
            tries: [],
            value: '',
            result: '',
        };
    },
    methods: {
        onSubmitForm() {

            if (this.value === this.answer.join('')) {
                this.tries.push({
                    try: this.value,
                    result: '홈런',
                });
                this.result = '홈럼';
                this.value = '';
                this.tries = [];
                this.$refs.answer.focus();
            } else {

            }

            this.value = '';
            this.$refs.answer.focus();
        },
    }
};
</script>

