# Treasure Moment
TreasureMoment es una app desarrollada en SwiftUI que permite a los usuarios importar fotos y almacenarlas junto con su ubicación geográfica. Los usuarios pueden ver las fotos en un mapa, y cada foto se asocia con las coordenadas de la ubicación en la que fue hecha. Rastrea la ubicación en tiempo real, guarda la foto con nombre, visualiza el detalle. Basada en todo lo aprendido en mis proyectos anteriores. 
## Características
### Retos como:

### 1. **Correcta visualización de la imagen en la lista:**
Uno de los retos más complicados fue garantizar que las imágenes seleccionadas se mostraran correctamente en la interfaz, tanto en la lista de fotos como en el mapa. La dificultad radicaba en que, al trabajar con imágenes almacenadas como datos (Data), tuve que asegurarme de que las imágenes se deserializaran y se presentaran adecuadamente en la vista. Además, era importante manejar correctamente el redibujado de la vista cuando se seleccionaba una nueva imagen.

Solución:
Implementé un sistema para convertir los datos de la imagen de vuelta a un objeto UIImage y la visualización se realizó de forma asíncrona para evitar bloqueos en la interfaz. Usé Image(uiImage: UIImage) y el modificador .resizable() para garantizar que las imágenes se mostraran de forma escalable y adecuada dentro de sus respectivos contenedores.

### 2. **Ubicación de los botones "Start Tracking Location" y "Read Location":**
Organizar la interfaz para incluir los botones de "Start Tracking Location" y "Read Location" de manera que fueran accesibles y estéticamente agradables fue un desafío. Los botones necesitaban estar en una ubicación intuitiva, pero también debía asegurarme de que no interfieran con otras funcionalidades de la app, como la visualización de la imagen.

Solución:
Colocarlos dentro de una barra de herramientas secundarias (ToolbarItemGroup) en la parte superior, asegurando que siempre estuvieran visibles, pero de manera no intrusiva. Usé una interfaz de MapReader para permitir una mejor interacción entre el mapa y los controles de localización.

### 3: **Visualizar la última localización disponible al importar la imagen:**
Otro reto fue asociar la ubicación geográfica con cada foto de manera correcta. Cuando se importaba una imagen, necesitaba asociar las coordenadas de la última localización disponible del dispositivo a la foto, pero sólo si ya estaba disponible. Si la localización no estaba lista en ese momento, la app debía manejar la visualización de una ubicación predeterminada y, una vez que la localización real estuviera disponible, actualizarla automáticamente.

Solución:
Implementé un sistema de seguimiento de ubicación con CLLocationManager, y utilicé LocationFetcher para obtener la última ubicación conocida al importar una imagen. Si la ubicación no estaba disponible en el momento de la importación, se utilizaba una ubicación predeterminada para mostrar en el mapa y, en cuanto la localización real estuviera disponible, se actualizaba tanto en la base de datos como en la vista del mapa.
