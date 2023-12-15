<script setup>
import {useForm} from '@inertiajs/vue3';
import ActionMessage from '@/Components/ActionMessage.vue';
import FormSection from '@/Components/FormSection.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import PrimaryButton from '@/Components/PrimaryButton.vue';
import TextInput from '@/Components/TextInput.vue';
import AppLayout from "@/Layouts/AppLayout.vue";

const createUserForm = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
});


const createApiToken = () => {
    createUserForm.post(route('admin.users.store'), {
        preserveScroll: true,
        onSuccess: () => {
            createUserForm.reset();
        },
    });
};


</script>

<template>
    <AppLayout>
        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">

        <!-- Generate API Token -->
        <FormSection @submitted="createApiToken">
            <template #title>
                Create User
            </template>

            <template #description>
                Create a new account.
            </template>

            <template #form>
                <!-- Token Name -->
                <div class="col-span-6 sm:col-span-4">
                    <InputLabel for="name" value="Name" />
                    <TextInput
                        id="name"
                        v-model="createUserForm.name"
                        autofocus
                        class="mt-1 block w-full"
                        type="text"
                    />
                    <InputError :message="createUserForm.errors.name" class="mt-2" />
                </div>
                <div class="col-span-6 sm:col-span-4">
                    <InputLabel for="email" value="Email" />
                    <TextInput
                        id="email"
                        v-model="createUserForm.email"
                        autofocus
                        class="mt-1 block w-full"
                        type="email"
                    />
                    <InputError :message="createUserForm.errors.email" class="mt-2" />
                </div>
                <div class="col-span-6 sm:col-span-4">
                    <InputLabel for="password" value="Password" />
                    <TextInput
                        id="name"
                        v-model="createUserForm.password"
                        autofocus
                        class="mt-1 block w-full"
                        type="password"
                    />
                    <InputError :message="createUserForm.errors.password" class="mt-2" />
                </div>
                <div class="col-span-6 sm:col-span-4">
                    <InputLabel for="password_confirmation" value="Confirm Password" />
                    <TextInput
                        id="password_confirmation"
                        v-model="createUserForm.password_confirmation"
                        autofocus
                        class="mt-1 block w-full"
                        type="password"
                    />
                    <InputError :message="createUserForm.errors.password_confirmation" class="mt-2" />
                </div>
            </template>

            <template #actions>
                <ActionMessage :on="createUserForm.recentlySuccessful" class="me-3">
                    Created.
                </ActionMessage>

                <PrimaryButton :class="{ 'opacity-25': createUserForm.processing }" :disabled="createUserForm.processing">
                    Create
                </PrimaryButton>
            </template>
        </FormSection>
            </div>
        </div>
    </AppLayout>
</template>
