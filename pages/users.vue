<template>
    <div class="p-6 bg-white rounded-2xl shadow-md">
        <div class="flex justify-between items-center mb-4">
            <h2 class="text-xl font-semibold">Users</h2>
            <div class="flex items-center space-x-4">
                <input type="text" v-model="searchQuery" placeholder="Search users" class="px-4 py-2 border rounded-lg focus:outline-none focus:ring focus:ring-indigo-300" />
                <button class="px-4 py-2 bg-indigo-600 text-white rounded-lg shadow hover:bg-indigo-700" @click="printTable">Print</button>
                <button class="px-4 py-2 bg-indigo-600 text-white rounded-lg shadow hover:bg-indigo-700">Add user</button>
            </div>
        </div>
        <p class="text-gray-500 mb-6">A list of all the users in your account including their name, title, email, and role.</p>
        <div class="overflow-x-auto">
            <table class="min-w-full divide-y divide-gray-200">
                <thead class="bg-gray-100">
                    <tr>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Name</th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider hidden sm:table-cell">Title</th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider hidden md:table-cell">Email</th>
                        <th scope="col" class="px-6 py-3 text-left text-xs font-medium text-gray-500 uppercase tracking-wider">Role</th>
                        <th class="px-6 py-3"></th>
                    </tr>
                </thead>
                <tbody class="bg-white divide-y divide-gray-200">
                    <tr v-for="user in paginatedUsers" :key="user.email">
                        <td class="px-6 py-4 text-sm font-medium text-gray-900">{{ user.name }}</td>
                        <td class="px-6 py-4 text-sm text-gray-500 hidden sm:table-cell">{{ user.title }}</td>
                        <td class="px-6 py-4 text-sm text-gray-500 hidden md:table-cell">{{ user.email }}</td>
                        <td class="px-6 py-4 text-sm text-gray-500">{{ user.role }}</td>
                        <td class="px-6 py-4 text-right">
                            <button class="text-indigo-600 hover:text-indigo-900 font-medium">Edit</button>
                        </td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Enhanced Pagination Controls -->
        <div class="flex justify-between items-center mt-4">
            <span class="text-sm text-gray-700">Showing {{ startItem }} to {{ endItem }} of {{ filteredUsers.length }} results</span>
            <div class="flex items-center space-x-2">
                <button :disabled="currentPage === 1" @click="previousPage" class="px-3 py-2 border rounded-lg disabled:opacity-50">&laquo;</button>
                <button v-for="page in visiblePageNumbers" :key="page" :class="['px-3 py-2 rounded-lg', currentPage === page ? 'bg-indigo-600 text-white' : 'border bg-white text-gray-700']" @click="goToPage(page)">
                    {{ page }}
                </button>
                <span v-if="showEllipsisAfter">...</span>
                <button :disabled="currentPage === totalPages" @click="nextPage" class="px-3 py-2 border rounded-lg disabled:opacity-50">&raquo;</button>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
interface User {
    name: string;
    title: string;
    email: string;
    role: string;
}

const users: User[] = [
    { name: 'Lindsay Walton', title: 'Front-end Developer', email: 'lindsay.walton@example.com', role: 'Member' },
    { name: 'Courtney Henry', title: 'Designer', email: 'courtney.henry@example.com', role: 'Admin' },
    { name: 'Tom Cook', title: 'Director of Product', email: 'tom.cook@example.com', role: 'Member' },
    { name: 'Whitney Francis', title: 'Copywriter', email: 'whitney.francis@example.com', role: 'Admin' },
    { name: 'Leonard Krasner', title: 'Senior Designer', email: 'leonard.krasner@example.com', role: 'Owner' },
    { name: 'Floyd Miles', title: 'Principal Designer', email: 'floyd.miles@example.com', role: 'Member' },
    { name: 'Jane Doe', title: 'Backend Developer', email: 'jane.doe@example.com', role: 'Admin' },
    { name: 'John Smith', title: 'UX Designer', email: 'john.smith@example.com', role: 'Member' }
    // Add more users as needed
];

const searchQuery = ref('');
const currentPage = ref(1);
const itemsPerPage = 10;

// Computed properties for filtered and paginated users
const filteredUsers = computed(() => {
    return users.filter((user) => Object.values(user).join(' ').toLowerCase().includes(searchQuery.value.toLowerCase()));
});

const totalPages = computed(() => Math.ceil(filteredUsers.value.length / itemsPerPage));

const paginatedUsers = computed(() => {
    const start = (currentPage.value - 1) * itemsPerPage;
    const end = start + itemsPerPage;
    return filteredUsers.value.slice(start, end);
});

const startItem = computed(() => (currentPage.value - 1) * itemsPerPage + 1);
const endItem = computed(() => Math.min(currentPage.value * itemsPerPage, filteredUsers.value.length));

const visiblePageNumbers = computed(() => {
    const maxVisiblePages = 5;
    const pages = [];

    for (let i = 1; i <= totalPages.value; i++) {
        if (i <= maxVisiblePages || i === totalPages.value) {
            pages.push(i);
        }
    }

    return pages;
});

const showEllipsisAfter = computed(() => totalPages.value > visiblePageNumbers.value.length);

const goToPage = (page: number) => {
    currentPage.value = page;
};

const nextPage = () => {
    if (currentPage.value < totalPages.value) {
        currentPage.value++;
    }
};

const previousPage = () => {
    if (currentPage.value > 1) {
        currentPage.value--;
    }
};

const printTable = () => {
    window.print();
};
</script>
