<template>
    <div v-if="trainings" class="table-container">
        <div class="header">Mes Formations</div>
        <table class="styled-table">
            <thead>
            <tr>
                <th class="col-code">Nom</th>
                <th class="col-date">Date</th>
            </tr>
            </thead>
            <tbody>
            <tr
                v-for="(training, index) in filledTrainings"
                :key="index"
                :class="{ 'selected': training.selected }"
                @click="selectTraining(index)"
            >
                <td class="col-code">{{ training.name }}</td>
                <td class="col-date">{{ training.date }}</td>
            </tr>
            </tbody>
        </table>
        <div class="footer">
            <button class="footer-button button-add">Démarrer</button>
            <button class="footer-button button-edit">Modifier</button>
            <button class="footer-button button-delete">Supprimer</button>
        </div>
    </div>
</template>

<script lang="ts" setup>
import { onMounted, computed } from 'vue';
import useTrainings from '../composables/trainings';

const { trainings, getTrainings } = useTrainings();

onMounted(getTrainings);

const filledTrainings = computed(() => {
    const fillLength = 6 - trainings.value.length;
    return fillLength > 0 ? trainings.value.concat(Array(fillLength).fill({})) : trainings.value;
});

const selectTraining = (index: string | number) => {
    filledTrainings.value[index].selected = !filledTrainings.value[index].selected;
}
</script>

<style scoped>
.header {
    position: sticky;
    top: 0;
    background-color: #1C3356;
    text-align: center;
    color: white;
    padding: 8px;
    border: 1px solid #000;
    z-index: 1;
    font-size: 20px;
}

.table-container {
    margin-left: 60px;
    margin-right: 30px;
    margin-top: 30px;
    max-height: 336px;
    width: 424px;
    overflow-y: auto;
    -ms-overflow-style: none;
    scrollbar-width: none;
    border-radius: 10px;
}

.table-container::-webkit-scrollbar {
    display: none;
}

.styled-table {
    width: 100%;
    border-collapse: collapse;
    background-color: #1C3356;
    color: white;
}

.styled-table th,
.styled-table td {
    border: 1px solid #000;
    padding: 8px;
    text-align: left;
    height: 3em;
}

.styled-table tbody tr{
    height: 3em;
}

.styled-table thead {
    border-bottom: 2px solid #000;
    background-color: #1C3356;
}

.styled-table thead tr th {
    position: sticky;
    top: 0;
    background-color: #1C3356;
}

.col-name {
    width: 50%;
}

.col-town {
    width: 50%;
}

.footer {
    position: sticky;
    bottom: 0;
    background-color: rgba(28, 51, 86, 0.8);
    border-radius: 10px;
    padding: 8px;
    border: 1px solid #000;
    color: white;
    text-align: center;
    font-size: 16px;
    font-weight: bold;
    height: 3em;
    display: flex;
    justify-content: space-around;
}

.footer-button {
    color: white;
    border: none;
    padding: 5px;
    text-align: center;
    font-size: 1em;
    cursor: pointer;
    transition: background-color 0.3s ease;
    border-radius: 10px;
    flex: 1;
    min-width: 100px;
    margin: 0 10px;
    outline: none !important;
    box-shadow: none !important;
}

.button-add {
    background-color: #36BB4E;
}

.button-add:hover {
    background-color: #2da03c;
}

.button-edit {
    background-color: #BB5E36;
}

.button-edit:hover {
    background-color: #a54f2d;
}

.button-delete {
    background-color: #BB3636;
}

.button-delete:hover {
    background-color: #a02e2e;
}

@media (max-width: 975px) {
    .table-container {
        margin-left: 20px;
        margin-right: 20px;
    }
}
</style>
