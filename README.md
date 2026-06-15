<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>BlueBox · Mercadillo del cole</title>
    <style>
        :root {
            --azul: #0066ff;
            --azul-oscuro: #004ecc;
            --azul-claro: #e9f1ff;
            --gris-fondo: #f7f8fa;
            --blanco: #ffffff;
            --texto: #1a1d23;
            --texto-claro: #6b7280;
            --borde: #e5e7eb;
            --rojo: #ef4444;
            --verde: #10b981;
            --amarillo: #f59e0b;
            --rosa: #ff69b4;
            --sombra: 0 4px 12px rgba(0,0,0,0.06);
            --sombra-hover: 0 10px 25px -5px rgba(0,0,0,0.1);
            --radio: 16px;
            --radio-sm: 10px;
        }

        * { margin:0; padding:0; box-sizing:border-box; }
        body {
            font-family: 'Inter', system-ui, -apple-system, sans-serif;
            background: var(--gris-fondo);
            color: var(--texto);
            padding-bottom: 140px;
        }

        .header {
            background: rgba(255,255,255,0.92);
            backdrop-filter: blur(12px);
            border-bottom: 1px solid rgba(0,0,0,0.05);
            padding: 14px 28px;
            position: sticky;
            top: 0;
            z-index: 100;
            display: flex;
            align-items: center;
            justify-content: space-between;
            flex-wrap: wrap;
            gap: 15px;
        }
        .logo { display:flex; align-items:center; gap:12px; text-decoration:none; color:var(--texto); }
        .caja-azul {
            width:44px; height:40px; background:var(--azul);
            border-radius:7px 7px 9px 9px; position:relative;
            box-shadow:0 3px 0 #0041a8, 0 6px 14px rgba(0,102,255,0.25);
        }
        .caja-azul::before {
            content:''; position:absolute; top:-6px; left:7px; right:7px;
            height:12px; background:#3388ff; border-radius:4px 4px 0 0;
        }
        .caja-azul::after {
            content:''; position:absolute; top:4px; left:50%; transform:translateX(-50%);
            width:24px; height:3px; background:rgba(255,255,255,0.5); border-radius:4px;
        }
        .logo-texto { font-size:1.6rem; font-weight:700; color:#111; }
        .logo-texto span { color:var(--azul); font-weight:800; }

        .header-acciones { display:flex; align-items:center; gap:10px; flex-wrap:wrap; }

        .btn {
            padding:9px 18px; border-radius:30px; font-weight:600; font-size:0.9rem;
            border:1.5px solid #d1d5db; background:white; cursor:pointer; transition:all 0.2s;
            text-decoration:none; color:var(--texto);
        }
        .btn:hover { background:#f3f4f6; }
        .btn-primario { background:var(--azul); color:white; border-color:var(--azul); }
        .btn-primario:hover { background:var(--azul-oscuro); }

        .perfil-usuario { display:flex; align-items:center; gap:8px; font-weight:600; cursor:pointer; }
        .avatar {
            width:36px; height:36px; border-radius:50%; object-fit:cover;
            background:var(--azul); display:flex; align-items:center; justify-content:center;
            color:white; font-weight:700; overflow:hidden;
        }
        .avatar img { width:100%; height:100%; object-fit:cover; }
        .corona { font-size:1.2rem; margin-left:2px; }

        .buscador {
            max-width:500px; margin:20px auto; display:flex; gap:10px; align-items:center;
        }
        .buscador input {
            flex:1; padding:14px 20px; border-radius:50px; border:2px solid #e2e8f0;
            background:white; font-size:1rem;
        }
        .buscador input:focus { border-color:var(--azul); outline:none; box-shadow:0 0 0 4px rgba(0,102,255,0.1); }
        .btn-tic {
            background:white; border:2px solid var(--verde); color:var(--verde);
            font-weight:700; border-radius:30px; padding:12px 18px; cursor:pointer; transition:0.2s;
            display:flex; align-items:center; gap:6px;
        }
        .btn-tic.activo { background:var(--verde); color:white; }

        .contenedor { max-width:1300px; margin:0 auto; padding:20px; }
        .grid { display:grid; grid-template-columns:repeat(auto-fill, minmax(250px, 1fr)); gap:22px; }

        .tarjeta {
            background:white; border-radius:var(--radio); overflow:hidden;
            box-shadow:var(--sombra); transition:all 0.25s; display:flex; flex-direction:column;
            border:1px solid rgba(0,0,0,0.04); cursor:pointer;
        }
        .tarjeta:hover { transform:translateY(-4px); box-shadow:var(--sombra-hover); }
        .tarjeta.marco-dorado { border:3px solid #d4af37; box-shadow:0 0 15px rgba(212,175,55,0.3); }
        .tarjeta.marco-neon { border:3px solid #ff00ff; box-shadow:0 0 20px rgba(255,0,255,0.3); }
        .tarjeta.marco-galaxia {
            border:3px solid transparent;
            background:linear-gradient(white,white) padding-box, linear-gradient(45deg,#ff0066,#6600ff,#00ccff,#ff0066) border-box;
        }
        .tarjeta.marco-fresa { border:3px solid #ff4d6d; box-shadow:0 0 15px rgba(255,77,109,0.4); background:#fff5f7; }
        .tarjeta.marco-oceano { border:3px solid #00b4d8; box-shadow:0 0 15px rgba(0,180,216,0.3); }
        .tarjeta.marco-esmeralda { border:3px solid #2d6a4f; box-shadow:0 0 15px rgba(45,106,79,0.3); }

        .img-producto {
            height:200px; background:#f1f3f6; display:flex; align-items:center; justify-content:center;
            font-size:3rem; color:#cbd5e1; overflow:hidden;
        }
        .img-producto img { width:100%; height:100%; object-fit:cover; }

        .info-tarjeta { padding:16px; flex:1; display:flex; flex-direction:column; gap:8px; }
        .nombre-prod { font-weight:650; }
        .precio { font-size:1.4rem; font-weight:800; }
        .vendedor-info { display:flex; align-items:center; gap:6px; font-size:0.85rem; }
        .vendedor-info .nombre-vendedor { cursor:pointer; font-weight:600; color:var(--azul); }
        .estrellas { color:var(--amarillo); letter-spacing:2px; }
        .badge-destacado { background:#fef3c7; color:#92400e; padding:2px 8px; border-radius:12px; font-size:0.7rem; font-weight:700; }
        .badge-vip { background:#d4af37; color:white; padding:2px 8px; border-radius:12px; font-size:0.7rem; font-weight:700; margin-left:4px; }

        .btn-chat {
            margin-top:auto; border:1.5px solid var(--azul); color:var(--azul);
            padding:10px; border-radius:30px; font-weight:700; text-align:center; cursor:pointer;
            background:white; transition:0.2s;
        }
        .btn-chat:hover { background:var(--azul-claro); }

        .acciones-vendedor { display:flex; gap:8px; margin-top:8px; }
        .btn-vender, .btn-denuncia {
            background:#f3f4f6; border:none; border-radius:30px; padding:8px 12px;
            font-size:0.8rem; cursor:pointer; font-weight:600;
        }
        .btn-vender:hover { background:#d1fae5; color:#065f46; }
        .btn-denuncia:hover { background:#fee2e2; color:#991b1b; }

        .estado-vacio {
            grid-column:1/-1; background:white; border-radius:var(--radio);
            padding:70px; text-align:center; border:2px dashed #d1d5db; color:var(--texto-claro);
        }

        .fab {
            position:fixed; width:60px; height:60px; border-radius:50%; border:none;
            font-size:2rem; cursor:pointer; box-shadow:0 8px 24px rgba(0,0,0,0.2);
            transition:all 0.3s; z-index:99; display:flex; align-items:center; justify-content:center;
        }
        .fab-azul { background:var(--azul); color:white; bottom:32px; right:32px; }
        .fab-azul:hover { transform:scale(1.1) rotate(90deg); background:var(--azul-oscuro); }
        .fab-ajustes { background:#64748b; color:white; bottom:32px; right:110px; font-size:1.5rem; }
        .fab-ajustes:hover { background:#475569; }
        .fab-vip { background:#f59e0b; color:white; bottom:32px; right:190px; font-size:1.5rem; }
        .fab-vip:hover { background:#e5980b; }

        /* MODALES */
        .overlay {
            position:fixed; inset:0; background:rgba(15,23,42,0.5);
            backdrop-filter:blur(4px); z-index:200; display:flex; align-items:center; justify-content:center;
            animation:fade 0.2s;
        }
        @keyframes fade { from{opacity:0} to{opacity:1} }
        .modal {
            background:white; border-radius:24px; padding:30px 25px; width:90%; max-width:500px;
            max-height:85vh; overflow-y:auto; box-shadow:0 30px 60px rgba(0,0,0,0.2);
            position:relative; animation:slide 0.25s;
        }
        @keyframes slide { from{opacity:0; transform:translateY(40px)} to{opacity:1; transform:translateY(0)} }
        .modal-cerrar {
            position:absolute; top:14px; right:18px; background:#f1f5f9; border:none;
            width:32px; height:32px; border-radius:50%; font-size:1.3rem; cursor:pointer;
            color:#64748b; display:flex; align-items:center; justify-content:center;
        }
        .modal h2 { font-size:1.6rem; margin-bottom:20px; text-align:center; }

        .grupo-form { margin-bottom:16px; }
        .grupo-form label { display:block; font-weight:600; margin-bottom:5px; }
        .grupo-form input, .grupo-form textarea {
            width:100%; padding:12px 14px; border:1.5px solid #e2e8f0;
            border-radius:12px; background:#f8fafc; font-size:0.95rem;
        }
        .upload-wrapper { display:flex; align-items:center; gap:10px; flex-wrap:wrap; }
        .upload-btn { background:var(--azul-claro); color:var(--azul); padding:10px 16px; border-radius:30px; font-weight:650; cursor:pointer; }
        .preview { width:100px; height:100px; object-fit:cover; border-radius:50%; margin-top:10px; display:none; }
        .btn-formulario {
            width:100%; padding:14px; background:var(--azul); color:white;
            border:none; border-radius:50px; font-weight:700; font-size:1rem; cursor:pointer; margin-top:8px;
        }
        .enlace-modal { text-align:center; margin-top:14px; }
        .enlace-modal span { color:var(--azul); font-weight:700; cursor:pointer; }

        /* DETALLE PRODUCTO */
        .producto-detalle { text-align:center; }
        .producto-detalle .img-detalle {
            width:100%; max-height:300px; object-fit:contain; border-radius:12px;
            background:#f1f3f6; margin-bottom:16px;
        }
        .producto-detalle .precio-grande { font-size:2rem; font-weight:800; color:#0f172a; margin:10px 0; }
        .producto-detalle .vendedor-detalle {
            display:flex; align-items:center; gap:12px; justify-content:center;
            margin:16px 0; cursor:pointer;
        }
        .producto-detalle .vendedor-detalle img {
            width:48px; height:48px; border-radius:50%; object-fit:cover;
        }
        .descripcion { background:#f8fafc; padding:14px; border-radius:12px; margin:16px 0; text-align:left; }
        .acciones-detalle { display:flex; gap:10px; justify-content:center; flex-wrap:wrap; margin-top:20px; }

        /* CHAT */
        .chat-modal { display:flex; flex-direction:column; height:70vh; max-height:600px; }
        .chat-top { display:flex; align-items:center; gap:12px; padding-bottom:16px; border-bottom:1px solid #e2e8f0; margin-bottom:12px; }
        .chat-avatar { width:42px; height:42px; border-radius:50%; background:var(--azul); color:white; display:flex; align-items:center; justify-content:center; font-weight:700; }
        .mensajes { flex:1; overflow-y:auto; padding:8px 0; display:flex; flex-direction:column; gap:12px; }
        .bubble { max-width:75%; padding:10px 16px; border-radius:20px; font-size:0.9rem; word-break:break-word; }
        .bubble.enviado { align-self:flex-end; background:var(--azul); color:white; }
        .bubble.recibido { align-self:flex-start; background:#f1f5f9; color:#1e293b; }
        .chat-input { display:flex; gap:8px; margin-top:14px; }
        .chat-input input { flex:1; padding:12px 16px; border:1.5px solid #e2e8f0; border-radius:50px; font-size:0.9rem; }
        .chat-input button { padding:12px 22px; background:var(--azul); color:white; border:none; border-radius:50px; font-weight:700; cursor:pointer; }
        .valoracion { margin-top:14px; padding-top:14px; border-top:1px solid #e2e8f0; text-align:center; }
        .estrellas-valorar { font-size:1.8rem; cursor:pointer; }
        .estrella { color:#d1d5db; transition:color 0.2s; }
        .estrella.activa { color:var(--amarillo); }
    </style>
</head>
<body>

<header class="header">
    <a class="logo" href="#" onclick="location.reload()">
        <div class="caja-azul"></div>
        <span class="logo-texto">Blue<span>Box</span></span>
    </a>
    <div class="header-acciones" id="headerAcciones"></div>
</header>

<main class="contenedor">
    <div class="buscador">
        <input type="text" id="busqueda" placeholder="🔍 Buscar productos..." oninput="filtrarProductos()">
        <button class="btn-tic" id="btnToggleVendidos" onclick="toggleVendidos()">
            <span>✅</span> Vendidos
        </button>
    </div>
    <div class="grid" id="gridProductos"></div>
</main>

<button class="fab fab-vip" id="btnFabVIP" style="display:none" onclick="abrirModalCodigoVIP()">📦</button>
<button class="fab fab-ajustes" id="btnFabAjustes" style="display:none" onclick="abrirAjustes()">⚙️</button>
<button class="fab fab-azul" id="btnFabPublicar" style="display:none" onclick="abrirFormularioPublicar()">+</button>

<div id="contenedorModal"></div>

<script>
    (() => {
        // ── STORAGE ──
        const LS = {
            usuarios: 'bb_usuarios',
            productos: 'bb_productos',
            chats: 'bb_chats',
            sesion: 'bb_sesion',
            ratings: 'bb_ratings',
            vipCodes: 'bb_vipcodes',
            denuncias: 'bb_denuncias',
            baneos: 'bb_baneos',
            clean: 'bb_v7_clean'
        };
        if (!localStorage.getItem(LS.clean)) {
            Object.values(LS).forEach(k => localStorage.removeItem(k));
            localStorage.setItem(LS.clean, '1');
        }

        const obtener = clave => JSON.parse(localStorage.getItem(clave) || 'null');
        const guardar = (clave, valor) => localStorage.setItem(clave, JSON.stringify(valor));

        let usuarios = obtener(LS.usuarios) || [];
        let productos = obtener(LS.productos) || [];
        let conversaciones = obtener(LS.chats) || {};
        let ratings = obtener(LS.ratings) || {};
        let vipCodes = obtener(LS.vipCodes) || {};
        let denuncias = obtener(LS.denuncias) || [];
        let baneos = obtener(LS.baneos) || [];
        let sesion = obtener(LS.sesion);

        const persistir = () => {
            guardar(LS.usuarios, usuarios);
            guardar(LS.productos, productos);
            guardar(LS.chats, conversaciones);
            guardar(LS.ratings, ratings);
            guardar(LS.vipCodes, vipCodes);
            guardar(LS.denuncias, denuncias);
            guardar(LS.baneos, baneos);
            sesion ? guardar(LS.sesion, sesion) : localStorage.removeItem(LS.sesion);
        };

        const escapar = texto => { const d = document.createElement('div'); d.textContent = texto; return d.innerHTML; };

        function esAdmin(user) { return user && (user.rol === 'admin' || user.nombre === 'Adam'); }

        // Ratings
        function obtenerRating(vendedorId) {
            const r = ratings[vendedorId];
            if (!r || r.count === 0) return { promedio: 0, total: 0, estrellas5: 0 };
            const cincoEstrellas = Object.values(r.users || {}).filter(v => v === 5).length;
            return { promedio: r.total / r.count, total: r.count, estrellas5: cincoEstrellas };
        }
        function usuarioPuedeValorar(vendedorId) {
            if (!sesion || sesion.id === vendedorId) return false;
            return !(ratings[vendedorId]?.users?.[sesion.id]);
        }
        function valorarVendedor(vendedorId, estrellas) {
            if (!sesion) return;
            if (!ratings[vendedorId]) ratings[vendedorId] = { total: 0, count: 0, users: {} };
            const r = ratings[vendedorId];
            if (r.users[sesion.id]) {
                r.total += estrellas - r.users[sesion.id];
            } else {
                r.total += estrellas;
                r.count++;
            }
            r.users[sesion.id] = estrellas;
            persistir();
            refrescarTodo();
        }

        const MARCOS = {
            'marco-dorado': { nombre: 'Dorado', icono: '🥇' },
            'marco-neon': { nombre: 'Neón', icono: '💖' },
            'marco-galaxia': { nombre: 'Galaxia', icono: '🌌' },
            'marco-fresa': { nombre: 'Fresa', icono: '🍓' },
            'marco-oceano': { nombre: 'Océano', icono: '🌊' },
            'marco-esmeralda': { nombre: 'Esmeralda', icono: '🍀' }
        };

        function obtenerPerfilVIP(userId) {
            return vipCodes[userId] || { activeFrame: null, unlockedFrames: [] };
        }

        // Render principal
        const headerAcciones = document.getElementById('headerAcciones');
        const btnFabPublicar = document.getElementById('btnFabPublicar');
        const btnFabAjustes = document.getElementById('btnFabAjustes');
        const btnFabVIP = document.getElementById('btnFabVIP');
        const gridProductos = document.getElementById('gridProductos');
        let mostrarVendidos = false;

        window.toggleVendidos = () => {
            mostrarVendidos = !mostrarVendidos;
            document.getElementById('btnToggleVendidos').classList.toggle('activo', mostrarVendidos);
            renderizarProductos(document.getElementById('busqueda').value);
        };

        function renderizarHeader() {
            if (sesion) {
                const user = usuarios.find(u => u.id === sesion.id);
                const admin = esAdmin(user);
                const inicial = sesion.nombre.charAt(0).toUpperCase();
                const coronaHTML = admin ? '<span class="corona">👑</span>' : '';
                const fotoPerfil = user?.fotoPerfil || null;
                headerAcciones.innerHTML = `
                    <div class="perfil-usuario" onclick="verPerfil('${sesion.id}')">
                        <div class="avatar">${fotoPerfil ? `<img src="${fotoPerfil}" alt="Foto">` : inicial}${coronaHTML}</div>
                        <span>${escapar(sesion.nombre)}</span>
                    </div>
                    <button class="btn" onclick="cerrarSesion()">Salir</button>
                    ${admin ? '<button class="btn" onclick="abrirPanelAdmin()" style="background:#fef3c7;border-color:#d4af37;">🛡️ Admin</button>' : ''}
                `;
                btnFabPublicar.style.display = 'flex';
                btnFabAjustes.style.display = 'flex';
                btnFabVIP.style.display = 'flex';
            } else {
                headerAcciones.innerHTML = `
                    <button class="btn" onclick="mostrarLogin()">Iniciar sesión</button>
                    <button class="btn btn-primario" onclick="mostrarRegistro()">Registrarse</button>
                `;
                btnFabPublicar.style.display = 'none';
                btnFabAjustes.style.display = 'none';
                btnFabVIP.style.display = 'none';
            }
        }

        function renderizarProductos(filtro = '') {
            productos = obtener(LS.productos) || [];
            const termino = filtro.trim().toLowerCase();
            let lista = termino ? productos.filter(p => p.nombre.toLowerCase().includes(termino)) : [...productos];
            lista = mostrarVendidos ? lista.filter(p => p.vendido) : lista.filter(p => !p.vendido);

            if (lista.length === 0) {
                gridProductos.innerHTML = `<div class="estado-vacio"><div style="font-size:3rem;">📭</div><h3>${mostrarVendidos ? 'No hay productos vendidos' : 'No hay productos'}</h3></div>`;
                return;
            }

            gridProductos.innerHTML = lista.map(p => {
                const vendedor = usuarios.find(u => u.id === p.vendedorId);
                const nombreVendedor = vendedor?.nombre || 'Desconocido';
                const rating = obtenerRating(p.vendedorId);
                const destacado = rating.estrellas5 >= 10;
                const perfilVendedor = obtenerPerfilVIP(p.vendedorId);
                const estiloActivo = perfilVendedor.activeFrame || '';
                const badgeVIP = estiloActivo === 'marco-fresa' ? '<span class="badge-vip">🍓 VIP</span>' : '';
                const badgeDestacado = destacado ? '<span class="badge-destacado">⭐ Destacado</span>' : '';
                const imagen = p.imagen ? `<img src="${p.imagen}" alt="${escapar(p.nombre)}">` : '📷';

                const esPropietario = sesion && p.vendedorId === sesion.id;
                const accionesHTML = esPropietario && !p.vendido ? `
                    <div class="acciones-vendedor">
                        <button class="btn-vender" onclick="event.stopPropagation(); marcarVendido('${p.id}')">✅ Marcar vendido</button>
                    </div>` : '';

                const denunciaHTML = (sesion && !esPropietario) ? `
                    <button class="btn-denuncia" onclick="event.stopPropagation(); denunciarProducto('${p.id}')">🚩 Denunciar</button>` : '';

                return `
                    <div class="tarjeta ${estiloActivo}" onclick="verProducto('${p.id}')">
                        <div class="img-producto">${imagen}</div>
                        <div class="info-tarjeta">
                            <div class="nombre-prod">${escapar(p.nombre)}</div>
                            <div class="precio">${Number(p.precio).toFixed(2)} €</div>
                            <div class="vendedor-info">
                                <span class="nombre-vendedor" onclick="event.stopPropagation(); verPerfil('${p.vendedorId}')">👤 ${escapar(nombreVendedor)}</span>
                                ${renderizarEstrellas(rating.promedio)} (${rating.total})
                                ${badgeVIP} ${badgeDestacado}
                            </div>
                            ${!p.vendido ? `<button class="btn-chat" onclick="event.stopPropagation(); abrirChat('${p.id}')">💬 Contactar</button>` : '<p style="color:green;font-weight:600;">✅ Vendido</p>'}
                            ${accionesHTML}
                            ${denunciaHTML}
                        </div>
                    </div>`;
            }).join('');
        }

        function renderizarEstrellas(prom) {
            const llenas = Math.round(prom);
            return `<span class="estrellas">${'★'.repeat(llenas)}${'☆'.repeat(5 - llenas)}</span>`;
        }

        window.filtrarProductos = () => renderizarProductos(document.getElementById('busqueda').value);
        function refrescarTodo() {
            renderizarHeader();
            renderizarProductos(document.getElementById('busqueda')?.value || '');
        }

        // Marcar vendido
        window.marcarVendido = (id) => {
            if (!sesion) return;
            const prod = productos.find(p => p.id === id);
            if (prod && prod.vendedorId === sesion.id) {
                prod.vendido = !prod.vendido;
                persistir();
                refrescarTodo();
            }
        };

        // Denunciar
        window.denunciarProducto = (productoId) => {
            if (!sesion) return window.mostrarLogin();
            const producto = productos.find(p => p.id === productoId);
            if (!producto) return;
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>🚩 Denunciar producto</h2>
                        <p><strong>${escapar(producto.nombre)}</strong></p>
                        <div class="grupo-form"><label>Motivo de la denuncia</label><textarea id="motivoDenuncia" rows="3" placeholder="Describe el problema..."></textarea></div>
                        <button class="btn-formulario" id="btnEnviarDenuncia">Enviar denuncia</button>
                    </div>
                </div>`;
            document.getElementById('btnEnviarDenuncia').addEventListener('click', () => {
                const motivo = document.getElementById('motivoDenuncia').value.trim();
                if (!motivo) return alert('Escribe un motivo.');
                denuncias.push({ id: 'd_' + Date.now(), denuncianteId: sesion.id, denunciadoId: producto.vendedorId, productoId: producto.id, motivo });
                persistir();
                cerrarModal();
                alert('Denuncia enviada.');
            });
        };

        // Login / Registro
        window.mostrarLogin = () => {
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>🔐 Iniciar sesión</h2>
                        <form id="formLogin">
                            <div class="grupo-form"><label>Correo</label><input type="email" id="loginEmail" required></div>
                            <div class="grupo-form"><label>Contraseña</label><input type="password" id="loginPassword" required></div>
                            <p id="errorLogin" style="color:red;display:none;">Credenciales incorrectas</p>
                            <button type="submit" class="btn-formulario">Entrar</button>
                        </form>
                        <p class="enlace-modal">¿No tienes cuenta? <span onclick="mostrarRegistro()">Regístrate</span></p>
                    </div>
                </div>`;
            document.getElementById('formLogin').addEventListener('submit', e => {
                e.preventDefault();
                const email = document.getElementById('loginEmail').value.trim().toLowerCase();
                const pass = document.getElementById('loginPassword').value.trim();
                const usuario = usuarios.find(u => u.email === email && u.password === pass);
                if (usuario && !baneos.includes(usuario.id)) {
                    sesion = { id: usuario.id, nombre: usuario.nombre, email: usuario.email };
                    persistir();
                    cerrarModal();
                    refrescarTodo();
                } else {
                    document.getElementById('errorLogin').style.display = 'block';
                }
            });
        };

        window.mostrarRegistro = () => {
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>📝 Crear cuenta</h2>
                        <form id="formRegistro">
                            <div class="grupo-form"><label>Nombre</label><input type="text" id="regNombre" required></div>
                            <div class="grupo-form"><label>Correo</label><input type="email" id="regEmail" required></div>
                            <div class="grupo-form"><label>Contraseña</label><input type="password" id="regPassword" required></div>
                            <button type="submit" class="btn-formulario">Registrarse</button>
                        </form>
                    </div>`;
            document.getElementById('formRegistro').addEventListener('submit', e => {
                e.preventDefault();
                const nombre = document.getElementById('regNombre').value.trim();
                const email = document.getElementById('regEmail').value.trim().toLowerCase();
                const pass = document.getElementById('regPassword').value.trim();
                if (usuarios.some(u => u.email === email)) return alert('Correo ya registrado.');
                const nuevo = { id: 'u_' + Date.now(), nombre, email, password: pass, rol: nombre === 'Adam' ? 'admin' : 'normal' };
                usuarios.push(nuevo);
                sesion = { id: nuevo.id, nombre: nuevo.nombre, email: nuevo.email };
                if (nombre === 'Adam') vipCodes[nuevo.id] = { activeFrame: 'marco-dorado', unlockedFrames: ['marco-dorado'] };
                persistir();
                cerrarModal();
                refrescarTodo();
            });
        };

        window.cerrarSesion = () => { sesion = null; persistir(); refrescarTodo(); };

        // Publicar producto (con descripción)
        window.abrirFormularioPublicar = () => {
            if (!sesion) return window.mostrarLogin();
            if (baneos.includes(sesion.id)) return alert('Estás baneado.');
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>📦 Nuevo producto</h2>
                        <form id="formPublicar">
                            <div class="grupo-form"><label>Nombre</label><input type="text" id="nombreProd" required></div>
                            <div class="grupo-form"><label>Precio €</label><input type="number" id="precioProd" step="0.01" required></div>
                            <div class="grupo-form"><label>Descripción</label><textarea id="descProd" rows="3" placeholder="Describe el producto, estado, etc."></textarea></div>
                            <div class="grupo-form"><label>Imagen</label>
                                <div class="upload-wrapper">
                                    <label class="upload-btn" for="imagenProd">📁 Elegir</label>
                                    <input type="file" id="imagenProd" accept="image/*" style="display:none" onchange="vistaPrevia(this)">
                                    <span id="infoArchivo">Sin archivo</span>
                                </div>
                                <img id="previewImg" class="preview" style="border-radius:12px; width:100%; height:auto; max-height:200px;">
                            </div>
                            <button type="submit" class="btn-formulario">Publicar</button>
                        </form>
                    </div>`;
            document.getElementById('formPublicar').addEventListener('submit', e => {
                e.preventDefault();
                const nombre = document.getElementById('nombreProd').value.trim();
                const precio = parseFloat(document.getElementById('precioProd').value);
                const descripcion = document.getElementById('descProd').value.trim();
                const archivo = document.getElementById('imagenProd').files[0];
                const guardar = (img) => {
                    productos.unshift({ id: 'p_' + Date.now(), nombre, precio, descripcion, imagen: img || null, vendedorId: sesion.id, fecha: new Date().toISOString(), vendido: false });
                    persistir();
                    cerrarModal();
                    refrescarTodo();
                };
                if (archivo) { const r = new FileReader(); r.onload = e => guardar(e.target.result); r.readAsDataURL(archivo); }
                else guardar(null);
            });
        };

        window.vistaPrevia = (input) => {
            const archivo = input.files[0];
            const preview = document.getElementById('previewImg');
            const info = document.getElementById('infoArchivo');
            if (archivo) {
                info.textContent = archivo.name;
                const reader = new FileReader();
                reader.onload = e => { preview.src = e.target.result; preview.style.display = 'block'; };
                reader.readAsDataURL(archivo);
            } else { info.textContent = 'Sin archivo'; preview.style.display = 'none'; }
        };

        // Ver producto detallado
        window.verProducto = (productoId) => {
            const producto = productos.find(p => p.id === productoId);
            if (!producto) return;
            const vendedor = usuarios.find(u => u.id === producto.vendedorId);
            const nombreVendedor = vendedor?.nombre || 'Desconocido';
            const fotoVendedor = vendedor?.fotoPerfil || null;
            const rating = obtenerRating(producto.vendedorId);
            const esPropietario = sesion && producto.vendedorId === sesion.id;
            const vendido = producto.vendido;

            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal producto-detalle">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        ${producto.imagen ? `<img src="${producto.imagen}" class="img-detalle" alt="${escapar(producto.nombre)}">` : '<div style="font-size:5rem;">📷</div>'}
                        <h2>${escapar(producto.nombre)}</h2>
                        <div class="precio-grande">${Number(producto.precio).toFixed(2)} €</div>
                        ${vendido ? '<p style="color:green; font-weight:600;">✅ Vendido</p>' : ''}
                        <div class="descripcion">${escapar(producto.descripcion || 'Sin descripción.')}</div>
                        <div class="vendedor-detalle" onclick="verPerfil('${producto.vendedorId}')">
                            <img src="${fotoVendedor || ''}" onerror="this.style.display='none'" style="background:var(--azul);"> 
                            <div>
                                <strong>${escapar(nombreVendedor)}</strong><br>
                                ${renderizarEstrellas(rating.promedio)} (${rating.total})
                            </div>
                        </div>
                        <div class="acciones-detalle">
                            ${!esPropietario && !vendido ? `<button class="btn-chat" onclick="cerrarModal(); abrirChat('${producto.id}')">💬 Contactar</button>` : ''}
                            ${esPropietario && !vendido ? `<button class="btn-vender" onclick="marcarVendido('${producto.id}')">✅ Marcar vendido</button>` : ''}
                            ${!esPropietario && !vendido ? `<button class="btn-denuncia" onclick="denunciarProducto('${producto.id}')">🚩 Denunciar</button>` : ''}
                        </div>
                    </div>
                </div>`;
        };

        // Perfil de usuario (mismo que antes)
        window.verPerfil = (userId) => {
            const usuario = usuarios.find(u => u.id === userId);
            if (!usuario) return;
            const rating = obtenerRating(userId);
            const perfilVIP = obtenerPerfilVIP(userId);
            const productosUsuario = productos.filter(p => p.vendedorId === userId && !p.vendido);
            const foto = usuario.fotoPerfil || null;
            const inicial = usuario.nombre.charAt(0).toUpperCase();
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal perfil-modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <div class="avatar-grande" style="width:100px;height:100px;border-radius:50%;margin:0 auto;overflow:hidden;">${foto ? `<img src="${foto}" style="width:100%;height:100%;object-fit:cover;">` : inicial}</div>
                        <h2>${escapar(usuario.nombre)}</h2>
                        ${renderizarEstrellas(rating.promedio)} <span>(${rating.total} valoraciones)</span>
                        <p style="margin:10px 0;">Productos publicados: ${productosUsuario.length}</p>
                        <div style="display:flex;flex-wrap:wrap;gap:8px;justify-content:center;">
                            ${productosUsuario.map(p => `<div style="width:100px;height:100px;background:#f3f4f6;border-radius:8px;overflow:hidden;">${p.imagen ? `<img src="${p.imagen}" style="width:100%;height:100%;object-fit:cover;">` : '📷'}</div>`).join('')}
                        </div>
                    </div>
                </div>`;
        };

        // Ajustes (foto de perfil y marcos)
        window.abrirAjustes = () => {
            if (!sesion) return window.mostrarLogin();
            const user = usuarios.find(u => u.id === sesion.id);
            const perfilVIP = obtenerPerfilVIP(sesion.id);
            const unlocked = perfilVIP.unlockedFrames || [];
            const active = perfilVIP.activeFrame || null;
            const marcosHTML = Object.entries(MARCOS).map(([clave, datos]) => {
                const desbloqueado = unlocked.includes(clave);
                const seleccionado = active === clave;
                return `<div class="opcion-marco ${seleccionado ? 'seleccionado' : ''} ${!desbloqueado ? 'bloqueado' : ''}" onclick="${desbloqueado ? `seleccionarMarco('${clave}')` : ''}" title="${datos.nombre}"><span class="muestra">${datos.icono}</span></div>`;
            }).join('');
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>⚙️ Ajustes</h2>
                        <div class="grupo-form"><label>Foto de perfil</label><div class="upload-wrapper"><label class="upload-btn" for="fotoPerfil">📁 Cambiar foto</label><input type="file" id="fotoPerfil" accept="image/*" style="display:none" onchange="cambiarFotoPerfil(this)"></div></div>
                        <h3 style="margin-top:20px;">Marcos para productos</h3>
                        <div class="lista-marcos" style="display:flex; flex-wrap:wrap; gap:12px; margin-top:12px;">${marcosHTML}</div>
                        ${active ? `<p style="text-align:center;margin-top:10px;">Marco activo: ${MARCOS[active].nombre}</p>` : '<p style="text-align:center;">Ningún marco seleccionado</p>'}
                    </div>
                </div>`;
        };

        window.cambiarFotoPerfil = (input) => {
            const file = input.files[0];
            if (!file) return;
            const reader = new FileReader();
            reader.onload = (e) => {
                const user = usuarios.find(u => u.id === sesion.id);
                if (user) {
                    user.fotoPerfil = e.target.result;
                    persistir();
                    refrescarTodo();
                    cerrarModal();
                }
            };
            reader.readAsDataURL(file);
        };

        window.seleccionarMarco = (clave) => {
            if (!sesion) return;
            const perfil = vipCodes[sesion.id] || { activeFrame: null, unlockedFrames: [] };
            if (!perfil.unlockedFrames.includes(clave)) return;
            perfil.activeFrame = clave;
            vipCodes[sesion.id] = perfil;
            persistir();
            refrescarTodo();
            cerrarModal();
        };

        // Código VIP (solo "MERMELADADEFRESA" desbloquea marco fresa)
        window.abrirModalCodigoVIP = () => {
            if (!sesion) return window.mostrarLogin();
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>📦 Código VIP</h2>
                        <input type="text" id="codigoVIPInput" placeholder="Código secreto">
                        <button class="btn-formulario" onclick="canjearCodigo()">Canjear</button>
                        <p id="mensajeCodigo" style="text-align:center;margin-top:10px;"></p>
                    </div>
                </div>`;
        };

        window.canjeearCodigo = () => {
            const codigo = document.getElementById('codigoVIPInput').value.trim().toUpperCase();
            if (codigo === 'MERMELADADEFRESA') {
                const perfil = vipCodes[sesion.id] || { activeFrame: null, unlockedFrames: [] };
                if (!perfil.unlockedFrames.includes('marco-fresa')) {
                    perfil.unlockedFrames.push('marco-fresa');
                    perfil.activeFrame = 'marco-fresa';
                    vipCodes[sesion.id] = perfil;
                    persistir();
                    document.getElementById('mensajeCodigo').textContent = '✅ ¡Código canjeado! Marco Fresa activado.';
                    setTimeout(() => { cerrarModal(); refrescarTodo(); }, 1000);
                } else {
                    document.getElementById('mensajeCodigo').textContent = 'Ya tienes el marco Fresa.';
                }
            } else {
                document.getElementById('mensajeCodigo').textContent = '❌ Código incorrecto.';
            }
        };

        // Admin panel (simplificado)
        window.abrirPanelAdmin = () => {
            if (!sesion || !esAdmin(usuarios.find(u => u.id === sesion.id))) return;
            const denunciasHTML = denuncias.length === 0 ? '<p>No hay denuncias.</p>' : denuncias.map(d => {
                const denunciante = usuarios.find(u => u.id === d.denuncianteId);
                const denunciado = usuarios.find(u => u.id === d.denunciadoId);
                const prod = productos.find(p => p.id === d.productoId);
                return `<div style="border:1px solid #e5e7eb;border-radius:12px;padding:12px;margin-bottom:8px;">
                    <strong>Producto:</strong> ${escapar(prod?.nombre || 'Eliminado')}<br>
                    <strong>Denunciante:</strong> ${escapar(denunciante?.nombre || '?')}<br>
                    <strong>Denunciado:</strong> ${escapar(denunciado?.nombre || '?')}<br>
                    <strong>Motivo:</strong> ${escapar(d.motivo)}<br>
                    <button onclick="banearUsuario('${d.denunciadoId}')" style="margin-top:6px;background:#fee2e2;border:none;padding:6px 12px;border-radius:20px;cursor:pointer;">🔨 Banear</button>
                    <button onclick="desbanearUsuario('${d.denunciadoId}')" style="margin-left:6px;background:#d1fae5;border:none;padding:6px 12px;border-radius:20px;cursor:pointer;">✅ Desbanear</button>
                </div>`;
            }).join('');
            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal" style="max-width:600px;">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <h2>🛡️ Panel Admin</h2>
                        <h3>Denuncias</h3> ${denunciasHTML}
                        <h3>Baneados</h3> <p>${baneos.length ? baneos.map(id => { const u = usuarios.find(x => x.id === id); return u ? escapar(u.nombre) : id; }).join(', ') : 'Ninguno'}</p>
                    </div>
                </div>`;
        };

        window.banearUsuario = (userId) => { if (!baneos.includes(userId)) baneos.push(userId); persistir(); alert('Usuario baneado.'); cerrarModal(); refrescarTodo(); };
        window.desbanearUsuario = (userId) => { baneos = baneos.filter(id => id !== userId); persistir(); alert('Usuario desbaneado.'); cerrarModal(); refrescarTodo(); };

        // Chat (versión resumida)
        window.abrirChat = (productoId) => {
            if (!sesion) return window.mostrarLogin();
            const producto = productos.find(p => p.id === productoId);
            if (!producto || producto.vendedorId === sesion.id) return;
            const vendedor = usuarios.find(u => u.id === producto.vendedorId);
            const nombreVendedor = vendedor?.nombre || 'Desconocido';
            const fotoVendedor = vendedor?.fotoPerfil;
            const chatId = [sesion.id, producto.vendedorId].sort().join('_') + '_' + producto.id;
            if (!conversaciones[chatId]) conversaciones[chatId] = [];
            const puedeValorar = usuarioPuedeValorar(producto.vendedorId);
            const miValoracion = ratings[producto.vendedorId]?.users?.[sesion.id] || 0;

            contenedorModal.innerHTML = `
                <div class="overlay" onclick="if(event.target===this) cerrarModal()">
                    <div class="modal chat-modal">
                        <button class="modal-cerrar" onclick="cerrarModal()">✕</button>
                        <div class="chat-top">
                            <div class="chat-avatar">${fotoVendedor ? `<img src="${fotoVendedor}" style="width:100%;height:100%;border-radius:50%;">` : nombreVendedor.charAt(0)}</div>
                            <div><strong>${escapar(nombreVendedor)}</strong><br><small>${escapar(producto.nombre)} · ${producto.precio}€</small></div>
                        </div>
                        <div class="mensajes" id="chatMensajes">${renderMensajes(chatId)}</div>
                        <div class="chat-input">
                            <input id="inputMensaje" placeholder="Mensaje...">
                            <button onclick="enviarMensaje('${chatId}')">Enviar</button>
                        </div>
                        <div class="valoracion">
                            <p>⭐ Valorar a ${escapar(nombreVendedor)}</p>
                            <div class="estrellas-valorar" id="estrellasValorar">
                                ${[1,2,3,4,5].map(i => `<span class="estrella ${i <= miValoracion ? 'activa' : ''}" onclick="calificarVendedor('${producto.vendedorId}', ${i})">★</span>`).join('')}
                            </div>
                        </div>
                    </div>
                </div>`;
        };

        function renderMensajes(chatId) {
            const mensajes = conversaciones[chatId] || [];
            return mensajes.length === 0 ? '<p style="text-align:center;">Sin mensajes</p>' : mensajes.map(m => `<div class="bubble ${m.remitente === sesion.id ? 'enviado' : 'recibido'}">${escapar(m.texto)}</div>`).join('');
        }

        window.enviarMensaje = (chatId) => {
            const input = document.getElementById('inputMensaje');
            const texto = input.value.trim();
            if (!texto) return;
            conversaciones[chatId].push({ remitente: sesion.id, texto, fecha: Date.now() });
            persistir();
            document.getElementById('chatMensajes').innerHTML = renderMensajes(chatId);
            input.value = '';
        };

        window.calificarVendedor = (vendedorId, estrellas) => {
            if (!usuarioPuedeValorar(vendedorId)) return;
            valorarVendedor(vendedorId, estrellas);
            cerrarModal();
            refrescarTodo();
            alert('¡Gracias por tu valoración!');
        };

        window.cerrarModal = () => document.getElementById('contenedorModal').innerHTML = '';
        refrescarTodo();
    })();
</script>
</body>
</html>
