<script setup>
import { reactive } from 'vue';
import router from '../router';
import axios from 'axios';
import { useToast } from 'vue-toastification';

const form = reactive({
    type: 'Full-Time',
    title: '',
    description: '',
    salary: '',
    location: '',
    company: {
        name: '',
        description: '',
        contactEmail: '',
        contactPhone: ''
    }
})

const toast = useToast();

const handleSubmit = async () => {
    const newJob = {
        type: form.type,
        title: form.title,
        description: form.description,
        salary: form.salary,
        location: form.location,
        company: {
            name: form.company.name,
            description: form.company.description,
            contactEmail: form.company.contactEmail,
            contactPhone: form.company.contactPhone
    }
}

try {
        const response = await axios.post(`/api/jobs`, newJob);
        toast.success('Job added successfully!');
        router.push(`/jobs/${response.data.id}`);
    } catch (error) {
        console.error('Error fetching job:', error);
        toast.error('Failed to add job. Please try again.');

    }
}


</script>

<template>
<section class="bg-green-50">
      <div class="container m-auto max-w-2xl py-24">
        <div
          class="bg-white px-6 py-8 mb-4 shadow-md rounded-md border m-4 md:m-0"
        >
          <form @submit.prevent="handleSubmit">
            <h2 class="text-3xl text-center font-semibold mb-6">Adicionar Vaga</h2>

            <div class="mb-4">
              <label for="type" class="block text-gray-700 font-bold mb-2"
                >Tipo de Vaga</label
              >
              <select
                v-model="form.type"
                id="type"
                name="type"
                class="border rounded w-full py-2 px-3"
                required
              >
                <option value="Full-Time">Tempo Integral</option>
                <option value="Part-Time">Meio Período</option>
                <option value="Remote">Remoto</option>
                <option value="Internship">Estágio</option>
              </select>
            </div>

            <div class="mb-4">
              <label class="block text-gray-700 font-bold mb-2"
                >Nome da Vaga</label
              >
              <input
                v-model="form.title"
                type="text"
                id="name"
                name="name"
                class="border rounded w-full py-2 px-3 mb-2"
                placeholder="Ex: Desenvolvedor Front-end Sênior"
                required
              />
            </div>
            <div class="mb-4">
              <label
                for="description"
                class="block text-gray-700 font-bold mb-2"
                >Descrição da Vaga</label
              >
              <textarea
                v-model="form.description"
                id="description"
                name="description"
                class="border rounded w-full py-2 px-3"
                rows="4"
                placeholder="Adicione deveres, expectativas, requisitos, etc."
              ></textarea>
            </div>

            <div class="mb-4">
              <label for="type" class="block text-gray-700 font-bold mb-2"
                >Salário</label
              >
              <select
                v-model="form.salary"
                id="salary"
                name="salary"
                class="border rounded w-full py-2 px-3"
                required
              >
                <option value="Under $50K">Até R$ 5.000 </option>
                <option value="$50K - $60K">R$ 5.000 - R$ 8.000 </option>
                <option value="$60K - $70K">R$ 8.000 - R$ 12.000 </option>
                <option value="$70K - $80K">R$ 12.000 - R$ 15.000 </option>
                <option value="$80K - $90K">R$ 15.000 - R$ 18.000 </option>
                <option value="$90K - $100K">R$ 18.000 - R$ 22.000 </option>
                <option value="$100K - $125K">R$ 22.000 - R$ 28.000 </option>
                <option value="$125K - $150K">R$ 28.000 - R$ 35.000 </option>
                <option value="$150K - $175K">R$ 35.000 - R$ 45.000 </option>
                <option value="$175K - $200K">R$ 45.000 - R$ 55.000 </option>
                <option value="Over $200K">Acima de R$ 55.000 </option>
              </select>
            </div>

            <div class="mb-4">
              <label class="block text-gray-700 font-bold mb-2">
                Localização
              </label>
              <input
                v-model="form.location"
                type="text"
                id="location"
                name="location"
                class="border rounded w-full py-2 px-3 mb-2"
                placeholder="Localização da Empresa"
                required
              />
            </div>

            <h3 class="text-2xl mb-5">Informações da Empresa</h3>

            <div class="mb-4">
              <label for="company" class="block text-gray-700 font-bold mb-2"
                >Nome da Empresa</label
              >
              <input
                v-model="form.company.name"
                type="text"
                id="company"
                name="company"
                class="border rounded w-full py-2 px-3"
                placeholder="Nome da Empresa"
              />
            </div>

            <div class="mb-4">
              <label
                for="company_description"
                class="block text-gray-700 font-bold mb-2"
                >Descrição da Empresa</label
              >
              <textarea
                v-model="form.company.description"
                id="company_description"
                name="company_description"
                class="border rounded w-full py-2 px-3"
                rows="4"
                placeholder="O que sua empresa faz?"
              ></textarea>
            </div>

            <div class="mb-4">
              <label
                for="contact_email"
                class="block text-gray-700 font-bold mb-2"
                >Email de Contato</label
              >
              <input
                v-model="form.company.contactEmail"
                type="email"
                id="contact_email"
                name="contact_email"
                class="border rounded w-full py-2 px-3"
                placeholder="Endereço de email para candidatos"
                required
              />
            </div>
            <div class="mb-4">
              <label
                for="contact_phone"
                class="block text-gray-700 font-bold mb-2"
                >Telefone de Contato</label
              >
              <input
                v-model="form.company.contactPhone"
                type="tel"
                id="contact_phone"
                name="contact_phone"
                class="border rounded w-full py-2 px-3"
                placeholder="Telefone opcional para candidatos"
              />
            </div>

            <div>
              <button
                class="bg-green-500 hover:bg-green-600 text-white font-bold py-2 px-4 rounded-full w-full focus:outline-none focus:shadow-outline"
                type="submit"
              >
                Adicionar Vaga
              </button>
            </div>
          </form>
        </div>
      </div>
    </section>
</template>