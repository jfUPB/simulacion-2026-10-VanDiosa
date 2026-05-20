# Unidad 8

## Bitácora de proceso de aprendizaje
### Actividad 01   
✍️Indica qué herramienta te interesa explorar y por qué    
Me interesa explorar los geometry nodes de blender, porque durante el semestre estuvimos usando p5 (codigo), y siento que en blender podria lograr algo parecido a alguna de las unidades pero usando su motor de renderizado, materiales y profundidad 3D

✍️Explica qué relación tiene esa herramienta con tu línea de énfasis o interés profesional     
Como estudiante de IDED, los efectos visuales y contenidos de arte generativos son de mi interes; y blender es como el top de la industria, profundizar el nos geometry nodes me permitiria crear no solo dibujus si no sistemas, herramientas, estructuras, objetos que sean automaticos y dinamicos

✍️Busca 2 o 3 referentes realizados con esa herramienta o cercanos a su ecosistema    
[🔗](https://www.youtube.com/watch?v=H3PqfKscepg&t=919s)
<img width="596" height="259" alt="image" src="https://github.com/user-attachments/assets/268810f2-15d2-4ac5-9584-b52fd4a3b963" />

[🔗](https://www.youtube.com/watch?v=DfLIDHAQFDM)
<img width="289" height="271" alt="image" src="https://github.com/user-attachments/assets/426421b3-9eb9-4aa3-99ee-f8521e61f165" />

✍️Explica qué te interesa de esos referentes


✍️Propón uno o dos posibles contextos profesionales para tu pieza final

## Bitácora de aplicación 
### Actividad 05: Visualizer   
✍️Herramienta elegida     
Elegi BLENDER, ya que como estudiante de IDED enfocada en la linea de animacion, este programa responde a parte de mis objetivos profesionales. Elegi BLENDER para mostrar un sistema matematico que antes hicimos en 2D en un entorno 3D, con luces, materiales y acabados con mayor profundidad atmosferica

✍️Sistema transferido   
Busque transferir el principio de comportamiento colectivo. En lugar de usar codigo para simular un campo de flujo y comportamiento de grupos en un plano bidimensional, use el sistema de nodos de Blender. El sistema genera una forma de disco en 3D con miles de partculas que se mueven e interactuan usando un analisis de la canción; la musica (especificamente los graves del bajo y el bombo) es la que genera el movimiento que empuja las bolitas para formar esa especie de onda que sube y rebota de manera organica

✍️Contexto profesional concreto     
Me imagine esta pieza como algo direccionado a la industria de entretenimineot y marketing, ya que no se queda solo en un video musical tradicional, si no que podria ser un visualizer para promocional bafles o algun hardware de sonido. Considero que sirve para poder mostrar el poder, la fidelidad de los graves de los equipos de audio, de una forma mas atractia y moderna

✍️Concepto visual    
La idea principal que tuve fue no hacer un fondo de un MV que fuera meramente decorativo, sino simular el comportamiento fisico de un parlante real, los patrones de las ondas sonoras. El disco simula la rejilla de un bafle que reacciona con mayor magnitud ante los impactos graves. Escogi colores que simularan un poco la iluminacion led de los bafles, y un suelo reflejante para aportar a esa sensacion de tridimensionalidad 

✍️Referencias    
<img width="1920" height="1080" alt="MoodBoard" src="https://github.com/user-attachments/assets/23c80f42-a591-4f67-8fda-6376fac1a39d" />

✍️Bocetos     
<img width="1920" height="1080" alt="BOCETO" src="https://github.com/user-attachments/assets/aafa5d8c-bfa3-43b5-95e3-476809dc97ea" />


✍️Explicación de la transferencia     
En p5.js creabamos una simulación de movimiento usando fuerzas para controlar particulas y agentes autonomos, experimentando con flow fields (campos de flujo), y flocking (comportamiento de cardumenes)

Para transferir esto a Blender, cambie las lineas de codigo por Geometry Nodes. El principio que me traje del curso fue el comportamiento colectivo (flocking): el disco genera miles de particulas que no se mueven de forma aislada, sino que actuan como un grupo compacto. La musica (los graves del bajo y el bombo) funciona como la fuerza que activa la simulación, haciendo que todo el conjunto de agentes autonomos salte y rebote al mismo tiempo, recreando el movimiento fisico de la rejilla de un bafle real

✍️Mapa de decisiones     
+ Logica (Sistema): Decidi dejar el audio aislado para que el sistema reaccionara solo a las frecuencias mas bajas (graves: bajo y bateria). Esto evita que el movimiento de las bolitas sea caotico y hace que el rebote sea mas limpio

+ Tecnica (Herramienta): Elegi renderizar con el motor Blender Eevee para optimizar tiempos y configure la salida en una secuencia de imagenes fijas en formato PNG, asegurando que no se perdiera el proceso si el programa se llegaba a cerrar

+ Visualidad (Estetica): Cambie la gestion de color del render al perfil Filmic (High Contrast). Esto fue clave porque los colores neon tipo led dejaron de verse lavados o quemados, logrando un contraste con el negro puro del fondo y el reflejo del piso

+ Presentación (Salida): Use el editor de video de Blender (Video Sequencer) para armar la secuencia final, forzando la salida a formato .mp4 con audio en codec AAC para asegurar que la musica sonara fuerte y sincronizada en cualquier lado

<img width="1831" height="855" alt="MAPA DE DECISIONES" src="https://github.com/user-attachments/assets/0aafd557-5627-474e-97e4-e2aa053914b6" />


🤖Evidencia del uso de IA     
La IA la use para solucionar problemas con el redimiento tanto del viewport como a la hora de exportar, ya que, en el primer intento de exportar cada frame se demoraba mucho, y al ser 3711 necesitaba mas eficiencia. Me recomento usar EEVEE, el perfil de color Filmic para destacar los colores y evitar que se quemaran (vieran muy blancos), me ayudo con la configuracion de codificacion (el default hacia que el video saliera como .mkv, y yo queria algo mas global como .mp4), ademas el video salia mudo y no tenia el conocimiento de como activar el audio

Las decisiones del concepto de parlante, centar el analisis de audio en los bajos, los colores, y la seleccion de la musica, fueron totalmente mias

🌟Código, archivo, proyecto o documentación técnica según la herramienta      
Geometry Nodes:     
<img width="959" height="503" alt="GEOMETRYNODES" src="https://github.com/user-attachments/assets/662fad38-afd1-4d0e-a832-75e91b777941" />
Shader Bolitas:     
<img width="572" height="275" alt="SHADERBOLITAS" src="https://github.com/user-attachments/assets/e7132834-4b32-4d80-900d-b377e3be8778" />
Shader Suelo:    
<img width="571" height="275" alt="SHADERSUELO" src="https://github.com/user-attachments/assets/d266433b-f850-4fe4-9e33-6f9f9c65cd9a" />
Compositing:    
<img width="410" height="328" alt="COMPOSITING" src="https://github.com/user-attachments/assets/6c944c58-26a5-4313-af09-fa4d70dcb06f" />

📸Registro visual de la pieza    
Proceso:   
<img width="479,5" height="253" alt="P1" src="https://github.com/user-attachments/assets/6011a9ef-c9cc-4e92-975d-856f61966018" />
<img width="479,5" height="253" alt="P2" src="https://github.com/user-attachments/assets/b2e7074d-2a89-456e-b627-16cc8c443dcf" />
<img width="479,5" height="252" alt="P3" src="https://github.com/user-attachments/assets/59d1f87a-e791-4257-8aca-fb3f79780d8e" />
<img width="478,5" height="251" alt="P5" src="https://github.com/user-attachments/assets/2fb108df-b2a9-400a-be8c-5eb4c733c103" />
<img width="479,5" height="251,5" alt="P7" src="https://github.com/user-attachments/assets/6633af1d-f43c-46db-ae9e-fe6da0cfa286" />

[Final](https://www.youtube.com/watch?v=FYGWzzakdHw)
<img width="1920" height="1080" alt="final" src="https://github.com/user-attachments/assets/4cc43bfc-3eea-478f-acb1-0bbdec79dd60" />



## Bitácora de reflexión
