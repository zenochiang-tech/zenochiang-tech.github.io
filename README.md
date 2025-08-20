<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>镜头印象 - 摄影博客</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Georgia', serif;
            line-height: 1.6;
            color: #333;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 0 20px;
        }

        /* Header */
        header {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 1000;
            transition: all 0.3s ease;
        }

        nav {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 1rem 0;
        }

        .logo {
            font-size: 2rem;
            font-weight: bold;
            color: #764ba2;
            text-decoration: none;
            transition: transform 0.3s ease;
        }

        .logo:hover {
            transform: scale(1.05);
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            text-decoration: none;
            color: #333;
            font-weight: 500;
            transition: all 0.3s ease;
            position: relative;
        }

        .nav-links a:hover {
            color: #764ba2;
            transform: translateY(-2px);
        }

        .nav-links a::after {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: #764ba2;
            transition: width 0.3s ease;
        }

        .nav-links a:hover::after {
            width: 100%;
        }

        /* Main Content */
        main {
            margin-top: 80px;
            padding: 2rem 0;
        }

        /* Hero Section */
        .hero {
            text-align: center;
            padding: 4rem 0;
            color: white;
            margin-bottom: 3rem;
        }

        .hero h1 {
            font-size: 3.5rem;
            margin-bottom: 1rem;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
            animation: fadeInUp 1s ease;
        }

        .hero p {
            font-size: 1.3rem;
            margin-bottom: 2rem;
            opacity: 0.9;
            animation: fadeInUp 1s ease 0.2s both;
        }

        /* Filter Buttons */
        .filter-container {
            text-align: center;
            margin-bottom: 3rem;
            animation: fadeInUp 1s ease 0.4s both;
        }

        .filter-btn {
            background: rgba(255, 255, 255, 0.9);
            border: none;
            padding: 12px 24px;
            margin: 0 10px;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-weight: 500;
            color: #333;
            backdrop-filter: blur(10px);
        }

        .filter-btn:hover, .filter-btn.active {
            background: #764ba2;
            color: white;
            transform: translateY(-3px);
            box-shadow: 0 10px 25px rgba(118, 75, 162, 0.3);
        }

        /* Gallery Grid */
        .gallery {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 2rem;
            padding: 2rem 0;
            animation: fadeInUp 1s ease 0.6s both;
        }

        .photo-card {
            background: white;
            border-radius: 15px;
            overflow: hidden;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.15);
            transition: all 0.4s ease;
            cursor: pointer;
            opacity: 1;
            transform: translateY(0);
        }

        .photo-card:hover {
            transform: translateY(-10px);
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.25);
        }

        .photo-card.hidden {
            opacity: 0;
            transform: translateY(20px);
            pointer-events: none;
        }

        .photo-img {
            width: 100%;
            height: 250px;
            object-fit: cover;
            transition: transform 0.4s ease;
        }

        .photo-card:hover .photo-img {
            transform: scale(1.05);
        }

        .photo-info {
            padding: 1.5rem;
        }

        .photo-title {
            font-size: 1.3rem;
            font-weight: bold;
            margin-bottom: 0.5rem;
            color: #333;
        }

        .photo-category {
            color: #764ba2;
            font-weight: 500;
            text-transform: uppercase;
            font-size: 0.9rem;
            letter-spacing: 1px;
            margin-bottom: 0.8rem;
        }

        .photo-description {
            color: #666;
            font-size: 1rem;
            line-height: 1.5;
        }

        /* Modal */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.9);
            z-index: 2000;
            animation: fadeIn 0.3s ease;
        }

        .modal-content {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            max-width: 90%;
            max-height: 90%;
            background: white;
            border-radius: 10px;
            overflow: hidden;
            animation: scaleIn 0.3s ease;
        }

        .modal-img {
            width: 100%;
            max-height: 70vh;
            object-fit: cover;
        }

        .modal-info {
            padding: 2rem;
        }

        .close-modal {
            position: absolute;
            top: 20px;
            right: 30px;
            color: white;
            font-size: 40px;
            cursor: pointer;
            transition: opacity 0.3s ease;
        }

        .close-modal:hover {
            opacity: 0.7;
        }

        /* Footer */
        footer {
            background: rgba(255, 255, 255, 0.95);
            text-align: center;
            padding: 2rem 0;
            margin-top: 4rem;
            backdrop-filter: blur(10px);
        }

        .social-links {
            margin-bottom: 1rem;
        }

        .social-links a {
            color: #764ba2;
            font-size: 1.5rem;
            margin: 0 1rem;
            transition: transform 0.3s ease;
            text-decoration: none;
        }

        .social-links a:hover {
            transform: scale(1.2);
        }

        /* Animations */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        @keyframes scaleIn {
            from {
                opacity: 0;
                transform: translate(-50%, -50%) scale(0.8);
            }
            to {
                opacity: 1;
                transform: translate(-50%, -50%) scale(1);
            }
        }

        /* Responsive Design */
        @media (max-width: 768px) {
            .hero h1 {
                font-size: 2.5rem;
            }
            
            .hero p {
                font-size: 1.1rem;
            }
            
            .gallery {
                grid-template-columns: 1fr;
                gap: 1.5rem;
            }
            
            .nav-links {
                gap: 1rem;
            }
            
            .filter-btn {
                margin: 5px;
                padding: 10px 20px;
            }
        }
    </style>
