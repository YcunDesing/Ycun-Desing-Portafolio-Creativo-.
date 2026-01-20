<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>YCUN DESIGN | Editor de Portafolio</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;800&family=Playfair+Display:wght@700&display=swap" rel="stylesheet">
    <style>
        body { font-family: 'Inter', sans-serif; background-color: #ffffff; scroll-behavior: smooth; color: #000000; }
        .serif { font-family: 'Playfair Display', serif; }
        .project-card { transition: all 0.4s ease; position: relative; }
        
        /* Colores Personalizados */
        .text-custom-pink { color: #FF7EB9; }
        .bg-custom-pink { background-color: #FF7EB9; }
        .bg-custom-fuchsia { background-color: #FF5EB4; }
        .bg-custom-amber { background-color: #FFC048; }
        .bg-custom-cyan { background-color: #A2E1E1; }
        .bg-custom-lavender { background-color: #D6B6F7; }
        
        /* Capa de edición */
        .edit-overlay { 
            position: absolute; top: 15px; right: 15px; z-index: 50;
            display: none;
        }
        .editing .edit-overlay { display: block; }
        
        .img-preview { 
            width: 100%; height: 100%; object-fit: cover; 
            transition: transform 0.6s cubic-bezier(0.165, 0.84, 0.44, 1);
        }
        .project-card:hover .img-preview { transform: scale(1.05); }
        
        .mockup-box {
            position: relative; width: 100%; height: 500px; border-radius: 30px;
            overflow: hidden; display: flex; flex-direction: column;
            justify-content: center; align-items: center; border: 1px solid rgba(0,0,0,0.05);
        }

        .file-input { display: none; }
        
        .upload-btn {
            background: rgba(255, 255, 255, 0.9);
            backdrop-filter: blur(5px);
            padding: 12px;
            border-radius: 50%;
            cursor: pointer;
            box-shadow: 0 4px 15px rgba(0,0,0,0.1);
            transition: all 0.3s ease;
        }
        .upload-btn:hover { transform: scale(1.1); background: #ffffff; }

        .contact-link {
            transition: all 0.3s ease;
            border: 1px solid #e5e7eb;
        }
        .contact-link:hover {
            border-color: #FF5EB4;
            transform: translateY(-2px);
            background-color: #fffafb;
        }

        .btn-gradient {
            background: linear-gradient(135deg, #FF7EB9 0%, #FF5EB4 100%);
        }
    </style>
</head>
<body class="antialiased">

    <!-- Panel de Control Flotante -->
    <div class="fixed bottom-8 right-8 z-[100] flex flex-col items-end space-y-4">
        <div id="saveNotice" class="hidden bg-black text-white text-[10px] px-4 py-2 rounded-full uppercase tracking-widest animate-bounce">
            Modo Edición Activo
        </div>
        <button onclick="toggleEditMode()" id="editBtn" class="btn-gradient text-white px-8 py-4 rounded-full font-bold shadow-2xl flex items-center space-x-3 hover:brightness-110 transition-all">
            <span id="btnText">Activar Modo Editor</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 9a2 2 0 012-2h.93a2 2 0 001.664-.89l.812-1.22A2 2 0 0110.07 4h3.86a2 2 0 011.664.89l.812 1.22A2 2 0 0018.07 7H19a2 2 0 012 2v9a2 2 0 01-2 2H5a2 2 0 01-2-2V9z" />
            </svg>
        </button>
    </div>

    <!-- Navegación -->
    <nav class="fixed w-full z-50 bg-white/80 backdrop-blur-md border-b border-gray-100">
        <div class="max-w-7xl mx-auto px-6 h-20 flex items-center justify-between">
            <h1 class="text-2xl font-black tracking-tighter cursor-pointer" onclick="window.scrollTo(0,0)">YCUN<span class="text-custom-pink font-light">DESIGN</span></h1>
            <div class="flex space-x-6 md:space-x-10 text-[10px] font-black uppercase tracking-[0.2em] text-gray-400">
                <a href="#proyectos" class="hover:text-black transition">Portafolio</a>
                <a href="#contacto" class="hover:text-black transition">Contacto</a>
            </div>
        </div>
    </nav>

    <!-- Cabecera -->
    <header class="pt-48 pb-20 px-6">
        <div class="max-w-7xl mx-auto">
            <span class="text-custom-pink font-bold tracking-[0.3em] text-[10px] uppercase mb-4 block">Creatividad Dominicana</span>
            <h2 class="text-6xl md:text-9xl serif leading-[0.85] mb-8">
                Diseño con <br><span class="italic text-gray-200">fuerza.</span>
            </h2>
            <p class="text-gray-400 max-w-xl text-lg font-light leading-relaxed">
                Personaliza tu portafolio con colores vibrantes. Activa el editor y sube las imágenes para dar vida a tu marca.
            </p>
        </div>
    </header>

    <!-- Galería -->
    <section id="proyectos" class="py-20 px-6 bg-white">
        <div class="max-w-7xl mx-auto grid grid-cols-1 md:grid-cols-2 gap-16">
            
            <!-- Proyecto 1: Delicias Jireh (Ambar) -->
            <div class="project-card">
                <div class="edit-overlay">
                    <label for="input-1" class="upload-btn block">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                        </svg>
                    </label>
                    <input type="file" id="input-1" class="file-input" accept="image/*" onchange="handleFileUpload(this, 'img-1', 'placeholder-1')">
                </div>
                <div class="mockup-box bg-custom-amber">
                    <img id="img-1" src="" class="img-preview hidden">
                    <div id="placeholder-1" class="text-center p-12">
                        <h4 class="text-4xl serif text-black mb-3 uppercase tracking-tighter">Delicias Jireh</h4>
                        <p class="text-black/60 italic text-sm">Sube la portada de pastelería</p>
                    </div>
                </div>
                <div class="mt-8">
                    <span class="text-[10px] font-bold uppercase tracking-widest mb-1 block">Branding Gastronómico</span>
                    <h5 class="text-2xl font-black italic">Pastelería Artesanal</h5>
                </div>
            </div>

            <!-- Proyecto 2: Nova Glow (Fucsia) -->
            <div class="project-card">
                <div class="edit-overlay">
                    <label for="input-2" class="upload-btn block">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                        </svg>
                    </label>
                    <input type="file" id="input-2" class="file-input" accept="image/*" onchange="handleFileUpload(this, 'img-2', 'placeholder-2')">
                </div>
                <div class="mockup-box bg-custom-fuchsia">
                    <img id="img-2" src="" class="img-preview hidden">
                    <div id="placeholder-2" class="text-center p-12">
                        <h4 class="text-4xl serif text-white mb-3 uppercase tracking-tighter">Nova Glow</h4>
                        <p class="text-white/60 italic text-sm">Sube la imagen del logo</p>
                    </div>
                </div>
                <div class="mt-8">
                    <span class="text-[10px] font-bold text-custom-pink uppercase tracking-widest mb-1 block">Beauty Branding</span>
                    <h5 class="text-2xl font-black italic">Cuidado & Maquillaje</h5>
                </div>
            </div>

            <!-- Proyecto 3: Sri Sri (Cian) -->
            <div class="project-card">
                <div class="edit-overlay">
                    <label for="input-3" class="upload-btn block">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                        </svg>
                    </label>
                    <input type="file" id="input-3" class="file-input" accept="image/*" onchange="handleFileUpload(this, 'img-3', 'placeholder-3')">
                </div>
                <div class="mockup-box bg-custom-cyan">
                    <img id="img-3" src="" class="img-preview hidden">
                    <div id="placeholder-3" class="text-center p-12">
                        <h4 class="text-4xl serif text-black mb-3 uppercase tracking-tighter">Sri Sri Tattva</h4>
                        <p class="text-black/40 italic text-sm">Sube el post del jabón</p>
                    </div>
                </div>
                <div class="mt-8">
                    <span class="text-[10px] font-bold uppercase tracking-widest mb-1 block text-gray-400">Social Media Content</span>
                    <h5 class="text-2xl font-black italic">Bienestar Natural</h5>
                </div>
            </div>

            <!-- Proyecto 4: Infografía (Lavanda) -->
            <div class="project-card">
                <div class="edit-overlay">
                    <label for="input-4" class="upload-btn block">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 text-black" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-8l-4-4m0 0L8 8m4-4v12" />
                        </svg>
                    </label>
                    <input type="file" id="input-4" class="file-input" accept="image/*" onchange="handleFileUpload(this, 'img-4', 'placeholder-4')">
                </div>
                <div class="mockup-box bg-custom-lavender">
                    <img id="img-4" src="" class="img-preview hidden">
                    <div id="placeholder-4" class="text-center p-12">
                        <h4 class="text-3xl serif text-black mb-3 uppercase tracking-widest">Infografía</h4>
                        <p class="text-black/50 italic text-sm">Sube la importancia del logo</p>
                    </div>
                </div>
                <div class="mt-8">
                    <span class="text-[10px] font-bold uppercase tracking-widest mb-1 block text-gray-400">Diseño Educativo</span>
                    <h5 class="text-2xl font-black italic">Teoría de Marca</h5>
                </div>
            </div>

        </div>
    </section>

    <!-- SECCIÓN DE CONTACTO -->
    <section id="contacto" class="py-32 px-6 bg-gray-50 border-t border-gray-100">
        <div class="max-w-7xl mx-auto">
            <div class="grid md:grid-cols-2 gap-16 items-center">
                <div>
                    <h3 class="text-5xl md:text-7xl serif mb-8 leading-tight">Haz que tu marca <span class="text-custom-pink italic">brille.</span></h3>
                    <p class="text-gray-500 text-lg mb-10 font-light italic">"Hablemos sobre tu próxima gran idea."</p>
                    
                    <div class="space-y-4">
                        <a href="mailto:ycundesign@gmail.com" class="contact-link flex items-center justify-between p-6 bg-white rounded-2xl group">
                            <span class="font-bold tracking-widest uppercase text-[10px] text-gray-400">Email</span>
                            <span class="text-sm font-medium">ycundesign@gmail.com</span>
                        </a>
                        
                        <!-- WHATSAPP CON MENSAJE AUTOMÁTICO -->
                        <a href="https://wa.me/18297829962?text=Hola,%20quiero%20más%20información%20de%20tus%20servicios" target="_blank" class="contact-link flex items-center justify-between p-6 bg-white rounded-2xl group">
                            <span class="font-bold tracking-widest uppercase text-[10px] text-gray-400">WhatsApp</span>
                            <span class="text-sm font-black text-custom-pink">Enviar mensaje directo</span>
                        </a>

                        <a href="https://www.instagram.com/Ycun_desing" target="_blank" class="contact-link flex items-center justify-between p-6 bg-white rounded-2xl group">
                            <span class="font-bold tracking-widest uppercase text-[10px] text-gray-400">Instagram</span>
                            <span class="text-sm font-medium">@Ycun_desing</span>
                        </a>
                    </div>
                </div>
                
                <div class="bg-black p-10 rounded-[40px] shadow-2xl text-center">
                    <div class="w-20 h-20 bg-custom-pink rounded-full flex items-center justify-center mx-auto mb-6">
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-10 w-10 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="1.5" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                        </svg>
                    </div>
                    <h4 class="text-2xl font-black mb-4 italic text-balance text-white">"Un buen logo vale más que mil palabras"</h4>
                    <p class="text-custom-pink text-[10px] uppercase tracking-[0.3em] font-bold">YCUN DESIGN &bull; RD</p>
                </div>
            </div>
        </div>
    </section>

    <!-- Footer -->
    <footer class="py-20 px-6 text-center text-[10px] text-gray-300 font-bold uppercase tracking-[0.5em]">
        &copy; 2024 YCUN DESIGN - Santo Domingo, República Dominicana
    </footer>

    <script>
        let isEditing = false;

        function toggleEditMode() {
            isEditing = !isEditing;
            const body = document.body;
            const btn = document.getElementById('editBtn');
            const btnText = document.getElementById('btnText');
            const notice = document.getElementById('saveNotice');

            if (isEditing) {
                body.classList.add('editing');
                btnText.innerText = "Modo Editor: ON";
                notice.classList.remove('hidden');
            } else {
                body.classList.remove('editing');
                btnText.innerText = "Activar Modo Editor";
                notice.classList.add('hidden');
            }
        }

        function handleFileUpload(input, imgId, placeholderId) {
            const file = input.files[0];
            if (file) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    const img = document.getElementById(imgId);
                    const placeholder = document.getElementById(placeholderId);
                    
                    img.src = e.target.result;
                    img.classList.remove('hidden');
                    placeholder.classList.add('hidden');
                }
                reader.readAsDataURL(file);
            }
        }
    </script>

</body>
</html>
