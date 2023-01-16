<script setup>

const props = defineProps({
    info: {
        name: String,
        edad: Number,
        email: String,
        contacto: Number
    }
})

</script>

<template>
    <v-container>
        <v-row align="center" justify="center">
            <v-col cols="8">
                <v-table theme="dark">
                    <template v-slot:default>
                        <thead>
                            <tr>
                                <th class="text-left">
                                    Nombre
                                </th>
                                <th class="text-left">
                                    Edad
                                </th>
                                <th class="text-left">
                                    E-mail
                                </th>
                                <th class="text-left">
                                    Telefono
                                </th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(data, index) of props.info" :key="index">
                                <td>{{ data.name }}</td>
                                <td>{{ data.edad }}</td>
                                <td>{{ data.email }}</td>
                                <td>{{ data.contacto }}</td>
                            </tr>
                        </tbody>
                    </template>
                </v-table>
            </v-col>
        </v-row>
    </v-container>
</template>

<style scoped>

</style>