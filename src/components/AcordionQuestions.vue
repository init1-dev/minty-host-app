<template>
    <div class="q-container">
        <div 
            v-for="item in faqs" 
            :key="item.name"
            class="flex flex-col question">
            <p class="q-title">{{ item.pregunta }}</p>
            <small class="q-answer">{{ item.respuesta }}</small>
        </div>
    </div>
</template>
  
<script setup>

    const faqs = [
    {
        "pregunta": "¿Cuál es el precio del alquiler?",
        "respuesta": "El precio del alquiler mensual es de $X."
    },
    {
        "pregunta": "¿Cuánto es el depósito de seguridad?",
        "respuesta": "El depósito de seguridad es de $Y y se devolverá al finalizar el contrato si no hay daños significativos."
    },
    {
        "pregunta": "¿Cuánto dura el contrato de arrendamiento?",
        "respuesta": "El contrato de arrendamiento tiene una duración de Z meses."
    },
    {
        "pregunta": "¿Están permitidas las mascotas?",
        "respuesta": "Sí, se permiten mascotas con un depósito adicional de $Z."
    },
    {
        "pregunta": "¿Cuáles son los servicios incluidos en el alquiler?",
        "respuesta": "El alquiler incluye servicios como agua, electricidad, gas e internet. [Puedes agregar o quitar según sea necesario.]"
    },
    {
        "pregunta": "¿Cuándo se vence el pago del alquiler?",
        "respuesta": "El pago del alquiler vence el primer día de cada mes."
    },
    {
        "pregunta": "¿Cuáles son las condiciones para renovar el contrato?",
        "respuesta": "Las condiciones para renovar el contrato serán discutidas al acercarse la fecha de vencimiento del contrato actual."
    },
    {
        "pregunta": "¿Hay estacionamiento disponible?",
        "respuesta": "Sí, hay estacionamiento disponible por un costo adicional de $W."
    },
    {
        "pregunta": "¿Cuál es la política de cancelación?",
        "respuesta": "La política de cancelación se especifica en el contrato de arrendamiento. En general, se requiere un aviso de X días antes de la fecha de vencimiento del contrato."
    },
    {
        "pregunta": "¿Se permite personalizar o pintar las paredes?",
        "respuesta": "Se permite personalizar el espacio, pero se debe obtener aprobación previa del arrendador y se pueden aplicar ciertas restricciones."
    }
    ]
</script>

<style>
 .question {
    padding: 1rem;
    background-color: lightgray;
    margin-bottom: 1rem;
    border-radius: 1rem;
    font-weight: bold;
 }

 .q-title {
    color: black;
 }

 .q-answer {
    color: grey
 }

 .q-container {
    margin-top: 1rem;
 }
</style>