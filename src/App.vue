<script setup>
import { ref, reactive, watch, onMounted} from 'vue';
import { uid } from 'uid'
import Header from './components/header.vue';
import Formulario from './components/Formulario.vue';
import pacientes from './components/pacientes.vue';

const paciente = ref([]);

const Paciente = reactive({
  id: null,
  nombre: '',
  propietario:'',
  email:'',
  alta:'',
  sintoma:''
})

watch(paciente, () => {
  guardarLocalStorage()
}, {
  deep:true
})

const guardarLocalStorage = () => {
  localStorage.setItem('Pacientes', JSON.stringify(paciente.value))
}

onMounted(() => {
  const pacientesStorage = localStorage.getItem('Pacientes')
  if (pacientesStorage) {
    paciente.value = JSON.parse(pacientesStorage)
  }
})

const GuardarPaciente = () => {
  if (Paciente.id) {
    const { id } = Paciente
    const i = paciente.value.findIndex((pacienteState) => pacienteState.id === id)
    paciente.value[i] = {...Paciente}
  }else {
    paciente.value.push({
    ...Paciente, 
    id:uid()
  })
  }
  // REINICIAR EL OBJETO
  Object.assign(Paciente, {
    nombre: '',
    propietario:'',
    email:'',
    alta:'',
    sintoma:'',
    id:null
  })
}

const ActualizarPaciente = (id) => {
    const pacienteEditar = paciente.value.filter(Paciente => Paciente.id === id ) [0]
    // esto ayuda a llenar el formulario para editarlo
    Object.assign(Paciente, pacienteEditar)
} 

const EliminarPaciente = (id) => {
  paciente.value = paciente.value.filter(Paciente => Paciente.id !== id )
}
</script>

<template>
  <div class="container mx-auto mt-20">
    <Header/>
    <div class="mt-12 md:flex">
      <Formulario
      v-model:nombre="Paciente.nombre"
      v-model:propietario="Paciente.propietario"
      v-model:email="Paciente.email"
      v-model:alta="Paciente.alta"
      v-model:sintoma="Paciente.sintoma"
      @guardar-paciente="GuardarPaciente"
      :id="Paciente.id"
      />

    <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center"> Administrar tus Pacientes</h3>
        <p class="text-lg mt-5 text-center mb-10">
            Información de 
      <span class="text-indigo-600 font-bold">Pacientes</span>
  </p>
        <div v-if="paciente.length > 0 ">
          <pacientes
          v-for="Paciente in paciente"
          :pacient="Paciente"
          @Actualizar-paciente="ActualizarPaciente"
          @Eliminar-Pacinte="EliminarPaciente"
          />
        </div>
        <p v-else class="mt-10 text-2xl text-center"> No hay pacientes.</p>
    </div>
  </div>
  </div>
  
</template>

