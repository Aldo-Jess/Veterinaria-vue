<script setup>

  defineEmits(['Actualizar-paciente', 'Eliminar-Pacinte'])

  defineProps({
    pacient: {
      type: Object,
      Required: true
    }
  })

</script>


<template>
  <div class="mx-5 my-10 bg-white shadow-md px-5 py-10 rounded-xl">
      <p class="font-bold mb-3 text-gray-700 uppercase">ID:
          <span class="font-normal normal-case">
          {{  pacient.id }}
          </span>
      </p>

      <p class="font-bold mb-3 text-gray-700 uppercase"> Nombre: 
          <span class="font-normal normal-case">
            {{ pacient.nombre }}
          </span>
      </p>

      <p class="font-bold mb-3 text-gray-700 uppercase">Propietario: 
          <span class="font-normal normal-case">
            {{ pacient.propietario }}
          </span>
      </p>

      <p class="font-bold mb-3 text-gray-700 uppercase">Email: 
          <span class="font-normal normal-case">
            {{ pacient.email }}
          </span>
      </p>

      <p class="font-bold mb-3 text-gray-700 uppercase">Fecha Alta:
          <span class="font-normal normal-case">
            {{ pacient.alta }}
          </span>
      </p>

      <p class="font-bold mb-3 text-gray-700 uppercase">Síntomas:
          <span class="font-normal normal-case">
            {{ pacient.sintoma }}
          </span>
      </p>

      <div class="grid md:grid-cols-2  gap-5 mt-10 ">
          <button 
              type="button"
              class="block w-full py-2 px-10 bg-indigo-600 hover:bg-indigo-700 text-white font-bold uppercase rounded-lg"
              @click="$emit('Actualizar-paciente', pacient.id)"
          >Editar</button>

          <button 
              type="button"
              class="block w-full py-2 px-10 bg-red-600 hover:bg-red-700 text-white font-bold uppercase rounded-lg"
              @click="$emit('Eliminar-Pacinte', pacient.id)"
          >Eliminar</button>
      </div>
  </div>
</template>