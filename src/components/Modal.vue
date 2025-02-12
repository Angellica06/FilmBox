<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
    show: Boolean,
    title: String,
    description: String,
    image: String,
    date: String,
    assessment: String
});

const emit = defineEmits(['closeModal']);

const close = () => {
    emit('closeModal');
};
</script>

<template>
    <div v-if="show" class="modal-overlay px-3" @click="close">
        <div class="modal-content" @click.stop>
            <button class="close-btn" @click="close">X</button>
            <img v-if="image" :src="image" :alt="title" />
            <div class="modal-text">
                <h2 class="text-center">{{ title }}</h2>
                <p>{{ description }}</p>
                <p><strong>Data de lançamento:</strong> {{ date }}</p>
                <p><strong>Avaliação:</strong> ⭐ {{ assessment }}</p>
            </div>
        </div>
    </div>
</template>

<style scoped>
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.6);
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 2.4rem;
}

.modal-content {
    display: flex;
    background: #222;
    color: #fff;
    padding: 1.5rem;
    border-radius: 8px;
    max-width: 500px;
}

.modal-content img {
    display: flex;
    align-self: center;
    width: 50%;
    border-radius: 6px;
}

.modal-text {
    padding-left: 1.5rem;
    line-height: 1.2rem;
    display: flex;
    flex-direction: column;
    text-align: justify;
}

.close-btn {
    position: absolute;
    top: 10px;
    right: 10px;
    border: none;
    background: #fff718;
    color: #000;
    font-weight: 600;
    cursor: pointer;
    border-radius: .2rem;
}
</style>