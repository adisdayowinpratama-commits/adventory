<script setup lang="ts">
import { ref } from 'vue'
import { Link } from '@inertiajs/vue3'
import {
    LayoutDashboard,
    Package,
    Tags,
    ArrowDownToLine,
    ArrowUpFromLine,
    Truck,
    Warehouse,
    ChartNoAxesCombined,
    Bell,
    Users,
    Settings,
    Boxes,
    ChevronDown,
    Menu,
    X,
    CircleHelp,
} from 'lucide-vue-next'

const sidebarOpen = ref(false)

const navigation = [
    { label: 'Dashboard', icon: LayoutDashboard, href: '/dashboard', active: true },
    { label: 'Manajemen Barang', icon: Package },
    { label: 'Kategori', icon: Tags },
    { label: 'Stok Masuk', icon: ArrowDownToLine },
    { label: 'Stok Keluar', icon: ArrowUpFromLine },
    { label: 'Supplier', icon: Truck },
    { label: 'Manajemen Gudang', icon: Warehouse },
]

const management = [
    { label: 'Laporan & Analitik', icon: ChartNoAxesCombined },
    { label: 'Pengguna', icon: Users },
]

</script>

<template>
    <div class="min-h-screen bg-[#f5f7f6] text-[#172b25]">

        <!-- Mobile overlay -->
        <div
            v-if="sidebarOpen"
            class="fixed inset-0 z-40 bg-black/40 lg:hidden"
            @click="sidebarOpen = false"
        ></div>

        <!-- Sidebar -->
        <aside
            :class="[
                'fixed inset-y-0 left-0 z-50 flex w-64 flex-col bg-[#102b25] text-white transition-transform duration-300 lg:translate-x-0',
                sidebarOpen ? 'translate-x-0' : '-translate-x-full'
            ]"
        >
            <!-- Brand -->
            <div class="flex h-20 items-center justify-between border-b border-white/10 px-6">
                <div class="flex items-center gap-3">
                    <div class="flex h-10 w-10 items-center justify-center rounded-xl bg-[#16a36a]">
                        <Boxes :size="23" class="text-white" />
                    </div>

                    <div>
                        <h1 class="text-xl font-bold tracking-wide">Adventory</h1>
                        <p class="text-[10px] tracking-[2px] text-emerald-300">
                            ADVANCED INVENTORY
                        </p>
                    </div>
                </div>

                <button
                    class="text-white lg:hidden"
                    @click="sidebarOpen = false"
                    aria-label="Close sidebar"
                >
                    <X :size="22" />
                </button>
            </div>

            <!-- Main navigation -->
            <div class="sidebar-scroll min-h-0 flex-1 overflow-y-auto overscroll-contain px-4 py-6">
                <p class="mb-3 px-3 text-[10px] font-semibold uppercase tracking-[2px] text-emerald-300/60">
                    Main Menu
                </p>

                <nav class="space-y-1">
                    <template v-for="item in navigation" :key="item.label">
                        <Link
                            v-if="item.href"
                            :href="item.href"
                            @click="sidebarOpen = false"
                            class="flex items-center gap-3 rounded-xl px-3 py-3 text-sm font-medium transition"
                            :class="item.active
                                ? 'bg-[#16a36a] text-white shadow-lg shadow-emerald-950/20'
                                : 'text-emerald-50/70 hover:bg-white/10 hover:text-white'"
                        >
                            <component :is="item.icon" :size="19" />
                            {{ item.label }}
                        </Link>

                        <div
                            v-else
                            class="flex cursor-not-allowed items-center justify-between rounded-xl px-3 py-3 text-sm text-emerald-50/45"
                        >
                            <span class="flex items-center gap-3">
                                <component :is="item.icon" :size="19" />
                                {{ item.label }}
                            </span>
                            <span class="rounded bg-white/10 px-1.5 py-0.5 text-[9px]">
                                Soon
                            </span>
                        </div>
                    </template>
                </nav>

                <p class="mb-3 mt-9 px-3 text-[10px] font-semibold uppercase tracking-[2px] text-emerald-300/60">
                    Management
                </p>

                <nav class="space-y-1">
                    <div
                        v-for="item in management"
                        :key="item.label"
                        class="flex cursor-not-allowed items-center justify-between rounded-xl px-3 py-3 text-sm text-emerald-50/45"
                    >
                        <span class="flex items-center gap-3">
                            <component :is="item.icon" :size="19" />
                            {{ item.label }}
                        </span>
                        <span class="rounded bg-white/10 px-1.5 py-0.5 text-[9px]">
                            Soon
                        </span>
                    </div>

                    <div class="flex cursor-not-allowed items-center gap-3 rounded-xl px-3 py-3 text-sm text-emerald-50/45">
                        <Settings :size="19" />
                        Pengaturan
                    </div>
                </nav>
            </div>

            <!-- Sidebar footer -->
            <div class="border-t border-white/10 p-4">
                <div class="flex items-center gap-3 rounded-xl bg-white/5 p-3">
                    <div class="flex h-9 w-9 items-center justify-center rounded-lg bg-emerald-500/20 text-sm font-bold text-emerald-300">
                        A
                    </div>
                    <div class="min-w-0 flex-1">
                        <p class="truncate text-sm font-semibold">Adventory Admin</p>
                        <p class="text-xs text-emerald-100/50">Administrator</p>
                    </div>
                    <CircleHelp :size="17" class="text-emerald-100/50" />
                </div>
            </div>
        </aside>

        <!-- Main content -->
        <div class="min-h-screen lg:pl-64">

            <!-- Topbar -->
            <header class="sticky top-0 z-30 flex h-20 items-center justify-between border-b border-gray-200 bg-white/95 px-5 backdrop-blur sm:px-8">
                <div class="flex items-center gap-3">
                    <button
                        class="rounded-lg p-2 text-gray-600 hover:bg-gray-100 lg:hidden"
                        @click="sidebarOpen = true"
                        aria-label="Open sidebar"
                    >
                        <Menu :size="22" />
                    </button>

                    <div>
                        <p class="text-xs text-gray-400">Workspace / Overview</p>
                        <h2 class="text-lg font-bold text-[#173b30]">Dashboard</h2>
                    </div>
                </div>

                <div class="flex items-center gap-3">
                    <div class="hidden text-right sm:block">
                        <p class="text-sm font-semibold text-gray-700">Adventory Admin</p>
                        <p class="text-xs text-gray-400">Administrator</p>
                    </div>

                    <div class="flex h-10 w-10 items-center justify-center rounded-xl bg-[#e1f4eb] font-bold text-[#138253]">
                        AD
                    </div>
                    <ChevronDown :size="16" class="text-gray-400" />
                </div>
            </header>

            <!-- Page content -->
            <main class="p-5 sm:p-8">
                <slot />
            </main>

        </div>
    </div>
</template>