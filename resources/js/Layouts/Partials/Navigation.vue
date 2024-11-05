<script setup>
import {
    Sidebar,
    SidebarContent,
    SidebarGroup,
    SidebarGroupContent,
    SidebarGroupLabel,
    SidebarMenu,
    SidebarMenuButton,
    SidebarMenuItem,
} from '@/Components/ui/sidebar';
import { Home, Settings, Truck, User } from 'lucide-vue-next';

const items = [
    {
        title: 'Dashboard',
        url: route('dashboard'),
        route: 'dashboard',
        icon: Home,
    },
    {
        title: 'Menu',
        url: '#',
        route: 'vehicles.*',
        icon: Truck,
    },
    {
        title: 'Drivers',
        url: '#',
        route: 'drivers.*',
        icon: User,
    },
    {
        title: 'Settings',
        url: '#',
        route: 'settings.*',
        icon: Settings,
    },
];
</script>

<template>
    <Sidebar>
        <SidebarContent>
            <SidebarGroup>
                <SidebarGroupLabel class="my-8 text-2xl">{{
                    $page.props.app.name
                }}</SidebarGroupLabel>
                <SidebarGroupContent>
                    <SidebarMenu>
                        <SidebarMenuItem
                            v-for="item in items"
                            :key="item.title"
                        >
                            <SidebarMenuButton
                                asChild
                                :class="{
                                    'font-bold': route().current(item.route),
                                }"
                            >
                                <a :href="item.url">
                                    <component :is="item.icon" />
                                    <span class="text-md">{{
                                        item.title
                                    }}</span>
                                </a>
                            </SidebarMenuButton>
                        </SidebarMenuItem>
                    </SidebarMenu>
                </SidebarGroupContent>
            </SidebarGroup>
        </SidebarContent>
    </Sidebar>
</template>
