<template>
    <v-container>

        <v-card max-width="500" class="mx-auto">
            <v-card-title>Formulário de Cadastro</v-card-title>
            <v-card-subtitle>Cliente {{ fullName }} - {{ now }}</v-card-subtitle>
            <v-card-text>
                <v-form>
                    <v-text-field v-model="user.name" prepend-inner-icon="mdi-account" variant="underlined"
                        label="Nome" />
                    <v-text-field v-model="user.surname" prepend-inner-icon="mdi-account-outline" variant="underlined"
                        label="Sobrenome" />
                    <v-text-field v-model="user.email" prepend-inner-icon="mdi-email" variant="underlined"
                        label="E-mail" />
                    <v-text-field v-model="user.password" prepend-inner-icon="mdi-lock" variant="underlined"
                        label="Senha" />

                    <v-list density="compact">
                        <v-list-item-title class="mb-2">Requisitos para a senha</v-list-item-title>
                        <v-list-item v-for="req in passReq" :key="req" :class="{ 'text-success': req.checked }"
                            :prepend-icon="req.checked ? 'mdi-check' : 'mdi-close-octagon'">
                            {{ req.name }}
                        </v-list-item>
                    </v-list>
                </v-form>
            </v-card-text>
            <v-card-actions>
                <v-btn color="error">Cancelar</v-btn>
                <v-spacer />
                <v-btn color="primary" :disabled="ready">Salvar</v-btn>
            </v-card-actions>
        </v-card>

    </v-container>
</template>
<script setup>
import { ref, watch, computed } from 'vue'
const user = ref({
    name: '',
    surname: '',
    email: '',
    password: ''
})
// Password Requirements
const passReq = ref([
    { name: 'A senha deve ter no mínimo 8 caracteres', checked: false },
    { name: 'A senha deve conter no mínimo 1 número', checked: false },
    { name: 'A senha deve conter no mínimo 1 letra minúscula', checked: false },
    { name: 'A senha deve conter no mínimo 1 caractere especial', checked: false },
    { name: 'A senha deve conter no mínimo 1 letra maíscula', checked: false }
]);
// observador de variável ou objeto, neste caso estamos usando arrow function para observar a propriedade password do objeto user
// se fosse observar a variavel, não precisaria de usar a arrow function no primeiro argumento da funcão watch
watch(() => user.value.password, (val) => {
    passReq.value[0].checked = val.length >= 8;
    passReq.value[1].checked = !!val.match(/[\d]/); // !! converts to boolean
    passReq.value[2].checked = !!val.match(/[a-z]/);
    passReq.value[3].checked = !!val.match(/[^\w]/);
    passReq.value[4].checked = !!val.match(/[A-Z]/);
});
// computed properties computa o valor da propriedade baseado no seu processamento
// se usar { } pode processar mais coisas porém precisa do return
// se não usar { } não precisa do return, mas só pode processar uma coisa
const fullName = computed(() => { return user.value.name + ' ' + user.value.surname });
const now = computed(() => new Date().toLocaleString());
const ready = computed( () => {
    const req = passReq.value.every((obj) => obj.checked === true);
    return !(user.value.name && user.value.surname && user.value.email && req);
});
</script>