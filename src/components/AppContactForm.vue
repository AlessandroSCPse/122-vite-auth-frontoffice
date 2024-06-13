<script>
import axios from 'axios';
import { store } from '../store.js';

// Quando l'utente invia il form
// leggiamo i campi del form
// e li inviamo all'api http://127.0.0.1:8000/api/contacts con metodo post
// leggiamo la risposta
// success -> true visualizzare per l'utente un messaggio di ringraziamento
// success -> false mostriamo i messaggi d'errore in pagina

export default {
    name: 'AppContactForm',
    data() {
        return {
            store,
            userName: '',
            userEmail: '',
            userMessage: '',
            errors: {},
            success: null,
            isLoading: false
        };
    },
    methods: {
        sendForm() {
            const userData = {
                name: this.userName,
                email: this.userEmail,
                message: this.userMessage,
            };

            this.isLoading = true;

            axios.post(`${this.store.apiBaseUrl}/api/contacts`, userData)
            .then(response => {
                this.success = response.data.success;

                if(response.data.success) {
                    // Mostreremo un messaggio di ringraziamento
                    this.errors = {};
                    this.userName = '';
                    this.userEmail = '';
                    this.userMessage = '';
                } else {
                    // Salviamo gli errori nei data
                    this.errors = response.data.errors;
                }

                this.isLoading = false;
            });
        }
    }
}
</script>

<template>
    <div v-if="success" class="alert alert-success" role="alert">
        Grazie per averci contattato abbiamo ricevuto la tua richiesta e ti contatteremo il prima possibile.
    </div>

    <form @submit.prevent="sendForm">
        <div class="mb-3">
            <label for="name" class="form-label">Name</label>
            <input type="text" class="form-control" id="name" v-model="userName">
        </div>

        <div v-if="errors.name">
            <div v-for="error in errors.name" class="alert alert-danger" role="alert">
                {{ error }}
            </div>
        </div>

        <div class="mb-3">
            <label for="email" class="form-label">Email</label>
            <input type="email" class="form-control" id="email" v-model="userEmail">
        </div>

        <div v-if="errors.email">
            <div v-for="error in errors.email" class="alert alert-danger" role="alert">
                {{ error }}
            </div>
        </div>

        <div class="mb-3">
            <label for="message" class="form-label">Message</label>
            <textarea class="form-control" id="message" rows="5" v-model="userMessage"></textarea>
        </div>

        <div v-if="errors.message">
            <div v-for="error in errors.message" class="alert alert-danger" role="alert">
                {{ error }}
            </div>
        </div>

        <button :disabled="isLoading" type="submit" class="btn btn-primary">{{ isLoading ? 'Invio...' : 'Invia' }}</button>
    </form>
</template>
