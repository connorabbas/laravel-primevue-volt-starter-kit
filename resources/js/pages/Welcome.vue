<script setup>
import { usePage } from '@inertiajs/vue3';
import { LayoutGrid, LogIn, Settings, UserPlus } from 'lucide-vue-next';
import Card from '@/components/primevue/volt/Card.vue';
import Button from '@/components/primevue/volt/Button.vue';

defineProps({
    laravelVersion: {
        type: String,
        required: true,
    },
    phpVersion: {
        type: String,
        required: true,
    },
});

const page = usePage();
</script>

<template>
    <InertiaHead title="Welcome" />

    <div class="min-h-full">
        <div class="h-screen flex items-center justify-center">
            <Card pt:body:class="p-4 py-6 sm:p-12">
                <template #content>
                    <div class="text-center md:text-left">
                        <div class="flex gap-3">
                            <div class="block text-6xl font-bold text-red-500 dark:text-red-400 mb-1">
                                Laravel,
                            </div>
                            <div class="text-6xl font-bold text-indigo-500 dark:text-indigo-400 mb-1">
                                Inertia.js,
                            </div>
                        </div>
                        <div class="text-6xl text-green-500 dark:text-green-400 text-emerald font-bold mb-4">
                            & PrimeVue Volt
                        </div>
                        <p class="mt-0 mb-4 text-muted-color leading-normal">
                            A starter kit using
                            <a
                                href="https://laravel.com/docs/master"
                                class="underline text-primary hover:text-color"
                            >Laravel</a>,
                            <a
                                href="https://inertiajs.com/"
                                class="underline text-primary hover:text-color"
                            >Inertia.js</a>, and
                            <a
                                href="https://volt.primevue.org/"
                                class="underline text-primary hover:text-color"
                            >PrimeVue Volt</a>.
                        </p>
                        <template v-if="page.props.auth.user">
                            <InertiaLink :href="route('dashboard')">
                                <Button
                                    label="Dashboard"
                                    class="mr-4"
                                >
                                    <template #icon>
                                        <LayoutGrid />
                                    </template>
                                </Button>
                            </InertiaLink>
                            <InertiaLink :href="route('profile.edit')">
                                <Button
                                    outlined
                                    label="Profile Settings"
                                    class="mr-4"
                                >
                                    <template #icon>
                                        <Settings />
                                    </template>
                                </Button>
                            </InertiaLink>
                        </template>
                        <template v-else>
                            <InertiaLink :href="route('login')">
                                <Button
                                    label="Login"
                                    class="mr-4"
                                >
                                    <template #icon>
                                        <LogIn />
                                    </template>
                                </Button>
                            </InertiaLink>
                            <InertiaLink :href="route('register')">
                                <Button
                                    outlined
                                    label="Register"
                                    class="mr-4"
                                >
                                    <template #icon>
                                        <UserPlus />
                                    </template>
                                </Button>
                            </InertiaLink>
                        </template>
                        <div class="mt-6">
                            <p class="m-0 text-sm text-muted-color">
                                Laravel v{{ laravelVersion }} (PHP v{{
                                    phpVersion
                                }})
                            </p>
                        </div>
                    </div>
                </template>
            </Card>
        </div>
    </div>
</template>
