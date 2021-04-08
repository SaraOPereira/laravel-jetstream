<template>
    <div class="min-h-screen bg-white flex">
        <div class="flex-1 flex flex-col justify-center py-12 px-4 sm:px-6 lg:flex-none lg:px-20 xl:px-24">
            <div class="mx-auto w-full max-w-sm lg:w-96">
                <div>
                    <img class="h-12 w-auto" src="https://tailwindui.com/img/logos/v1/workflow-mark-on-white.svg" alt="Workflow">
                    <h2 class="mt-6 text-3xl leading-9 font-extrabold text-gray-900">
                        Sign in to your account
                    </h2>
                </div>

                <div class="mt-8">
                    <div class="mt-6">
                        <jet-validation-errors class="mb-4" />

                        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
                            {{ status }}
                        </div>

                        <form @submit.prevent="submit" class="space-y-6">
                            <div>
                                <jet-label for="email" class="block text-sm font-medium leading-5 text-gray-700" value="Email" />
                                <div class="mt-1 rounded-md shadow-sm">
                                    <jet-input id="email" type="email" class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md placeholder-gray-400 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 transition duration-150 ease-in-out sm:text-sm sm:leading-5" v-model="form.email" required autofocus />
                                </div>
                            </div>

                            <div>
                                <jet-label for="password" class="block text-sm font-medium leading-5 text-gray-700" value="Password" />
                                <div class="mt-1 rounded-md shadow-sm">
                                    <jet-input id="password" type="password" class="appearance-none block w-full px-3 py-2 border border-gray-300 rounded-md placeholder-gray-400 focus:outline-none focus:shadow-outline-blue focus:border-blue-300 transition duration-150 ease-in-out sm:text-sm sm:leading-5" v-model="form.password" required autocomplete="current-password" />
                                </div>
                            </div>

                            <div class="flex items-center justify-between">
                                <div class="flex items-center">
                                    <jet-checkbox name="remember" class="form-checkbox h-4 w-4 text-indigo-600 transition duration-150 ease-in-out" v-model:checked="form.remember" />
                                    <label for="remember" class="ml-2 block text-sm leading-5 text-gray-900">
                                        Remember me
                                    </label>
                                </div>

                                <div class="text-sm leading-5">
                                    <inertia-link v-if="canResetPassword" :href="route('password.request')" class="font-medium text-indigo-600 hover:text-indigo-500 focus:outline-none focus:underline transition ease-in-out duration-150">
                                        Forgot your password?
                                    </inertia-link>
                                </div>
                            </div>

                            <div>
                                <span class="block w-full rounded-md shadow-sm">
                                    <jet-button :class="{ 'opacity-25': form.processing }" :disabled="form.processing" class="w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-indigo-600 hover:bg-indigo-500 focus:outline-none focus:border-indigo-700 focus:shadow-outline-indigo active:bg-indigo-700 transition duration-150 ease-in-out">
                                        Log in
                                    </jet-button>
                                </span>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
        <div class="hidden lg:block relative w-0 flex-1">
            <img class="absolute inset-0 h-full w-full object-cover" src="https://images.unsplash.com/photo-1505904267569-f02eaeb45a4c?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1908&q=80" alt="background image">
        </div>
    </div>
</template>

<script>
    import JetAuthenticationCard from '@/Jetstream/AuthenticationCard'
    import JetAuthenticationCardLogo from '@/Jetstream/AuthenticationCardLogo'
    import JetButton from '@/Jetstream/Button'
    import JetInput from '@/Jetstream/Input'
    import JetCheckbox from '@/Jetstream/Checkbox'
    import JetLabel from '@/Jetstream/Label'
    import JetValidationErrors from '@/Jetstream/ValidationErrors'

    export default {
        components: {
            JetAuthenticationCard,
            JetAuthenticationCardLogo,
            JetButton,
            JetInput,
            JetCheckbox,
            JetLabel,
            JetValidationErrors
        },

        props: {
            canResetPassword: Boolean,
            status: String
        },

        data() {
            return {
                form: this.$inertia.form({
                    email: '',
                    password: '',
                    remember: false
                })
            }
        },

        methods: {
            submit() {
                this.form
                    .transform(data => ({
                        ... data,
                        remember: this.form.remember ? 'on' : ''
                    }))
                    .post(this.route('login'), {
                        onFinish: () => this.form.reset('password'),
                    })
            }
        }
    }
</script>
