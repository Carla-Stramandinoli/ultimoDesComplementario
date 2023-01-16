<script setup>
import { reactive } from 'vue';
import useVuelidate from '@vuelidate/core';
import { required, email, minLength, numeric, maxLength } from '@vuelidate/validators';

const state = reactive({
    name: '',
    edad: '',
    email: '',
    contacto: ''
});

const rules = {
    name: { required, minLength: minLength(3) },
    edad: { required, numeric, maxLength: maxLength(2) },
    email: { required, email },
    contacto: { required, numeric, maxLength: maxLength(10), minLength: minLength(10) }
}
const emit = defineEmits([]);

const v$ = useVuelidate(rules, state);

function validarFormulario() {
    let validate = this.v$.$validate();
    let thisComponent = this;
    console.log(this.state)
    validate.then(function (result) {
        console.log(result);
        if (!result) {
            console.log("Los campos obligatorios deben estar completos");
            return;
        }
        console.log('validarFormulario');
        emit("enviar",thisComponent.state);
        // setTimeout(() => { thisComponent.v$.$reset() }, 1000)
        })
};

</script>

<template>
    <v-form ref="form">
        <v-container id="formulario">
            <v-row align="center" justify="center">
                <v-col cols="8">
                    <v-text-field v-model="v$.name.$model"  @blur="v$.name.$touch" label="Name" placeholder="Pepe">
                    </v-text-field>
                    <div class="div-error" :rules="name" v-for="(error, index) of v$.name.$errors" :key="index">{{
                        error.$message
                    }}
                    </div>
                </v-col>
                <v-col cols="8">
                    <v-text-field v-model="v$.edad.$model" @blur="v$.edad.$touch" label="Edad" placeholder="18">
                    </v-text-field>
                    <div class="div-error" :rules="edad" v-for="(error, index) of v$.edad.$errors" :key="index">{{
                        error.$message
                    }}
                    </div>
                </v-col>
                <v-col cols="8">
                    <v-text-field v-model="v$.email.$model" @blur="v$.email.$touch" label="E-mail"
                        placeholder="pepe@lo.com">
                    </v-text-field>
                    <div class="div-error" :rules="email" v-for="(error, index) of v$.email.$errors" :key="index">{{
                        error.$message
                    }}
                    </div>
                </v-col>
                <v-col cols="8">
                    <v-text-field v-model="v$.contacto.$model" @blur="v$.contacto.$touch" label="Telefono de contacto"
                        placeholder="1512312345">
                    </v-text-field>
                    <div class="div-error" :rules="contacto" v-for="(error, index) of v$.contacto.$errors" :key="index">
                        {{
                            error.$message
                        }}
                    </div>
                </v-col>
            </v-row>

            <div class="text-center">
                <v-btn @click="validarFormulario()" class="ma-2" outlined color="indigo">
                    Submit
                </v-btn>
                <v-btn type="reset">Reset</v-btn>
            </div>
        </v-container>
    </v-form>
</template>

<style scoped>
.div-error {
    margin-top: 1px;
    font-size: 14px;
    color: red;
}
</style>