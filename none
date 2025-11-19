import React, { useState, useRef, useEffect } from 'react';
import { Moon, Star, Download, RefreshCw, Type, Palette, Image as ImageIcon, Heart, CloudMoon, Sparkles } from 'lucide-react';

const RamadhanPosterMaker = () => {
  const posterRef = useRef(null);
  const [loading, setLoading] = useState(false);
  const [isFontLoaded, setIsFontLoaded] = useState(false);

  // Load Google Fonts and html2canvas
  useEffect(() => {
    const fontLink = document.createElement("link");
    fontLink.href = "https://fonts.googleapis.com/css2?family=Amiri:ital,wght@0,400;0,700;1,400&family=Playfair+Display:wght@400;700&family=Poppins:wght@300;400;600&display=swap";
    fontLink.rel = "stylesheet";
    document.head.appendChild(fontLink);
    fontLink.onload = () => setIsFontLoaded(true);

    const script = document.createElement('script');
    script.src = 'https://html2canvas.hertzen.com/dist/html2canvas.min.js';
    script.async = true;
    document.body.appendChild(script);

    return () => {
      document.head.removeChild(fontLink);
      document.body.removeChild(script);
    };
  }, []);

  const [content, setContent] = useState({
    title: "Marhaban ya Ramadhan",
    subtitle: "Selamat Menunaikan Ibadah Puasa 1446 H",
    quote: "Semoga Allah menerima amal ibadah kita dan mengampuni segala dosa-dosa kita.",
    footer: "Keluarga Besar Bapak Fulan & Ibu Fulanah"
  });

  const themes = [
    {
      id: 'midnight',
      name: 'Midnight Gold',
      bg: 'bg-gradient-to-br from-slate-900 via-indigo-950 to-slate-900',
      text: 'text-amber-100',
      accent: 'text-amber-400',
      border: 'border-amber-500/30',
      decoration: 'gold-dots'
    },
    {
      id: 'emerald',
      name: 'Royal Emerald',
      bg: 'bg-gradient-to-bl from-emerald-900 via-teal-900 to-emerald-950',
      text: 'text-emerald-50',
      accent: 'text-yellow-400',
      border: 'border-emerald-400/30',
      decoration: 'geometric'
    },
    {
      id: 'sunset',
      name: 'Desert Sunset',
      bg: 'bg-gradient-to-tr from-orange-900 via-amber-800 to-red-900',
      text: 'text-orange-50',
      accent: 'text-orange-200',
      border: 'border-orange-400/30',
      decoration: 'sand'
    },
    {
      id: 'clean',
      name: 'Modern White',
      bg: 'bg-gradient-to-br from-slate-50 via-white to-slate-100',
      text: 'text-slate-800',
      accent: 'text-teal-600',
      border: 'border-slate-200',
      decoration: 'minimal'
    }
  ];

  const [currentTheme, setCurrentTheme] = useState(themes[0]);
  const [selectedIcon, setSelectedIcon] = useState('moon'); // moon, lantern, mosque

  const handleDownload = async () => {
    if (!window.html2canvas || !posterRef.current) {
      alert("Mohon tunggu sebentar, fitur unduh sedang disiapkan...");
      return;
    }
    
    setLoading(true);
    try {
      const canvas = await window.html2canvas(posterRef.current, {
        scale: 2, // Higher resolution
        backgroundColor: null,
        logging: false,
        useCORS: true
      });
      
      const image = canvas.toDataURL("image/png");
      const link = document.createElement("a");
      link.href = image;
      link.download = `Poster-Ramadhan-${Date.now()}.png`;
      link.click();
    } catch (error) {
      console.error("Gagal mengunduh:", error);
      alert("Maaf, terjadi kesalahan saat mengunduh poster.");
    }
    setLoading(false);
  };

  const randomize = () => {
    const randomTheme = themes[Math.floor(Math.random() * themes.length)];
    setCurrentTheme(randomTheme);
    
    const quotes = [
      "Mohon maaf lahir dan batin atas segala khilaf dan salah.",
      "Mari sucikan hati, jernihkan pikiran menyambut bulan suci.",
      "Ramadhan berkah, mari berlomba-lomba dalam kebaikan.",
      "Semoga kita menjadi pribadi yang lebih bertaqwa."
    ];
    
    setContent(prev => ({
      ...prev,
      quote: quotes[Math.floor(Math.random() * quotes.length)]
    }));
  };

  // Decorative SVG Components
  const LanternIcon = ({ className }) => (
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" className={className}>
      <path d="M12 2L12 5M12 5L8 9H16L12 5ZM12 5V9M8 9L9 19H15L16 9M10 19L10 22M14 19L14 22" strokeLinecap="round" strokeLinejoin="round"/>
    </svg>
  );

  const MosqueIcon = ({ className }) => (
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="1.5" className={className}>
       <path d="M3 21h18M5 21V7l8-4 8 4v14M10 10a3 3 0 1 0 6 0" strokeLinecap="round" strokeLinejoin="round"/>
    </svg>
  );

  return (
    <div className="min-h-screen bg-slate-100 text-slate-800 font-sans flex flex-col md:flex-row">
      
      {/* Sidebar Controls */}
      <div className="w-full md:w-96 bg-white shadow-xl z-10 flex flex-col h-auto md:h-screen overflow-y-auto border-r border-slate-200">
        <div className="p-6 border-b border-slate-100 bg-gradient-to-r from-teal-600 to-teal-500 text-white">
          <h1 className="text-2xl font-bold flex items-center gap-2">
            <Moon className="w-6 h-6 fill-current" /> Poster Ramadhan
          </h1>
          <p className="text-teal-100 text-sm mt-1">Buat ucapan otomatis & indah.</p>
        </div>

        <div className="p-6 space-y-8 flex-1">
          
          {/* Text Inputs */}
          <div className="space-y-4">
            <div className="flex items-center gap-2 text-teal-700 font-semibold border-b pb-2 mb-3">
              <Type size={18} />
              <h2>Isi Konten</h2>
            </div>
            
            <div>
              <label className="block text-xs font-medium text-slate-500 uppercase mb-1">Judul Utama</label>
              <input 
                type="text" 
                value={content.title}
                onChange={(e) => setContent({...content, title: e.target.value})}
                className="w-full px-3 py-2 border rounded-lg focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition bg-slate-50"
              />
            </div>
             <div>
              <label className="block text-xs font-medium text-slate-500 uppercase mb-1">Sub-Judul</label>
              <input 
                type="text" 
                value={content.subtitle}
                onChange={(e) => setContent({...content, subtitle: e.target.value})}
                className="w-full px-3 py-2 border rounded-lg focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition bg-slate-50"
              />
            </div>
            <div>
              <label className="block text-xs font-medium text-slate-500 uppercase mb-1">Ucapan / Doa</label>
              <textarea 
                rows="3"
                value={content.quote}
                onChange={(e) => setContent({...content, quote: e.target.value})}
                className="w-full px-3 py-2 border rounded-lg focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition bg-slate-50"
              />
            </div>
            <div>
              <label className="block text-xs font-medium text-slate-500 uppercase mb-1">Nama Pengirim / Footer</label>
              <input 
                type="text" 
                value={content.footer}
                onChange={(e) => setContent({...content, footer: e.target.value})}
                className="w-full px-3 py-2 border rounded-lg focus:ring-2 focus:ring-teal-500 focus:border-teal-500 outline-none transition bg-slate-50"
              />
            </div>
          </div>

          {/* Theme Selection */}
          <div className="space-y-4">
            <div className="flex items-center gap-2 text-teal-700 font-semibold border-b pb-2 mb-3">
              <Palette size={18} />
              <h2>Pilih Tema</h2>
            </div>
            <div className="grid grid-cols-2 gap-3">
              {themes.map((t) => (
                <button
                  key={t.id}
                  onClick={() => setCurrentTheme(t)}
                  className={`p-2 rounded-lg border-2 text-left transition-all relative overflow-hidden ${
                    currentTheme.id === t.id ? 'border-teal-500 ring-1 ring-teal-500' : 'border-slate-200 hover:border-teal-300'
                  }`}
                >
                  <div className={`absolute inset-0 opacity-20 ${t.bg}`}></div>
                  <span className="relative z-10 text-sm font-medium text-slate-700">{t.name}</span>
                </button>
              ))}
            </div>
          </div>

          {/* Icon Selection */}
          <div className="space-y-4">
            <div className="flex items-center gap-2 text-teal-700 font-semibold border-b pb-2 mb-3">
              <ImageIcon size={18} />
              <h2>Ikon Dekorasi</h2>
            </div>
            <div className="flex gap-4 justify-center">
              <button 
                onClick={() => setSelectedIcon('moon')}
                className={`p-3 rounded-full border transition-all ${selectedIcon === 'moon' ? 'bg-teal-50 border-teal-500 text-teal-600' : 'border-slate-200 text-slate-400 hover:bg-slate-50'}`}
              >
                <CloudMoon size={24} />
              </button>
              <button 
                onClick={() => setSelectedIcon('lantern')}
                className={`p-3 rounded-full border transition-all ${selectedIcon === 'lantern' ? 'bg-teal-50 border-teal-500 text-teal-600' : 'border-slate-200 text-slate-400 hover:bg-slate-50'}`}
              >
                <LanternIcon className="w-6 h-6" />
              </button>
               <button 
                onClick={() => setSelectedIcon('mosque')}
                className={`p-3 rounded-full border transition-all ${selectedIcon === 'mosque' ? 'bg-teal-50 border-teal-500 text-teal-600' : 'border-slate-200 text-slate-400 hover:bg-slate-50'}`}
              >
                <MosqueIcon className="w-6 h-6" />
              </button>
            </div>
          </div>
          
          <button 
            onClick={randomize}
            className="w-full py-2 px-4 bg-indigo-50 text-indigo-600 rounded-lg hover:bg-indigo-100 transition flex items-center justify-center gap-2 font-medium border border-indigo-200"
          >
            <RefreshCw size={18} /> Acak Tema & Doa
          </button>

        </div>
        
        <div className="p-6 bg-slate-50 border-t border-slate-200">
          <button 
            onClick={handleDownload}
            disabled={loading}
            className="w-full py-3 px-4 bg-teal-600 text-white rounded-xl hover:bg-teal-700 transition shadow-lg shadow-teal-600/30 flex items-center justify-center gap-2 font-bold disabled:opacity-70 disabled:cursor-not-allowed transform active:scale-95"
          >
            {loading ? (
              <span className="animate-pulse">Memproses...</span>
            ) : (
              <>
                <Download size={20} /> Unduh Poster
              </>
            )}
          </button>
        </div>
      </div>

      {/* Main Preview Area */}
      <div className="flex-1 p-4 md:p-10 flex items-center justify-center bg-slate-200 overflow-hidden relative">
        {/* Background pattern for workspace */}
        <div className="absolute inset-0 opacity-10 pointer-events-none" style={{backgroundImage: 'radial-gradient(#cbd5e1 1px, transparent 1px)', backgroundSize: '20px 20px'}}></div>

        {/* The Poster Canvas */}
        <div 
          ref={posterRef}
          id="poster-canvas"
          className={`
            relative w-full max-w-[500px] aspect-[4/5] shadow-2xl rounded-none overflow-hidden transition-all duration-500
            flex flex-col items-center text-center
            ${currentTheme.bg} ${currentTheme.text}
          `}
        >
          {/* Decorative Borders/Frames */}
          <div className={`absolute inset-4 border-2 opacity-40 pointer-events-none ${currentTheme.border}`}></div>
          <div className={`absolute inset-6 border opacity-20 pointer-events-none ${currentTheme.border}`}></div>
          
          {/* Islamic Geometric Pattern Overlay */}
          <div className="absolute inset-0 opacity-10" style={{
             backgroundImage: `url("data:image/svg+xml,%3Csvg width='60' height='60' viewBox='0 0 60 60' xmlns='http://www.w3.org/2000/svg'%3E%3Cg fill='none' fill-rule='evenodd'%3E%3Cg fill='%23ffffff' fill-opacity='1'%3E%3Cpath d='M36 34v-4h-2v4h-4v2h4v4h2v-4h4v-2h-4zm0-30V0h-2v4h-4v2h4v4h2V6h4V4h-4zM6 34v-4H4v4H0v2h4v4h2v-4h4v-2H6zM6 4V0H4v4H0v2h4v4h2V6h4V4H6z'/%3E%3C/g%3E%3C/g%3E%3C/svg%3E")`
          }}></div>

          {/* Top Decoration */}
          <div className="mt-12 mb-6 relative z-10 animate-fade-in-down">
            {selectedIcon === 'moon' && <CloudMoon className={`w-24 h-24 ${currentTheme.accent} drop-shadow-lg`} />}
            {selectedIcon === 'lantern' && <LanternIcon className={`w-24 h-24 ${currentTheme.accent} drop-shadow-lg`} />}
            {selectedIcon === 'mosque' && <MosqueIcon className={`w-24 h-24 ${currentTheme.accent} drop-shadow-lg`} />}
            
            {/* Sparkles around icon */}
            <Star className={`w-4 h-4 absolute -top-2 -right-4 ${currentTheme.text} opacity-60 animate-pulse`} />
            <Star className={`w-3 h-3 absolute top-10 -left-6 ${currentTheme.text} opacity-40 animate-pulse`} style={{animationDelay: '0.5s'}} />
          </div>

          {/* Content Container */}
          <div className="flex-1 flex flex-col items-center justify-center px-8 pb-12 w-full z-10">
            
            <h2 className={`text-lg md:text-xl tracking-[0.2em] uppercase mb-2 opacity-90 font-sans font-light`}>
              {content.subtitle}
            </h2>
            
            <h1 className={`text-4xl md:text-5xl font-bold mb-6 leading-tight ${currentTheme.accent}`} style={{ fontFamily: '"Amiri", serif' }}>
              {content.title}
            </h1>

            <div className="w-16 h-0.5 bg-current opacity-30 mb-6"></div>

            <p className={`text-sm md:text-base italic leading-relaxed max-w-xs mx-auto opacity-90 mb-8`} style={{ fontFamily: '"Playfair Display", serif' }}>
              "{content.quote}"
            </p>

            {/* Ornament Separator */}
            <div className="flex items-center gap-2 opacity-50 mb-auto">
               <span className={`h-px w-8 ${currentTheme.bg === 'bg-white' ? 'bg-slate-400' : 'bg-white'}`}></span>
               <Heart size={12} className="fill-current" />
               <span className={`h-px w-8 ${currentTheme.bg === 'bg-white' ? 'bg-slate-400' : 'bg-white'}`}></span>
            </div>
          </div>

          {/* Footer */}
          <div className="w-full p-6 bg-black/10 backdrop-blur-sm z-10 mt-auto">
            <p className="text-xs font-semibold uppercase tracking-wider opacity-80">
              {content.footer}
            </p>
          </div>

        </div>
        
        {/* Helper text */}
        <div className="absolute bottom-4 left-0 right-0 text-center text-slate-400 text-xs">
          Pratinjau mungkin sedikit berbeda dengan hasil unduhan
        </div>
      </div>
    </div>
  );
};

export default RamadhanPosterMaker;
