<template>
    <div>
        <!-- Botão Flutuante -->
        <button class="chat-button" @click="isChatOpen = !isChatOpen">
            💬
        </button>

        <!-- Janela do Chat -->
        <div v-if="isChatOpen" class="chat-window">
            <div class="chat-header">
                <span>
                    Envie-nos uma mensagem

                </span>
                <button class="close-btn" @click="isChatOpen = false">
                    <i class="pi pi-minus"></i>
                </button>
            </div>

            <div class="chat-body">

                <p class="paragraph-intro">
                    Este é o ínicio da sua conversação connosco.
                </p>
                <div class="container-message">
                    <div class="chat-message bot">

                        <div class="message">
                            <div class="msg">Olá, sou o Tobi</div>
                        </div>


                    </div>

                    <div class="chat-message bot">
                        <div class="msg">
                            <div class="message">
                                <div class="msg">
                                    Bem-vindo à Vodacom. Por favor, selecione um idioma / Welcome to Vodacom Please
                                    Select A
                                    Language
                                    <br />1. Portuguese<br />2. English

                                </div>

                            </div>
                        </div>
                    </div>
                </div>






                <div class="user-messages">
                    <div v-for="(msg, index) in messages" :key="index" class="chat-message user">
                        <div class="message"><div class="msg">{{ msg }}</div></div>
                    </div>
                </div>
                <div class="options">
                    <button @click="selectOption('Português')">Português</button>
                    <button @click="selectOption('English')">English</button>
                </div>
            </div>

            <!-- Campo de envio -->
            <div class="chat-footer">
                <button @click="sendMessage">
                    <Paperclip class="iconFix" />
                </button>
                <input type="text" v-model="newMessage" placeholder="Digite sua mensagem..."
                    @keyup.enter="sendMessage" />
                <button @click="sendMessage">
                    <SendHorizonal class="iconSend" />
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { Paperclip, SendHorizonal } from "lucide-vue-next";

const isChatOpen = ref(false);
const newMessage = ref("");
const messages = ref([]);

function sendMessage() {
    if (newMessage.value.trim() !== "") {
        messages.value.push(newMessage.value);
        newMessage.value = "";
    }
}

function selectOption(option) {
    messages.value.push(`Idioma selecionado: ${option}`);
}
</script>

<style>
:root {
    --main-color: #ef4444;
    --bg-chat: #f0f0f0;
    --bg-user: #f0f0f0;
    --gray-icons: #888;
}
</style>

<style scoped>
.chat-button {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: var(--main-color);
    color: white;
    border: none;
    border-radius: 50%;
    padding: 15px;
    font-size: 20px;
    cursor: pointer;
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.2);
}

.chat-window {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 450px;
    background: white;
    border-radius: 8px;
    box-shadow: rgba(100, 100, 111, 0.2) 0px 7px 29px 0px;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    border: 2px solid #ddd;
}


.chat-header {
    background: var(--main-color);
    color: white;
    padding: 25px 25px;
    font-weight: 600;
    display: flex;
    justify-content: space-between;
    align-items: center;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
}

.chat-header span {
    font-size: 1.3rem;
}

.close-btn {
    background: transparent;
    border: none;
    color: white;
    font-size: 18px;
    cursor: pointer;
}

/* Corpo */
.chat-body {
    padding: 10px;
    flex: 1;
    overflow-y: auto;
}

.chat-message {
    margin: 5px 0;
}


.chat-message .message {
    margin-top: 10px;
}


.chat-message.bot .message {
    display: flex;
    justify-content: flex-start;
}

.chat-message.user .message {
    display: flex;
    justify-content: flex-end;
}

.chat-message .message .msg {
    border-radius: 10px;
    max-width: 70%;
    min-width: 0px;
    padding: 15px;
}

.chat-message.bot .message .msg {
    background: var(--bg-chat);
    border-top-left-radius: 0px;
}

.chat-message.user .message .msg {
    background: var(--main-color);
    border-top-left-radius: 0px;
    text-align: right;
    color: #fff;
}

.options {
    display: flex;
    justify-content: flex-end;
}

.options button {
    margin: 5px 5px 0 0;
    padding: 5px 20px;
    border: none;
    background: transparent;
    cursor: pointer;
    border-radius: 40px;
    border: 1px solid #999;
}

/* Rodapé */
.chat-footer {
    display: flex;
    border-top: 1px solid #ccc;
    padding: 15px 25px;
}

.chat-footer input {
    flex: 1;
    border: none;
    padding: 10px;
    outline: none;
}

.chat-footer button {
    background: transparent;
    border: none;
    color: white;
    padding: 10px;
    cursor: pointer;
}

.iconSend {
    fill: var(--gray-icons);
    stroke-width: 1;
}

.iconFix {
    color: var(--gray-icons);
    stroke-width: 2;
    width: 20px;
    transform: rotate(315deg);
}

.paragraph-intro {
    font-size: 13px;
    text-align: center;
    padding: 10px 0px;
    color: #777;
}
</style>
