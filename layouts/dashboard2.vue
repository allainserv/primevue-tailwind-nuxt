<template>
    <div class="flex h-screen bg-gray-100 relative">
        <!-- Sidebar Overlay for Mobile -->
        <div v-if="isSidebarOpen" class="fixed inset-0 bg-black bg-opacity-50 md:hidden z-20" @click="isSidebarOpen = false"></div>

        <!-- Sidebar -->
        <aside
            class="w-64 bg-gray-900 text-white flex flex-col p-4 space-y-4 fixed inset-y-0 left-0 transform -translate-x-full md:translate-x-0 md:relative transition-transform duration-300 ease-in-out z-30"
            :class="{ 'translate-x-0': isSidebarOpen }"
        >
            <div class="flex items-center space-x-2 text-lg font-semibold">
                <UsersIcon class="w-6 h-6 text-indigo-400" />
                <span>JOBS</span>
            </div>

            <nav class="flex-1">
                <ul class="space-y-2 text-sm">
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 bg-gray-800 rounded-md hover:bg-gray-700"> <HomeIcon class="w-5 h-5" /> <span>Dashboard</span> </a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><UsersIcon class="w-5 h-5" /> <span>Jobs</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><FolderIcon class="w-5 h-5" /> <span>Applicants</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><CalendarIcon class="w-5 h-5" /> <span>Certificates</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><DocumentIcon class="w-5 h-5" /> <span>Skills</span></a>
                    </li>
                    <li>
                        <a href="#" class="flex items-center space-x-2 px-3 py-2 rounded-md hover:bg-gray-700"><ChartBarIcon class="w-5 h-5" /> <span>Reports</span></a>
                    </li>
                </ul>
            </nav>
            <a href="#" class="flex items-center space-x-2 px-3 py-2 text-gray-400 hover:text-white hover:bg-gray-700"><CogIcon class="w-5 h-5" /> <span>Settings</span></a>
        </aside>

        <!-- Main content -->
        <div class="flex-1 flex flex-col relative">
            <!-- Header -->
            <header class="flex items-center justify-between bg-white p-4 shadow z-10 relative">
                <button class="md:hidden" @click="isSidebarOpen = !isSidebarOpen">
                    <Bars3Icon class="w-6 h-6 text-gray-700" />
                </button>
                <input type="text" placeholder="Search" class="px-4 py-2 border rounded-md w-1/3 hidden md:block" />
                <div class="flex items-center space-x-4">
                    <BellIcon class="w-6 h-6 text-gray-500" />
                    <Menu as="div" class="relative">
                        <MenuButton class="flex items-center space-x-2 cursor-pointer">
                            <span class="text-gray-700">Tom Cook</span>
                            <img src="https://via.placeholder.com/32" class="rounded-full w-8 h-8" />
                        </MenuButton>
                        <MenuItems class="absolute right-0 mt-2 w-48 bg-white border rounded-md shadow-lg z-20">
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
            <main class="flex-1 p-6 bg-gray-100 border-dashed border-2 border-gray-300 relative z-0">
                <!-- Placeholder for content -->
                <slot />
            </main>
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue';
import { HomeIcon, UsersIcon, FolderIcon, CalendarIcon, DocumentIcon, ChartBarIcon, CogIcon, BellIcon, Bars3Icon } from '@heroicons/vue/24/solid';
import { Menu, MenuButton, MenuItems, MenuItem } from '@headlessui/vue';
const isSidebarOpen = ref(false);
</script>
