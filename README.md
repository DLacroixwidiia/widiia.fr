# widiia.fr
import React, { useState, useEffect, useRef } from 'react';
import { 
  MessageSquare, 
  TrendingUp, 
  Mail, 
  ShieldCheck, 
  Phone, 
  Mail as MailIcon, 
  Menu, 
  X, 
  ArrowRight,
  Zap,
  Cpu,
  Search,
  Code2,
  Rocket,
  ChevronDown,
  ExternalLink
} from 'lucide-react';

// --- Configuration des Agents ---
const AGENTS = [
  {
    id: 'sav',
    title: 'Agent SAV',
    icon: <MessageSquare className="w-8 h-8" />,
    description: "L'IA qui transforme chaque plainte en une expérience client mémorable.",
    details: "Nos agents SAV gèrent les réclamations, répondent aux questions fréquentes et escaladent les problèmes complexes. Réduction des coûts de support de 60%."
  },
  {
    id: 'prospection',
    title: 'Agent de Prospection',
    icon: <TrendingUp className="w-8 h-8" />,
    description: "Une machine de guerre commerciale qui chasse 24h/24 sans jamais se fatiguer.",
    details: "Analyse des bases de données, envoi de messages personnalisés et prise de rendez-vous avec les prospects qualifiés uniquement."
  },
  {
    id: 'commande-mail',
    title: 'Agent Commande Mail',
    icon: <Mail className="w-8 h-8" />,
    description: "L'automatisation ultime du back-office. Du mail au CRM en une seconde.",
    details: "Extraction automatique des données de commandes reçues par email et injection directe dans votre système de gestion sans aucune erreur humaine."
  }
];

