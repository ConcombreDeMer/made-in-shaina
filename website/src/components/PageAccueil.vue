<template>
    <form @submit.prevent="">
        <PartForm v-if="currentStep === 0"
        title="Animal"
        :previous="false"
        :next="true"
        @goNext="handleGoNext()">
            <FloatingLabelInput class="nom" v-model="form.animal.nom" label="Nom"/>
        </PartForm>

        <PartForm v-if="currentStep === 1"
        title="Propriétaire"
        :previous="true"
        :next="true"
        @goBack="handleGoBack()"
        @goNext="handleGoNext()">
            <FloatingLabelInput class="prenom" v-model="form.proprietaire.prenom" label="Prénom"/>
            <FloatingLabelInput class="nom" v-model="form.proprietaire.nom" label="Nom"/>
            <FloatingLabelInput class="telephone" v-model="form.proprietaire.telephone" label="Numéro de téléphone"/>
            <FloatingLabelInput class="email" v-model="form.proprietaire.email" label="Email"/>
        </PartForm>

        <PartForm v-if="currentStep === 2"
        title="Personnes à contacter"
        :previous="true"
        :next="true"
        @goBack="handleGoBack()"
        @goNext="handleGoNext()">
            <FloatingLabelInput class="prenom" v-model="form.contact.prenom" label="Prénom"/>
            <FloatingLabelInput class="nom" v-model="form.contact.nom" label="Nom"/>
        </PartForm>

        <PartForm v-if="currentStep === 3"
        title="Vétérinaire"
        :previous="true"
        :next="false"
        @goBack="handleGoBack()">
            <FloatingLabelInput class="nom" v-model="form.veterinaire.nom" label="Nom"/>
            <FloatingLabelInput class="telephone" v-model="form.veterinaire.telephone" label="Numéro de téléphone"/>
            <FloatingLabelInput class="adresse" v-model="form.veterinaire.adresse" label="Adresse"/>
        </PartForm>

        <button v-if="currentStep === 3" class="submit-button" type="submit" @click="handleSubmit">Créer mon porte clé</button>
    </form>
</template>

<script setup lang="ts">
import FloatingLabelInput from './utils/FloatingLabelInput.vue';
import PartForm from './utils/PartForm.vue';
import { ref } from 'vue';

const currentStep = ref(2);

const form = ref({
    animal : {
        nom: ''
    },
    proprietaire : {
        prenom: '',
        nom: '',
        telephone: '',
        email: ''
    },
    contact : {
        prenom: '',
        nom: ''
    },
    veterinaire : {
        nom: '',
        telephone: '',
        adresse: ''
    }
});

const validateAnimal = () => {
    return form.value.animal.nom.trim() !== '';
};

const validateProprietaire = () => {
    return form.value.proprietaire.prenom.trim() !== '' &&
           form.value.proprietaire.nom.trim() !== '' &&
           form.value.proprietaire.telephone.trim() !== '' &&
           form.value.proprietaire.email.trim() !== '';
};

const validateVeterinaire = () => {
    return form.value.veterinaire.nom.trim() !== '' &&
           form.value.veterinaire.telephone.trim() !== '' &&
           form.value.veterinaire.adresse.trim() !== '';
};

const handleGoBack = () => {
    if (currentStep.value > 0) {
        currentStep.value--;
    }
};

const handleGoNext = () => {
    if (currentStep.value === 0 && !validateAnimal()) {
        alert("Veuillez remplir le nom de l'animal");
        return;
    }
    if (currentStep.value === 1 && !validateProprietaire()) {
        alert("Veuillez remplir tous les champs du propriétaire");
        return;
    }
    if (currentStep.value === 3 && !validateVeterinaire()) {
        alert("Veuillez remplir tous les champs du vétérinaire");
        return;
    }
    
    if (currentStep.value < 3) {
        currentStep.value++;
    }
};

const handleSubmit = () => {
    if (!validateVeterinaire()) {
        alert("Veuillez remplir tous les champs du vétérinaire");
        return;
    }
    console.log(form.value);
};
</script>

<style scoped>
form {
    display: flex;
    flex-direction: column;
    gap: 1rem;
}


.submit-button{
    background-color: #6F7B47;
    color: white;
    padding: 14px 20px;
    margin: 8px 0;
    border: none;
    border-radius: 10px;
    cursor: pointer;
    width: 20%;
    height: 5vh;
    font-size: 2vh;
    font-weight: lighter;
    position: absolute;
    bottom: 10%;
    left: 50%;
    transform: translateX(-50%);
}
</style>