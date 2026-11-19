<script setup lang="ts">
import AdventoryLayout from '@/layouts/AdventoryLayout.vue'
import { Head } from '@inertiajs/vue3'

import {
    Package,
    Boxes,
    AlertTriangle,
    XCircle,
    ArrowDownLeft,
    ArrowUpRight,
    TrendingUp,
    Clock3,
    MoreHorizontal,
} from 'lucide-vue-next'

defineOptions({
    layout: AdventoryLayout,
})

// Data sementara untuk preview UI.
// Nantinya akan diganti dengan data dari database MySQL.
const statistics = [
    {
        title: 'Total Produk',
        value: '1,284',
        description: 'Produk terdaftar',
        icon: Package,
        color: 'bg-blue-50 text-blue-600',
    },
    {
        title: 'Total Stok',
        value: '8,450',
        description: 'Unit tersedia',
        icon: Boxes,
        color: 'bg-emerald-50 text-emerald-600',
    },
    {
        title: 'Stok Menipis',
        value: '08',
        description: 'Perlu pengisian ulang',
        icon: AlertTriangle,
        color: 'bg-amber-50 text-amber-600',
    },
    {
        title: 'Stok Habis',
        value: '03',
        description: 'Produk tidak tersedia',
        icon: XCircle,
        color: 'bg-rose-50 text-rose-600',
    },
]

const stockMovements = [
    { day: 'Sen', incoming: 65, outgoing: 35 },
    { day: 'Sel', incoming: 80, outgoing: 50 },
    { day: 'Rab', incoming: 50, outgoing: 40 },
    { day: 'Kam', incoming: 90, outgoing: 60 },
    { day: 'Jum', incoming: 70, outgoing: 45 },
    { day: 'Sab', incoming: 45, outgoing: 30 },
    { day: 'Min', incoming: 75, outgoing: 55 },
]

const transactions = [
    {
        code: 'TRX-2026-001',
        product: 'Wireless Mouse Logitech',
        type: 'Stok Masuk',
        quantity: '+25 Unit',
        date: '19 Nov 2026',
    },
    {
        code: 'TRX-2026-002',
        product: 'Mechanical Keyboard',
        type: 'Stok Keluar',
        quantity: '-10 Unit',
        date: '19 Nov 2026',
    },
    {
        code: 'TRX-2026-003',
        product: 'Monitor LED 24 Inch',
        type: 'Stok Masuk',
        quantity: '+12 Unit',
        date: '18 Nov 2026',
    },
    {
        code: 'TRX-2026-004',
        product: 'USB Flash Drive 64GB',
        type: 'Stok Keluar',
        quantity: '-15 Unit',
        date: '18 Nov 2026',
    },
]

const lowStockProducts = [
    { name: 'Wireless Mouse', category: 'Aksesoris', stock: 3, minimum: 10 },
    { name: 'USB Hub 4 Port', category: 'Aksesoris', stock: 5, minimum: 15 },
    { name: 'HDMI Cable 2M', category: 'Kabel', stock: 2, minimum: 10 },
    { name: 'Webcam HD', category: 'Elektronik', stock: 0, minimum: 5 },
]
</script>

