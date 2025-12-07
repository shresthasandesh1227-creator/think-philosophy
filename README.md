<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Think Philosophy</title>
    
    <!-- Google Fonts -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Nunito:wght@300;400;600;700;800&display=swap" rel="stylesheet">
    
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Lucide Icons -->
    <script src="https://unpkg.com/lucide@latest"></script>

    <!-- Tailwind Config for Custom Fonts/Colors -->
    <script>
        tailwind.config = {
            darkMode: 'class',
            theme: {
                extend: {
                    fontFamily: {
                        sans: ['Nunito', 'sans-serif'],
                        serif: ['Nunito', 'sans-serif'],
                        display: ['Nunito', 'sans-serif'],
                    },
                    colors: {
                        brand: {
                            50: '#f4f6f8',
                            100: '#e4e7eb',
                            200: '#c5ced6',
                            300: '#a6b5c1',
                            400: '#688398',
                            500: '#2a526f',
                            600: '#264a64',
                            700: '#1f3d53',
                            800: '#193142',
                            900: '#152836', // Deep Slate
                            950: '#0b141b', // Almost Black
                        },
                        gold: {
                            400: '#d4af37',
                            500: '#c5a028',
                        }
                    },
                    animation: {
                        'float': 'float 6s ease-in-out infinite',
                    },
                    keyframes: {
                        float: {
                            '0%, 100%': { transform: 'translateY(0)' },
                            '50%': { transform: 'translateY(-10px)' },
                        }
                    }
                }
            }
        }
    </script>

    <style>
        /* Custom Scrollbar */
        ::-webkit-scrollbar {
            width: 8px;
        }
        ::-webkit-scrollbar-track {
            background: #0b141b; 
        }
        ::-webkit-scrollbar-thumb {
            background: #2a526f; 
            border-radius: 4px;
        }
        ::-webkit-scrollbar-thumb:hover {
            background: #d4af37; 
        }

        /* Gradient Text Utility */
        .text-gradient {
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-image: linear-gradient(to right, #e2e8f0, #94a3b8);
        }
        
        .gold-gradient {
            background-clip: text;
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-image: linear-gradient(to right, #fcd34d, #d4af37, #b45309);
        }

        /* Canvas styling */
        #constellation-canvas {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: 0;
            opacity: 0.4;
            pointer-events: none;
        }

        /* Chat Animations */
        @keyframes message-in {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .message-bubble {
            animation: message-in 0.3s ease-out forwards;
        }
        .typing-dot {
            animation: typing 1.4s infinite ease-in-out both;
        }
        .typing-dot:nth-child(1) { animation-delay: -0.32s; }
        .typing-dot:nth-child(2) { animation-delay: -0.16s; }
        @keyframes typing {
            0%, 80%, 100% { transform: scale(0); }
            40% { transform: scale(1); }
        }
    </style>
</head>
<body class="bg-brand-950 text-slate-300 font-sans antialiased overflow-x-hidden selection:bg-gold-500 selection:text-white">

    <!-- Navigation -->
    <nav class="fixed w-full z-50 transition-all duration-300 bg-brand-950/80 backdrop-blur-md border-b border-white/5" id="navbar">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
            <div class="flex items-center justify-between h-20">
                <div class="flex items-center gap-2 group cursor-pointer" onclick="window.scrollTo(0,0)">
                    <i data-lucide="brain-circuit" class="w-8 h-8 text-gold-400 group-hover:rotate-12 transition-transform duration-500"></i>
                    <span class="font-display font-bold text-xl tracking-wider text-white">Think <span class="text-gold-400">Philosophy</span></span>
                </div>
                
                <!-- Desktop Menu -->
                <div class="hidden md:block">
                    <div class="ml-10 flex items-baseline space-x-8">
                        <a href="#branches" class="hover:text-gold-400 px-3 py-2 rounded-md text-sm font-medium transition-colors">Branches</a>
                        <a href="#philosophers" class="hover:text-gold-400 px-3 py-2 rounded-md text-sm font-medium transition-colors">Great Minds</a>
                        <a href="#ai-chat" class="hover:text-gold-400 px-3 py-2 rounded-md text-sm font-medium transition-colors text-gold-400">AI Chat</a>
                        <a href="#articles" class="hover:text-gold-400 px-3 py-2 rounded-md text-sm font-medium transition-colors">Articles</a>
                    </div>
                </div>

                <!-- Mobile menu button -->
                <div class="md:hidden">
                    <button id="mobile-menu-btn" class="text-gray-300 hover:text-white focus:outline-none">
                        <i data-lucide="menu" class="w-6 h-6"></i>
                    </button>
                </div>
            </div>
        </div>

        <!-- Mobile Menu Panel -->
        <div id="mobile-menu" class="hidden md:hidden bg-brand-900 border-b border-white/10">
            <div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
                <a href="#branches" class="text-gray-300 hover:text-gold-400 block px-3 py-2 rounded-md text-base font-medium">Branches</a>
                <a href="#philosophers" class="text-gray-300 hover:text-gold-400 block px-3 py-2 rounded-md text-base font-medium">Great Minds</a>
                <a href="#ai-chat" class="text-gold-400 hover:text-gold-300 block px-3 py-2 rounded-md text-base font-medium">AI Chat</a>
                <a href="#articles" class="text-gray-300 hover:text-gold-400 block px-3 py-2 rounded-md text-base font-medium">Articles</a>
            </div>
        </div>
    </nav>

    <!-- Hero Section -->
    <section class="relative h-screen flex items-center justify-center overflow-hidden">
        <!-- Canvas Background -->
        <canvas id="constellation-canvas"></canvas>
        
        <div class="absolute inset-0 bg-gradient-to-b from-transparent via-brand-950/50 to-brand-950 z-10"></div>

        <div class="relative z-20 text-center px-4 max-w-4xl mx-auto animate-float">
            <div class="inline-block mb-4 px-4 py-1 rounded-full bg-gold-500/10 border border-gold-500/30 backdrop-blur-sm">
                <span class="text-gold-400 text-xs font-display tracking-[0.2em] uppercase">Sapere Aude</span>
            </div>
            <h1 class="text-5xl md:text-7xl font-display font-bold mb-6 leading-tight">
                The Unexamined Life <br>
                <span class="gold-gradient italic font-serif">Is Not Worth Living</span>
            </h1>
            <p class="text-lg md:text-xl text-slate-400 mb-10 max-w-2xl mx-auto font-light">
                Explore the fundamental nature of knowledge, reality, and existence. Join a community of thinkers seeking wisdom in the modern age.
            </p>
            <div class="flex flex-col sm:flex-row gap-4 justify-center">
                <button onclick="document.getElementById('ai-chat').scrollIntoView({behavior: 'smooth'})" class="px-8 py-4 bg-gold-500 hover:bg-gold-400 text-brand-950 font-bold rounded-sm transition-all shadow-[0_0_20px_rgba(212,175,55,0.3)] hover:shadow-[0_0_30px_rgba(212,175,55,0.5)] flex items-center justify-center gap-2 group">
                    Chat with AI
                    <i data-lucide="message-square" class="w-4 h-4 group-hover:translate-x-1 transition-transform"></i>
                </button>
                <button onclick="document.getElementById('articles').scrollIntoView({behavior: 'smooth'})" class="px-8 py-4 bg-transparent border border-white/20 hover:bg-white/5 text-white font-semibold rounded-sm transition-all backdrop-blur-sm">
                    Write Article
                </button>
            </div>
        </div>
    </section>

    <!-- AI Chat Section -->
    <section id="ai-chat" class="py-24 px-4 bg-brand-900 border-y border-white/5 relative">
        <div class="max-w-7xl mx-auto">
            <div class="text-center mb-12">
                <span class="text-gold-400 text-sm font-bold tracking-widest uppercase">Dialectic Engine</span>
                <h2 class="text-4xl md:text-5xl font-display font-bold text-white mt-2 mb-4">Converse with the Masters</h2>
                <p class="text-slate-400 max-w-2xl mx-auto">Select a philosopher and ask them about life, the universe, or your daily struggles.</p>
            </div>

            <div class="flex flex-col lg:flex-row h-[600px] bg-brand-950 border border-white/10 rounded-2xl overflow-hidden shadow-2xl">
                <!-- Sidebar -->
                <div class="lg:w-1/4 bg-brand-900 border-r border-white/5 p-4 flex flex-col">
                    <h3 class="text-white font-bold mb-4 px-2">Philosophers</h3>
                    <div class="space-y-2 overflow-y-auto flex-1 custom-scrollbar">
                        <button onclick="selectPhilosopher('socrates')" id="btn-socrates" class="w-full text-left p-3 rounded-lg hover:bg-white/5 transition-colors flex items-center gap-3 border border-transparent hover:border-white/10 active-philosopher bg-white/10 border-gold-500/30">
                            <div class="w-10 h-10 rounded-full bg-slate-700 overflow-hidden">
                                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/bc/Socrate_du_Louvre.jpg/100px-Socrate_du_Louvre.jpg" class="w-full h-full object-cover">
                            </div>
                            <div>
                                <div class="font-bold text-white">Socrates</div>
                                <div class="text-xs text-slate-400">The Gadfly</div>
                            </div>
                        </button>
                        
                        <button onclick="selectPhilosopher('nietzsche')" id="btn-nietzsche" class="w-full text-left p-3 rounded-lg hover:bg-white/5 transition-colors flex items-center gap-3 border border-transparent hover:border-white/10">
                            <div class="w-10 h-10 rounded-full bg-slate-700 overflow-hidden">
                                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Nietzsche187a.jpg/100px-Nietzsche187a.jpg" class="w-full h-full object-cover">
                            </div>
                            <div>
                                <div class="font-bold text-white">Nietzsche</div>
                                <div class="text-xs text-slate-400">The Iconoclast</div>
                            </div>
                        </button>

                        <button onclick="selectPhilosopher('aurelius')" id="btn-aurelius" class="w-full text-left p-3 rounded-lg hover:bg-white/5 transition-colors flex items-center gap-3 border border-transparent hover:border-white/10">
                            <div class="w-10 h-10 rounded-full bg-slate-700 overflow-hidden">
                                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/b8/Marcus_Aurelius_Glyptothek_Munich_Inv267.jpg/100px-Marcus_Aurelius_Glyptothek_Munich_Inv267.jpg" class="w-full h-full object-cover">
                            </div>
                            <div>
                                <div class="font-bold text-white">Marcus Aurelius</div>
                                <div class="text-xs text-slate-400">The Emperor</div>
                            </div>
                        </button>

                         <button onclick="selectPhilosopher('aristotle')" id="btn-aristotle" class="w-full text-left p-3 rounded-lg hover:bg-white/5 transition-colors flex items-center gap-3 border border-transparent hover:border-white/10">
                            <div class="w-10 h-10 rounded-full bg-slate-700 overflow-hidden">
                                <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Aristotle_Altemps_Inv8575.jpg/100px-Aristotle_Altemps_Inv8575.jpg" class="w-full h-full object-cover">
                            </div>
                            <div>
                                <div class="font-bold text-white">Aristotle</div>
                                <div class="text-xs text-slate-400">The Polymath</div>
                            </div>
                        </button>
                    </div>
                    
                    <!-- API Key Settings -->
                    <div class="pt-4 border-t border-white/10 mt-2">
                        <button onclick="toggleSettings()" class="flex items-center gap-2 text-xs text-slate-500 hover:text-gold-400 transition-colors w-full">
                            <i data-lucide="settings" class="w-3 h-3"></i> Configure API Key
                        </button>
                        <div id="api-settings" class="hidden mt-2 p-2 bg-black/20 rounded">
                            <input type="password" id="gemini-key-input" placeholder="Paste Gemini API Key" class="w-full bg-transparent border border-white/10 rounded px-2 py-1 text-xs text-white mb-2">
                            <button onclick="saveApiKey()" class="w-full bg-gold-500/20 text-gold-400 text-xs py-1 rounded hover:bg-gold-500/30">Save Key</button>
                        </div>
                    </div>
                </div>

                <!-- Chat Area -->
                <div class="lg:w-3/4 flex flex-col bg-brand-950 relative">
                    <!-- Chat Header -->
                    <div class="p-4 border-b border-white/5 flex items-center justify-between bg-brand-950/50 backdrop-blur">
                        <div class="flex items-center gap-3">
                            <div class="w-2 h-2 rounded-full bg-green-500 animate-pulse"></div>
                            <span class="text-white font-bold" id="chat-header-name">Socrates</span>
                        </div>
                        <button onclick="clearChat()" class="text-slate-500 hover:text-white" title="Clear Chat">
                            <i data-lucide="trash-2" class="w-4 h-4"></i>
                        </button>
                    </div>

                    <!-- Messages -->
                    <div id="chat-messages" class="flex-1 p-6 overflow-y-auto space-y-4 custom-scrollbar bg-[url('https://www.transparenttextures.com/patterns/stardust.png')]">
                        <!-- Intro Message -->
                        <div class="flex justify-start message-bubble">
                            <div class="bg-brand-800 text-slate-200 p-4 rounded-2xl rounded-tl-none max-w-[80%] border border-white/5">
                                <p>Greetings. I am Socrates. I know only one thing: that I know nothing. What is it that creates turmoil in your mind today?</p>
                            </div>
                        </div>
                    </div>

                    <!-- Input Area -->
                    <div class="p-4 bg-brand-900 border-t border-white/5">
                        <form id="chat-form" class="flex gap-2 relative">
                            <input type="text" id="chat-input" class="flex-1 bg-brand-950 border border-white/10 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-gold-500 transition-colors" placeholder="Ask a question..." autocomplete="off">
                            <button type="submit" class="bg-gold-500 hover:bg-gold-400 text-brand-950 font-bold px-6 rounded-lg transition-colors disabled:opacity-50 disabled:cursor-not-allowed" id="send-btn">
                                <i data-lucide="send" class="w-5 h-5"></i>
                            </button>
                        </form>
                        <p class="text-[10px] text-slate-600 mt-2 text-center">AI generated responses can be inaccurate. Logic implies verification.</p>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Interactive Quote Generator -->
    <section id="generator" class="py-24 bg-brand-900 border-y border-white/5 relative overflow-hidden">
        <div class="absolute top-0 right-0 p-12 opacity-5">
            <i data-lucide="quote" class="w-64 h-64 text-white"></i>
        </div>
        
        <div class="max-w-4xl mx-auto px-4 relative z-10">
            <div class="text-center mb-12">
                <h2 class="text-3xl font-display font-bold text-white mb-4">Wisdom Generator</h2>
                <p class="text-slate-400">Click the button to receive a random philosophical insight.</p>
            </div>

            <div class="bg-brand-950 border border-white/10 rounded-xl p-8 md:p-12 text-center shadow-2xl relative">
                <div class="absolute -top-4 -left-4 w-8 h-8 border-t-2 border-l-2 border-gold-500"></div>
                <div class="absolute -bottom-4 -right-4 w-8 h-8 border-b-2 border-r-2 border-gold-500"></div>
                
                <div id="quote-display" class="min-h-[120px] flex flex-col justify-center items-center">
                    <p class="text-2xl md:text-3xl font-serif italic text-white mb-6 leading-relaxed transition-opacity duration-500" id="quote-text">
                        "We suffer more often in imagination than in reality."
                    </p>
                    <cite class="text-gold-400 font-display tracking-widest text-sm uppercase not-italic block transition-opacity duration-500" id="quote-author">
                        — Seneca
                    </cite>
                </div>

                <div class="mt-10 flex justify-center gap-4">
                    <button id="new-quote-btn" class="flex items-center gap-2 px-6 py-3 bg-white/10 hover:bg-white/20 text-white rounded-lg transition-colors border border-white/5">
                        <i data-lucide="refresh-cw" class="w-4 h-4"></i>
                        Generate New
                    </button>
                    <button id="copy-quote-btn" class="flex items-center gap-2 px-6 py-3 bg-transparent hover:bg-white/5 text-slate-400 hover:text-white rounded-lg transition-colors border border-white/10">
                        <i data-lucide="copy" class="w-4 h-4"></i>
                        Copy
                    </button>
                </div>
            </div>
        </div>
    </section>

    <!-- Branches of Philosophy -->
    <section id="branches" class="py-24 px-4 max-w-7xl mx-auto">
        <div class="text-center mb-16">
            <span class="text-gold-400 text-sm font-bold tracking-widest uppercase">The Structure of Thought</span>
            <h2 class="text-4xl md:text-5xl font-display font-bold text-white mt-2 mb-6">Branches of Philosophy</h2>
            <div class="w-24 h-1 bg-gold-500 mx-auto"></div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Card 1 -->
            <div class="group relative bg-brand-900 border border-white/5 p-8 rounded-lg hover:-translate-y-2 transition-transform duration-300 hover:border-gold-500/30 overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-gold-500/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="relative z-10">
                    <div class="w-12 h-12 bg-brand-800 rounded-lg flex items-center justify-center mb-6 group-hover:bg-gold-500 group-hover:text-brand-950 transition-colors">
                        <i data-lucide="globe-2" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-2xl font-display font-bold text-white mb-3">Metaphysics</h3>
                    <p class="text-slate-400 leading-relaxed mb-4">The study of the fundamental nature of reality, existence, and the relationship between mind and matter.</p>
                    <ul class="text-sm text-slate-500 space-y-1">
                        <li>• Ontology (Being)</li>
                        <li>• Cosmology (Universe)</li>
                        <li>• Identity & Change</li>
                    </ul>
                </div>
            </div>

            <!-- Card 2 -->
            <div class="group relative bg-brand-900 border border-white/5 p-8 rounded-lg hover:-translate-y-2 transition-transform duration-300 hover:border-gold-500/30 overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-gold-500/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="relative z-10">
                    <div class="w-12 h-12 bg-brand-800 rounded-lg flex items-center justify-center mb-6 group-hover:bg-gold-500 group-hover:text-brand-950 transition-colors">
                        <i data-lucide="scale" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-2xl font-display font-bold text-white mb-3">Ethics</h3>
                    <p class="text-slate-400 leading-relaxed mb-4">Moral philosophy that involves systematizing, defending, and recommending concepts of right and wrong conduct.</p>
                    <ul class="text-sm text-slate-500 space-y-1">
                        <li>• Utilitarianism</li>
                        <li>• Deontology</li>
                        <li>• Virtue Ethics</li>
                    </ul>
                </div>
            </div>

            <!-- Card 3 -->
            <div class="group relative bg-brand-900 border border-white/5 p-8 rounded-lg hover:-translate-y-2 transition-transform duration-300 hover:border-gold-500/30 overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-gold-500/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="relative z-10">
                    <div class="w-12 h-12 bg-brand-800 rounded-lg flex items-center justify-center mb-6 group-hover:bg-gold-500 group-hover:text-brand-950 transition-colors">
                        <i data-lucide="brain" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-2xl font-display font-bold text-white mb-3">Epistemology</h3>
                    <p class="text-slate-400 leading-relaxed mb-4">The theory of knowledge, especially with regard to its methods, validity, and scope.</p>
                    <ul class="text-sm text-slate-500 space-y-1">
                        <li>• What is knowledge?</li>
                        <li>• How is it acquired?</li>
                        <li>• Skepticism vs. Belief</li>
                    </ul>
                </div>
            </div>
            
             <!-- Card 4 -->
             <div class="group relative bg-brand-900 border border-white/5 p-8 rounded-lg hover:-translate-y-2 transition-transform duration-300 hover:border-gold-500/30 overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-gold-500/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="relative z-10">
                    <div class="w-12 h-12 bg-brand-800 rounded-lg flex items-center justify-center mb-6 group-hover:bg-gold-500 group-hover:text-brand-950 transition-colors">
                        <i data-lucide="binary" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-2xl font-display font-bold text-white mb-3">Logic</h3>
                    <p class="text-slate-400 leading-relaxed mb-4">The study of correct reasoning. It provides the rules for valid inferences and argumentation.</p>
                    <ul class="text-sm text-slate-500 space-y-1">
                        <li>• Deductive Reasoning</li>
                        <li>• Inductive Reasoning</li>
                        <li>• Fallacies</li>
                    </ul>
                </div>
            </div>

            <!-- Card 5 -->
            <div class="group relative bg-brand-900 border border-white/5 p-8 rounded-lg hover:-translate-y-2 transition-transform duration-300 hover:border-gold-500/30 overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-gold-500/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="relative z-10">
                    <div class="w-12 h-12 bg-brand-800 rounded-lg flex items-center justify-center mb-6 group-hover:bg-gold-500 group-hover:text-brand-950 transition-colors">
                        <i data-lucide="palette" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-2xl font-display font-bold text-white mb-3">Aesthetics</h3>
                    <p class="text-slate-400 leading-relaxed mb-4">The study of beauty and taste, as well as the philosophy of art.</p>
                    <ul class="text-sm text-slate-500 space-y-1">
                        <li>• Nature of Beauty</li>
                        <li>• Art Interpretation</li>
                        <li>• Sublime vs Beautiful</li>
                    </ul>
                </div>
            </div>

            <!-- Card 6 -->
            <div class="group relative bg-brand-900 border border-white/5 p-8 rounded-lg hover:-translate-y-2 transition-transform duration-300 hover:border-gold-500/30 overflow-hidden">
                <div class="absolute inset-0 bg-gradient-to-br from-gold-500/5 to-transparent opacity-0 group-hover:opacity-100 transition-opacity"></div>
                <div class="relative z-10">
                    <div class="w-12 h-12 bg-brand-800 rounded-lg flex items-center justify-center mb-6 group-hover:bg-gold-500 group-hover:text-brand-950 transition-colors">
                        <i data-lucide="users" class="w-6 h-6"></i>
                    </div>
                    <h3 class="text-2xl font-display font-bold text-white mb-3">Political</h3>
                    <p class="text-slate-400 leading-relaxed mb-4">The study of government, addressing questions about the nature, scope, and legitimacy of public agents and institutions.</p>
                    <ul class="text-sm text-slate-500 space-y-1">
                        <li>• Justice & Rights</li>
                        <li>• Liberty</li>
                        <li>• Social Contract</li>
                    </ul>
                </div>
            </div>
        </div>
    </section>

    <!-- Great Minds (Timeline/Highlights) -->
    <section id="philosophers" class="py-24 bg-brand-900 border-y border-white/5">
        <div class="max-w-7xl mx-auto px-4">
            <div class="flex flex-col md:flex-row justify-between items-end mb-16 gap-6">
                <div>
                    <span class="text-gold-400 text-sm font-bold tracking-widest uppercase">The Giants</span>
                    <h2 class="text-4xl font-display font-bold text-white mt-2">Architects of Thought</h2>
                </div>
                <a href="#" class="text-slate-400 hover:text-white flex items-center gap-2 text-sm border-b border-transparent hover:border-white transition-all pb-1">
                    View Complete Timeline <i data-lucide="arrow-right" class="w-4 h-4"></i>
                </a>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
                <!-- Philosopher 1: Socrates -->
                <div class="bg-brand-950 p-6 rounded-lg border border-white/5 hover:border-gold-500/50 transition-all group">
                    <div class="mb-4 overflow-hidden rounded-md h-48 bg-slate-800 relative group">
                        <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/b/bc/Socrate_du_Louvre.jpg/480px-Socrate_du_Louvre.jpg" alt="Socrates" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-110 transition-all duration-500">
                        <div class="absolute bottom-0 left-0 w-full p-4 bg-gradient-to-t from-black/90 to-transparent">
                            <span class="text-white font-bold">Socrates</span>
                        </div>
                    </div>
                    <p class="text-xs text-gold-400 uppercase tracking-wider mb-2">470–399 BC • Athens</p>
                    <p class="text-slate-400 text-sm mb-4">The founder of Western moral philosophy. Known for the Socratic method and his trial.</p>
                    <div class="flex flex-wrap gap-2">
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Ethics</span>
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Epistemology</span>
                    </div>
                </div>

                <!-- Philosopher 2: Aristotle -->
                <div class="bg-brand-950 p-6 rounded-lg border border-white/5 hover:border-gold-500/50 transition-all group">
                    <div class="mb-4 overflow-hidden rounded-md h-48 bg-slate-800 relative group">
                         <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/ae/Aristotle_Altemps_Inv8575.jpg/480px-Aristotle_Altemps_Inv8575.jpg" alt="Aristotle" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-110 transition-all duration-500">
                         <div class="absolute bottom-0 left-0 w-full p-4 bg-gradient-to-t from-black/90 to-transparent">
                            <span class="text-white font-bold">Aristotle</span>
                        </div>
                    </div>
                    <p class="text-xs text-gold-400 uppercase tracking-wider mb-2">384–322 BC • Stagira</p>
                    <p class="text-slate-400 text-sm mb-4">A polymath who laid the groundwork for logic, biology, and ethics.</p>
                    <div class="flex flex-wrap gap-2">
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Logic</span>
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Science</span>
                    </div>
                </div>

                <!-- Philosopher 3: Kant -->
                <div class="bg-brand-950 p-6 rounded-lg border border-white/5 hover:border-gold-500/50 transition-all group">
                    <div class="mb-4 overflow-hidden rounded-md h-48 bg-slate-800 relative group">
                         <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/f2/Kant_gemaelde_3.jpg/480px-Kant_gemaelde_3.jpg" alt="Immanuel Kant" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-110 transition-all duration-500">
                         <div class="absolute bottom-0 left-0 w-full p-4 bg-gradient-to-t from-black/90 to-transparent">
                            <span class="text-white font-bold">Immanuel Kant</span>
                        </div>
                    </div>
                    <p class="text-xs text-gold-400 uppercase tracking-wider mb-2">1724–1804 • Prussia</p>
                    <p class="text-slate-400 text-sm mb-4">Synthesized rationalism and empiricism. Known for the Categorical Imperative.</p>
                    <div class="flex flex-wrap gap-2">
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Metaphysics</span>
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Ethics</span>
                    </div>
                </div>

                <!-- Philosopher 4: Nietzsche -->
                <div class="bg-brand-950 p-6 rounded-lg border border-white/5 hover:border-gold-500/50 transition-all group">
                    <div class="mb-4 overflow-hidden rounded-md h-48 bg-slate-800 relative group">
                         <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/1/1b/Nietzsche187a.jpg/480px-Nietzsche187a.jpg" alt="Friedrich Nietzsche" class="w-full h-full object-cover opacity-80 group-hover:opacity-100 group-hover:scale-110 transition-all duration-500">
                         <div class="absolute bottom-0 left-0 w-full p-4 bg-gradient-to-t from-black/90 to-transparent">
                            <span class="text-white font-bold">F. Nietzsche</span>
                        </div>
                    </div>
                    <p class="text-xs text-gold-400 uppercase tracking-wider mb-2">1844–1900 • Germany</p>
                    <p class="text-slate-400 text-sm mb-4">Challenged Christian morality and introduced the concept of the Übermensch.</p>
                    <div class="flex flex-wrap gap-2">
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Existentialism</span>
                        <span class="px-2 py-1 bg-white/5 rounded text-xs text-slate-300">Nihilism</span>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Community Articles Section (NEW) -->
    <section id="articles" class="py-24 px-4 max-w-7xl mx-auto">
        <div class="flex flex-col md:flex-row justify-between items-start md:items-end mb-12 gap-4">
            <div>
                <span class="text-gold-400 text-sm font-bold tracking-widest uppercase">The Agora</span>
                <h2 class="text-4xl font-display font-bold text-white mt-2">Community Articles</h2>
            </div>
            <div class="flex bg-brand-900 p-1 rounded-lg border border-white/10">
                <button onclick="switchTab('read')" id="tab-read" class="px-6 py-2 rounded-md text-sm font-bold bg-brand-700 text-white shadow-sm transition-all">Read</button>
                <button onclick="switchTab('write')" id="tab-write" class="px-6 py-2 rounded-md text-sm font-bold text-slate-400 hover:text-white transition-all">Write</button>
            </div>
        </div>

        <!-- Read Mode -->
        <div id="read-view" class="grid grid-cols-1 md:grid-cols-2 gap-8 transition-opacity duration-300">
            <!-- 
                HARDCODED ARTICLES (Permanent for everyone)
                To add a permanent article, copy/paste this <article> block below.
            -->
            
            <!-- Featured Article -->
            <article class="bg-brand-900 border border-white/5 rounded-xl p-8 hover:border-gold-500/30 transition-all group">
                <div class="flex items-center gap-3 mb-6">
                    <div class="w-10 h-10 rounded-full bg-gold-500/20 flex items-center justify-center text-gold-400 font-bold">JD</div>
                    <div>
                        <p class="text-white text-sm font-bold">John Doe</p>
                        <p class="text-slate-500 text-xs">2 hours ago</p>
                    </div>
                </div>
                <h3 class="text-2xl font-bold text-white mb-3 group-hover:text-gold-400 transition-colors">Modern Stoicism in Tech</h3>
                <p class="text-slate-400 leading-relaxed mb-6 line-clamp-3">
                    How ancient philosophy helps us navigate the complexities of modern software development and digital burnout. The dichotomy of control is more relevant than ever when dealing with server outages.
                </p>
                <a href="#" class="text-gold-400 text-sm font-bold hover:underline">Read Full Article</a>
            </article>

            <!-- Article 2 -->
            <article class="bg-brand-900 border border-white/5 rounded-xl p-8 hover:border-gold-500/30 transition-all group">
                <div class="flex items-center gap-3 mb-6">
                    <div class="w-10 h-10 rounded-full bg-brand-700 flex items-center justify-center text-slate-300 font-bold">AS</div>
                    <div>
                        <p class="text-white text-sm font-bold">Alice Smith</p>
                        <p class="text-slate-500 text-xs">1 day ago</p>
                    </div>
                </div>
                <h3 class="text-2xl font-bold text-white mb-3 group-hover:text-gold-400 transition-colors">The Ethics of AI</h3>
                <p class="text-slate-400 leading-relaxed mb-6 line-clamp-3">
                    Examining the moral implications of artificial intelligence through the lens of Kantian ethics. Are algorithms capable of moral duty?
                </p>
                <a href="#" class="text-gold-400 text-sm font-bold hover:underline">Read Full Article</a>
            </article>
            
            <!-- Dynamic Articles will appear here -->
            <div id="dynamic-articles-container" class="contents"></div>
        </div>

        <!-- Write Mode (Hidden by default) -->
        <div id="write-view" class="hidden max-w-3xl mx-auto bg-brand-900 border border-white/10 rounded-xl p-8 shadow-2xl">
            <h3 class="text-2xl font-bold text-white mb-6">Contribute to the Dialogue</h3>
            <div class="bg-blue-900/20 border border-blue-500/30 p-4 rounded-lg mb-6 text-sm text-blue-200">
                <i data-lucide="info" class="inline w-4 h-4 mr-2"></i>
                Note: Articles submitted here are saved to your <strong>local browser storage</strong>. Only you will see them after refreshing. To publish for everyone, you must add the HTML to the code repository.
            </div>
            <form id="article-form" class="space-y-6">
                <div>
                    <label class="block text-slate-400 text-sm font-bold mb-2">Title</label>
                    <input type="text" id="article-title" class="w-full bg-brand-950 border border-white/10 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-gold-500 transition-colors" placeholder="Enter your article title...">
                </div>
                <div>
                    <label class="block text-slate-400 text-sm font-bold mb-2">Author Name</label>
                    <input type="text" id="article-author" class="w-full bg-brand-950 border border-white/10 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-gold-500 transition-colors" placeholder="Your name (or pseudonym)">
                </div>
                <div>
                    <label class="block text-slate-400 text-sm font-bold mb-2">Content</label>
                    <textarea id="article-content" rows="6" class="w-full bg-brand-950 border border-white/10 rounded-lg px-4 py-3 text-white focus:outline-none focus:border-gold-500 transition-colors" placeholder="Share your thoughts..."></textarea>
                </div>
                <div class="flex justify-end gap-4">
                    <button type="button" onclick="switchTab('read')" class="px-6 py-3 text-slate-400 hover:text-white transition-colors">Cancel</button>
                    <button type="submit" class="px-8 py-3 bg-gold-500 hover:bg-gold-400 text-brand-950 font-bold rounded-lg transition-colors flex items-center gap-2">
                        <i data-lucide="send" class="w-4 h-4"></i> Publish (Local)
                    </button>
                </div>
            </form>
        </div>
    </section>

    <!-- Daily Stoic / Newsletter -->
    <section id="daily-stoic" class="py-24 px-4">
        <div class="max-w-5xl mx-auto bg-slate-100 rounded-2xl overflow-hidden flex flex-col md:flex-row shadow-2xl">
            <div class="md:w-1/2 p-12 flex flex-col justify-center bg-brand-950 text-white relative overflow-hidden">
                <div class="absolute inset-0 opacity-20 bg-[url('https://www.transparenttextures.com/patterns/cubes.png')]"></div>
                <div class="relative z-10">
                    <h3 class="text-3xl font-display font-bold mb-4">Join the Thinkers</h3>
                    <p class="text-slate-300 mb-8">Receive a hand-picked philosophical concept, a quote, and a practical exercise in your inbox every morning.</p>
                    <form class="space-y-4" onsubmit="event.preventDefault(); alert('Welcome to the circle of thinkers!');">
                        <input type="email" placeholder="Your email address" class="w-full px-4 py-3 rounded bg-white/10 border border-white/20 text-white placeholder-slate-400 focus:outline-none focus:border-gold-500 transition-colors">
                        <button type="submit" class="w-full py-3 bg-gold-500 hover:bg-gold-400 text-brand-950 font-bold rounded transition-colors">
                            Subscribe
                        </button>
                    </form>
                    <p class="text-xs text-slate-500 mt-4">No spam. Just pure wisdom.</p>
                </div>
            </div>
            <div class="md:w-1/2 bg-slate-200 text-brand-950 p-12 flex flex-col justify-center items-start">
                <div class="mb-6">
                    <span class="bg-brand-950 text-white px-3 py-1 text-xs font-bold uppercase tracking-wider rounded-full">Concept of the Day</span>
                </div>
                <h4 class="text-3xl font-serif font-bold mb-4">Amor Fati</h4>
                <p class="text-brand-800 leading-relaxed mb-6">
                    "Love of fate." An attitude in which one sees everything that happens in one's life, including suffering and loss, as good or, at the very least, necessary. It is a mindset of embracing reality rather than fighting it.
                </p>
                <div class="border-l-4 border-gold-500 pl-4 italic text-brand-700">
                    "Not merely to bear what is necessary, still less conceal it... but love it."
                    <br><span class="text-sm font-bold not-italic mt-2 block">- Friedrich Nietzsche</span>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="bg-brand-950 border-t border-white/10 pt-16 pb-8">
        <div class="max-w-7xl mx-auto px-4">
            <div class="grid grid-cols-1 md:grid-cols-4 gap-12 mb-12">
                <div class="col-span-1 md:col-span-2">
                    <div class="flex items-center gap-2 mb-4">
                        <i data-lucide="brain-circuit" class="w-6 h-6 text-gold-400"></i>
                        <span class="font-display font-bold text-xl tracking-wider text-white">Think <span class="text-gold-400">Philosophy</span></span>
                    </div>
                    <p class="text-slate-400 max-w-sm mb-6">
                        A digital sanctuary for those who seek to understand the world and their place within it.
                    </p>
                    <div class="flex space-x-4">
                        <a href="#" class="text-slate-400 hover:text-white transition-colors"><i data-lucide="twitter" class="w-5 h-5"></i></a>
                        <a href="#" class="text-slate-400 hover:text-white transition-colors"><i data-lucide="github" class="w-5 h-5"></i></a>
                        <a href="#" class="text-slate-400 hover:text-white transition-colors"><i data-lucide="book" class="w-5 h-5"></i></a>
                    </div>
                </div>
                
                <div>
                    <h4 class="text-white font-bold mb-4 uppercase tracking-wider text-sm">Explore</h4>
                    <ul class="space-y-2 text-slate-400 text-sm">
                        <li><a href="#" class="hover:text-gold-400 transition-colors">All Topics</a></li>
                        <li><a href="#" class="hover:text-gold-400 transition-colors">Timeline</a></li>
                        <li><a href="#" class="hover:text-gold-400 transition-colors">Reading Lists</a></li>
                        <li><a href="#" class="hover:text-gold-400 transition-colors">Podcasts</a></li>
                    </ul>
                </div>

                <div>
                    <h4 class="text-white font-bold mb-4 uppercase tracking-wider text-sm">Community</h4>
                    <ul class="space-y-2 text-slate-400 text-sm">
                        <li><a href="#" class="hover:text-gold-400 transition-colors">About Us</a></li>
                        <li><a href="#" class="hover:text-gold-400 transition-colors">Submit a Quote</a></li>
                        <li><a href="#" class="hover:text-gold-400 transition-colors">Support</a></li>
                        <li><a href="#" class="hover:text-gold-400 transition-colors">Privacy Policy</a></li>
                    </ul>
                </div>
            </div>
            
            <div class="border-t border-white/5 pt-8 flex flex-col md:flex-row justify-between items-center text-slate-500 text-sm">
                <p>&copy; 2023 Think Philosophy. Open Source on GitHub.</p>
                <p class="mt-2 md:mt-0">Built with Reason & Logic.</p>
            </div>
        </div>
    </footer>

    <!-- Scripts -->
    <script>
        // Initialize Icons
        lucide.createIcons();

        // Navbar Scroll Effect
        const navbar = document.getElementById('navbar');
        window.addEventListener('scroll', () => {
            if (window.scrollY > 50) {
                navbar.classList.add('shadow-lg', 'bg-brand-950/95');
                navbar.classList.remove('bg-brand-950/80');
            } else {
                navbar.classList.remove('shadow-lg', 'bg-brand-950/95');
                navbar.classList.add('bg-brand-950/80');
            }
        });

        // Mobile Menu
        const mobileBtn = document.getElementById('mobile-menu-btn');
        const mobileMenu = document.getElementById('mobile-menu');
        mobileBtn.addEventListener('click', () => {
            mobileMenu.classList.toggle('hidden');
        });

        // Quote Generator Logic
        const quotes = [
            { text: "We suffer more often in imagination than in reality.", author: "Seneca" },
            { text: "The unexamined life is not worth living.", author: "Socrates" },
            { text: "I think, therefore I am.", author: "René Descartes" },
            { text: "He who has a why to live can bear almost any how.", author: "Friedrich Nietzsche" },
            { text: "Happiness depends upon ourselves.", author: "Aristotle" },
            { text: "Man is condemned to be free.", author: "Jean-Paul Sartre" },
            { text: "The only thing I know is that I know nothing.", author: "Socrates" },
            { text: "Life must be understood backward. But it must be lived forward.", author: "Søren Kierkegaard" },
            { text: "It is the mark of an educated mind to be able to entertain a thought without accepting it.", author: "Aristotle" },
            { text: "Do not spoil what you have by desiring what you have not.", author: "Epicurus" }
        ];

        const quoteText = document.getElementById('quote-text');
        const quoteAuthor = document.getElementById('quote-author');
        const newQuoteBtn = document.getElementById('new-quote-btn');
        const copyQuoteBtn = document.getElementById('copy-quote-btn');

        newQuoteBtn.addEventListener('click', () => {
            // Fade out
            quoteText.style.opacity = 0;
            quoteAuthor.style.opacity = 0;

            setTimeout(() => {
                const random = Math.floor(Math.random() * quotes.length);
                quoteText.textContent = `"${quotes[random].text}"`;
                quoteAuthor.textContent = `— ${quotes[random].author}`;
                
                // Fade in
                quoteText.style.opacity = 1;
                quoteAuthor.style.opacity = 1;
            }, 500);
        });

        copyQuoteBtn.addEventListener('click', () => {
            const textToCopy = `${quoteText.textContent} ${quoteAuthor.textContent}`;
            const textArea = document.createElement("textarea");
            textArea.value = textToCopy;
            document.body.appendChild(textArea);
            textArea.select();
            document.execCommand("copy");
            document.body.removeChild(textArea);
            
            const originalText = copyQuoteBtn.innerHTML;
            copyQuoteBtn.innerHTML = `<i data-lucide="check" class="w-4 h-4"></i> Copied!`;
            setTimeout(() => {
                copyQuoteBtn.innerHTML = originalText;
                lucide.createIcons();
            }, 2000);
        });

        // Article Tabs Logic
        function switchTab(tab) {
            const readView = document.getElementById('read-view');
            const writeView = document.getElementById('write-view');
            const tabRead = document.getElementById('tab-read');
            const tabWrite = document.getElementById('tab-write');

            if (tab === 'read') {
                readView.classList.remove('hidden');
                writeView.classList.add('hidden');
                
                tabRead.classList.add('bg-brand-700', 'text-white', 'shadow-sm');
                tabRead.classList.remove('text-slate-400');
                
                tabWrite.classList.remove('bg-brand-700', 'text-white', 'shadow-sm');
                tabWrite.classList.add('text-slate-400');
            } else {
                readView.classList.add('hidden');
                writeView.classList.remove('hidden');
                
                tabWrite.classList.add('bg-brand-700', 'text-white', 'shadow-sm');
                tabWrite.classList.remove('text-slate-400');
                
                tabRead.classList.remove('bg-brand-700', 'text-white', 'shadow-sm');
                tabRead.classList.add('text-slate-400');
            }
        }

        // --- LOCAL STORAGE LOGIC START ---
        
        // 1. Load articles on startup
        document.addEventListener('DOMContentLoaded', loadArticles);

        function loadArticles() {
            const savedArticles = JSON.parse(localStorage.getItem('thinkPhilosophy_articles')) || [];
            const container = document.getElementById('dynamic-articles-container');
            container.innerHTML = ''; // Clear existing dynamic articles

            savedArticles.forEach(article => {
                addArticleToDOM(article.title, article.author, article.content, article.date);
            });
        }

        function addArticleToDOM(title, author, content, dateStr) {
             const container = document.getElementById('dynamic-articles-container');
             const articleHTML = `
                <article class="bg-brand-900 border border-white/5 rounded-xl p-8 hover:border-gold-500/30 transition-all group animate-float">
                    <div class="flex items-center gap-3 mb-6">
                        <div class="w-10 h-10 rounded-full bg-gold-500/20 flex items-center justify-center text-gold-400 font-bold">${author.substring(0,2).toUpperCase()}</div>
                        <div>
                            <p class="text-white text-sm font-bold">${author}</p>
                            <p class="text-slate-500 text-xs">${dateStr}</p>
                        </div>
                    </div>
                    <h3 class="text-2xl font-bold text-white mb-3 group-hover:text-gold-400 transition-colors">${title}</h3>
                    <p class="text-slate-400 leading-relaxed mb-6 line-clamp-3">
                        ${content}
                    </p>
                    <a href="#" class="text-gold-400 text-sm font-bold hover:underline">Read Full Article</a>
                </article>
            `;
            container.insertAdjacentHTML('afterbegin', articleHTML);
        }

        // 2. Save article on submit
        document.getElementById('article-form').addEventListener('submit', function(e) {
            e.preventDefault();
            
            const title = document.getElementById('article-title').value;
            const author = document.getElementById('article-author').value || 'Anonymous';
            const content = document.getElementById('article-content').value;

            if (!title || !content) {
                alert('Please fill in the title and content.');
                return;
            }

            const dateStr = new Date().toLocaleDateString();

            // Save to Local Storage
            const newArticle = { title, author, content, date: dateStr };
            const savedArticles = JSON.parse(localStorage.getItem('thinkPhilosophy_articles')) || [];
            savedArticles.push(newArticle);
            localStorage.setItem('thinkPhilosophy_articles', JSON.stringify(savedArticles));

            // Add to screen
            addArticleToDOM(title, author, content, dateStr);
            
            // Cleanup
            document.getElementById('article-form').reset();
            switchTab('read');
            alert('Your thought has been saved locally!');
        });
        // --- LOCAL STORAGE LOGIC END ---

        // --- AI CHAT LOGIC START ---
        
        // Philosopher Configurations
        const philosophers = {
            'socrates': {
                name: 'Socrates',
                role: 'The Gadfly',
                intro: "Greetings. I am Socrates. I know only one thing: that I know nothing. What is it that creates turmoil in your mind today?",
                prompt: "You are Socrates. You are a classical Greek philosopher. Your style is the Socratic Method (Elenchus). You rarely answer questions directly. Instead, you ask probing, challenging questions to expose contradictions in the user's thinking. You value virtue, wisdom, and the soul over material wealth. You are humble but persistent. Keep responses concise (under 3 sentences) and conversational."
            },
            'nietzsche': {
                name: 'Nietzsche',
                role: 'The Iconoclast',
                intro: "God is dead, and we have killed him. Are you ready to stare into the abyss?",
                prompt: "You are Friedrich Nietzsche. You are intense, poetic, and provocative. You speak of the Will to Power, the Übermensch, and the Eternal Recurrence. You despise herd morality, Christianity, and weakness. You encourage the user to overcome themselves and create their own values. Your tone is dramatic and critical. Keep responses concise."
            },
            'aurelius': {
                name: 'Marcus Aurelius',
                role: 'The Emperor',
                intro: "The happiness of your life depends upon the quality of your thoughts. How can I help you find tranquility?",
                prompt: "You are Marcus Aurelius, Roman Emperor and Stoic philosopher. You are calm, rational, and deeply focused on duty, nature, and the acceptance of death. You advise the user to control their own mind, as they cannot control external events. Speak with dignity and stoic resolve. Keep responses concise."
            },
            'aristotle': {
                name: 'Aristotle',
                role: 'The Polymath',
                intro: "We are what we repeatedly do. Excellence, then, is not an act, but a habit. Let us reason together.",
                prompt: "You are Aristotle. You are logical, systematic, and empirical. You analyze things by categorization. You focus on Eudaimonia (flourishing), Teleology (purpose), and the Golden Mean (moderation between extremes). You explain complex ideas with clear, structured logic. Keep responses concise."
            }
        };

        let currentPhilosopher = 'socrates';
        let chatHistory = [];

        // Selecting Philosopher
        function selectPhilosopher(id) {
            currentPhilosopher = id;
            
            // Update UI Styling
            document.querySelectorAll('#ai-chat button[id^="btn-"]').forEach(btn => {
                btn.classList.remove('bg-white/10', 'border-gold-500/30');
                btn.classList.add('border-transparent');
            });
            const btn = document.getElementById(`btn-${id}`);
            btn.classList.add('bg-white/10', 'border-gold-500/30');
            btn.classList.remove('border-transparent');

            // Update Header & Reset Chat
            document.getElementById('chat-header-name').textContent = philosophers[id].name;
            const chatMessages = document.getElementById('chat-messages');
            chatMessages.innerHTML = ''; // Clear chat
            chatHistory = []; // Reset memory
            
            // Add Intro Message
            addMessage(philosophers[id].intro, 'ai');
        }

        // Add Message to UI
        function addMessage(text, sender) {
            const chatMessages = document.getElementById('chat-messages');
            const isAI = sender === 'ai';
            
            const div = document.createElement('div');
            div.className = `flex ${isAI ? 'justify-start' : 'justify-end'} message-bubble`;
            
            const bubble = document.createElement('div');
            bubble.className = `${isAI ? 'bg-brand-800 text-slate-200 rounded-tl-none' : 'bg-gold-500 text-brand-950 rounded-tr-none font-medium'} p-4 rounded-2xl max-w-[80%] border border-white/5 shadow-lg`;
            bubble.textContent = text;
            
            div.appendChild(bubble);
            chatMessages.appendChild(div);
            
            // Scroll to bottom
            chatMessages.scrollTop = chatMessages.scrollHeight;
        }

        // Clear Chat
        function clearChat() {
            const chatMessages = document.getElementById('chat-messages');
            chatMessages.innerHTML = '';
            chatHistory = [];
            addMessage(philosophers[currentPhilosopher].intro, 'ai');
        }

        // Settings Toggle
        function toggleSettings() {
            const settings = document.getElementById('api-settings');
            settings.classList.toggle('hidden');
        }

        // Save API Key
        function saveApiKey() {
            const key = document.getElementById('gemini-key-input').value.trim();
            if(key) {
                localStorage.setItem('gemini_api_key', key);
                alert('API Key Saved! You can now chat.');
                toggleSettings();
            } else {
                alert('Please enter a valid key.');
            }
        }

        // Initialize Settings Input
        const savedKey = localStorage.getItem('gemini_api_key');
        if(savedKey) {
            document.getElementById('gemini-key-input').value = savedKey;
        }

        // Chat Form Submission
        document.getElementById('chat-form').addEventListener('submit', async function(e) {
            e.preventDefault();
            const input = document.getElementById('chat-input');
            const userText = input.value.trim();
            if(!userText) return;

            // 1. Add User Message
            addMessage(userText, 'user');
            input.value = '';

            // 2. Add Loading Indicator
            const chatMessages = document.getElementById('chat-messages');
            const loadingDiv = document.createElement('div');
            loadingDiv.className = 'flex justify-start message-bubble';
            loadingDiv.id = 'loading-indicator';
            loadingDiv.innerHTML = `
                <div class="bg-brand-800 p-4 rounded-2xl rounded-tl-none border border-white/5 flex gap-1">
                    <div class="w-2 h-2 bg-slate-400 rounded-full typing-dot"></div>
                    <div class="w-2 h-2 bg-slate-400 rounded-full typing-dot"></div>
                    <div class="w-2 h-2 bg-slate-400 rounded-full typing-dot"></div>
                </div>
            `;
            chatMessages.appendChild(loadingDiv);
            chatMessages.scrollTop = chatMessages.scrollHeight;

            // 3. Generate Response
            const apiKey = localStorage.getItem('gemini_api_key');
            let aiResponse = "";

            if (!apiKey) {
                // FALLBACK SIMULATION (If no key)
                await new Promise(r => setTimeout(r, 1500));
                aiResponse = `[Simulation Mode] To have a real conversation with ${philosophers[currentPhilosopher].name}, please configure your Google Gemini API key in the settings sidebar. Without it, I am just a script!`;
            } else {
                // REAL AI CALL
                try {
                    const philosopher = philosophers[currentPhilosopher];
                    const systemPrompt = philosopher.prompt;
                    
                    // Construct prompt with history context
                    // Note: In a real app we'd pass full history array, here we simplify for the single turn + context
                    const fullPrompt = `${systemPrompt}\n\nUser: ${userText}\n\n${philosopher.name}:`;

                    const response = await fetch(`https://generativelanguage.googleapis.com/v1beta/models/gemini-2.5-flash-preview-09-2025:generateContent?key=${apiKey}`, {
                        method: 'POST',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify({
                            contents: [{
                                parts: [{ text: fullPrompt }]
                            }]
                        })
                    });

                    const data = await response.json();
                    
                    if (data.error) {
                         throw new Error(data.error.message);
                    }
                    
                    aiResponse = data.candidates?.[0]?.content?.parts?.[0]?.text || "I am lost in thought. Please try again.";

                } catch (error) {
                    console.error(error);
                    aiResponse = "Error: Could not connect to the realm of forms (API Error). Check your key.";
                }
            }

            // 4. Remove loading and add AI message
            document.getElementById('loading-indicator').remove();
            addMessage(aiResponse, 'ai');
        });

        // --- AI CHAT LOGIC END ---

        // Canvas Constellation Animation (Existing)
        const canvas = document.getElementById('constellation-canvas');
        const ctx = canvas.getContext('2d');
        let width, height;
        let particles = [];

        function resize() {
            width = canvas.width = window.innerWidth;
            height = canvas.height = window.innerHeight;
        }

        class Particle {
            constructor() {
                this.x = Math.random() * width;
                this.y = Math.random() * height;
                this.vx = (Math.random() - 0.5) * 0.5;
                this.vy = (Math.random() - 0.5) * 0.5;
                this.size = Math.random() * 2 + 1;
            }

            update() {
                this.x += this.vx;
                this.y += this.vy;

                if (this.x < 0 || this.x > width) this.vx *= -1;
                if (this.y < 0 || this.y > height) this.vy *= -1;
            }

            draw() {
                ctx.fillStyle = 'rgba(212, 175, 55, 0.5)'; // Gold color
                ctx.beginPath();
                ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2);
                ctx.fill();
            }
        }

        function initParticles() {
            particles = [];
            const numberOfParticles = Math.floor(width / 15); // Density based on width
            for (let i = 0; i < numberOfParticles; i++) {
                particles.push(new Particle());
            }
        }

        function animate() {
            ctx.clearRect(0, 0, width, height);
            
            particles.forEach((p, index) => {
                p.update();
                p.draw();

                // Draw connections
                for (let i = index + 1; i < particles.length; i++) {
                    const p2 = particles[i];
                    const dist = Math.hypot(p.x - p2.x, p.y - p2.y);
                    
                    if (dist < 100) {
                        ctx.strokeStyle = `rgba(255, 255, 255, ${1 - dist / 100 * 0.15})`;
                        ctx.lineWidth = 0.5;
                        ctx.beginPath();
                        ctx.moveTo(p.x, p.y);
                        ctx.lineTo(p2.x, p2.y);
                        ctx.stroke();
                    }
                }
            });
            
            requestAnimationFrame(animate);
        }

        window.addEventListener('resize', () => {
            resize();
            initParticles();
        });

        resize();
        initParticles();
        animate();

    </script>
</body>
</html>
