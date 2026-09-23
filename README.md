# Colmena del Macizo 360°

Recorrido web interactivo construido con fotografías panorámicas equirectangulares de Colmena del Macizo. El visitante puede explorar cada espacio en 360°, acercar o alejar la vista, usar pantalla completa y desplazarse entre escenas mediante hotspots.



Para inspeccionar la versión local, ejecuta desde la raíz del proyecto:

```powershell
python -m http.server 4173 --directory dist
```

Después abre [http://127.0.0.1:4173](http://127.0.0.1:4173) en el navegador.

> El proyecto debe servirse mediante HTTP. Abrir `dist/index.html` directamente puede impedir que el navegador cargue correctamente las imágenes panorámicas.

## Funcionalidades

- Visor panorámico 360° con arrastre mediante mouse o pantalla táctil.
- Zoom con rueda, gestos y botones en pantalla.
- Rotación automática después de un periodo de inactividad.
- Modo de pantalla completa.
- Orientación mediante el movimiento del teléfono en dispositivos compatibles.
- Hotspot en la escena principal para ingresar a la escena **Colmena 360°**.
- Hotspot de retorno hacia la escena principal.
- Interfaz adaptable a computadores y dispositivos móviles.
- Estados de carga y mensajes de error en español.
- Controles con etiquetas accesibles para lectores de pantalla.

## Escenas

| Identificador | Archivo | Descripción |
| --- | --- | --- |
| `principal` | `assets/colmenadelmacizo.JPG` | Escena inicial del recorrido. |
| `colmena` | `assets/colmena.JPG` | Segunda escena, accesible desde el hotspot de la escena principal. |


## Tecnología

El sitio es estático y no necesita un proceso de compilación. Utiliza:

- HTML, CSS y JavaScript.
- [Pannellum 2.5.6](https://pannellum.org/) para renderizar las panorámicas equirectangulares.
- jsDelivr para cargar los archivos CSS y JavaScript de Pannellum.

Debido a que el visor se carga desde un CDN, la experiencia requiere conexión a internet aunque se ejecute en el servidor local.

## Modificar los hotspots

La configuración se encuentra dentro del objeto `scenes` en `dist/index.html`. Cada hotspot de navegación utiliza esta estructura:

```javascript
{
  pitch: -19,
  yaw: 43,
  type: 'scene',
  text: 'Entrar a Colmena 360°',
  sceneId: 'colmena',
  targetPitch: -6,
  targetYaw: 0,
  cssClass: 'scene-corner-hotspot'
}
```

- `pitch`: posición vertical del hotspot.
- `yaw`: posición horizontal del hotspot.
- `sceneId`: escena que se abrirá al seleccionarlo.
- `targetPitch` y `targetYaw`: orientación inicial al entrar en la escena de destino.
- `text`: etiqueta visible y accesible del hotspot.

## Agregar otra escena

1. Copia la fotografía equirectangular en `assets/`.
2. Agrega una entrada nueva dentro de `scenes` en `index.html`.
3. Añade un hotspot con `type: 'scene'` y el `sceneId` correspondiente.
4. Recarga la página en el servidor local y comprueba la transición y la orientación inicial.

Para obtener una proyección correcta, la imagen panorámica debe tener una relación de aspecto **2:1**; por ejemplo, `8000 × 4000 px`.

