<script setup>
const pepitesFilterState = usePepitesFilterState();
const { $directus, $readItems } = useNuxtApp();

const emit = defineEmits(['refresh']);

const { data: categories } = await useAsyncData(
    "categories",
    async () => {
        const items = await $directus.request($readItems('Categories'));

        return items;
    }, {
        server: true 
    }
);

const selected = ref('');

function handleClick(cat) {
    if (cat === selected.value) {
        selected.value = '';
        pepitesFilterState.value.category = {};
    } else {
        selected.value = cat;
        pepitesFilterState.value.category = {
            category: {
                value: {
                    _eq: cat
                }
            }
        }
    }
    emit('refresh');
}

</script>

<template>
    <div class="box flex column gap5">
        <p class="filterTitle">Catégories</p>

        <button 
            v-for="cat in categories" :key="cat.id"
            :class="{ 'active' : selected === cat.value }" 
            @click.prevent="handleClick(cat.value)"
        >
            {{ cat.text }}
        </button>
    </div>
</template>

<style scoped>
.filterTitle {
    font-size: 1.2rem;
    font-weight: 600;
    padding-bottom: 5px;
    border-bottom: 1px solid var(--theme-color);
}
button {
    font-size: 1rem;
    font-weight: 600;
    background-color: var(--gray-dimmed);
    padding: 8px 16px;
    border-radius: 10px;
    margin-right: 10px;
    cursor: pointer;
    user-select: none;
}
button.active {
    background-color: var(--success);
}
</style>