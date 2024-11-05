<template>
    <SidebarProvider :style="sidebarStyles">
        <Navigation />
        <main class="flex flex-col flex-grow gap-4 p-4 bg-slate-50 lg:p-6">
            <header class="flex justify-between">
                <SidebarTrigger />
                <DropdownMenu>
                    <DropdownMenuTrigger>
                        <div class="flex items-center space-x-2">
                            <Label
                                class="text-sm font-normal capitalize cursor-pointer select-none"
                                >{{ $page.props.auth.user.name }}</Label
                            >
                            <Avatar>
                                <AvatarImage
                                    src="https://avatar.iran.liara.run/public/boy?username=Scott"
                                    alt="@radix-vue"
                                />
                                <AvatarFallback>{{
                                    $page.props.auth.user.name
                                }}</AvatarFallback>
                            </Avatar>
                        </div>
                    </DropdownMenuTrigger>
                    <DropdownMenuContent align="end">
                        <DropdownMenuItem
                            class="space-x-2"
                            @click="$inertia.get(route('profile.edit'))"
                        >
                            <User class="w-5 h-5" />
                            <span>Profile</span>
                        </DropdownMenuItem>
                        <DropdownMenuSeparator />
                        <DropdownMenuItem
                            class="space-x-2"
                            @click="$inertia.post(route('logout'))"
                        >
                            <LogOut class="w-5 h-5" />
                            <span>Logout</span>
                        </DropdownMenuItem>
                    </DropdownMenuContent>
                </DropdownMenu>
            </header>
            <Breadcrumbs :breadcrumbs="$page.props.breadcrumbs" />
            <slot />
            <!-- <Toaster v-if="$page.props.flash.type"/> -->
        </main>
    </SidebarProvider>
</template>

<script setup>
import { Avatar, AvatarFallback, AvatarImage } from '@/Components/ui/avatar';
import { SidebarProvider, SidebarTrigger } from '@/Components/ui/sidebar';
import { usePage } from '@inertiajs/vue3';
import { watchEffect } from 'vue';
import Navigation from './Partials/Navigation.vue';
import {
    DropdownMenu,
    DropdownMenuContent,
    DropdownMenuItem,
    DropdownMenuSeparator,
    DropdownMenuTrigger,
} from '@/Components/ui/dropdown-menu';
import Label from '@/Components/ui/label/Label.vue';
import { LogOut, User } from 'lucide-vue-next';
import Breadcrumbs from '@/Components/Breadcrumbs.vue';

const { props } = usePage();

const sidebarStyles = {
    '--sidebar-width': '20rem',
    '--sidebar-width-mobile': '20rem',
};

watchEffect(() => {
    window.Laravel = window.Laravel || {};
    if (props.auth.permissions) {
        window.Laravel.jsPermissions = props.auth.permissions;
    }
});
</script>
