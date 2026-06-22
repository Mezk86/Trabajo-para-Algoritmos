# Trabajo-para-Algoritmos

<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RetroVerse - Carga de Inventario</title>
    <style>
        /* --- ESTILOS GLOBALES --- */
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }

        body {
            background-color: #fbfaf7;
            color: #2e2b2a;
            display: flex;
            justify-content: center;
            align-items: center;
            min-height: 100vh;
            padding: 20px;
        }

        /* --- CONTENEDOR PRINCIPAL --- */
        .form-container {
            background-color: #ffffff;
            width: 100%;
            max-width: 650px;
            border-radius: 8px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.08);
            overflow: hidden;
            border: 1px solid #dcd5cc;
        }

        /* --- ENCABEZADO TÉCNICO --- */
        .form-header {
            background-color: #1a2c3b;
            color: #ffffff;
            padding: 25px 30px;
            border-bottom: 4px solid #c07a50;
        }

        .form-header h1 {
            font-family: 'Georgia', serif;
            font-size: 20px;
            font-weight: normal;
            letter-spacing: 0.5px;
            margin-bottom: 5px;
        }

        .form-header p {
            color: #d1e0ec;
            font-size: 13px;
            text-transform: uppercase;
            letter-spacing: 1px;
        }

        /* --- CUERPO DEL FORMULARIO --- */
        form {
            padding: 30px;
        }

        .form-group {
            margin-bottom: 20px;
        }

        .form-group.row-mixed {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        label {
            display: block;
            font-size: 13.5px;
            font-weight: 600;
            color: #1a2c3b;
            margin-bottom: 8px;
        }

        label span.technical-info {
            font-size: 11px;
            color: #7a6e67;
            font-weight: normal;
            font-family: monospace;
        }

        /* --- INPUTS Y CONTROLES --- */
        input[type="text"],
        input[type="number"],
        select {
            width: 100%;
            padding: 10px 12px;
            border: 1px solid #dcd5cc;
            border-radius: 4px;
            background-color: #fdfcfb;
            font-size: 14.5px;
            color: #2e2b2a;
            transition: all 0.2s ease;
        }

        input:focus, select:focus {
            outline: none;
            border-color: #1a2c3b;
            background-color: #ffffff;
            box-shadow: 0 0 0 3px rgba(26, 44, 59, 0.1);
        }

        /* --- SUB-REGISTRO ANIDADO (FECHA) --- */
        .nested-fieldset {
            border: 1px dashed #c07a50;
            background-color: #f7f4ed;
            padding: 15px 20px;
            border-radius: 6px;
            margin-top: 5px;
        }

        .nested-fieldset legend {
            font-size: 12px;
            font-weight: bold;
            color: #c07a50;
            background-color: #ffffff;
            padding: 2px 8px;
            border: 1px solid #dcd5cc;
            border-radius: 4px;
            text-transform: uppercase;
        }

        .date-grid {
            display: grid;
            grid-template-columns: 1fr 1fr 1.2fr;
            gap: 12px;
        }

        /* --- BOTONES Y MENSAJES --- */
        .btn-submit {
            background-color: #c07a50;
            color: #ffffff;
            border: none;
            width: 100%;
            padding: 13px;
            font-size: 15px;
            font-weight: bold;
            border-radius: 4px;
            cursor: pointer;
            transition: background-color 0.2s;
            margin-top: 10px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        .btn-submit:hover {
            background-color: #a6643b;
        }

        .alert-box {
            margin-top: 20px;
            padding: 12px 15px;
            border-radius: 4px;
            font-size: 13.5px;
            display: none;
        }

        .alert-box.success {
            background-color: #e6f3ed;
            color: #1e6b45;
            border: 1px solid #ccdcd5;
        }

        .alert-box.error {
            background-color: #fcebe9;
            color: #ad2313;
            border: 1px solid #f7c9c4;
        }
    </style>
</head>
<body>

    <div class="form-container">
        <div class="form-header">
            <h1>SISTEMA DE GESTIÓN RETROVERSE</h1>
            <p>Alta de Registro Interno: PRODUCTO_RETRO</p>
        </div>

        <form id="retroForm" novalidate>
            
            <div class="form-group">
                <label for="win_7">Clave Única Identificadora <span class="technical-info">[win_7 : AN(15)]</span></label>
                <input type="text" id="win_7" placeholder="Ej: WIN.7-1985-001" maxlength="15" required>
            </div>

            <div class="form-group">
                <label for="denominacion">Denominación del Artículo <span class="technical-info">[denominacion : AN(60)]</span></label>
                <input type="text" id="denominacion" placeholder="Ej: Sega Genesis Core System Model 1" maxlength="60" required>
            </div>

            <div class="form-group">
                <label for="precio_base">Precio Base <span class="technical-info">[precio_base : Real]</span></label>
                <input type="number" id="precio_base" step="0.01" min="0" placeholder="0.00" required>
            </div>

            <div class="form-group row-mixed">
                <div>
                    <label for="estado_operativo">Estado Operativo <span class="technical-info">[Conjunto]</span></label>
                    <select id="estado_operativo" required>
                        <option value="" disabled selected>Seleccione...</option>
                        <option value="Funciona">Funciona</option>
                        <option value="Repuesto">Repuesto</option>
                    </select>
                </div>
                <div>
                    <label for="categoria">Categoría <span class="technical-info">[Conjunto]</span></label>
                    <select id="categoria" required>
                        <option value="" disabled selected>Seleccione...</option>
                        <option value="Consolas">Consolas</option>
                        <option value="Juegos">Juegos</option>
                        <option value="Computación">Computación</option>
                    </select>
                </div>
            </div>

            <div class="form-group">
                <fieldset class="nested-fieldset">
                    <legend>fecha_fabricacion : Registro Continente</legend>
                    <div class="date-grid">
                        <div>
                            <label for="dia" style="font-size: 12px; margin-bottom: 4px;">Día <span class="technical-info">[Contenido]</span></label>
                            <input type="number" id="dia" min="1" max="31" placeholder="DD" required>
                        </div>
                        <div>
                            <label for="mes" style="font-size: 12px; margin-bottom: 4px;">Mes <span class="technical-info">[Contenido]</span></label>
                            <input type="number" id="mes" min="1" max="12" placeholder="MM" required>
                        </div>
                        <div>
                            <label for="anio" style="font-size: 12px; margin-bottom: 4px;">Año <span class="technical-info">[Contenido]</span></label>
                            <input type="number" id="anio" min="1970" max="2005" placeholder="AAAA" required>
                        </div>
                    </div>
                </fieldset>
            </div>

            <button type="submit" class="btn-submit">Guardar Registro en Archivo</button>

            <div id="alertBox" class="alert-box"></div>

        </form>
    </div>

    <script>
        document.getElementById('retroForm').addEventListener('submit', function(event) {
            event.preventDefault(); // Detener el envío convencional

            const alertBox = document.getElementById('alertBox');
            alertBox.style.display = 'none';
            alertBox.className = 'alert-box';

            // 1. Captura de Valores
            const win7 = document.getElementById('win_7').value.trim();
            const denominacion = document.getElementById('denominacion').value.trim();
            const precioBase = parseFloat(document.getElementById('precio_base').value);
            const estadoOperativo = document.getElementById('estado_operativo').value;
            const categoria = document.getElementById('categoria').value;
            
            // Sub-registro
            const dia = parseInt(document.getElementById('dia').value);
            const mes = parseInt(document.getElementById('mes').value);
            const anio = parseInt(document.getElementById('anio').value);

            // 2. Validación de consistencia lógica
            if (!win7 || !denominacion || isNaN(precioBase) || !estadoOperativo || !categoria || isNaN(dia) || isNaN(mes) || isNaN(anio)) {
                showFeedback('Error: Todos los campos del registro son obligatorios.', 'error');
                return;
            }

            if (precioBase < 0) {
                showFeedback('Error: El precio_base no puede ser un valor negativo.', 'error');
                return;
            }

            // Validación semántica/congruente de la Fecha
            if (!validarFechaConsistente(dia, mes, anio)) {
                showFeedback('Error: La fecha de fabricación ingresada no es válida o es inconsistente.', 'error');
                return;
            }

            // 3. Simulación de empaquetado del Registro Heterogéneo exitoso
            const registroProductoRetro = {
                win_7: win7,
                denominacion: denominacion,
                precio_base: precioBase,
                estado_operativo: estadoOperativo,
                categoria: categoria,
                fecha_fabricacion: {
                    dia: dia,
                    mes: mes,
                    año: anio
                }
            };

            console.log("Estructura de memoria interna grabada:", registroProductoRetro);
            showFeedback(`Registro grabado con éxito en el ambiente. Clave activa: ${registroProductoRetro.win_7}`, 'success');
            
            // Opcional: limpiar formulario tras el guardado
            document.getElementById('retroForm').reset();
        });

        // Función auxiliar para validar fechas reales
        function validarFechaConsistente(d, m, a) {
            if (m < 1 || m > 12) return false;
            if (d < 1 || d > 31) return false;
            
            // Validar meses con 30 días
            if ((m === 4 || m === 6 || m === 9 || m === 11) && d > 30) return false;
            
            // Validar Febrero (incluyendo años bisiestos del entorno retro)
            if (m === 2) {
                const esBisiesto = (a % 4 === 0 && (a % 100 !== 0 || a % 400 === 0));
                if (esBisiesto && d > 29) return false;
                if (!esBisiesto && d > 28) return false;
            }
            return true;
        }

        function showFeedback(message, type) {
            const alertBox = document.getElementById('alertBox');
            alertBox.textContent = message;
            alertBox.classList.add(type);
            alertBox.style.display = 'block';
        }
    </script>
</body>
</html>
