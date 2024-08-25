<script setup>
import icons from '@/assets/icons.json';
const { $directusBaseUrl, $logout } = useNuxtApp();
const userState = useUserState();

const diet = ref(userState.diet);

const selectedAvararId = ref(null)
function handleAvatarSelection() {
    // logique pour sélectionner un nouvel avatar
}

function saveProfile() {
    // Logique pour sauvegarder le profil dans le backend Directus
};

onMounted(() => {
    selectedAvararId.value = userState.avatarFileId
})
</script>

<template>
    <PageStructure showHeader>
        <template #header>
            <h1 class="mainWidth">Mon profil</h1>
        </template>

        <template #scrollableContent>
            <div class="mainWidth">
                <form @submit.prevent="saveProfile" class="profile-form">
                    <!-- Champs de profil -->
                    <fieldset class="form-group">
                        <label for="firstName">Prénom</label>
                        <input type="text" id="firstName" v-model="userState.firstName" readonly>
                    </fieldset>

                    <fieldset class="form-group">
                        <label for="lastName">Nom</label>
                        <input type="text" id="lastName" v-model="userState.lastName" readonly>
                    </fieldset>

                    <fieldset class="form-group">
                        <label for="email">Email</label>
                        <input type="email" id="email" v-model="userState.email" readonly>
                    </fieldset>

                    <!-- User could select new avart from colllection -->
                    <AuthenticationAvatar @selection="handleAvatarSelection"/>

                    <!-- <fieldset class="form-group">
                        <legend>Ma diet</legend>

                        <div>
                            <label for="radioVegan">Vegan</label>
                            <input id="radioVegan" type="radio" value="vegan">
                        </div>
                        <div>
                            <label for="radioVegan">Veggie</label>
                            <input id="radioVegggie" type="radio" value="veggie">
                        </div>
                        <div>
                            <label for="radioOmnivorous">Omnivore</label>
                            <input id="radioOmnivorous" type="radio" value="omnivorous">
                        </div>
                        <div>
                            <label for="radioCarnivorous">Carnivore</label>
                            <input id="radioCarnivorous" type="radio" value="carnivore">
                        </div>
                    </fieldset> -->


                    <!-- Button would save new data to profile -->
                    <button class="save-button" @click="saveProfile">Enregistrer</button>
                </form>

                <!-- Bouton de déconnexion -->
                <div class="button logout pointer" @click="$logout">
                    <div class="flex column gap5 alignCenter">
                        <svg viewBox="0 -960 960 960" class="icon shrink0">
                            <path :d="icons.logout.path" />
                        </svg>
                        <span>Se déconnecter</span>
                    </div>
                </div>
            </div>
        </template>
    </PageStructure>
</template>

<style scoped>
.profile-form {
    display: flex;
    flex-direction: column;
    gap: 20px;
    margin-top: 20px;
}

.form-group {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.radio-group {
    display: flex;
    gap: 20px;
}

.avatar-preview {
    width: 100px;
    height: 100px;
    border-radius: 50%;
    margin-top: 10px;
    object-fit: cover;
}

input[type="file"] {
    padding: 10px;
}

input, textarea, button {
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 5px;
    font-size: 16px;
}

button.save-button {
    background-color: var(--theme-color-pepite);
    color: white;
    cursor: pointer;
    transition: background-color 0.3s;
}

button.save-button:hover {
    background-color: var(--theme-color-account-dark);
}

.button {
    padding: 10px 5px;
    border-radius: 5px;
}
.button.logout {
    background-color: var(--theme-color-account);
    margin-top: 25px;
}
.icon {
    width: 20px;
    height: 20px;
    fill: white;
}
.flex {
    display: flex;
}
.column {
    flex-direction: column;
}
.gap5 {
    gap: 5px;
}
.alignCenter {
    align-items: center;
}
.pointer {
    cursor: pointer;
}
img {
    width: min(100%, 200px);
}
</style>
