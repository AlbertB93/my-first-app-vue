<template>

    <div class="person" v-bind:class="{
        paid: person.paidAmount}" >
        <p>
            {{ person.id }}. Imię: {{ person.name }}, kwota: {{ person.amount }}
        </p>
        <button v-if="!person.paidAmount" @click="personPaid(person.id)"> Zapłacił
        </button>
    </div>
    <div>

    </div>
</template>


<script>
export default{
    props: ['person'],
    methods: {
        personPaid(){
            this.$emit('personPaidFee',this.person.id)
        }
    }

}
</script>

<style>
.person {
    border: solid 1px black;
    margin: 6px;
    padding: 4px;
}

.person p {
    font-size: 1em;
}
</style>