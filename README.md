<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🎁 Rompecabezas - Emma y Manu</title>

    <link rel="stylesheet" href="style.css">
</head>

<body>

<div class="contenedor">

    <h1>🎁 Descubre la sorpresa 🎁</h1>

    <p class="subtitulo">
        Completa el rompecabezas para descubrir el mensaje.
    </p>

    <div id="tablero"></div>

    <div id="progreso">
        <span id="contador">0</span> / 64 piezas
    </div>

    <div id="mensajeFinal">

        <h2>🎉 ¡Feliz cumpleaños, Emma y Manu! 🎂</h2>

        <p>
            Espero que disfruten esta sorpresa.
        </p>

        <button id="reiniciar">
            Volver a jugar
        </button>

    </div>

</div>

<script src="script.js"></script>

</body>
</html>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    background: linear-gradient(180deg, #6bb8ff 0%, #cdeeff 100%);
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    color: #333;
}

.contenedor {
    width: min(96vw, 900px);
    padding: 20px;
    text-align: center;
}

h1 {
    margin-bottom: 10px;
}

.subtitulo {
    margin-bottom: 20px;
    color: #555;
}

#tablero {
    width: min(90vw, 640px);
    height: min(90vw, 640px);

    margin: auto;

    display: grid;

    grid-template-columns: repeat(8, 1fr);
    grid-template-rows: repeat(8, 1fr);

    gap: 2px;

    background: white;

    border-radius: 12px;

    padding: 6px;

    box-shadow: 0 10px 25px rgba(0,0,0,.20);
}

.pieza {
    background-size: 800% 800%;
    background-repeat: no-repeat;
    border-radius: 3px;
    cursor: pointer;
    opacity: 0;
    transition: opacity .35s;
}

.visible {
    opacity: 1;
}

#progreso {
    margin-top: 20px;
    font-size: 24px;
    font-weight: bold;
}

#mensajeFinal {

    display: none;

    margin-top: 30px;

    background: white;

    padding: 25px;

    border-radius: 15px;

    box-shadow: 0 10px 25px rgba(0,0,0,.20);

}

#mensajeFinal h2{
    color:#d62828;
    margin-bottom:15px;
}

#reiniciar{

    margin-top:20px;

    padding:14px 28px;

    border:none;

    border-radius:10px;

    background:#ff7b00;

    color:white;

    font-size:18px;

    cursor:pointer;

}

#reiniciar:hover{

    background:#ff5d00;

}
const tablero = document.getElementById("tablero");
const contador = document.getElementById("contador");
const mensajeFinal = document.getElementById("mensajeFinal");
const reiniciar = document.getElementById("reiniciar");

const filas = 8;
const columnas = 8;
const total = filas * columnas;

let piezasMostradas = 0;

const imagen = "foto.jpg";

function crearTablero() {

    tablero.innerHTML = "";
    piezasMostradas = 0;
    contador.textContent = "0";
    mensajeFinal.style.display = "none";

    for (let fila = 0; fila < filas; fila++) {

        for (let columna = 0; columna < columnas; columna++) {

            const pieza = document.createElement("div");

            pieza.className = "pieza";

            pieza.style.backgroundImage = `url(${imagen})`;

            pieza.style.backgroundSize = `${columnas * 100}% ${filas * 100}%`;

            pieza.style.backgroundPosition =
                `${(columna * 100) / (columnas - 1)}% ${(fila * 100) / (filas - 1)}%`;

            tablero.appendChild(pieza);

        }
    }

}

crearTablero();

document.body.addEventListener("click", () => {

    if (piezasMostradas >= total)
        return;

    tablero.children[piezasMostradas].classList.add("visible");

    piezasMostradas++;

    contador.textContent = piezasMostradas;

    if (piezasMostradas === total) {

        mensajeFinal.style.display = "block";

    }

});

reiniciar.addEventListener("click", crearTablero);
