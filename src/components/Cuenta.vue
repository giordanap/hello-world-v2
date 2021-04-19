<template>
    <h2>Tipo de Cuenta: {{ cuenta }}</h2>
    <h2>Saldo: {{ saldo }}</h2>
    <h2>Cuenta {{estado? 'Activa' : 'Desactivada'}}</h2>
    <div v-for="(servicio,index) in servicios" :key="index">
        {{index + 1}} - {{ servicio }}
    </div>
    <AccionSaldo 
        texto="Aumentar Saldo" 
        @accion="aumentar"
    />
    <AccionSaldo 
        texto="Disminuir Saldo" 
        @accion="disminuir"
        :disabled="disable"
    />
</template>

<script>
import AccionSaldo from './AccionSaldo'

export default {
    components: {
        AccionSaldo
    },
    data() {
        return {
            saldo: 1000,
            cuenta: 'Visa',
            estado: false,
            servicios: ['giro', 'abono', 'transferencia'],
            disable: false
        }
    },
    methods: {
        aumentar() {
            this.saldo = this.saldo + 100
            this.disable = false
        },
        disminuir() {
            if (this.saldo == 0) {
                this.disable = true
                alert('Saldo Agotado')
                return
            }
            this.saldo = this.saldo - 100
        }
    }
}
</script>

<style>

</style>