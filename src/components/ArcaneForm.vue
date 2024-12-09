<template>
    <div>
        <h4>Agregar Personaje</h4>
    </div>
    <div>
        <form @submit.prevent="addCharacter">
            <div>
                <label for="name">Nombre</label>
                <input type="text" class="input" id="name" v-model="name" placeholder="Nombre del personaje" required />
            </div>
            <div>
                <label for="origin">Origen</label>
                <input type="text" class="input" id="origin" v-model="origins" placeholder="Origen del personaje"
                    required />
            </div>

            <div>
                <label for="specialAbility">Habilidad especial</label>
                <input type="text" class="input" id="specialAbility" v-model="specialAbility"
                    placeholder="Habilidad única/especial del personaje" required />
            </div>
            <div>
                <div>
                    <label for="missionFulfilled">Misión cumplida:</label>
                    <input type="checkbox" class="input" v-model="missionFulfilled" id="missionFulfilled">
                    <label for="missionFulfilled">Sí</label>
                </div>
            </div>
            <div>
                <label for="allies">Aliados</label>
                <input type="text" class="input" id="allies" v-model="allies" placeholder="Aliados del personaje"
                    required />
            </div>

            <div>
                <button type="submit" class="btn">Añadir</button>
            </div>
        </form>
    </div>
    <div>
        <h4> Registrados</h4>
        <div>
            <table>
                <thead>
                    <tr>
                        <th>Nombre</th>
                        <th>Origen</th>
                        <th>Habilidad especial</th>
                        <th>Aliados</th>
                        <th>Misión cumplida</th>
                    </tr>
                </thead>
                <tbody>
                    <tr v-for="char in characters" :key="char.name">
                        <td>{{ char.name }}</td>
                        <td>{{ char.origins }}</td>
                        <td>{{ char.specialAbility }}</td>
                        <td>{{ char.allies.join(', ') }}</td>
                        <td>{{ char.missionFulfilled ? 'Sí' : 'No' }}</td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>




<script setup>

import { ref } from 'vue';

const characters = ref([
    {
        name: 'Jinx',
        origins: 'Piltover',
        specialAbility: 'Manipulación de explosivos',
        allies: ['Ekko'],
        missionFulfilled: true
    },
    {
        name: 'Vi',
        origins: 'Zaun',
        specialAbility: 'Combate cuerpo a cuerpo',
        allies: ['Caitlyn'],
        missionFulfilled: false
    }
]);

const name = ref('');
const origins = ref('');
const specialAbility = ref('');
const allies = ref([]);
const missionFulfilled = ref(false);


const addCharacter = () => {
    const alliesList = allies.value.split(',').map(allie => allie.trim());

    const newCharacter = {
        name: name.value,
        origins: origins.value,
        specialAbility: specialAbility.value,
        allies: alliesList,
        missionFulfilled: missionFulfilled.value
    };

    characters.value.push(newCharacter);

    putDefaultValues();
};


const putDefaultValues = () => {
    name.value = '';
    origins.value = '';
    specialAbility.value = '';
    allies.value = '';
    missionFulfilled.value = false;
}

</script>

<style scoped>

th{
    padding: 5px;
}

td{
    padding: 5px;
}

.btn {
    background-color: rgb(103, 177, 166);
    border-radius: 30px;
    padding: 10px 20px;
    margin: 5px;
}
.btn:active{
    transform: scale(0.9); 
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.3);
}

.input {
    border-radius: 10px;
    padding: 5px 10px;
    margin: 5px; 
    border: 1px solid #ababab;
}
</style>