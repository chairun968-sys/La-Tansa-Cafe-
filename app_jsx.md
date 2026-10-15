```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
```md
import React, { useState, useEffect, useRef } from 'react';
import {
Coffee, ShoppingBag, LayoutDashboard, History, Wallet,
BookOpen, Printer, Download, MessageCircle, QrCode,
Upload, X, Trash2, Plus, CheckCircle2,
Edit2, Minus, Eye, EyeOff, Package, Lock, Star, Calculator, ArrowUpRight, ArrowDownLeft, Landmark, FileText
} from 'lucide-react';

const getImgUrl = (item) => item.image || `https://placehold.co/300x200/1A1A1A/D4AF37?text=${encodeURIComponent(item.name)}`;

const INITIAL_SPECIAL_MENUS = \[
{ id: 'special-1', name: 'Nasi Kebuli Spesial La-Tansa', description: 'Hidangan eksklusif Nasi Kebuli dengan daging kambing empuk, kismis, dan rempah pilihan. Porsi besar cocok untuk makan bersama.', price: 45000, category: 'Spesial', image: 'https://images.unsplash.com/photo-1631515243349-e0cb75fb8d3a?auto=format&fit=crop&q=80&w=800&h=400', isAvailable: true },
{ id: 'special-2', name: 'Ayam Bakar Madu Sultan', description: 'Ayam bakar empuk dengan olesan madu murni bakar khas La-Tansa, disajikan dengan sambal terasi spesial dan lalapan segar.', price: 25000, category: 'Spesial', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=800&h=400', isAvailable: true }
\];

const INITIAL_PACKAGES = \[
{ id: 'pkt-A', name: 'Paket A', price: 10000, description: 'Nasi + Ayam Pilihan + Sayur Pilihan + Es Teh', image: 'https://images.unsplash.com/photo-1546069901-ba9599a7e63c?auto=format&fit=crop&q=80&w=300&h=200', isAvailable: true },
{ id: 'pkt-B', name: 'Paket B', price: 12000, description: 'Nasi + Ayam Spesial + Telur + Sayur + Air Mineral', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=300&h=200', isAvailable: true },
{ id: 'pkt-C', name: 'Paket C', price: 9000, description: 'Nasi + Ikan Lele / Goreng + Tempe/Tahu + Sayur', image: 'https://images.unsplash.com/photo-1519708227418-c8fd9a32b7a2?auto=format&fit=crop&q=80&w=300&h=200', isAvailable: true },
{ id: 'pkt-D', name: 'Paket D', price: 8000, description: 'Nasi + Telur Dadar/Ceplok + Sayur + Gorengan', image: 'https://images.unsplash.com/photo-1525385133512-2f3bdd039054?auto=format&fit=crop&q=80&w=300&h=200', isAvailable: true },
\];

const INITIAL_MENU = \[
{ id: 1, name: 'Ayam Kecap', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1604908176997-125f25cc6f3d?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 2, name: 'Ayam Balado', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1588166524941-3bf61a9c41db?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 3, name: 'Ayam Opor', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1598514982205-f36b96d1e8d4?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 4, name: 'Ayam Asam Manis', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1580476262798-bddd9f4b7369?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 5, name: 'Ayam Kremes', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1626082927389-6cd097cdc6ec?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 6, name: 'Ayam Rica Rica', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1504674900247-0877df9cc836?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 7, name: 'Ayam Serundeng', price: 6000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 8, name: 'Ayam Krispy', price: 7000, category: 'Ayam', image: 'https://images.unsplash.com/photo-1626645738196-c2a7c87a8f58?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 9, name: 'Ikan Lele', price: 6000, category: 'Ikan', image: 'https://images.unsplash.com/photo-1580476262798-bddd9f4b7369?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 10, name: 'Ikan Kuah', price: 7000, category: 'Ikan', image: 'https://images.unsplash.com/photo-1548943487-a2e4e43b4859?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 11, name: 'Ikan Goreng', price: 7000, category: 'Ikan', image: 'https://images.unsplash.com/photo-1519708227418-c8fd9a32b7a2?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 12, name: 'Telur Dadar', price: 5000, category: 'Telur', image: 'https://images.unsplash.com/photo-1525385133512-2f3bdd039054?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 13, name: 'Telur Ceplok', price: 5000, category: 'Telur', image: 'https://images.unsplash.com/photo-1482049016688-2d3e1b311543?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 14, name: 'Telur Rebus', price: 5000, category: 'Telur', image: 'https://images.unsplash.com/photo-1587486913049-53fc88980cfc?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 15, name: 'Sayur Kacang Panjang', price: 3000, category: 'Sayur-sayuran', image: 'https://images.unsplash.com/photo-1512621776951-a57141f2eefd?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 16, name: 'Sayur Kangkung', price: 3000, category: 'Sayur-sayuran', image: 'https://images.unsplash.com/photo-1564834724105-918b73d1b9e0?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 17, name: 'Sayur Capcai', price: 3000, category: 'Sayur-sayuran', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 18, name: 'Sayur Sop', price: 3000, category: 'Sayur-sayuran', image: 'https://images.unsplash.com/photo-1547592180-85f173990554?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 19, name: 'Sayur Bening Bayam', price: 3000, category: 'Sayur-sayuran', image: 'https://images.unsplash.com/photo-1615486171434-f8623b378eb8?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 20, name: 'Sayur Tumis Toge', price: 3000, category: 'Sayur-sayuran', image: 'https://images.unsplash.com/photo-1534939561126-855b8675edd7?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 21, name: 'Mie Kuning', price: 3000, category: 'Makanan Lainnya', image: 'https://images.unsplash.com/photo-1585032226651-759b368d7246?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 22, name: 'Mie Hun', price: 3000, category: 'Makanan Lainnya', image: 'https://images.unsplash.com/photo-1569718212165-3a8278d5f624?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 23, name: 'Tempe Oreg', price: 3000, category: 'Makanan Lainnya', image: 'https://images.unsplash.com/photo-1610927845353-832049e7bdf8?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 24, name: 'Oseng Tahu', price: 3000, category: 'Makanan Lainnya', image: 'https://images.unsplash.com/photo-1511690656952-34342bb7c2f2?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 25, name: 'Terong Kecap', price: 3000, category: 'Makanan Lainnya', image: 'https://images.unsplash.com/photo-1604908176997-125f25cc6f3d?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 26, name: 'Tumis Usus', price: 3000, category: 'Makanan Lainnya', image: 'https://images.unsplash.com/photo-1555939594-58d7cb561ad1?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 27, name: 'Tempe Goreng', price: 1000, category: 'Gorengan', image: 'https://images.unsplash.com/photo-1577906096429-f73c2c312435?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 28, name: 'Tahu Goreng', price: 1000, category: 'Gorengan', image: 'https://images.unsplash.com/photo-1628294895950-9805252327bc?auto=format&fit=crop&q=80&w=300&h=200' },
{ id: 29, name: 'Tempe Mendoan', price: 1000, category: 'Gorengan', image: 'https://images.unsplash.com/photo-1596649281358-8b9eb98b671a?auto=format&fit=crop&q=80&w=300&h=200' }
\];

const HIJRI_MONTHS = \[
"Muharram", "Safar", "Rabiul Awal", "Rabiul Akhir",
"Jumadil Awal", "Jumadil Akhir", "Rajab", "Sya'ban",
"Ramadhan", "Syawal", "Dzulqa'dah", "Dzulhijjah"
\];

const speakNotification = (text) => {
try {
if ('speechSynthesis' in window) {
window.speechSynthesis.cancel();
const utterance = new SpeechSynthesisUtterance(text);
utterance.lang = 'id-ID';
utterance.rate = 0.95;
utterance.pitch = 0.7;

```
  const voices = window.speechSynthesis.getVoices();
  const maleVoice = voices.find(v => (v.lang.includes('id') || v.lang.includes('ind')) && (v.name.toLowerCase().includes('male') || v.name.toLowerCase().includes('pria') || v.name.toLowerCase().includes('google')));
  if (maleVoice) {
    utterance.voice = maleVoice;
  } else {
    const indoVoice = voices.find(v => v.lang.includes('id') || v.lang.includes('ind'));
    if (indoVoice) utterance.voice = indoVoice;
  }

  window.speechSynthesis.speak(utterance);
}

```

} catch (e) {
console.log("Speech synthesis not supported", e);
}
};

const generateWaLink = (order) => {
const phone = "6285156641883";
const text = `Halo Admin La-Tansa Cafe, pesanan telah dikirimkan:\n\n*ID Pesanan:* ${order.id}\n*Waktu:* ${order.date}\n*Jenis:* ${order.type}\n*Pemesan:* ${order.customer}\n\n*Rincian Pesanan:*\n${order.details}\n\n*Pembayaran:* ${order.payment.toUpperCase()}\n*Total Tagihan:* Rp ${order.total.toLocaleString('id-ID')}\n\nMohon segera diproses. Terima kasih!`;
return `https://api.whatsapp.com/send?phone=${phone}&text=${encodeURIComponent(text)}`;
};

function Receipt({ data, innerRef }) { return (     

```
  <div className="text-center pb-4 border-b border-[#EAD9B8]">
    <h2 className="text-xl font-serif font-bold text-[#2C2416] tracking-tight">LA-TANSA CAFE</h2>
    <p className="text-[10px] text-[#7A6B52] mt-0.5 uppercase tracking-[0.25em] font-medium">Struk Pesanan Resmi</p>
  </div>

  <div className="py-3 border-b border-[#EAD9B8] text-xs space-y-1.5">
    <div className="flex justify-between">
      <span className="text-[#7A6B52]">ID Transaksi:</span>
      <span className="font-bold text-[#2C2416]">{data.id}</span>
    </div>
    <div className="flex justify-between">
      <span className="text-[#7A6B52]">Waktu:</span>
      <span className="text-[#2C2416]">{data.date}</span>
    </div>
    <div className="flex justify-between">
      <span className="text-[#7A6B52]">Jenis Layanan:</span>
      <span className="font-medium text-[#2C2416]">{data.type}</span>
    </div>
  </div>

  <div className="py-3 border-b border-[#EAD9B8] text-xs">
    <span className="text-[#7A6B52] block mb-1 font-semibold uppercase tracking-wider text-[10px]">Informasi Pemesan:</span>
    <div className="whitespace-pre-line text-[#2C2416] leading-relaxed font-medium">{data.customer}</div>
  </div>

  <div className="py-3 border-b border-[#EAD9B8] text-xs">
    <span className="text-[#7A6B52] block mb-1.5 font-semibold uppercase tracking-wider text-[10px]">Rincian Item:</span>
    <div className="whitespace-pre-line text-[#2C2416] font-medium leading-relaxed bg-[#FBF9F5] p-3 rounded border border-[#EAD9B8]/40">
      {data.details}
    </div>
  </div>

  <div className="py-3 border-b border-[#EAD9B8] text-xs flex justify-between items-center">
    <span className="text-[#7A6B52]">Metode Pembayaran:</span>
    <span className="font-bold uppercase tracking-wider text-[#2C2416] bg-[#F5F1E8] px-2 py-0.5 rounded border border-[#EAD9B8]">{data.payment}</span>
  </div>

  <div className="pt-4 flex justify-between items-center">
    <span className="font-serif font-bold text-sm text-[#2C2416]">Total Pembayaran</span>
    <span className="text-lg font-bold text-[#8C6D28]">Rp {data.total.toLocaleString('id-ID')}</span>
  </div>

  <div className="mt-5 pt-3 border-t border-dashed border-[#D4AF37]/50 text-center">
    <p className="text-[10px] text-[#7A6B52] italic font-serif">Terima kasih atas kunjungan & partisipasi Anda.</p>
  </div>
</div>

```

); }

export default function App() { const \[activeTab, setActiveTab\] = useState('online'); const \[menuItems, setMenuItems\] = useState(INITIAL_MENU.map(item => ({...item, isAvailable: item.isAvailable !== false}))); const \[specialMenus, setSpecialMenus\] = useState(INITIAL_SPECIAL_MENUS); const \[packages, setPackages\] = useState(INITIAL_PACKAGES); const \[orders, setOrders\] = useState(\[\]);

const \[transactions, setTransactions\] = useState(\[ { id: 'TRX-101', date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'IN', category: 'PENJUALAN', amount: 150000, note: 'Penjualan Outlet Kasir' }, { id: 'TRX-102', date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'OUT', category: 'BAHAN_BAKU', amount: 50000, note: 'Belanja Ayam & Bumbu Dapur' }, { id: 'TRX-103', date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'OUT', category: 'PERALATAN', amount: 30000, note: 'Pembelian Gas LPG & Wadah Mika' }, { id: 'TRX-104', date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'SAVING', category: 'TABUNGAN_REKENING', amount: 20000, note: 'Setoran Tabungan Harian Toko' } \]);

const \[customQrisImage, setCustomQrisImage\] = useState(null); const \[showReceiptModal, setShowReceiptModal\] = useState(false); const \[currentReceiptData, setCurrentReceiptData\] = useState(null); const \[isStaffLoggedIn, setIsStaffLoggedIn\] = useState(false); const \[showLoginModal, setShowLoginModal\] = useState(false); const \[pendingTab, setPendingTab\] = useState(null); const \[loginPassword, setLoginPassword\] = useState(''); const \[loginError, setLoginError\] = useState('');

const receiptRef = useRef(null);

useEffect(() => { if ('speechSynthesis' in window) { window.speechSynthesis.onvoiceschanged = () => { window.speechSynthesis.getVoices(); }; } }, \[\]);

const btnClass = "bg-gradient-to-r from-\[#D4AF37\] to-\[#AA821C\] text-\[#050505\] py-3 px-6 rounded-md font-bold tracking-wide hover:from-\[#E3C365\] hover:to-\[#C69A27\] transition-all disabled:opacity-50 text-sm shadow-\[0_4px_15px_rgba(212,175,55,0.2)\] border-none hover:shadow-\[0_4px_20px_rgba(212,175,55,0.4)\]"; const inputClass = "w-full p-3 bg-\[#111111\]/80 backdrop-blur-sm border border-\[#D4AF37\]/30 rounded-md focus:outline-none focus:border-\[#D4AF37\] focus:ring-1 focus:ring-\[#D4AF37\] transition-all text-sm font-\['Inter',sans-serif\] text-\[#E5E7EB\] placeholder-\[#6B7280\]"; const cardClass = "bg-\[#141414\]/90 backdrop-blur-md p-8 rounded-xl shadow-\[0_8px_30px_rgba(0,0,0,0.6)\] border border-\[#D4AF37\]/20 relative z-10";

const handleTabClick = (tabId) => { if (tabId === 'online') { setActiveTab('online'); } else { if (isStaffLoggedIn) { setActiveTab(tabId); } else { setPendingTab(tabId); setShowLoginModal(true); setLoginError(''); setLoginPassword(''); } } };

const handleLoginSubmit = (e) => { e.preventDefault(); if (loginPassword === 'latansacafe123') { setIsStaffLoggedIn(true); setShowLoginModal(false); setActiveTab(pendingTab); setPendingTab(null); } else { setLoginError('Sandi salah! Gunakan sandi yang benar.'); } };

const handleCreateOrder = (orderData) => { const newOrder = { id: `ORD-${Math.floor(Math.random() * 1000000)}`, date: new Date().toLocaleString(), ...orderData };

```
setOrders([newOrder, ...orders]);

if (orderData.total > 0) {
  setTransactions([{
    id: `TRX-${Math.floor(Math.random() * 1000000)}`,
    date: new Date().toLocaleDateString(),
    hijriMonth: 'Rabiul Awal',
    quarter: 'Triwulan I (Q1)',
    type: 'IN',
    category: 'PENJUALAN',
    amount: orderData.total,
    note: `Pendapatan: ${newOrder.id} - ${orderData.type}`
  }, ...transactions]);

  speakNotification("Pemberitahuan: Pesanan masuk. Mohon segera diproses demi kemaslahatan umat.");
  setTimeout(() => {
    speakNotification("Pemberitahuan: Transaksi berhasil. Saldo berkurang, pahala bertambah karena ikut memakmurkan ekonomi pondok.");
  }, 5000);
} else {
  speakNotification("Pemberitahuan: Pesanan masuk. Mohon segera diproses demi kemaslahatan umat.");
}

setCurrentReceiptData(newOrder);
setShowReceiptModal(true);

```

};

const downloadReceiptImage = () => { const receiptElement = receiptRef.current; if (!receiptElement) return;

```
if (window.html2canvas) {
  window.html2canvas(receiptElement, { backgroundColor: '#FFFFFF', scale: 2 }).then(canvas => {
    const link = document.createElement('a');
    link.download = `Nota-${currentReceiptData.id}.png`;
    link.href = canvas.toDataURL('image/png');
    link.click();
  }).catch(err => {
    console.error(err);
    window.print();
  });
} else {
  window.print();
}

```

};

const handleDirectPrint = () => { window.print(); };

return (     

```
  <style>{`
    @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;0,700;1,400&family=Inter:wght@300;400;500;600&display=swap');
    .font-serif { font-family: 'Playfair Display', serif; }
    ::-webkit-scrollbar { width: 8px; height: 8px; }
    ::-webkit-scrollbar-track { background: #050505; }
    ::-webkit-scrollbar-thumb { background: #D4AF37; border-radius: 4px; }
    @keyframes blob {
      0% { transform: translate(0px, 0px) scale(1); }
      33% { transform: translate(30px, -50px) scale(1.1); }
      66% { transform: translate(-20px, 20px) scale(0.9); }
      100% { transform: translate(0px, 0px) scale(1); }
    }
    .animate-blob { animation: blob 10s infinite alternate; }
    .animation-delay-2000 { animation-delay: 2s; }
    .menu-card-3d:hover {
      transform: perspective(1000px) translateZ(10px) translateY(-5px);
      box-shadow: 0 15px 35px rgba(212, 175, 55, 0.15);
    }
    @media print {
      body * {
        visibility: hidden;
      }
      .printable-receipt, .printable-receipt * {
        visibility: visible;
      }
      .printable-receipt {
        position: fixed;
        left: 0;
        top: 0;
        width: 100vw;
        height: 100vh;
        margin: 0;
        padding: 20px;
        display: flex;
        align-items: center;
        justify-content: center;
        background: #FFFFFF !important;
        color: #2C2416 !important;
        z-index: 99999;
      }
      .no-print {
        display: none !important;
      }
    }
  `}</style>

  {showReceiptModal && currentReceiptData && (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md p-4 overflow-y-auto no-print">
      <div className="bg-[#141414] border-2 border-[#D4AF37] p-6 rounded-2xl max-w-lg w-full shadow-[0_0_50px_rgba(212,175,55,0.3)] relative max-h-[90vh] flex flex-col">
        <div className="flex justify-between items-center mb-4 pb-2 border-b border-[#D4AF37]/20">
          <h3 className="text-xl font-serif font-bold text-[#D4AF37]">Nota / Struk Pemesanan</h3>
          <button onClick={() => setShowReceiptModal(false)} className="text-[#9CA3AF] hover:text-[#D4AF37]"><X size={20}/></button>
        </div>
        
        <div className="flex-1 overflow-y-auto mb-6 pr-1 flex justify-center py-2 printable-receipt">
          <Receipt data={currentReceiptData} innerRef={receiptRef} />
        </div>

        <div className="flex gap-3 pt-3 border-t border-[#D4AF37]/20">
          <button onClick={handleDirectPrint} className={`${btnClass} flex-1 flex items-center justify-center gap-2`}>
            <Printer size={16} /> Print Struk
          </button>
          <button onClick={downloadReceiptImage} className="px-5 py-3 bg-[#1A1A1A] border border-[#D4AF37]/40 text-[#D4AF37] font-bold text-sm rounded-md hover:bg-[#D4AF37]/10 transition-colors flex items-center gap-2">
            <Download size={16} /> Download
          </button>
          <button onClick={() => setShowReceiptModal(false)} className="px-4 py-3 bg-[#1A1A1A] text-[#9CA3AF] font-bold text-sm rounded-md hover:text-[#D4AF37] transition-colors">
            Tutup
          </button>
        </div>
      </div>
    </div>
  )}

  {showLoginModal && (
    <div className="fixed inset-0 z-50 flex items-center justify-center bg-black/80 backdrop-blur-md p-4 no-print">
      <div className="bg-[#141414] border-2 border-[#D4AF37] p-8 rounded-2xl max-w-md w-full shadow-[0_0_50px_rgba(212,175,55,0.3)] relative">
        <button onClick={() => setShowLoginModal(false)} className="absolute top-4 right-4 text-[#9CA3AF] hover:text-[#D4AF37]"><X size={20}/></button>
        <div className="text-center mb-6">
          <div className="w-12 h-12 bg-[#D4AF37]/10 border border-[#D4AF37]/30 rounded-full flex items-center justify-center mx-auto mb-3 text-[#D4AF37]">
            <Lock size={24} />
          </div>
          <h3 className="text-2xl font-serif font-bold text-[#D4AF37]">Autentikasi Staf</h3>
          <p className="text-xs text-[#9CA3AF] mt-1">Masukkan sandi untuk mengakses Kasir & Dasbor Admin</p>
        </div>
        
        <form onSubmit={handleLoginSubmit} className="space-y-4">
          <div>
            <input 
              type="password" 
              autoFocus
              required
              placeholder="Masukkan sandi..." 
              value={loginPassword} 
              onChange={e => setLoginPassword(e.target.value)} 
              className={inputClass}
            />
          </div>
          {loginError && <p className="text-xs text-red-500 font-medium text-center">{loginError}</p>}
          <button type="submit" className={`${btnClass} w-full`}>Masuk Sistem</button>
        </form>
      </div>
    </div>
  )}

  <nav className="no-print w-full md:w-64 bg-[#0A0A0A]/80 backdrop-blur-xl border-r border-[#D4AF37]/20 p-8 flex flex-col gap-4 z-20 shadow-[4px_0_24px_rgba(0,0,0,0.8)] relative">
    <div className="mb-10 text-center md:text-left relative">
      <div className="absolute -left-4 top-2 w-1 h-12 bg-[#D4AF37] rounded-r-md hidden md:block shadow-[0_0_10px_#D4AF37]"></div>
      <h1 className="text-4xl font-serif font-bold tracking-tight text-[#D4AF37] leading-none mb-1 drop-shadow-[0_2px_4px_rgba(212,175,55,0.3)]">La-Tansa</h1>
      <h2 className="text-xs font-medium uppercase tracking-[0.3em] text-[#9CA3AF]">Cafe & Resto</h2>
    </div>

    <div className="flex flex-col gap-2">
      {[
        { id: 'online', icon: ShoppingBag, label: 'Pemesanan' },
        { id: 'kasir', icon: Coffee, label: 'Kasir POS (Protected)' },
        { id: 'admin', icon: LayoutDashboard, label: 'Dasbor Admin (Protected)' }
      ].map(tab => (
        <button 
          key={tab.id}
          onClick={() => handleTabClick(tab.id)}
          className={`flex items-center gap-3 p-3 text-sm font-medium rounded-lg transition-all duration-300 ${activeTab === tab.id ? 'bg-gradient-to-r from-[#D4AF37] to-[#B38B22] text-[#050505] shadow-[0_0_20px_rgba(212,175,55,0.3)] translate-x-2' : 'text-[#9CA3AF] hover:text-[#D4AF37] hover:bg-[#141414] hover:translate-x-1'}`}
        >
          <tab.icon size={18} /> {tab.label} {tab.id !== 'online' && !isStaffLoggedIn && <Lock size={12} className="ml-auto opacity-60" />}
        </button>
      ))}
    </div>

    {isStaffLoggedIn && (
      <div className="mt-auto pt-4 border-t border-[#D4AF37]/20 flex items-center justify-between text-xs text-[#9CA3AF]">
        <span>Mode Staf Aktif</span>
        <button onClick={() => { setIsStaffLoggedIn(false); setActiveTab('online'); }} className="text-red-400 hover:underline">Keluar</button>
      </div>
    )}
  </nav>

  <main className="no-print flex-1 h-screen overflow-y-auto p-6 md:p-10 z-10 relative scroll-smooth">
    {activeTab === 'online' && <OnlineOrdering menuItems={menuItems} specialMenus={specialMenus} packages={packages} onCreateOrder={handleCreateOrder} customQrisImage={customQrisImage} btnClass={btnClass} inputClass={inputClass} cardClass={cardClass} />}
    {activeTab === 'kasir' && <POSKasir menuItems={menuItems} onCreateOrder={handleCreateOrder} btnClass={btnClass} cardClass={cardClass} />}
    {activeTab === 'admin' && <AdminDashboard orders={orders} transactions={transactions} setTransactions={setTransactions} menuItems={menuItems} setMenuItems={setMenuItems} specialMenus={specialMenus} setSpecialMenus={setSpecialMenus} packages={packages} setPackages={setPackages} customQrisImage={customQrisImage} setCustomQrisImage={setCustomQrisImage} btnClass={btnClass} inputClass={inputClass} onViewReceipt={(order) => { setCurrentReceiptData(order); setShowReceiptModal(true); }} />}
  </main>

  <div className="hidden printable-receipt">
    {currentReceiptData && <Receipt data={currentReceiptData} />}
  </div>
</div>

```

); }

function OnlineOrdering({ menuItems, specialMenus, packages, onCreateOrder, customQrisImage, btnClass, inputClass, cardClass }) { const \[orderType, setOrderType\] = useState('santri'); const \[paymentMethod, setPaymentMethod\] = useState('cash'); const \[cart, setCart\] = useState(\[\]); const \[qrisProof, setQrisProof\] = useState(null); const \[orderSuccessMsg, setOrderSuccessMsg\] = useState(false);

const \[santriForm, setSantriForm\] = useState({ namaPemesan: '', namaSantri: '', kelas: '', asrama: '', pilihanNasi: 'Nasi Biasa', waktu: '', catatan: '', selectedPackage: null });

const \[ifthorForm, setIfthorForm\] = useState({ wali: '', kelas: '', pilihanNasiIfthor: 'Nasi Biasa', hariTanggal: '', catatan: '' });

const addToCart = (item) => { const existing = cart.find(c => c.id === item.id); if (existing) { setCart(cart.map(c => c.id === item.id ? { ...c, qty: c.qty + 1 } : c)); } else { setCart(\[...cart, { ...item, qty: 1 }\]); } };

const removeOne = (id) => { const existing = cart.find(c => c.id === id); if (existing && existing.qty > 1) { setCart(cart.map(c => c.id === id ? { ...c, qty: c.qty - 1 } : c)); } else { setCart(cart.filter(c => c.id !== id)); } };

const packageTotal = santriForm.selectedPackage ? santriForm.selectedPackage.price : 0; const cartTotal = cart.reduce((sum, item) => sum + (item.price \* item.qty), 0); const totalCart = packageTotal + cartTotal;

const cartDetails = \[ santriForm.selectedPackage ? `*Paket:* ${santriForm.selectedPackage.name} - Rp ${santriForm.selectedPackage.price.toLocaleString('id-ID')} (${santriForm.selectedPackage.description})` : '', ...cart.map(c => `${c.name} (${c.qty}x) - Rp ${(c.price * c.qty).toLocaleString('id-ID')}`) \].filter(Boolean).join('\\n');

const isSubmitDisabled = (orderType === 'santri' && cart.length === 0 && !santriForm.selectedPackage) || (orderType === 'ifthor' && cart.length === 0);

const handleSantriSubmit = (e) => { e.preventDefault(); if (isSubmitDisabled) return; const orderData = { type: 'Pemesanan Santri', customer: `Pemesan (Wali): ${santriForm.namaPemesan}\nPenerima (Santri): ${santriForm.namaSantri}`, details: `Kelas: ${santriForm.kelas} | Asrama: ${santriForm.asrama}\nPilihan Nasi: ${santriForm.pilihanNasi}\n\nRincian Pesanan:\n${cartDetails}\n\nWaktu Pengambilan: ${santriForm.waktu}\nCatatan Tambahan: ${santriForm.catatan || '-'}`, payment: paymentMethod, total: totalCart }; onCreateOrder(orderData); setOrderSuccessMsg(true); const tempId = `ORD-${Math.floor(Math.random() * 1000000)}`; const waUrl = generateWaLink({ id: tempId, date: new Date().toLocaleString(), ...orderData }); window.open(waUrl, '\_blank'); };

const handleIfthorSubmit = (e) => { e.preventDefault(); if (cart.length === 0) return; const orderData = { type: 'Pemesanan Ifthor Jama'i', customer: `Wali Kelas (Pemesan): ${ifthorForm.wali}`, details: `Kelas yang Ifthor: ${ifthorForm.kelas}\nPilihan Nasi: ${ifthorForm.pilihanNasiIfthor}\n\nRincian Menu:\n${cartDetails}\n\nHari & Tanggal: ${ifthorForm.hariTanggal}\nCatatan Tambahan: ${ifthorForm.catatan || '-'}`, payment: paymentMethod, total: totalCart }; onCreateOrder(orderData); setOrderSuccessMsg(true); const tempId = `ORD-${Math.floor(Math.random() * 1000000)}`; const waUrl = generateWaLink({ id: tempId, date: new Date().toLocaleString(), ...orderData }); window.open(waUrl, '\_blank'); };

const handleQrisUpload = (e) => { const file = e.target.files\[0\]; if (file) { const reader = new FileReader(); reader.onloadend = () => setQrisProof(reader.result); reader.readAsDataURL(file); } };

const menuByCategory = menuItems.reduce((acc, item) => { if (!acc\[item.category\]) acc\[item.category\] = \[\]; acc\[item.category\].push(item); return acc; }, {});

return (     Menu La-Tansa Pilih hidangan dengan menyentuh tanda + 

```
      <div className="space-y-8 max-h-[650px] overflow-y-auto pr-2">
        <div className="space-y-4 mb-6">
          <h3 className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider flex items-center gap-2">
            <div className="w-4 h-px bg-[#D4AF37]/50"></div> Menu Spesial Pilihan <div className="flex-1 h-px bg-[#D4AF37]/20"></div>
          </h3>
          <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
            {specialMenus.map((sp, idx) => (
              <div key={sp.id || idx} className="relative rounded-xl overflow-hidden border-2 border-[#D4AF37] shadow-[0_0_20px_rgba(212,175,55,0.25)] group bg-[#1A1A1A] flex flex-col justify-between">
                <div>
                  <div className="absolute top-3 right-3 z-20 bg-[#D4AF37] text-[#050505] text-[10px] font-bold px-2.5 py-0.5 rounded-full uppercase tracking-widest shadow-lg">Spesial #{idx+1}</div>
                  <div className="h-32 overflow-hidden relative">
                    <img src={getImgUrl(sp)} alt={sp.name} className="w-full h-full object-cover group-hover:scale-105 transition-transform duration-700" />
                    <div className="absolute inset-0 bg-gradient-to-t from-[#1A1A1A] via-transparent to-transparent"></div>
                  </div>
                  <div className="p-4">
                    <h4 className="font-serif font-bold text-lg text-[#D4AF37] mb-1 line-clamp-1">{sp.name}</h4>
                    <p className="text-xs text-[#9CA3AF] line-clamp-2 mb-3">{sp.description}</p>
                  </div>
                </div>
                <div className="p-4 pt-0 flex items-center justify-between">
                  <span className="font-bold text-[#D4AF37]">Rp {sp.price.toLocaleString('id-ID')}</span>
                  {cart.find(c => c.id === sp.id) ? (
                    <div className="flex items-center justify-between bg-[#0A0A0A] border border-[#D4AF37] rounded-md p-1 shadow-[0_0_10px_rgba(212,175,55,0.4)]">
                      <button type="button" onClick={() => removeOne(sp.id)} className="w-7 h-7 flex items-center justify-center text-[#D4AF37] hover:bg-[#D4AF37]/20 rounded transition-colors"><Minus size={14}/></button>
                      <span className="text-xs font-bold text-[#E5E7EB] w-5 text-center">{cart.find(c => c.id === sp.id).qty}</span>
                      <button type="button" onClick={() => addToCart(sp)} className="w-7 h-7 flex items-center justify-center text-[#D4AF37] hover:bg-[#D4AF37]/20 rounded transition-colors"><Plus size={14}/></button>
                    </div>
                  ) : (
                    <button type="button" onClick={() => addToCart(sp)} className="px-4 py-1.5 bg-[#D4AF37] text-[#050505] font-bold text-xs rounded-md hover:bg-[#E3C365] transition-all shadow-[0_0_10px_rgba(212,175,55,0.4)]">
                      + Pesan
                    </button>
                  )}
                </div>
              </div>
            ))}
          </div>
        </div>

        <div className="space-y-4 mb-6">
          <h3 className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider flex items-center gap-2">
            <div className="w-4 h-px bg-[#D4AF37]/50"></div> Paket Santri Cepat (Pilih Salah Satu) <div className="flex-1 h-px bg-[#D4AF37]/20"></div>
          </h3>
          <div className="grid grid-cols-1 sm:grid-cols-2 gap-3">
            {packages.map(pkg => {
              const isSelected = santriForm.selectedPackage?.id === pkg.id;
              return (
                <div 
                  key={pkg.id}
                  onClick={() => setSantriForm({...santriForm, selectedPackage: isSelected ? null : pkg})}
                  className={`p-3 rounded-xl border-2 transition-all cursor-pointer flex gap-3 items-center ${isSelected ? 'bg-[#D4AF37]/10 border-[#D4AF37] shadow-[0_0_15px_rgba(212,175,55,0.3)]' : 'bg-[#141414] border-[#D4AF37]/20 hover:border-[#D4AF37]/50'}`}
                >
                  <img src={getImgUrl(pkg)} alt={pkg.name} className="w-14 h-14 rounded-lg object-cover border border-[#D4AF37]/30 shrink-0" />
                  <div className="flex-1 min-w-0">
                    <div className="flex justify-between items-center mb-0.5">
                      <span className="font-bold text-sm text-[#E5E7EB]">{pkg.name}</span>
                      <span className="text-xs font-bold text-[#D4AF37]">Rp {pkg.price.toLocaleString('id-ID')}</span>
                    </div>
                    <p className="text-[11px] text-[#9CA3AF] line-clamp-2 leading-tight">{pkg.description}</p>
                  </div>
                </div>
              );
            })}
          </div>
          {santriForm.selectedPackage && (
            <button type="button" onClick={() => setSantriForm({...santriForm, selectedPackage: null})} className="text-xs text-red-400 underline mt-1 block">Batalkan pilihan paket</button>
          )}
        </div>

        {Object.entries(menuByCategory).map(([category, items]) => (
          <div key={category}>
            <h3 className="text-sm font-bold text-[#D4AF37] uppercase tracking-wider mb-3 flex items-center gap-2">
              <div className="w-4 h-px bg-[#D4AF37]/50"></div> {category} <div className="flex-1 h-px bg-[#D4AF37]/20"></div>
            </h3>
            <div className="grid grid-cols-2 sm:grid-cols-3 xl:grid-cols-4 gap-3">
              {items.map(item => {
                const qtyInCart = cart.find(c => c.id === item.id)?.qty || 0;
                const isAvail = item.isAvailable !== false;
                return (
                  <div 
                    key={item.id} 
                    className={`menu-card-3d bg-[#1A1A1A] rounded-xl overflow-hidden border transition-all duration-300 flex flex-col h-full relative ${qtyInCart > 0 ? 'border-[#D4AF37] shadow-[0_0_15px_rgba(212,175,55,0.25)]' : 'border-[#D4AF37]/20 hover:border-[#D4AF37]/60'} ${!isAvail ? 'opacity-60 grayscale' : ''}`}
                  >
                    {!isAvail && (
                      <div className="absolute inset-0 z-20 flex items-center justify-center bg-black/60 backdrop-blur-[2px]">
                        <span className="text-red-500 font-bold text-xl tracking-widest border-2 border-red-500 px-3 py-1 rounded transform -rotate-12 bg-black/80">HABIS</span>
                      </div>
                    )}
                    <div className="h-16 overflow-hidden bg-[#0A0A0A] relative">
                      <img src={getImgUrl(item)} alt={item.name} className="w-full h-full object-cover opacity-80 hover:opacity-100 transition-opacity duration-500" />
                      {qtyInCart > 0 && (
                        <div className="absolute top-0 right-0 bg-[#D4AF37] text-[#050505] text-[10px] font-bold px-2 py-1 rounded-bl-lg">
                          {qtyInCart} di keranjang
                        </div>
                      )}
                    </div>
                    <div className="p-3 flex flex-col justify-between flex-1 bg-gradient-to-b from-[#1A1A1A] to-[#111111]">
                      <div>
                        <span className="text-xs font-bold text-[#E5E7EB] block mb-0.5 leading-tight">{item.name}</span>
                        <span className="text-[11px] font-bold text-[#D4AF37] block mb-3">Rp {item.price.toLocaleString('id-ID')}</span>
                      </div>
                      
                      <div className="mt-auto relative z-30">
                        {qtyInCart > 0 ? (
                          <div className="flex items-center justify-between bg-[#0A0A0A] border border-[#D4AF37]/30 rounded-md p-0.5">
                            <button type="button" onClick={() => removeOne(item.id)} className="w-7 h-7 flex items-center justify-center text-[#D4AF37] hover:bg-[#D4AF37]/20 rounded transition-colors"><Minus size={14}/></button>
                            <span className="text-xs font-bold text-[#E5E7EB] w-4 text-center">{qtyInCart}</span>
                            <button type="button" disabled={!isAvail} onClick={() => addToCart(item)} className={`w-7 h-7 flex items-center justify-center text-[#D4AF37] hover:bg-[#D4AF37]/20 rounded transition-colors ${!isAvail ? 'opacity-50 cursor-not-allowed' : ''}`}><Plus size={14}/></button>
                          </div>
                        ) : (
                          <button type="button" disabled={!isAvail} onClick={() => addToCart(item)} className={`w-full py-1.5 text-[10px] font-bold uppercase tracking-wider bg-[#141414] text-[#D4AF37] border border-[#D4AF37]/30 rounded-md transition-colors shadow-sm ${!isAvail ? 'opacity-50 cursor-not-allowed' : 'hover:bg-[#D4AF37] hover:text-[#050505]'}`}>
                            + Tambah
                          </button>
                        )}
                      </div>
                    </div>
                  </div>
                );
              })}
            </div>
          </div>
        ))}
      </div>
    </div>
  </div>

  <div className="flex-[1.2]">
    <div className="mb-6 flex justify-center gap-2 p-1.5 bg-[#111111]/80 backdrop-blur-sm border border-[#D4AF37]/20 rounded-lg w-fit mx-auto shadow-lg relative z-10">
      <button 
        onClick={() => setOrderType('santri')}
        className={`px-6 py-2 rounded-md text-sm font-bold transition-all duration-300 ${orderType === 'santri' ? 'bg-[#D4AF37] text-[#050505] shadow-[0_0_15px_rgba(212,175,55,0.4)] transform scale-105' : 'text-[#9CA3AF] hover:text-[#D4AF37]'}`}
      >
        Pemesanan Santri
      </button>
      <button 
        onClick={() => setOrderType('ifthor')}
        className={`px-6 py-2 rounded-md text-sm font-bold transition-all duration-300 ${orderType === 'ifthor' ? 'bg-[#D4AF37] text-[#050505] shadow-[0_0_15px_rgba(212,175,55,0.4)] transform scale-105' : 'text-[#9CA3AF] hover:text-[#D4AF37]'}`}
      >
        Ifthor Jama'i
      </button>
    </div>

    <div className={cardClass}>
      <div className="text-center mb-8 relative">
        <h2 className="text-3xl font-serif font-bold text-[#D4AF37] mb-2 drop-shadow-[0_2px_10px_rgba(212,175,55,0.2)]">
          {orderType === 'santri' ? 'Formulir Santri' : 'Formulir Ifthor'}
        </h2>
        <p className="text-sm text-[#9CA3AF]">Silakan isi detail pesanan Anda dengan lengkap.</p>
      </div>

      {orderType === 'santri' && (
        <div className="bg-[#1a1500]/50 border border-[#D4AF37]/50 text-[#D4AF37] p-4 rounded-md mb-8 text-sm flex items-start gap-3 shadow-inner backdrop-blur-sm">
          <span className="text-lg animate-pulse">⚠️</span>
          <p className="font-medium leading-relaxed">Perhatian: Layanan pemesanan ditutup secara otomatis pada hari Senin malam dan Kamis malam.</p>
        </div>
      )}

      {orderSuccessMsg && (
        <div className="bg-[#10B981]/20 border border-[#10B981] text-[#10B981] p-4 rounded-md mb-6 text-sm flex items-center gap-3">
          <CheckCircle2 size={22} className="shrink-0" />
          <p className="font-bold">Pesanan berhasil! WhatsApp admin terbuka dan pesanan telah terdaftar.</p>
        </div>
      )}

      <form onSubmit={orderType === 'santri' ? handleSantriSubmit : handleIfthorSubmit} className="space-y-5 relative z-10">
        {orderType === 'santri' && (
          <>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Nama Pemesan (Wali)</label>
                <input required value={santriForm.namaPemesan} onChange={e=>setSantriForm({...santriForm, namaPemesan: e.target.value})} className={inputClass} type="text" placeholder="Nama Anda..." />
              </div>
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Nama Penerima (Santri)</label>
                <input required value={santriForm.namaSantri} onChange={e=>setSantriForm({...santriForm, namaSantri: e.target.value})} className={inputClass} type="text" placeholder="Nama Santri..." />
              </div>
            </div>
            <div className="grid grid-cols-2 gap-4">
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Kelas</label>
                <input required value={santriForm.kelas} onChange={e=>setSantriForm({...santriForm, kelas: e.target.value})} className={inputClass} type="text" placeholder="Misal: XII-A" />
              </div>
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Asrama</label>
                <input required value={santriForm.asrama} onChange={e=>setSantriForm({...santriForm, asrama: e.target.value})} className={inputClass} type="text" placeholder="Nama asrama..." />
              </div>
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Pilihan Nasi</label>
              <select value={santriForm.pilihanNasi} onChange={e=>setSantriForm({...santriForm, pilihanNasi: e.target.value})} className={inputClass}>
                <option value="Nasi Biasa">Nasi Biasa</option>
                <option value="Nasi Kuning">Nasi Kuning</option>
                <option value="Nasi Daun Jeruk">Nasi Daun Jeruk</option>
              </select>
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Waktu Pengambilan</label>
              <input required value={santriForm.waktu} onChange={e=>setSantriForm({...santriForm, waktu: e.target.value})} className={inputClass} type="text" placeholder="Misal: Pukul 16:00 (Ba'da Ashar)" />
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Pesan Tambahan (Opsional)</label>
              <textarea value={santriForm.catatan} onChange={e=>setSantriForm({...santriForm, catatan: e.target.value})} className={inputClass} rows="2" placeholder="Contoh: Tolong dibungkus rapi, sambal dipisah..."></textarea>
            </div>
          </>
        )}

        {orderType === 'ifthor' && (
          <>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Nama Wali Kelas (Pemesan)</label>
              <input required value={ifthorForm.wali} onChange={e=>setIfthorForm({...ifthorForm, wali: e.target.value})} className={inputClass} type="text" placeholder="Masukkan nama Anda..." />
            </div>
            <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Kelas (Peserta Ifthor)</label>
                <input required value={ifthorForm.kelas} onChange={e=>setIfthorForm({...ifthorForm, kelas: e.target.value})} className={inputClass} type="text" placeholder="Misal: Kelas X-B" />
              </div>
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Pilihan Nasi</label>
                <select value={ifthorForm.pilihanNasiIfthor} onChange={e=>setIfthorForm({...ifthorForm, pilihanNasiIfthor: e.target.value})} className={inputClass}>
                  <option value="Nasi Biasa">Nasi Biasa</option>
                  <option value="Nasi Kuning">Nasi Kuning</option>
                  <option value="Nasi Daun Jeruk">Nasi Daun Jeruk</option>
                </select>
              </div>
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Hari & Tanggal Pelaksanaan</label>
              <input required value={ifthorForm.hariTanggal} onChange={e=>setIfthorForm({...ifthorForm, hariTanggal: e.target.value})} className={inputClass} type="text" placeholder="Misal: Rabu, 15 Ramadhan" />
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Catatan Tambahan (Opsional)</label>
              <textarea value={ifthorForm.catatan} onChange={e=>setIfthorForm({...ifthorForm, catatan: e.target.value})} className={inputClass} rows="2" placeholder="Catatan khusus..."></textarea>
            </div>
          </>
        )}

        <div className="bg-[#1A1A1A] p-4 rounded-xl border border-[#D4AF37]/30 my-4">
          <h4 className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2">Ringkasan Pesanan Anda</h4>
          {santriForm.selectedPackage && (
            <div className="flex justify-between text-xs py-1 text-[#E5E7EB]">
              <span>{santriForm.selectedPackage.name}</span>
              <span className="font-bold text-[#D4AF37]">Rp {santriForm.selectedPackage.price.toLocaleString('id-ID')}</span>
            </div>
          )}
          {cart.map(item => (
            <div key={item.id} className="flex justify-between text-xs py-1 text-[#E5E7EB]">
              <span>{item.name} ({item.qty}x)</span>
              <span className="font-bold text-[#D4AF37]">Rp {(item.price * item.qty).toLocaleString('id-ID')}</span>
            </div>
          ))}
          <div className="border-t border-[#D4AF37]/20 mt-3 pt-3 flex justify-between items-center">
            <span className="font-serif font-bold text-[#E5E7EB]">Total Pembayaran</span>
            <span className="text-lg font-bold text-[#D4AF37]">Rp {totalCart.toLocaleString('id-ID')}</span>
          </div>
        </div>

        <div className="space-y-3">
          <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider block">Metode Pembayaran</label>
          <div className="grid grid-cols-2 gap-4">
            <button 
              type="button" 
              onClick={() => setPaymentMethod('cash')} 
              className={`p-3 rounded-lg border text-sm font-bold transition-all ${paymentMethod === 'cash' ? 'bg-[#D4AF37] text-[#050505] border-[#D4AF37] shadow-[0_0_15px_rgba(212,175,55,0.3)]' : 'bg-[#1A1A1A] text-[#9CA3AF] border-[#D4AF37]/30 hover:border-[#D4AF37]'}`}
            >
              Tunai (Cash)
            </button>
            <button 
              type="button" 
              onClick={() => setPaymentMethod('qris')} 
              className={`p-3 rounded-lg border text-sm font-bold transition-all ${paymentMethod === 'qris' ? 'bg-[#D4AF37] text-[#050505] border-[#D4AF37] shadow-[0_0_15px_rgba(212,175,55,0.3)]' : 'bg-[#1A1A1A] text-[#9CA3AF] border-[#D4AF37]/30 hover:border-[#D4AF37]'}`}
            >
              QRIS Transfer
            </button>
          </div>
        </div>

        {paymentMethod === 'qris' && (
          <div className="bg-[#1A1A1A] p-4 rounded-xl border border-[#D4AF37]/40 text-center space-y-3">
            <p className="text-xs text-[#9CA3AF]">Scan QRIS di bawah ini untuk melakukan pembayaran:</p>
            <div className="w-48 h-48 mx-auto bg-white p-2 rounded-lg border border-[#D4AF37]/40 flex items-center justify-center">
              <img src={customQrisImage || "https://api.qrserver.com/v1/create-qr-code/?size=200x200&data=LA-TANSA-CAFE-QRIS-PAYMENT"} alt="QRIS Code" className="w-full h-full object-contain" />
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Upload Bukti Transfer QRIS</label>
              <input type="file" accept="image/*" onChange={handleQrisUpload} className="text-xs text-[#9CA3AF] file:mr-4 file:py-2 file:px-4 file:rounded-md file:border-0 file:text-xs file:font-bold file:bg-[#D4AF37] file:text-[#050505] hover:file:bg-[#E3C365]" />
            </div>
            {qrisProof && <p className="text-xs text-green-400 font-bold">Bukti transfer berhasil dilampirkan!</p>}
          </div>
        )}

        <button 
          type="submit" 
          disabled={isSubmitDisabled} 
          className={`${btnClass} w-full flex items-center justify-center gap-2`}
        >
          <MessageCircle size={18} /> Kirim Pesanan via WhatsApp & Buat Struk
        </button>
      </form>
    </div>
  </div>
</div>

```

); }

function POSKasir({ menuItems, onCreateOrder, btnClass, cardClass }) { const \[cart, setCart\] = useState(\[\]); const \[customerName, setCustomerName\] = useState(''); const \[paymentType, setPaymentType\] = useState('cash');

const addToCart = (item) => { const existing = cart.find(c => c.id === item.id); if (existing) { setCart(cart.map(c => c.id === item.id ? { ...c, qty: c.qty + 1 } : c)); } else { setCart(\[...cart, { ...item, qty: 1 }\]); } };

const removeOne = (id) => { const existing = cart.find(c => c.id === id); if (existing && existing.qty > 1) { setCart(cart.map(c => c.id === id ? { ...c, qty: c.qty - 1 } : c)); } else { setCart(cart.filter(c => c.id !== id)); } };

const total = cart.reduce((sum, item) => sum + (item.price \* item.qty), 0);

const handleCheckout = (e) => { e.preventDefault(); if (cart.length === 0) return;

```
const orderData = {
  type: 'Kasir POS Langsung',
  customer: `Kasir / Pelanggan: ${customerName || 'Umum'}`,
  details: cart.map(c => `${c.name} (${c.qty}x) - Rp ${(c.price * c.qty).toLocaleString('id-ID')}`).join('\n'),
  payment: paymentType,
  total: total
};

onCreateOrder(orderData);
setCart([]);
setCustomerName('');

```

};

return (    Kasir POS - Katalog Produk  {menuItems.map(item => { const qtyInCart = cart.find(c => c.id === item.id)?.qty || 0; return (  {qtyInCart > 0 && (  {qtyInCart}x  )}     {item.name} Rp {item.price.toLocaleString('id-ID')}   {qtyInCart > 0 ? (  <button type="button" onClick={() => removeOne(item.id)} className="w-7 h-7 flex items-center justify-center text-\[#D4AF37\] hover:bg-\[#D4AF37\]/20 rounded"> {qtyInCart} <button type="button" onClick={() => addToCart(item)} className="w-7 h-7 flex items-center justify-center text-\[#D4AF37\] hover:bg-\[#D4AF37\]/20 rounded">  ) : ( <button type="button" onClick={() => addToCart(item)} className="w-full py-2 bg-\[#D4AF37\] text-\[#050505\] font-bold text-xs rounded-md hover:bg-\[#E3C365\] transition-all shadow"> + Tambah  )}   ); })}   

```
  <div className="space-y-6">
    <div className={cardClass}>
      <h3 className="text-xl font-serif font-bold text-[#D4AF37] mb-4">Keranjang POS</h3>
      <form onSubmit={handleCheckout} className="space-y-4">
        <div>
          <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Nama Pembeli</label>
          <input value={customerName} onChange={e=>setCustomerName(e.target.value)} className="w-full p-2 bg-[#1A1A1A] border border-[#D4AF37]/30 rounded-md text-xs text-[#E5E7EB]" placeholder="Nama pembeli..." />
        </div>

        <div className="space-y-2 max-h-56 overflow-y-auto pr-1">
          {cart.length === 0 ? (
            <p className="text-xs text-[#9CA3AF] text-center py-6">Keranjang kasir masih kosong</p>
          ) : (
            cart.map(item => (
              <div key={item.id} className="flex justify-between items-center text-xs bg-[#1A1A1A] p-2 rounded border border-[#D4AF37]/20">
                <div>
                  <span className="font-bold text-[#E5E7EB] block">{item.name}</span>
                  <span className="text-[#9CA3AF]">{item.qty} x Rp {item.price.toLocaleString('id-ID')}</span>
                </div>
                <div className="flex items-center gap-2">
                  <span className="font-bold text-[#D4AF37]">Rp {(item.price * item.qty).toLocaleString('id-ID')}</span>
                  <button type="button" onClick={() => removeOne(item.id)} className="text-red-400 hover:text-red-300"><Trash2 size={14}/></button>
                </div>
              </div>
            ))
          )}
        </div>

        <div className="border-t border-[#D4AF37]/20 pt-3 flex justify-between items-center">
          <span className="font-serif font-bold text-[#E5E7EB]">Total Tagihan</span>
          <span className="text-lg font-bold text-[#D4AF37]">Rp {total.toLocaleString('id-ID')}</span>
        </div>

        <div>
          <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Metode Pembayaran</label>
          <select value={paymentType} onChange={e=>setPaymentType(e.target.value)} className="w-full p-2 bg-[#1A1A1A] border border-[#D4AF37]/30 rounded-md text-xs text-[#E5E7EB]">
            <option value="cash">Tunai (Cash)</option>
            <option value="qris">QRIS</option>
            <option value="transfer">Transfer Bank</option>
          </select>
        </div>

        <button type="submit" disabled={cart.length === 0} className={`${btnClass} w-full`}>
          Proses Pembayaran & Cetak Nota
        </button>
      </form>
    </div>
  </div>
</div>

```

); }

function AdminDashboard({ orders, transactions, setTransactions, menuItems, setMenuItems, specialMenus, setSpecialMenus, packages, setPackages, customQrisImage, setCustomQrisImage, btnClass, inputClass, cardClass, onViewReceipt }) { const \[activeAdminTab, setActiveAdminTab\] = useState('orders');

const \[newTrx, setNewTrx\] = useState({ date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'IN', category: 'PENJUALAN', amount: '', note: '' });

const \[savingDailyAmount, setSavingDailyAmount\] = useState(''); const \[savingNote, setSavingNote\] = useState('');

const handleAddTransaction = (e) => { e.preventDefault(); if (!newTrx.amount) return; const item = { id: `TRX-${Math.floor(Math.random() * 1000000)}`, ...newTrx, amount: parseInt(newTrx.amount) }; setTransactions(\[item, ...transactions\]); setNewTrx({ date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'IN', category: 'PENJUALAN', amount: '', note: '' }); };

const handleDailySavingSubmit = (e) => { e.preventDefault(); if (!savingDailyAmount) return; const item = { id: `TRX-SAV-${Math.floor(Math.random() * 1000000)}`, date: new Date().toLocaleDateString(), hijriMonth: 'Rabiul Awal', quarter: 'Triwulan I (Q1)', type: 'SAVING', category: 'TABUNGAN_REKENING', amount: parseInt(savingDailyAmount), note: savingNote || 'Setoran Tabungan Harian Rekening Toko' }; setTransactions(\[item, ...transactions\]); setSavingDailyAmount(''); setSavingNote(''); };

const totalIn = transactions.filter(t => t.type === 'IN').reduce((s, t) => s + t.amount, 0); const totalOut = transactions.filter(t => t.type === 'OUT').reduce((s, t) => s + t.amount, 0); const totalSaving = transactions.filter(t => t.type === 'SAVING').reduce((s, t) => s + t.amount, 0); const netProfit = totalIn - totalOut;

const totalMaterialCost = transactions.filter(t => t.category === 'BAHAN_BAKU').reduce((s, t) => s + t.amount, 0); const totalEquipCost = transactions.filter(t => t.category === 'PERALATAN').reduce((s, t) => s + t.amount, 0); const estimatedHPP = totalIn > 0 ? Math.round((totalMaterialCost / totalIn) \* 100) : 0;

const toggleAvailability = (id) => { setMenuItems(menuItems.map(m => m.id === id ? { ...m, isAvailable: !m.isAvailable } : m)); };

const handleQrisLogoUpload = (e) => { const file = e.target.files\[0\]; if (file) { const reader = new FileReader(); reader.onloadend = () => setCustomQrisImage(reader.result); reader.readAsDataURL(file); } };

return (   {\[ { id: 'orders', label: 'Riwayat Pesanan' }, { id: 'finance', label: 'Keuangan & HPP' }, { id: 'catalog', label: 'Kelola Katalog & Menu' }, { id: 'settings', label: 'Pengaturan QRIS' } \].map(tab => ( <button key={tab.id} onClick={() => setActiveAdminTab(tab.id)} className={`px-5 py-2 rounded-lg text-xs font-bold transition-all whitespace-nowrap ${activeAdminTab === tab.id ? 'bg-[#D4AF37] text-[#050505] shadow' : 'text-[#9CA3AF] hover:text-[#D4AF37]'}`} > {tab.label}  ))} 

```
  {activeAdminTab === 'orders' && (
    <div className={cardClass}>
      <h2 className="text-2xl font-serif font-bold text-[#D4AF37] mb-6">Riwayat Pesanan & Nota Tersimpan</h2>
      <div className="space-y-4 max-h-[600px] overflow-y-auto pr-2">
        {orders.length === 0 ? (
          <p className="text-center text-xs text-[#9CA3AF] py-10">Belum ada riwayat pesanan yang masuk.</p>
        ) : (
          orders.map(order => (
            <div key={order.id} className="bg-[#1A1A1A] p-4 rounded-xl border border-[#D4AF37]/30 flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
              <div className="space-y-1">
                <div className="flex items-center gap-3">
                  <span className="font-bold text-sm text-[#D4AF37]">{order.id}</span>
                  <span className="text-[10px] bg-[#D4AF37]/20 text-[#D4AF37] px-2 py-0.5 rounded font-bold uppercase">{order.type}</span>
                  <span className="text-xs text-[#9CA3AF]">{order.date}</span>
                </div>
                <p className="text-xs text-[#E5E7EB] font-medium whitespace-pre-line">{order.customer}</p>
                <p className="text-xs text-[#9CA3AF] font-mono bg-black/40 p-2 rounded border border-[#D4AF37]/10 whitespace-pre-line">{order.details}</p>
              </div>
              <div className="flex flex-col items-end gap-2 shrink-0">
                <span className="text-base font-bold text-[#D4AF37]">Rp {order.total.toLocaleString('id-ID')}</span>
                <button onClick={() => onViewReceipt(order)} className="px-4 py-2 bg-[#D4AF37] text-[#050505] font-bold text-xs rounded-md hover:bg-[#E3C365] transition-all flex items-center gap-1.5 shadow">
                  <FileText size={14} /> Lihat & Print Nota
                </button>
              </div>
            </div>
          ))
        )}
      </div>
    </div>
  )}

  {activeAdminTab === 'finance' && (
    <div className="space-y-6">
      <div className="grid grid-cols-1 md:grid-cols-4 gap-4">
        <div className={cardClass}>
          <span className="text-xs text-[#9CA3AF] uppercase tracking-wider block mb-1">Total Pemasukan (In)</span>
          <span className="text-2xl font-bold text-green-400">Rp {totalIn.toLocaleString('id-ID')}</span>
        </div>
        <div className={cardClass}>
          <span className="text-xs text-[#9CA3AF] uppercase tracking-wider block mb-1">Total Pengeluaran (Out)</span>
          <span className="text-2xl font-bold text-red-400">Rp {totalOut.toLocaleString('id-ID')}</span>
        </div>
        <div className={cardClass}>
          <span className="text-xs text-[#9CA3AF] uppercase tracking-wider block mb-1">Total Tabungan Toko</span>
          <span className="text-2xl font-bold text-[#D4AF37]">Rp {totalSaving.toLocaleString('id-ID')}</span>
        </div>
        <div className={cardClass}>
          <span className="text-xs text-[#9CA3AF] uppercase tracking-wider block mb-1">Estimasi HPP & Laba</span>
          <span className="text-2xl font-bold text-[#D4AF37]">{estimatedHPP}% <span className="text-xs text-[#9CA3AF] font-normal">(Net: Rp {netProfit.toLocaleString('id-ID')})</span></span>
        </div>
      </div>

      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
        <div className={cardClass}>
          <h3 className="text-xl font-serif font-bold text-[#D4AF37] mb-4 flex items-center gap-2">
            <Landmark size={18} /> Tabungan Harian Rekening Toko
          </h3>
          <form onSubmit={handleDailySavingSubmit} className="space-y-4">
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Jumlah Setoran Tabungan Hari Ini (Rp)</label>
              <input required type="number" value={savingDailyAmount} onChange={e=>setSavingDailyAmount(e.target.value)} className={inputClass} placeholder="Misal: 50000" />
            </div>
            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-2 block">Keterangan / Catatan Tabungan</label>
              <input type="text" value={savingNote} onChange={e=>setSavingNote(e.target.value)} className={inputClass} placeholder="Misal: Setoran tabungan harian toko..." />
            </div>
            <button type="submit" className={`${btnClass} w-full`}>Catat Tabungan Harian</button>
          </form>
        </div>

        <div className={cardClass}>
          <h3 className="text-xl font-serif font-bold text-[#D4AF37] mb-4">Catat Transaksi Baru & HPP</h3>
          <form onSubmit={handleAddTransaction} className="space-y-3">
            <div className="grid grid-cols-2 gap-3">
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-1 block">Jenis Arus</label>
                <select value={newTrx.type} onChange={e=>setNewTrx({...newTrx, type: e.target.value})} className={inputClass}>
                  <option value="IN">Pemasukan (IN)</option>
                  <option value="OUT">Pengeluaran (OUT)</option>
                  <option value="SAVING">Tabungan Rekening</option>
                </select>
              </div>
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-1 block">Kategori</label>
                <select value={newTrx.category} onChange={e=>setNewTrx({...newTrx, category: e.target.value})} className={inputClass}>
                  <option value="PENJUALAN">Penjualan</option>
                  <option value="BAHAN_BAKU">Bahan Baku</option>
                  <option value="PERALATAN">Peralatan</option>
                  <option value="TABUNGAN_REKENING">Tabungan Rekening</option>
                </select>
              </div>
            </div>

            <div className="grid grid-cols-2 gap-3">
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-1 block">Bulan Hijriah</label>
                <select value={newTrx.hijriMonth} onChange={e=>setNewTrx({...newTrx, hijriMonth: e.target.value})} className={inputClass}>
                  {HIJRI_MONTHS.map(m => <option key={m} value={m}>{m}</option>)}
                </select>
              </div>
              <div>
                <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-1 block">Triwulan</label>
                <select value={newTrx.quarter} onChange={e=>setNewTrx({...newTrx, quarter: e.target.value})} className={inputClass}>
                  <option value="Triwulan I (Q1)">Triwulan I (Q1)</option>
                  <option value="Triwulan II (Q2)">Triwulan II (Q2)</option>
                  <option value="Triwulan III (Q3)">Triwulan III (Q3)</option>
                  <option value="Triwulan IV (Q4)">Triwulan IV (Q4)</option>
                </select>
              </div>
            </div>

            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-1 block">Nominal (Rp)</label>
              <input required type="number" value={newTrx.amount} onChange={e=>setNewTrx({...newTrx, amount: e.target.value})} className={inputClass} placeholder="Nominal..." />
            </div>

            <div>
              <label className="text-xs font-bold text-[#D4AF37] uppercase tracking-wider mb-1 block">Catatan / Keterangan</label>
              <input type="text" value={newTrx.note} onChange={e=>setNewTrx({...newTrx, note: e.target.value})} className={inputClass} placeholder="Keterangan transaksi..." />
            </div>

            <button type="submit" className={`${btnClass} w-full`}>Simpan Transaksi</button>
          </form>
        </div>
      </div>

      <div className={cardClass}>
        <h3 className="text-xl font-serif font-bold text-[#D4AF37] mb-4">Riwayat Buku Besar & Tabungan</h3>
        <div className="space-y-2 max-h-96 overflow-y-auto pr-1">
          {transactions.map(trx => (
            <div key={trx.id} className="bg-[#1A1A1A] p-3 rounded-lg border border-[#D4AF37]/20 flex justify-between items-center text-xs">
              <div>
                <div className="flex items-center gap-2 mb-1">
                  <span className={`font-bold px-2 py-0.5 rounded text-[10px] ${trx.type === 'IN' ? 'bg-green-500/20 text-green-400' : trx.type === 'OUT' ? 'bg-red-500/20 text-red-400' : 'bg-amber-500/20 text-[#D4AF37]'}`}>{trx.type}</span>
                  <span className="text-[#9CA3AF] font-bold">{trx.category}</span>
                  <span className="text-[#D4AF37] bg-[#D4AF37]/10 px-2 py-0.5 rounded">{trx.hijriMonth} | {trx.quarter}</span>
                  <span className="text-[#9CA3AF]">{trx.date}</span>
                </div>
                <p className="text-[#E5E7EB] font-medium">{trx.note}</p>
              </div>
              <span className={`font-bold text-sm ${trx.type === 'IN' ? 'text-green-400' : trx.type === 'OUT' ? 'text-red-400' : 'text-[#D4AF37]'}`}>
                {trx.type === 'OUT' ? '-' : '+'} Rp {trx.amount.toLocaleString('id-ID')}
              </span>
            </div>
          ))}
        </div>
      </div>
    </div>
  )}

  {activeAdminTab === 'catalog' && (
    <div className={cardClass}>
      <h2 className="text-2xl font-serif font-bold text-[#D4AF37] mb-6">Kelola Ketersediaan Menu (Tersedia / Habis)</h2>
      <div className="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4 max-h-[600px] overflow-y-auto pr-2">
        {menuItems.map(item => {
          const isAvail = item.isAvailable !== false;
          return (
            <div key={item.id} className="bg-[#1A1A1A] p-4 rounded-xl border border-[#D4AF37]/20 flex items-center justify-between gap-3">
              <div className="flex items-center gap-3">
                <img src={getImgUrl(item)} alt={item.name} className="w-12 h-12 rounded-lg object-cover" />
                <div>
                  <span className="font-bold text-xs text-[#E5E7EB] block">{item.name}</span>
                  <span className="text-[11px] text-[#D4AF37]">Rp {item.price.toLocaleString('id-ID')}</span>
                </div>
              </div>
              <button 
                onClick={() => toggleAvailability(item.id)}
                className={`px-3 py-1.5 rounded-md text-xs font-bold transition-all ${isAvail ? 'bg-green-500/20 text-green-400 border border-green-500/40' : 'bg-red-500/20 text-red-400 border border-red-500/40'}`}
              >
                {isAvail ? 'Tersedia' : 'Habis'}
              </button>
            </div>
          );
        })}
      </div>
    </div>
  )}

  {activeAdminTab === 'settings' && (
    <div className={cardClass}>
      <h2 className="text-2xl font-serif font-bold text-[#D4AF37] mb-4">Pengaturan QRIS Pemb

````````````````````````````````````````````````````````````````````````````````````````````````````````````````````````