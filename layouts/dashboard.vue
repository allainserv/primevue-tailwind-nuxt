<template>
    <div class="flex h-screen bg-gray-100">
        <!-- Sidebar -->
        <aside class="w-64 bg-gray-900 text-white flex flex-col p-4 space-y-4 fixed inset-y-0 left-0 transform -translate-x-full md:translate-x-0 md:relative transition-transform duration-300 ease-in-out" :class="{ 'translate-x-0': isSidebarOpen }">
            <div class="flex items-center space-x-2 text-lg font-semibold">
                <HomeIcon class="w-6 h-6 text-indigo-400" />
                <span>Brand</span>
            </div>

            <nav class="flex-1">
                <ul class="space-y-2 text-sm font-normal">
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 bg-gray-800 rounded-md hover:bg-gray-700"> <HomeIcon class="w-5 h-5" /> <span>Dashboard</span> </a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><UsersIcon class="w-5 h-5" /> <span>Team</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><FolderIcon class="w-5 h-5" /> <span>Projects</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><CalendarIcon class="w-5 h-5" /> <span>Calendar</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><DocumentIcon class="w-5 h-5" /> <span>Documents</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><ChartBarIcon class="w-5 h-5" /> <span>Reports</span></a>
                    </li>
                </ul>
            </nav>
            <!-- <div>
                <h3 class="text-xs uppercase text-gray-500 mb-2">Your Teams</h3>
                <ul class="space-y-1">
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2"><UserCircleIcon class="w-5 h-5" /> <span>Heroicons</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2"><UserCircleIcon class="w-5 h-5" /> <span>Tailwind Labs</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2"><UserCircleIcon class="w-5 h-5" /> <span>Workcation</span></a>
                    </li>
                </ul>
            </div> -->
            <a href="#" class="flex items-center space-x-2 px-3 py-2 text-gray-400 hover:text-white"><CogIcon class="w-5 h-5" /> <span>Settings</span></a>
        </aside>

        <!-- Main content -->
        <div class="flex-1 flex flex-col">
            <!-- Header -->
            <header class="flex items-center justify-between bg-white p-4 shadow">
                <button class="md:hidden" @click="isSidebarOpen = !isSidebarOpen">
                    <Bars3Icon class="w-6 h-6 text-gray-700" />
                </button>
                <input type="text" placeholder="Search" class="px-4 py-2 border rounded-md w-1/3 hidden md:block" />
                <div class="flex items-center space-x-4">
                    <BellIcon class="w-6 h-6 text-gray-500" />
                    <Menu as="div" class="relative">
                        <MenuButton class="flex items-center space-x-2 cursor-pointer">
                            <span class="text-gray-700">Tom Cook</span>
                            <img src="https://placehold.co/32" class="rounded-full w-8 h-8" />
                        </MenuButton>
                        <MenuItems class="absolute right-0 mt-2 w-48 bg-white border rounded-md shadow-lg">
                            <MenuItem>
                                <a href="#" class="block px-4 py-2 text-gray-700 hover:bg-gray-100">Your profile</a>
                            </MenuItem>
                            <MenuItem>
                                <a href="#" class="block px-4 py-2 text-gray-700 hover:bg-gray-100">Sign out</a>
                            </MenuItem>
                        </MenuItems>
                    </Menu>
                </div>
            </header>

            <!-- Content -->
            <main class="flex-1 p-6 bg-gray-100 border-2 border-gray-300">
                <!-- Placeholder for content -->
                <slot />
            </main>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { HomeIcon, UsersIcon, FolderIcon, CalendarIcon, DocumentIcon, ChartBarIcon, UserCircleIcon, CogIcon, BellIcon, Bars3Icon } from '@heroicons/vue/24/solid';
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue';
const isSidebarOpen = ref(false);
</script>