<template>
    <Head title="Dashboard | Adventory" />

    <div class="space-y-7">

        <!-- Page heading -->
        <section class="flex flex-col justify-between gap-4 sm:flex-row sm:items-center">
            <div>
                <p class="mb-1 text-sm font-medium text-[#159565]">
                    Wednesday, November 19, 2026
                </p>
                <h1 class="text-2xl font-bold tracking-tight text-[#173b30] sm:text-3xl">
                    Selamat Datang di Adventory!
                </h1>
                <p class="mt-2 text-sm text-gray-500">
                    Berikut ringkasan kondisi inventaris bisnis kamu.
                </p>
            </div>

            <div class="inline-flex w-fit items-center gap-2 rounded-xl border border-gray-200 bg-white px-4 py-2.5 text-sm text-gray-600 shadow-sm">
                <Clock3 :size="17" class="text-[#159565]" />
                Overview Inventaris
            </div>
        </section>

        <!-- Statistics -->
        <section class="grid grid-cols-1 gap-4 sm:grid-cols-2 xl:grid-cols-4">
            <div
                v-for="item in statistics"
                :key="item.title"
                class="rounded-2xl border border-gray-100 bg-white p-5 shadow-sm transition hover:-translate-y-1 hover:shadow-md"
            >
                <div class="flex items-center justify-between">
                    <p class="text-sm font-medium text-gray-500">
                        {{ item.title }}
                    </p>
                    <div :class="['flex h-11 w-11 items-center justify-center rounded-xl', item.color]">
                        <component :is="item.icon" :size="21" />
                    </div>
                </div>

                <div class="mt-5">
                    <h3 class="text-3xl font-bold tracking-tight text-[#173b30]">
                        {{ item.value }}
                    </h3>
                    <p class="mt-1 text-xs text-gray-400">
                        {{ item.description }}
                    </p>
                </div>
            </div>
        </section>

        <!-- Charts -->
        <section class="grid grid-cols-1 gap-5 xl:grid-cols-3">

            <!-- Stock movement chart -->
            <div class="rounded-2xl border border-gray-100 bg-white p-5 shadow-sm xl:col-span-2 sm:p-6">
                <div class="flex items-center justify-between">
                    <div>
                        <h3 class="font-bold text-[#173b30]">
                            Pergerakan Stok
                        </h3>
                        <p class="mt-1 text-xs text-gray-400">
                            Ringkasan barang masuk dan keluar minggu ini
                        </p>
                    </div>

                    <button class="rounded-lg p-2 text-gray-400 hover:bg-gray-50">
                        <MoreHorizontal :size="20" />
                    </button>
                </div>

                <div class="mt-8 flex items-center gap-5 text-xs">
                    <span class="flex items-center gap-2 text-gray-500">
                        <span class="h-2.5 w-2.5 rounded-sm bg-[#16a36a]"></span>
                        Barang Masuk
                    </span>
                    <span class="flex items-center gap-2 text-gray-500">
                        <span class="h-2.5 w-2.5 rounded-sm bg-[#bce8d3]"></span>
                        Barang Keluar
                    </span>
                </div>

                <div class="mt-6 flex h-52 items-end justify-between gap-3 border-b border-gray-100 px-2">
                    <div
                        v-for="item in stockMovements"
                        :key="item.day"
                        class="flex h-full flex-1 flex-col items-center justify-end gap-3"
                    >
                        <div class="flex h-full w-full items-end justify-center gap-1.5">
                            <div
                                class="w-full max-w-5 rounded-t-md bg-[#16a36a] transition hover:bg-[#118554]"
                                :style="{ height: `${item.incoming}%` }"
                                :title="`Masuk: ${item.incoming}`"
                            ></div>

                            <div
                                class="w-full max-w-5 rounded-t-md bg-[#bce8d3] transition hover:bg-[#91d9b5]"
                                :style="{ height: `${item.outgoing}%` }"
                                :title="`Keluar: ${item.outgoing}`"
                            ></div>
                        </div>

                        <span class="mb-2 text-xs text-gray-400">
                            {{ item.day }}
                        </span>
                    </div>
                </div>
            </div>

            <!-- Stock summary -->
            <div class="rounded-2xl border border-gray-100 bg-white p-5 shadow-sm sm:p-6">
                <div class="flex items-center justify-between">
                    <div>
                        <h3 class="font-bold text-[#173b30]">
                            Kondisi Inventaris
                        </h3>
                        <p class="mt-1 text-xs text-gray-400">
                            Ringkasan ketersediaan produk
                        </p>
                    </div>
                    <Boxes :size="20" class="text-[#159565]" />
                </div>

                <div class="my-7 flex items-center justify-center">
                    <div class="relative flex h-40 w-40 items-center justify-center rounded-full border-[15px] border-[#e3f3eb]">
                        <div class="absolute inset-[-15px] rounded-full border-[15px] border-transparent border-t-[#16a36a] border-r-[#16a36a] -rotate-12"></div>
                        <div class="text-center">
                            <h3 class="text-3xl font-bold text-[#173b30]">94%</h3>
                            <p class="text-[11px] text-gray-400">Stok tersedia</p>
                        </div>
                    </div>
                </div>

                <div class="space-y-4">
                    <div class="flex items-center justify-between">
                        <span class="flex items-center gap-2 text-sm text-gray-500">
                            <span class="h-2 w-2 rounded-full bg-[#16a36a]"></span>
                            Stok tersedia
                        </span>
                        <span class="text-sm font-semibold text-gray-700">1,273</span>
                    </div>

                    <div class="flex items-center justify-between">
                        <span class="flex items-center gap-2 text-sm text-gray-500">
                            <span class="h-2 w-2 rounded-full bg-amber-400"></span>
                            Stok menipis
                        </span>
                        <span class="text-sm font-semibold text-gray-700">08</span>
                    </div>

                    <div class="flex items-center justify-between">
                        <span class="flex items-center gap-2 text-sm text-gray-500">
                            <span class="h-2 w-2 rounded-full bg-rose-500"></span>
                            Stok habis
                        </span>
                        <span class="text-sm font-semibold text-gray-700">03</span>
                    </div>
                </div>
            </div>
        </section>

        <!-- Recent transactions and low stock -->
        <section class="grid grid-cols-1 gap-5 xl:grid-cols-3">

            <!-- Transactions table -->
            <div class="overflow-hidden rounded-2xl border border-gray-100 bg-white shadow-sm xl:col-span-2">
                <div class="flex items-center justify-between p-5 sm:p-6">
                    <div>
                        <h3 class="font-bold text-[#173b30]">
                            Transaksi Terbaru
                        </h3>
                        <p class="mt-1 text-xs text-gray-400">
                            Aktivitas inventaris terakhir
                        </p>
                    </div>
                    <span class="rounded-lg bg-[#e8f6ef] px-3 py-2 text-xs font-semibold text-[#138253]">
                        Preview
                    </span>
                </div>

                <div class="overflow-x-auto">
                    <table class="w-full whitespace-nowrap text-left text-sm">
                        <thead class="border-y border-gray-100 bg-gray-50/70 text-xs text-gray-400">
                            <tr>
                                <th class="px-6 py-3 font-medium">Kode Transaksi</th>
                                <th class="px-6 py-3 font-medium">Produk</th>
                                <th class="px-6 py-3 font-medium">Jenis</th>
                                <th class="px-6 py-3 font-medium">Jumlah</th>
                                <th class="px-6 py-3 font-medium">Tanggal</th>
                            </tr>
                        </thead>

                        <tbody class="divide-y divide-gray-50">
                            <tr
                                v-for="transaction in transactions"
                                :key="transaction.code"
                                class="transition hover:bg-gray-50/70"
                            >
                                <td class="px-6 py-4 font-medium text-[#138253]">
                                    {{ transaction.code }}
                                </td>
                                <td class="px-6 py-4 font-medium text-gray-700">
                                    {{ transaction.product }}
                                </td>
                                <td class="px-6 py-4">
                                    <span
                                        :class="transaction.type === 'Stok Masuk'
                                            ? 'bg-emerald-50 text-emerald-700'
                                            : 'bg-blue-50 text-blue-700'"
                                        class="rounded-full px-2.5 py-1 text-xs font-medium"
                                    >
                                        {{ transaction.type }}
                                    </span>
                                </td>
                                <td
                                    :class="transaction.quantity.startsWith('+')
                                        ? 'text-emerald-600'
                                        : 'text-blue-600'"
                                    class="px-6 py-4 font-semibold"
                                >
                                    {{ transaction.quantity }}
                                </td>
                                <td class="px-6 py-4 text-gray-400">
                                    {{ transaction.date }}
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>

            <!-- Low stock -->
            <div class="rounded-2xl border border-gray-100 bg-white p-5 shadow-sm sm:p-6">
                <div class="flex items-center justify-between">
                    <div>
                        <h3 class="font-bold text-[#173b30]">
                            Stok Menipis
                        </h3>
                        <p class="mt-1 text-xs text-gray-400">
                            Produk yang perlu diperhatikan
                        </p>
                    </div>
                    <AlertTriangle :size="20" class="text-amber-500" />
                </div>

                <div class="mt-5 space-y-4">
                    <div
                        v-for="product in lowStockProducts"
                        :key="product.name"
                        class="border-b border-gray-50 pb-4 last:border-0 last:pb-0"
                    >
                        <div class="flex items-start justify-between gap-2">
                            <div>
                                <p class="text-sm font-semibold text-gray-700">
                                    {{ product.name }}
                                </p>
                                <p class="mt-1 text-xs text-gray-400">
                                    {{ product.category }}
                                </p>
                            </div>

                            <span
                                :class="product.stock === 0
                                    ? 'bg-rose-50 text-rose-600'
                                    : 'bg-amber-50 text-amber-600'"
                                class="rounded-lg px-2 py-1 text-xs font-semibold"
                            >
                                {{ product.stock }} Unit
                            </span>
                        </div>

                        <div class="mt-3 h-1.5 overflow-hidden rounded-full bg-gray-100">
                            <div
                                :class="product.stock === 0 ? 'bg-rose-500' : 'bg-amber-400'"
                                class="h-full rounded-full"
                                :style="{ width: `${Math.min(product.stock / product.minimum * 100, 100)}%` }"
                            ></div>
                        </div>

                        <p class="mt-1.5 text-[10px] text-gray-400">
                            Minimum stok: {{ product.minimum }} unit
                        </p>
                    </div>
                </div>
            </div>
        </section>

        <!-- Footer -->
        <footer class="border-t border-gray-200 pt-5 text-center text-xs text-gray-400">
            © 2026 Adventory. Advanced Inventory Management System.
        </footer>
    </div>
</template>