</head>
<body>
    <header>
        <nav class="container">
            <a href="#" class="logo">镜头印象</a>
            <ul class="nav-links">
                <li><a href="#home">首页</a></li>
                <li><a href="#gallery">作品集</a></li>
                <li><a href="#about">关于我</a></li>
                <li><a href="#contact">联系</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <section class="hero">
            <div class="container">
                <h1>用镜头捕捉世界</h1>
                <p>探索光影的艺术，记录生活中的美好瞬间</p>
            </div>
        </section>

        <section id="gallery" class="container">
            <div class="filter-container">
                <button class="filter-btn active" data-filter="all">全部作品</button>
                <button class="filter-btn" data-filter="portrait">人像摄影</button>
                <button class="filter-btn" data-filter="landscape">风景摄影</button>
                <button class="filter-btn" data-filter="street">街头摄影</button>
                <button class="filter-btn" data-filter="nature">自然摄影</button>
            </div>

            <div class="gallery">
                <div class="photo-card" data-category="portrait">
                    <img src="https://images.unsplash.com/photo-1544005313-94ddf0286df2?w=400&h=250&fit=crop" alt="人像摄影" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">人像摄影</div>
                        <h3 class="photo-title">温暖的微笑</h3>
                        <p class="photo-description">阳光透过窗帘洒在她的脸上，那一刻的微笑如此自然而温暖。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="landscape">
                    <img src="https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=400&h=250&fit=crop" alt="山景" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">风景摄影</div>
                        <h3 class="photo-title">群山之巅</h3>
                        <p class="photo-description">站在山顶俯瞰群山，云雾缭绕间感受大自然的壮丽。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="street">
                    <img src="https://images.unsplash.com/photo-1477959858617-67f85cf4f1df?w=400&h=250&fit=crop" alt="街头" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">街头摄影</div>
                        <h3 class="photo-title">城市印象</h3>
                        <p class="photo-description">繁华的街头，每个路人都有着属于自己的故事。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="nature">
                    <img src="https://images.unsplash.com/photo-1441974231531-c6227db76b6e?w=400&h=250&fit=crop" alt="森林" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">自然摄影</div>
                        <h3 class="photo-title">森林秘境</h3>
                        <p class="photo-description">阳光穿过茂密的树林，在地面投下斑驳的光影。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="portrait">
                    <img src="https://images.unsplash.com/photo-1507003211169-0a1dd7228f2d?w=400&h=250&fit=crop" alt="男性人像" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">人像摄影</div>
                        <h3 class="photo-title">深邃眼神</h3>
                        <p class="photo-description">黑白的色调更能突出人物内心的深度和情感。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="landscape">
                    <img src="https://images.unsplash.com/photo-1506905925346-21bda4d32df4?w=400&h=250&fit=crop" alt="海岸" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">风景摄影</div>
                        <h3 class="photo-title">海天一色</h3>
                        <p class="photo-description">日落时分的海岸线，天空与海水融为一体。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="street">
                    <img src="https://images.unsplash.com/photo-1519085360753-af0119f7cbe7?w=400&h=250&fit=crop" alt="夜景街道" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">街头摄影</div>
                        <h3 class="photo-title">夜色阑珊</h3>
                        <p class="photo-description">霓虹灯下的城市夜景，充满了现代都市的魅力。</p>
                    </div>
                </div>

                <div class="photo-card" data-category="nature">
                    <img src="https://images.unsplash.com/photo-1470071459604-3b5ec3a7fe05?w=400&h=250&fit=crop" alt="星空" class="photo-img">
                    <div class="photo-info">
                        <div class="photo-category">自然摄影</div>
                        <h3 class="photo-title">璀璨星河</h3>
                        <p class="photo-description">远离城市喧嚣，仰望满天繁星的夜空。</p>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <!-- Modal -->
    <div class="modal" id="photoModal">
        <span class="close-modal">&times;</span>
        <div class="modal-content">
            <img src="" alt="" class="modal-img" id="modalImg">
            <div class="modal-info" id="modalInfo">
                <div class="photo-category" id="modalCategory"></div>
                <h3 class="photo-title" id="modalTitle"></h3>
                <p class="photo-description" id="modalDescription"></p>
            </div>
        </div>
    </div>

    <footer>
        <div class="container">
            <div class="social-links">
                <a href="#">📷</a>
                <a href="#">📧</a>
                <a href="#">📱</a>
            </div>
            <p>&copy; 2025 镜头印象. 保留所有权利.</p>
        </div>
    </footer>

    <script>
        // Filter functionality
        const filterBtns = document.querySelectorAll('.filter-btn');
        const photoCards = document.querySelectorAll('.photo-card');
        
        filterBtns.forEach(btn => {
            btn.addEventListener('click', () => {
                // Remove active class from all buttons
                filterBtns.forEach(b => b.classList.remove('active'));
                // Add active class to clicked button
                btn.classList.add('active');
                
                const filter = btn.getAttribute('data-filter');
                
                photoCards.forEach(card => {
                    const category = card.getAttribute('data-category');
                    
                    if (filter === 'all' || category === filter) {
                        card.classList.remove('hidden');
                        setTimeout(() => {
                            card.style.transform = 'translateY(0)';
                            card.style.opacity = '1';
                        }, 100);
                    } else {
                        card.classList.add('hidden');
                    }
                });
            });
        });

        // Modal functionality
        const modal = document.getElementById('photoModal');
        const modalImg = document.getElementById('modalImg');
        const modalCategory = document.getElementById('modalCategory');
        const modalTitle = document.getElementById('modalTitle');
        const modalDescription = document.getElementById('modalDescription');
        const closeModal = document.querySelector('.close-modal');

        photoCards.forEach(card => {
            card.addEventListener('click', () => {
                const img = card.querySelector('.photo-img');
                const category = card.querySelector('.photo-category');
                const title = card.querySelector('.photo-title');
                const description = card.querySelector('.photo-description');

                modalImg.src = img.src;
                modalImg.alt = img.alt;
                modalCategory.textContent = category.textContent;
                modalTitle.textContent = title.textContent;
                modalDescription.textContent = description.textContent;

                modal.style.display = 'block';
                document.body.style.overflow = 'hidden';
            });
        });

        closeModal.addEventListener('click', () => {
            modal.style.display = 'none';
            document.body.style.overflow = 'auto';
        });

        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                modal.style.display = 'none';
                document.body.style.overflow = 'auto';
            }
        });

        // Smooth scroll for navigation
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

        // Header scroll effect
        window.addEventListener('scroll', () => {
            const header = document.querySelector('header');
            if (window.scrollY > 100) {
                header.style.background = 'rgba(255, 255, 255, 0.98)';
                header.style.boxShadow = '0 4px 30px rgba(0, 0, 0, 0.15)';
            } else {
                header.style.background = 'rgba(255, 255, 255, 0.95)';
                header.style.boxShadow = '0 4px 20px rgba(0, 0, 0, 0.1)';
            }
        });

        // Intersection Observer for animations
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.style.animationDelay = '0s';
                    entry.target.style.animationPlayState = 'running';
                }
            });
        }, observerOptions);

        photoCards.forEach(card => {
            observer.observe(card);
        });
    </script>
</body>
</html>