const App = () => {
  const [currentPage, setCurrentPage] = useState('home');
  const [selectedAgent, setSelectedAgent] = useState(null);
  const [isMenuOpen, setIsMenuOpen] = useState(false);
  const [scrollY, setScrollY] = useState(0);

  useEffect(() => {
    const handleScroll = () => setScrollY(window.scrollY);
    window.addEventListener('scroll', handleScroll);
    return () => window.removeEventListener('scroll', handleScroll);
  }, []);

  const Logo = ({ className = "w-10 h-10" }) => (
    <div className={`${className} relative group`}>
      <div className="absolute inset-0 bg-blue-500 rounded-full blur-md opacity-0 group-hover:opacity-50 transition-opacity"></div>
      <img 
        src="image_986a0a.png" 
        alt="Widiia Logo" 
        className="w-full h-full object-contain relative z-10"
      />
    </div>
  );

  const Navbar = () => (
    <nav className={`fixed w-full z-[100] transition-all duration-500 ${scrollY > 50 ? 'py-4 bg-black/60 backdrop-blur-xl border-b border-white/10' : 'py-8 bg-transparent'}`}>
      <div className="max-w-7xl mx-auto px-6 flex justify-between items-center">
        <div className="flex items-center cursor-pointer group" onClick={() => setCurrentPage('home')}>
          <Logo className="w-12 h-12 mr-3" />
          <div className="flex flex-col">
            <span className="text-2xl font-black tracking-[0.2em] text-white leading-none">WIDIIA</span>
            <span className="text-[10px] tracking-[0.4em] text-blue-400 font-bold uppercase">Intelligence Artificielle</span>
          </div>
        </div>
        
        <div className="hidden md:flex space-x-12 items-center">
          {['home', 'agents', 'contact'].map((page) => (
            <button 
              key={page}
              onClick={() => setCurrentPage(page)} 
              className={`text-sm tracking-widest uppercase font-bold transition-all hover:text-blue-400 ${currentPage === page ? 'text-blue-400' : 'text-white/60'}`}
            >
              {page === 'home' ? 'Genesis' : page === 'agents' ? 'The Fleet' : 'Contact'}
            </button>
          ))}
          <button 
            onClick={() => setCurrentPage('contact')}
            className="px-8 py-3 bg-white text-black font-black text-xs tracking-widest uppercase rounded-full hover:bg-blue-500 hover:text-white transition-all transform hover:scale-110 active:scale-95 shadow-[0_0_30px_rgba(255,255,255,0.2)]"
          >
            Launch Project
          </button>
        </div>

        <button onClick={() => setIsMenuOpen(!isMenuOpen)} className="md:hidden text-white">
          {isMenuOpen ? <X size={32} /> : <Menu size={32} />}
        </button>
      </div>
    </nav>
  );

  const HomePage = () => (
    <div className="relative overflow-hidden bg-black">
      {/* Background FX */}
      <div className="fixed inset-0 z-0 overflow-hidden pointer-events-none">
        <div className="absolute top-[-10%] right-[-10%] w-[60vw] h-[60vw] bg-blue-600/20 rounded-full blur-[150px] animate-pulse"></div>
        <div className="absolute bottom-[-10%] left-[-10%] w-[50vw] h-[50vw] bg-pink-600/10 rounded-full blur-[150px] animate-pulse" style={{ animationDelay: '2s' }}></div>
        <div className="absolute inset-0 bg-[url('https://grainy-gradients.vercel.app/noise.svg')] opacity-20 brightness-50"></div>
      </div>

      {/* Hero Section */}
      <section className="relative min-h-screen flex items-center justify-center pt-20">
        <div className="max-w-7xl mx-auto px-6 z-10 grid lg:grid-cols-2 gap-12 items-center">
          <div className="order-2 lg:order-1">
            <div className="inline-flex items-center space-x-2 px-3 py-1 rounded-full border border-blue-500/30 bg-blue-500/10 text-blue-400 text-[10px] font-black tracking-widest uppercase mb-6">
              <span className="relative flex h-2 w-2">
                <span className="animate-ping absolute inline-flex h-full w-full rounded-full bg-blue-400 opacity-75"></span>
                <span className="relative inline-flex rounded-full h-2 w-2 bg-blue-500"></span>
              </span>
              <span>Agents Autonomes v4.0</span>
            </div>
            <h1 className="text-7xl md:text-9xl font-black text-white leading-none tracking-tighter mb-8">
              L'IA QUI <br />
              <span className="text-transparent bg-clip-text bg-gradient-to-r from-blue-400 via-white to-pink-400">EXECUTE.</span>
            </h1>
            <p className="text-xl text-white/50 max-w-lg mb-12 font-medium leading-relaxed">
              WIDIIA conçoit des agents intelligents qui ne se contentent pas de répondre. Ils pensent, agissent et automatisent votre croissance.
            </p>
            <div className="flex flex-wrap gap-6">
              <button 
                onClick={() => setCurrentPage('contact')}
                className="group relative px-12 py-6 bg-blue-600 text-white font-black text-lg tracking-widest uppercase rounded-2xl overflow-hidden shadow-[0_20px_50px_rgba(37,99,235,0.4)] transition-all hover:scale-105"
              >
                <div className="absolute inset-0 bg-white/20 translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-500 skew-x-12"></div>
                Démarrer
              </button>
            </div>
          </div>
          
          <div className="order-1 lg:order-2 flex justify-center relative">
            <div className="absolute inset-0 bg-blue-500/20 blur-[100px] animate-pulse"></div>
            <div className="relative w-full aspect-square max-w-md animate-float">
                <img 
                    src="image_986a0a.png" 
                    alt="Logo Core" 
                    className="w-full h-full object-contain filter drop-shadow-[0_0_50px_rgba(59,130,246,0.5)]" 
                />
                <div className="absolute inset-0 border-[20px] border-white/5 rounded-full border-t-blue-500 animate-spin-slow"></div>
            </div>
          </div>
        </div>

        <div className="absolute bottom-10 left-1/2 -translate-x-1/2 flex flex-col items-center animate-bounce opacity-40">
           <span className="text-[10px] font-black tracking-[0.5em] uppercase text-white mb-2">Scroll to discover</span>
           <ChevronDown className="text-white" />
        </div>
      </section>

      {/* The Master Process Section */}
      <section className="py-40 relative">
        <div className="max-w-7xl mx-auto px-6">
          <div className="flex flex-col md:flex-row justify-between items-end mb-24 gap-8">
            <div className="max-w-2xl">
              <h2 className="text-5xl md:text-7xl font-black text-white uppercase tracking-tighter leading-none mb-6">
                NOTRE <br /><span className="text-blue-500 italic">ARCHITECTURE</span>
              </h2>
              <p className="text-white/40 text-lg">De la donnée brute à l'intelligence autonome. Voici comment nous forgeons vos agents.</p>
            </div>
            <div className="text-right">
              <span className="text-8xl font-black text-white/5 outline-text">01-03</span>
            </div>
          </div>

          <div className="grid lg:grid-cols-2 gap-20 items-center">
            <div className="space-y-4">
              {[
                { step: "01", title: "Audit de Flux", desc: "Nous disséquons vos processus manuels pour trouver les failles optimisables par l'IA." },
                { step: "02", title: "Forge Cognitive", desc: "Entraînement de vos agents sur vos données propriétaires pour une précision absolue." },
                { step: "03", title: "Déploiement Orbital", desc: "Mise en ligne de vos agents connectés à votre écosystème (Slack, CRM, Mail)." }
              ].map((item, idx) => (
                <div key={idx} className="group p-8 rounded-[2rem] bg-white/5 border border-white/10 hover:bg-white/[0.08] hover:border-blue-500/50 transition-all duration-500 cursor-default">
                  <div className="flex items-start gap-6">
                    <span className="text-4xl font-black text-blue-500/20 group-hover:text-blue-500 transition-colors">{item.step}</span>
                    <div>
                      <h3 className="text-2xl font-black text-white mb-2 uppercase">{item.title}</h3>
                      <p className="text-white/40 leading-relaxed">{item.desc}</p>
                    </div>
                  </div>
                </div>
              ))}
            </div>

            <div className="relative group">
               <div className="absolute -inset-4 bg-gradient-to-r from-blue-600 to-pink-600 rounded-[3rem] opacity-20 blur-2xl group-hover:opacity-40 transition-opacity"></div>
               <div className="relative bg-slate-900 rounded-[3rem] border border-white/10 overflow-hidden shadow-2xl transform transition-transform duration-700 hover:rotate-2">
                 <img 
                   src="image_995e11.png" 
                   alt="Widiia System" 
                   className="w-full h-auto grayscale group-hover:grayscale-0 transition-all duration-700"
                 />
                 <div className="absolute inset-0 bg-gradient-to-t from-black/80 via-transparent to-transparent flex items-end p-12">
                    <div className="flex items-center space-x-4">
                       <div className="w-3 h-3 bg-green-500 rounded-full animate-pulse"></div>
                       <span className="text-xs font-black tracking-widest text-white uppercase">System Status: Optimized</span>
                    </div>
                 </div>
               </div>
            </div>
          </div>
        </div>
      </section>

      {/* Featured Agents Grid */}
      <section className="py-40 bg-white/5">
        <div className="max-w-7xl mx-auto px-6">
            <div className="text-center mb-32">
                <h2 className="text-6xl md:text-8xl font-black text-white uppercase tracking-tighter mb-4">The Fleet</h2>
                <div className="w-24 h-2 bg-blue-500 mx-auto"></div>
            </div>

            <div className="grid md:grid-cols-3 gap-8">
                {AGENTS.map((agent, i) => (
                    <div 
                        key={agent.id}
                        onClick={() => { setSelectedAgent(agent); setCurrentPage('agent-detail'); }}
                        className="group relative h-[500px] overflow-hidden rounded-[2.5rem] cursor-pointer bg-slate-900"
                    >
                        <div className="absolute inset-0 bg-gradient-to-b from-transparent to-black/90 z-10"></div>
                        <div className="absolute top-10 left-10 z-20 w-16 h-16 rounded-2xl bg-white/10 flex items-center justify-center text-white backdrop-blur-xl group-hover:bg-blue-600 transition-all duration-500">
                            {agent.icon}
                        </div>
                        <div className="absolute bottom-10 left-10 right-10 z-20">
                            <h3 className="text-3xl font-black text-white mb-4 uppercase leading-none">{agent.title}</h3>
                            <p className="text-white/50 mb-6 line-clamp-2">{agent.description}</p>
                            <div className="flex items-center text-xs font-black tracking-widest text-blue-400 group-hover:translate-x-2 transition-transform">
                                ANALYSER <ArrowRight size={16} className="ml-2" />
                            </div>
                        </div>
                    </div>
                ))}
            </div>
        </div>
      </section>
    </div>
  );

  const AgentDetailPage = () => (
    <div className="min-h-screen pt-40 pb-24 bg-black px-6">
      <div className="max-w-6xl mx-auto">
        <button 
          onClick={() => setCurrentPage('agents')}
          className="flex items-center text-xs font-black tracking-[0.3em] text-blue-400 uppercase mb-20 hover:text-white transition"
        >
          <ArrowRight className="rotate-180 mr-2" /> Catalogue
        </button>

        <div className="grid lg:grid-cols-2 gap-24">
          <div>
            <div className="inline-block p-6 bg-blue-600 rounded-3xl text-white mb-10 shadow-[0_20px_40px_rgba(37,99,235,0.4)]">
                {selectedAgent.icon}
            </div>
            <h1 className="text-6xl md:text-8xl font-black text-white uppercase tracking-tighter leading-none mb-12">
              {selectedAgent.title}
            </h1>
            <p className="text-2xl text-white/40 font-medium italic mb-12 leading-relaxed">
              "{selectedAgent.description}"
            </p>
            <div className="flex items-center gap-10 border-t border-white/10 pt-12">
               <div>
                  <span className="block text-[10px] font-black text-blue-500 uppercase tracking-widest mb-2">SLA</span>
                  <span className="text-white text-xl font-bold">99.9%</span>
               </div>
               <div>
                  <span className="block text-[10px] font-black text-blue-500 uppercase tracking-widest mb-2">LATENCY</span>
                  <span className="text-white text-xl font-bold">&lt; 1.5s</span>
               </div>
               <div>
                  <span className="block text-[10px] font-black text-blue-500 uppercase tracking-widest mb-2">TYPE</span>
                  <span className="text-white text-xl font-bold">Autonome</span>
               </div>
            </div>
          </div>

          <div className="bg-white/[0.03] backdrop-blur-2xl border border-white/10 rounded-[3rem] p-12 relative overflow-hidden">
             <div className="absolute top-0 right-0 w-64 h-64 bg-blue-500/10 blur-[80px]"></div>
             <h2 className="text-3xl font-black text-white mb-8 uppercase tracking-tighter">Capabilities</h2>
             <p className="text-white/60 text-lg leading-relaxed mb-12">
               {selectedAgent.details}
             </p>
             <ul className="space-y-6">
                {["Integration API Native", "Contextual Memory", "Zéro-shot Reasoning", "Multi-modal Support"].map((cap, i) => (
                    <li key={i} className="flex items-center text-white/80 font-bold uppercase tracking-widest text-xs">
                        <div className="w-2 h-2 bg-blue-500 rounded-full mr-4"></div> {cap}
                    </li>
                ))}
             </ul>
             <button 
               onClick={() => setCurrentPage('contact')}
               className="w-full mt-16 py-6 bg-white text-black font-black text-xl uppercase tracking-tighter rounded-2xl hover:bg-blue-600 hover:text-white transition-all shadow-[0_20px_40px_rgba(255,255,255,0.1)]"
             >
                Déployer maintenant
             </button>
          </div>
        </div>
      </div>
    </div>
  );

  const ContactPage = () => (
    <div className="min-h-screen pt-40 pb-24 bg-black px-6">
        <div className="max-w-7xl mx-auto grid lg:grid-cols-2 gap-24">
            <div>
                <h1 className="text-7xl md:text-9xl font-black text-white uppercase tracking-tighter leading-none mb-12">
                    START THE <br /><span className="text-blue-500 italic">UPGRADE.</span>
                </h1>
                <p className="text-xl text-white/40 max-w-md mb-16 font-medium">L'avenir de votre entreprise commence par un simple message.</p>
                
                <div className="space-y-8">
                    <div className="group">
                        <span className="text-[10px] font-black text-blue-500 uppercase tracking-widest block mb-2">Send Intel</span>
                        <p className="text-2xl text-white font-black group-hover:text-blue-400 transition-colors">agence@widiia.fr</p>
                    </div>
                    <div className="group">
                        <span className="text-[10px] font-black text-blue-500 uppercase tracking-widest block mb-2">Direct Line</span>
                        <p className="text-2xl text-white font-black group-hover:text-blue-400 transition-colors">07 67 94 07 89</p>
                    </div>
                </div>
            </div>

            <div className="bg-slate-950 p-12 rounded-[4rem] border border-white/10 shadow-3xl shadow-blue-500/5">
                <form className="space-y-10" onSubmit={e => e.preventDefault()}>
                    <div className="space-y-6">
                        <input type="text" className="w-full bg-transparent border-b border-white/20 py-4 text-2xl font-black text-white placeholder:text-white/10 outline-none focus:border-blue-500 transition-all" placeholder="VOTRE NOM" />
                        <input type="email" className="w-full bg-transparent border-b border-white/20 py-4 text-2xl font-black text-white placeholder:text-white/10 outline-none focus:border-blue-500 transition-all" placeholder="VOTRE EMAIL" />
                        <textarea className="w-full bg-transparent border-b border-white/20 py-4 text-2xl font-black text-white placeholder:text-white/10 outline-none focus:border-blue-500 transition-all resize-none" placeholder="VOTRE PROJET" rows="2"></textarea>
                    </div>
                    <button className="px-12 py-6 bg-blue-600 text-white font-black text-xl uppercase tracking-widest rounded-full hover:scale-105 active:scale-95 transition-all shadow-[0_20px_40px_rgba(37,99,235,0.3)]">
                        Transmettre le briefing
                    </button>
                </form>
            </div>
        </div>
    </div>
  );

  const Footer = () => (
    <footer className="bg-black border-t border-white/10 py-24 px-6 overflow-hidden relative">
      <div className="max-w-7xl mx-auto flex flex-col items-center relative z-10">
        <Logo className="w-24 h-24 mb-12 opacity-40 grayscale" />
        <div className="flex flex-wrap justify-center gap-12 mb-20">
           {['Genesis', 'The Fleet', 'Contact'].map(item => (
               <button key={item} className="text-xs font-black tracking-[0.5em] uppercase text-white/40 hover:text-white transition">
                   {item}
               </button>
           ))}
        </div>
        <div className="text-center">
            <p className="text-[10px] font-black tracking-[1em] text-white/20 uppercase mb-4">© 2024 WIDIIA STUDIO</p>
            <p className="text-xs text-blue-500/40 font-bold uppercase tracking-widest italic">Crafting Autonomous Intelligence</p>
        </div>
      </div>
      <div className="absolute bottom-[-10rem] left-1/2 -translate-x-1/2 text-[15rem] font-black text-white/[0.02] whitespace-nowrap pointer-events-none select-none">
          WIDIIA NEXT GEN
      </div>
    </footer>
  );

  return (
    <div className="min-h-screen bg-black text-white selection:bg-blue-500 selection:text-white">
      <Navbar />
      <main>
        {currentPage === 'home' && <HomePage />}
        {currentPage === 'agents' && <HomePage />} {/* Redirige vers home ou scroll si besoin */}
        {currentPage === 'agent-detail' && <AgentDetailPage />}
        {currentPage === 'contact' && <ContactPage />}
      </main>
      <Footer />

      <style dangerouslySetInnerHTML={{ __html: `
        @import url('https://fonts.googleapis.com/css2?family=Syncopate:wght@400;700&family=Space+Grotesk:wght@300;400;500;600;700&display=swap');
        
        body { 
          font-family: 'Space Grotesk', sans-serif;
          background: #000;
        }
        
        h1, h2, h3, .font-black {
          font-family: 'Syncopate', sans-serif;
        }

        .outline-text {
          -webkit-text-stroke: 1px rgba(255,255,255,0.1);
        }

        @keyframes float {
          0%, 100% { transform: translateY(0); }
          50% { transform: translateY(-30px); }
        }
        .animate-float {
          animation: float 6s ease-in-out infinite;
        }

        @keyframes spin-slow {
          from { transform: rotate(0deg); }
          to { transform: rotate(360deg); }
        }
        .animate-spin-slow {
          animation: spin-slow 20s linear infinite;
        }

        ::-webkit-scrollbar {
          width: 5px;
        }
        ::-webkit-scrollbar-track {
          background: #000;
        }
        ::-webkit-scrollbar-thumb {
          background: #1e40af;
          border-radius: 10px;
        }
      `}} />
    </div>
  );
};

export default App;
