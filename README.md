# -portfolio-uxui-David-Junior-

html_content = '''<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>UX/UI Designer Portfolio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@300;400;500;600;700&family=Inter:wght@300;400;500;600&display=swap" rel="stylesheet">
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/gsap.min.js"></script>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/gsap/3.12.2/ScrollTrigger.min.js"></script>
    <script src="https://unpkg.com/lucide@latest"></script>
    <style>
        :root {
            --primary: #FF4D00;
            --secondary: #00D9FF;
            --dark: #0a0a0a;
            --light: #fafafa;
        }
        
        * {
            box-sizing: border-box;
        }
        
        html {
            scroll-behavior: smooth;
        }
        
        body {
            font-family: 'Inter', sans-serif;
            background-color: var(--dark);
            color: var(--light);
            overflow-x: hidden;
            cursor: none;
        }
        
        h1, h2, h3, h4, h5, h6 {
            font-family: 'Space Grotesk', sans-serif;
        }
        
        /* Custom Cursor */
        .cursor {
            width: 20px;
            height: 20px;
            border: 2px solid var(--primary);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9999;
            transition: transform 0.1s, background-color 0.2s;
            mix-blend-mode: difference;
        }
        
        .cursor-follower {
            width: 40px;
            height: 40px;
            background: rgba(255, 77, 0, 0.1);
            border-radius: 50%;
            position: fixed;
            pointer-events: none;
            z-index: 9998;
            transition: transform 0.3s ease-out;
        }
        
        .cursor.hover {
            transform: scale(2);
            background-color: var(--primary);
        }
        
        /* Grain Overlay */
        .grain {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            pointer-events: none;
            z-index: 9990;
            opacity: 0.03;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noiseFilter'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noiseFilter)'/%3E%3C/svg%3E");
        }
        
        /* Navigation */
        .nav-link {
            position: relative;
            overflow: hidden;
        }
        
        .nav-link::after {
            content: '';
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            height: 1px;
            background: var(--primary);
            transform: translateX(-100%);
            transition: transform 0.3s ease;
        }
        
        .nav-link:hover::after {
            transform: translateX(0);
        }
        
        /* Hero Text Animation */
        .hero-text {
            font-size: clamp(3rem, 10vw, 8rem);
            line-height: 0.9;
            font-weight: 700;
            letter-spacing: -0.04em;
        }
        
        .char {
            display: inline-block;
            opacity: 0;
            transform: translateY(100px);
        }
        
        /* Project Cards */
        .project-card {
            position: relative;
            overflow: hidden;
            border-radius: 24px;
            background: linear-gradient(145deg, #1a1a1a, #0f0f0f);
            transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
        }
        
        .project-card:hover {
            transform: translateY(-10px);
        }
        
        .project-card img {
            transition: transform 0.7s cubic-bezier(0.16, 1, 0.3, 1);
        }
        
        .project-card:hover img {
            transform: scale(1.05);
        }
        
        .project-overlay {
            position: absolute;
            inset: 0;
            background: linear-gradient(to top, rgba(0,0,0,0.9) 0%, rgba(0,0,0,0) 50%);
            opacity: 0;
            transition: opacity 0.5s ease;
        }
        
        .project-card:hover .project-overlay {
            opacity: 1;
        }
        
        .project-info {
            position: absolute;
            bottom: 0;
            left: 0;
            right: 0;
            padding: 2rem;
            transform: translateY(20px);
            opacity: 0;
            transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
        }
        
        .project-card:hover .project-info {
            transform: translateY(0);
            opacity: 1;
        }
        
        /* Skills Marquee */
        .marquee-container {
            overflow: hidden;
            white-space: nowrap;
        }
        
        .marquee-content {
            display: inline-flex;
            animation: marquee 20s linear infinite;
        }
        
        @keyframes marquee {
            0% { transform: translateX(0); }
            100% { transform: translateX(-50%); }
        }
        
        .skill-tag {
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
            padding: 1rem 2rem;
            margin: 0 1rem;
            background: rgba(255, 255, 255, 0.05);
            border: 1px solid rgba(255, 255, 255, 0.1);
            border-radius: 100px;
            font-family: 'Space Grotesk', sans-serif;
            font-weight: 500;
            transition: all 0.3s ease;
        }
        
        .skill-tag:hover {
            background: var(--primary);
            border-color: var(--primary);
            transform: scale(1.05);
        }
        
        /* About Section */
        .about-image {
            position: relative;
            overflow: hidden;
            border-radius: 24px;
        }
        
        .about-image::before {
            content: '';
            position: absolute;
            inset: 0;
            background: var(--primary);
            mix-blend-mode: multiply;
            opacity: 0;
            transition: opacity 0.5s ease;
            z-index: 1;
        }
        
        .about-image:hover::before {
            opacity: 0.3;
        }
        
        /* Contact Section */
        .contact-link {
            font-size: clamp(2rem, 5vw, 4rem);
            font-weight: 700;
            font-family: 'Space Grotesk', sans-serif;
            position: relative;
            display: inline-block;
            transition: color 0.3s ease;
        }
        
        .contact-link::before {
            content: '';
            position: absolute;
            width: 100%;
            height: 8px;
            background: var(--primary);
            bottom: 0;
            left: 0;
            transform: scaleX(0);
            transform-origin: right;
            transition: transform 0.5s cubic-bezier(0.16, 1, 0.3, 1);
            z-index: -1;
        }
        
        .contact-link:hover::before {
            transform: scaleX(1);
            transform-origin: left;
        }
        
        .contact-link:hover {
            color: var(--primary);
        }
        
        /* Scroll Progress */
        .scroll-progress {
            position: fixed;
            top: 0;
            left: 0;
            height: 3px;
            background: var(--primary);
            z-index: 10000;
            transform-origin: left;
            transform: scaleX(0);
        }
        
        /* Mobile Menu */
        .mobile-menu {
            position: fixed;
            inset: 0;
            background: var(--dark);
            z-index: 999;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.5s ease;
        }
        
        .mobile-menu.active {
            opacity: 1;
            pointer-events: all;
        }
        
        .mobile-menu a {
            font-size: 3rem;
            font-weight: 700;
            font-family: 'Space Grotesk', sans-serif;
            margin: 1rem 0;
            opacity: 0;
            transform: translateY(20px);
        }
        
        .mobile-menu.active a {
            opacity: 1;
            transform: translateY(0);
            transition: all 0.5s cubic-bezier(0.16, 1, 0.3, 1);
        }
        
        /* Responsive */
        @media (max-width: 768px) {
            body {
                cursor: auto;
            }
            .cursor, .cursor-follower {
                display: none;
            }
        }
        
        /* Selection */
        ::selection {
            background: var(--primary);
            color: white;
        }
    </style>
</head>
<body>
    <!-- Grain Overlay -->
    <div class="grain"></div>
    
    <!-- Custom Cursor -->
    <div class="cursor"></div>
    <div class="cursor-follower"></div>
    
    <!-- Scroll Progress -->
    <div class="scroll-progress"></div>
    
    <!-- Navigation -->
    <nav class="fixed top-0 left-0 right-0 z-50 px-6 py-6 mix-blend-difference">
        <div class="max-w-7xl mx-auto flex justify-between items-center">
            <a href="#" class="text-2xl font-bold font-['Space_Grotesk'] tracking-tighter hover-trigger">PORTFOLIO.</a>
            
            <div class="hidden md:flex items-center gap-8">
                <a href="#work" class="nav-link text-sm font-medium tracking-wide hover-trigger">WORK</a>
                <a href="#about" class="nav-link text-sm font-medium tracking-wide hover-trigger">ABOUT</a>
                <a href="#skills" class="nav-link text-sm font-medium tracking-wide hover-trigger">SKILLS</a>
                <a href="#contact" class="nav-link text-sm font-medium tracking-wide hover-trigger">CONTACT</a>
            </div>
            
            <button class="md:hidden hover-trigger" id="menuBtn">
                <i data-lucide="menu" class="w-6 h-6"></i>
            </button>
        </div>
    </nav>
    
    <!-- Mobile Menu -->
    <div class="mobile-menu" id="mobileMenu">
        <button class="absolute top-6 right-6 hover-trigger" id="closeMenu">
            <i data-lucide="x" class="w-8 h-8"></i>
        </button>
        <a href="#work" class="hover-trigger mobile-link">WORK</a>
        <a href="#about" class="hover-trigger mobile-link">ABOUT</a>
        <a href="#skills" class="hover-trigger mobile-link">SKILLS</a>
        <a href="#contact" class="hover-trigger mobile-link">CONTACT</a>
    </div>

    <!-- Hero Section -->
    <section class="min-h-screen flex items-center justify-center relative overflow-hidden px-6">
        <div class="absolute inset-0 z-0">
            <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-orange-500/20 rounded-full blur-[128px]"></div>
            <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-cyan-500/10 rounded-full blur-[128px]"></div>
        </div>
        
        <div class="max-w-7xl mx-auto relative z-10">
            <div class="mb-4 overflow-hidden">
                <p class="text-sm md:text-base font-medium tracking-[0.3em] text-gray-400 hero-subtitle opacity-0">UX/UI DESIGNER</p>
            </div>
            
            <h1 class="hero-text mb-8">
                <span class="block overflow-hidden">
                    <span class="hero-line inline-block">CRAFTING</span>
                </span>
                <span class="block overflow-hidden">
                    <span class="hero-line inline-block text-transparent bg-clip-text bg-gradient-to-r from-orange-500 to-red-600">DIGITAL</span>
                </span>
                <span class="block overflow-hidden">
                    <span class="hero-line inline-block">EXPERIENCES</span>
                </span>
            </h1>
            
            <div class="max-w-xl">
                <p class="text-lg md:text-xl text-gray-400 mb-8 hero-desc opacity-0 leading-relaxed">
                    I design intuitive interfaces and meaningful user experiences that bridge the gap between human needs and digital solutions.
                </p>
                
                <div class="flex flex-wrap gap-4 hero-buttons opacity-0">
                    <a href="#work" class="group relative px-8 py-4 bg-white text-black font-medium rounded-full overflow-hidden hover-trigger">
                        <span class="relative z-10 flex items-center gap-2">
                            View Work
                            <i data-lucide="arrow-right" class="w-4 h-4 transition-transform group-hover:translate-x-1"></i>
                        </span>
                        <div class="absolute inset-0 bg-orange-500 transform scale-x-0 group-hover:scale-x-100 transition-transform origin-left duration-500"></div>
                    </a>
                    <a href="#contact" class="px-8 py-4 border border-white/20 rounded-full font-medium hover:bg-white/10 transition-colors hover-trigger">
                        Get in Touch
                    </a>
                </div>
            </div>
        </div>
        
        <div class="absolute bottom-8 left-1/2 -translate-x-1/2 animate-bounce">
            <i data-lucide="chevron-down" class="w-6 h-6 text-gray-500"></i>
        </div>
    </section>

    <!-- Selected Work Section -->
    <section id="work" class="py-32 px-6 relative">
        <div class="max-w-7xl mx-auto">
            <div class="flex flex-col md:flex-row justify-between items-start md:items-end mb-16 gap-6">
                <div>
                    <p class="text-sm font-medium tracking-[0.3em] text-orange-500 mb-4">SELECTED WORK</p>
                    <h2 class="text-4xl md:text-6xl font-bold">Featured Projects</h2>
                </div>
                <p class="text-gray-400 max-w-md">A curated selection of projects showcasing my expertise in user experience design, interface design, and design systems.</p>
            </div>
            
            <div class="grid grid-cols-1 md:grid-cols-2 gap-8">
                <!-- Project 1 -->
                <div class="project-card group hover-trigger aspect-[4/3]">
                    <img src="https://images.unsplash.com/photo-1618005182384-a83a8bd57fbe?w=800&q=80" alt="Fintech App" class="w-full h-full object-cover">
                    <div class="project-overlay"></div>
                    <div class="project-info">
                        <span class="text-xs font-medium tracking-wider text-orange-500 mb-2 block">FINTECH</span>
                        <h3 class="text-2xl font-bold mb-2">Nova Banking</h3>
                        <p class="text-sm text-gray-300 mb-4">Complete redesign of mobile banking experience focusing on accessibility and trust.</p>
                        <div class="flex gap-2">
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">UI Design</span>
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">User Research</span>
                        </div>
                    </div>
                </div>
                
                <!-- Project 2 -->
                <div class="project-card group hover-trigger aspect-[4/3] md:mt-16">
                    <img src="https://images.unsplash.com/photo-1551650975-87deedd944c3?w=800&q=80" alt="E-commerce" class="w-full h-full object-cover">
                    <div class="project-overlay"></div>
                    <div class="project-info">
                        <span class="text-xs font-medium tracking-wider text-orange-500 mb-2 block">E-COMMERCE</span>
                        <h3 class="text-2xl font-bold mb-2">Luxe Marketplace</h3>
                        <p class="text-sm text-gray-300 mb-4">Premium shopping experience with focus on visual storytelling and seamless checkout.</p>
                        <div class="flex gap-2">
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">UX Strategy</span>
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">Prototyping</span>
                        </div>
                    </div>
                </div>
                
                <!-- Project 3 -->
                <div class="project-card group hover-trigger aspect-[4/3]">
                    <img src="https://images.unsplash.com/photo-1559028012-481c04fa702d?w=800&q=80" alt="Health App" class="w-full h-full object-cover">
                    <div class="project-overlay"></div>
                    <div class="project-info">
                        <span class="text-xs font-medium tracking-wider text-orange-500 mb-2 block">HEALTHCARE</span>
                        <h3 class="text-2xl font-bold mb-2">Mindful Health</h3>
                        <p class="text-sm text-gray-300 mb-4">Mental health platform designed with calming aesthetics and intuitive navigation.</p>
                        <div class="flex gap-2">
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">Design System</span>
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">Accessibility</span>
                        </div>
                    </div>
                </div>
                
                <!-- Project 4 -->
                <div class="project-card group hover-trigger aspect-[4/3] md:mt-16">
                    <img src="https://images.unsplash.com/photo-1460925895917-afdab827c52f?w=800&q=80" alt="Dashboard" class="w-full h-full object-cover">
                    <div class="project-overlay"></div>
                    <div class="project-info">
                        <span class="text-xs font-medium tracking-wider text-orange-500 mb-2 block">SAAS</span>
                        <h3 class="text-2xl font-bold mb-2">Analytics Pro</h3>
                        <p class="text-sm text-gray-300 mb-4">Data visualization dashboard transforming complex data into actionable insights.</p>
                        <div class="flex gap-2">
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">Data Viz</span>
                            <span class="text-xs px-3 py-1 bg-white/10 rounded-full">Dashboard</span>
                        </div>
                    </div>
                </div>
            </div>
            
            <div class="mt-16 text-center">
                <a href="#" class="inline-flex items-center gap-2 text-lg font-medium hover:text-orange-500 transition-colors hover-trigger">
                    View All Projects
                    <i data-lucide="arrow-up-right" class="w-5 h-5"></i>
                </a>
            </div>
        </div>
    </section>

    <!-- Skills Marquee -->
    <section id="skills" class="py-20 border-y border-white/10 overflow-hidden">
        <div class="marquee-container">
            <div class="marquee-content">
                <div class="skill-tag hover-trigger"><i data-lucide="figma" class="w-5 h-5"></i> Figma</div>
                <div class="skill-tag hover-trigger"><i data-lucide="pen-tool" class="w-5 h-5"></i> Prototyping</div>
                <div class="skill-tag hover-trigger"><i data-lucide="users" class="w-5 h-5"></i> User Research</div>
                <div class="skill-tag hover-trigger"><i data-lucide="layout" class="w-5 h-5"></i> Design Systems</div>
                <div class="skill-tag hover-trigger"><i data-lucide="smartphone" class="w-5 h-5"></i> Mobile Design</div>
                <div class="skill-tag hover-trigger"><i data-lucide="monitor" class="w-5 h-5"></i> Web Design</div>
                <div class="skill-tag hover-trigger"><i data-lucide="accessibility" class="w-5 h-5"></i> Accessibility</div>
                <div class="skill-tag hover-trigger"><i data-lucide="bar-chart" class="w-5 h-5"></i> Data Visualization</div>
                <!-- Duplicate for seamless loop -->
                <div class="skill-tag hover-trigger"><i data-lucide="figma" class="w-5 h-5"></i> Figma</div>
                <div class="skill-tag hover-trigger"><i data-lucide="pen-tool" class="w-5 h-5"></i> Prototyping</div>
                <div class="skill-tag hover-trigger"><i data-lucide="users" class="w-5 h-5"></i> User Research</div>
                <div class="skill-tag hover-trigger"><i data-lucide="layout" class="w-5 h-5"></i> Design Systems</div>
                <div class="skill-tag hover-trigger"><i data-lucide="smartphone" class="w-5 h-5"></i> Mobile Design</div>
                <div class="skill-tag hover-trigger"><i data-lucide="monitor" class="w-5 h-5"></i> Web Design</div>
                <div class="skill-tag hover-trigger"><i data-lucide="accessibility" class="w-5 h-5"></i> Accessibility</div>
                <div class="skill-tag hover-trigger"><i data-lucide="bar-chart" class="w-5 h-5"></i> Data Visualization</div>
            </div>
        </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-32 px-6">
        <div class="max-w-7xl mx-auto">
            <div class="grid grid-cols-1 lg:grid-cols-2 gap-16 items-center">
                <div class="order-2 lg:order-1">
                    <p class="text-sm font-medium tracking-[0.3em] text-orange-500 mb-4">ABOUT ME</p>
                    <h2 class="text-4xl md:text-5xl font-bold mb-6 leading-tight">Designing with purpose, empathy, and precision</h2>
                    <div class="space-y-4 text-gray-400 text-lg leading-relaxed">
                        <p>
                            With over 5 years of experience in UX/UI design, I specialize in creating digital products that not only look beautiful but solve real problems. My approach combines strategic thinking with meticulous attention to detail.
                        </p>
                        <p>
                            I believe great design is invisible—it should feel intuitive, natural, and effortless. Every pixel, interaction, and transition serves a purpose in telling the product's story.
                        </p>
                        <p>
                            Currently based in San Francisco, I've had the privilege of working with startups and Fortune 500 companies alike, helping them transform their digital presence.
                        </p>
                    </div>
                    
                    <div class="mt-8 flex flex-wrap gap-8">
                        <div>
                            <span class="block text-3xl font-bold text-orange-500">50+</span>
                            <span class="text-sm text-gray-500">Projects Completed</span>
                        </div>
                        <div>
                            <span class="block text-3xl font-bold text-orange-500">5+</span>
                            <span class="text-sm text-gray-500">Years Experience</span>
                        </div>
                        <div>
                            <span class="block text-3xl font-bold text-orange-500">30+</span>
                            <span class="text-sm text-gray-500">Happy Clients</span>
                        </div>
                    </div>
                </div>
                
                <div class="order-1 lg:order-2">
                    <div class="about-image aspect-[3/4] relative">
                        <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=600&q=80" alt="Designer Portrait" class="w-full h-full object-cover grayscale hover:grayscale-0 transition-all duration-700">
                        <div class="absolute -bottom-6 -left-6 w-48 h-48 border-2 border-orange-500 rounded-2xl -z-10"></div>
                        <div class="absolute -top-6 -right-6 w-32 h-32 bg-orange-500/20 rounded-full blur-2xl"></div>
                    </div>
                </div>
            </div>
        </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-32 px-6 relative overflow-hidden">
        <div class="absolute inset-0 z-0">
            <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[800px] h-[800px] bg-orange-500/10 rounded-full blur-[150px]"></div>
        </div>
        
        <div class="max-w-7xl mx-auto relative z-10 text-center">
            <p class="text-sm font-medium tracking-[0.3em] text-orange-500 mb-4">LET'S CONNECT</p>
            <h2 class="text-4xl md:text-6xl font-bold mb-8">Ready to start a project?</h2>
            <p class="text-xl text-gray-400 mb-12 max-w-2xl mx-auto">
                I'm always interested in hearing about new projects and opportunities. Whether you have a question or just want to say hi, feel free to reach out.
            </p>
            
            <div class="space-y-6 mb-16">
                <a href="mailto:hello@designer.com" class="contact-link hover-trigger block">hello@designer.com</a>
            </div>
            
            <div class="flex justify-center gap-6">
                <a href="#" class="w-14 h-14 rounded-full border border-white/20 flex items-center justify-center hover:bg-white hover:text-black transition-all hover-trigger">
                    <i data-lucide="linkedin" class="w-5 h-5"></i>
                </a>
                <a href="#" class="w-14 h-14 rounded-full border border-white/20 flex items-center justify-center hover:bg-white hover:text-black transition-all hover-trigger">
                    <i data-lucide="twitter" class="w-5 h-5"></i>
                </a>
                <a href="#" class="w-14 h-14 rounded-full border border-white/20 flex items-center justify-center hover:bg-white hover:text-black transition-all hover-trigger">
                    <i data-lucide="dribbble" class="w-5 h-5"></i>
                </a>
                <a href="#" class="w-14 h-14 rounded-full border border-white/20 flex items-center justify-center hover:bg-white hover:text-black transition-all hover-trigger">
                    <i data-lucide="github" class="w-5 h-5"></i>
                </a>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="py-8 px-6 border-t border-white/10">
        <div class="max-w-7xl mx-auto flex flex-col md:flex-row justify-between items-center gap-4">
            <p class="text-sm text-gray-500">© 2024 Portfolio. All rights reserved.</p>
            <p class="text-sm text-gray-500">Designed with passion</p>
        </div>
    </footer>

    <script>
        // Initialize Lucide Icons
        lucide.createIcons();
        
        // Register GSAP ScrollTrigger
        gsap.registerPlugin(ScrollTrigger);
        
        // Custom Cursor
        const cursor = document.querySelector('.cursor');
        const cursorFollower = document.querySelector('.cursor-follower');
        const hoverTriggers = document.querySelectorAll('.hover-trigger');
        
        let mouseX = 0, mouseY = 0;
        let cursorX = 0, cursorY = 0;
        let followerX = 0, followerY = 0;
        
        document.addEventListener('mousemove', (e) => {
            mouseX = e.clientX;
            mouseY = e.clientY;
        });
        
        function animateCursor() {
            cursorX += (mouseX - cursorX) * 0.2;
            cursorY += (mouseY - cursorY) * 0.2;
            followerX += (mouseX - followerX) * 0.1;
            followerY += (mouseY - followerY) * 0.1;
            
            cursor.style.left = cursorX - 10 + 'px';
            cursor.style.top = cursorY - 10 + 'px';
            cursorFollower.style.left = followerX - 20 + 'px';
            cursorFollower.style.top = followerY - 20 + 'px';
            
            requestAnimationFrame(animateCursor);
        }
        animateCursor();
        
        hoverTriggers.forEach(trigger => {
            trigger.addEventListener('mouseenter', () => cursor.classList.add('hover'));
            trigger.addEventListener('mouseleave', () => cursor.classList.remove('hover'));
        });
        
        // Scroll Progress
        gsap.to('.scroll-progress', {
            scaleX: 1,
            ease: 'none',
            scrollTrigger: {
                trigger: document.body,
                start: 'top top',
                end: 'bottom bottom',
                scrub: 0.3
            }
        });
        
        // Hero Animations
        gsap.to('.hero-subtitle', {
            opacity: 1,
            y: 0,
            duration: 1,
            delay: 0.2,
            ease: 'power3.out'
        });
        
        gsap.from('.hero-line', {
            y: 100,
            opacity: 0,
            duration: 1.2,
            stagger: 0.1,
            delay: 0.4,
            ease: 'power3.out'
        });
        
        gsap.to('.hero-desc', {
            opacity: 1,
            y: 0,
            duration: 1,
            delay: 0.8,
            ease: 'power3.out'
        });
        
        gsap.to('.hero-buttons', {
            opacity: 1,
            y: 0,
            duration: 1,
            delay: 1,
            ease: 'power3.out'
        });
        
        // Project Cards Animation
        gsap.utils.toArray('.project-card').forEach((card, i) => {
            gsap.from(card, {
                scrollTrigger: {
                    trigger: card,
                    start: 'top 85%',
                    toggleActions: 'play none none reverse'
                },
                y: 100,
                opacity: 0,
                duration: 1,
                delay: i * 0.1,
                ease: 'power3.out'
            });
        });
        
        // About Section Animation
        gsap.from('.about-image', {
            scrollTrigger: {
                trigger: '#about',
                start: 'top 70%'
            },
            x: 50,
            opacity: 0,
            duration: 1.2,
            ease: 'power3.out'
        });
        
        gsap.from('#about h2, #about p', {
            scrollTrigger: {
                trigger: '#about',
                start: 'top 70%'
            },
            y: 30,
            opacity: 0,
            duration: 1,
            stagger: 0.1,
            ease: 'power3.out'
        });
        
        // Mobile Menu
        const menuBtn = document.getElementById('menuBtn');
        const closeMenu = document.getElementById('closeMenu');
        const mobileMenu = document.getElementById('mobileMenu');
        const mobileLinks = document.querySelectorAll('.mobile-link');
        
        menuBtn.addEventListener('click', () => {
            mobileMenu.classList.add('active');
            mobileLinks.forEach((link, i) => {
                link.style.transitionDelay = `${i * 0.1}s`;
            });
        });
        
        closeMenu.addEventListener('click', () => {
            mobileMenu.classList.remove('active');
            mobileLinks.forEach(link => {
                link.style.transitionDelay = '0s';
            });
        });
        
        mobileLinks.forEach(link => {
            link.addEventListener('click', () => {
                mobileMenu.classList.remove('active');
            });
        });
        
        // Parallax Effect on Hero
        document.addEventListener('mousemove', (e) => {
            const moveX = (e.clientX - window.innerWidth / 2) * 0.01;
            const moveY = (e.clientY - window.innerHeight / 2) * 0.01;
            
            gsap.to('.hero-text', {
                x: moveX,
                y: moveY,
                duration: 1,
                ease: 'power2.out'
            });
        });
        
        // Smooth Scroll for Navigation
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });
    </script>
</body>
</html>'''

# Save the file
output_path = '/mnt/kimi/output/ux-ui-portfolio.html'
with open(output_path, 'w', encoding='utf-8') as f:
    f.write(html_content)

print(f"Portfolio saved to: {output_path}")
print(f"File size: {len(html_content)} characters")
