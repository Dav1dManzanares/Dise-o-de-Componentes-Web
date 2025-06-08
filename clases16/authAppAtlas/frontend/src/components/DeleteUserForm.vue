<template>
    <div class="modal">
        <div class="modal-content">
            <p>Estas seguro de eliminar a <strong>{{  User.email  }}</strong></p>
            <div class="buttons">
                <button class="danger" @click="deleteUser">Si, Eliminar</button>
                <button class="cancel" @click="$emit('close')">Cancelar</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import axios from 'axios'

const props = defineProps({
    User: {
        type: Object,
        required: true
    }
})

const emit = defineEmits(['refresh', 'close']);

const deleteUser = async () => {
    try {
        await axios.delete(`http://localhost:4000/api/auth/users/${props.User._id}`)
        emit('refresh')
        emit('close')
    } catch (error) {
        alert(error.response?.data?.message || 'Error al eliminar el usuario')
    }
}

</script>

<style scoped>

.modal {
    position: fixed;
    top: 0; left: 0;
    width: 100%; height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
    }

    .modal-content {
    background: white;
    padding: 2rem;
    border-radius: 12px;
    width: 90%;
    max-width: 400px;
    box-shadow: 0 4px 20px rgba(0,0,0,0.2);
    font-family: system-ui, sans-serif;
    }

    h2 {
    margin-bottom: 1rem;
    font-size: 1.25rem;
    color: #111827;
    text-align: center;
    }

    form {
    display: flex;
    flex-direction: column;
    gap: 0.75rem;
    }

    input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 6px;
    font-size: 1rem;
    }

    .buttons {
    display: flex;
    justify-content: flex-end;
    gap: 0.5rem;
    margin-top: 1rem;
    }

    button {
    padding: 0.4rem 1rem;
    font-size: 0.9rem;
    border: none;
    border-radius: 6px;
    cursor: pointer;
    transition: background 0.2s ease;
    }

    button.danger {
    background: #ef4444;
    color: white;
    }

    button.danger:hover {
    background: #ef4424;
    }

    button.cancel {
    background: #f3f4f6;
    color: #1f2937;
    }

    button.cancel:hover {
    background: #e5e7eb;
    }

</style>