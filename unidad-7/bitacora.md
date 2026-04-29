# Unidad 7

## Bitácora de proceso de aprendizaje   
### Actividad 01   
📤En base al trabajo de [Ji Lee](https://pleaseenjoy.com/#/word-as-image/), responder lo planteado:   

✍️Análisis de ejemplos de Ji Lee   
  <img width="202" height="202" alt="ACT1 1 1" src="https://github.com/user-attachments/assets/44a60112-9c3c-453e-b87b-9fb91456abde" />
  La letra "C" actua como una boca que se come al resto de los caracteres. El caos de las letras internas representa la acumulación y el desorden, dos caracteristicas propias del consumo excesivo   
  <img width="200" height="201" alt="ACT1 1 2" src="https://github.com/user-attachments/assets/11034e01-d798-4682-9b11-2d7f3ae28c6f" />
  Utiliza la jerarquia de escala. La letra "I" central crecio desmedidamente hasta aplastar a las demas, buscando simbolizar como un sistema prioriza un elemento sobre la base de la estructura   
  <img width="198" height="200" alt="ACT1 1 3" src="https://github.com/user-attachments/assets/68393838-3335-416e-beb5-87aea75ef890" />
  Al separar la "G" y colocarla debajo, Ji Lee hace una referencia historica y anatomica a la oreja cortada del artista, es como si el nombre fuera un retrato   

❓¿Cómo la manipulación tipográfica refuerza el significado?   
La manipulación tipografica no es solamente decorativa, si no funcional. Ji Lee usa:   
+ La escala para mostrar poder o presion
+ El desplazamiento para sugerir eventos o acciones (como caer o amputar)
+ La sustitución de partes de letras por formas geometricas (montañas, manecillas de reloj) para anclar la palabra a un objeto
Ji Lee busca reforzar el significado porque obliga al ojo a no solo leer la palabra, sino a interpretarla como un objeto con peso, historia y contexto

✍️Propuestas de palabras propias (Representación Visual)   
<img width="2480" height="3508" alt="ACT1 DIBUJOS" src="https://github.com/user-attachments/assets/3a96d473-bc7f-4523-84fb-a04d77d260e0" />

+ FRAGIL-> Una tipografia con grietas. Las letras "F-R--G-I-L" estan fijas y muy apretadas entre si, dejando un hueco muy exacto para la letra "A". La letra "A" se encuentra aislada y caida, esperando que alguien la coloque

+ DERRETIR-> Letras cuadradas y gruesas, de color celeste, para dar a entender que son hielos. El fondo muestra particulas cayendo (nieve). En el escenario hay un sol el cual segun su cercania va derritiendo mas rapido o mas lento la palabra

+ SOL-> El escenario es un cielo azul oscuro. Las letras "S--L" estan camufladas con el color del fondo, pero aun asi tienen un espacio entre ellas. La letra "O" es un circulo brillante y calido que actaa como un sol, iluminando lo que tiene cerca

✍️Palabra seleccionada   
La palabra que mas me interesa desarrollar es "FRAGIL". Elegi esta ya que presenta un reto de precision y tension, donde el usuario debe interactuar con extremo cuidado; si la comparo con las otras palabras que son mas atmosfericas, pienso que "FRAGIL" es mas desafiante

### Actividad 02    
📤Luego de estudiar el capitulo del libro relacionado con [Matter.js](https://natureofcode.com/physics-libraries/)    

✍️Explica con tus palabras qué hace cada uno de esos conceptos:    
+ Engine: Motor -> Es el cerebro que calcula la fisica. No se ve fisicamente, pero el toma decisiones cuadro a cuadro, hacia donde cae cada cosa o como chocan, todo basado en leyes matematicas
+ World: Mundo -> Es el escenario donde todo sucede; en donde se añaden lo objetos y donde existen las fuerzas globales (por ejemplo la gravedad)
+ Bodies: Cuerpos -> Son los objetos fisicos (rectangulos, circulos o formas complejas). Tienen propiedades como masa, friccion, rebote, etc. Sin un cuerpo, una letra es solo un dibujo, ya que el cuerpo le permite ser un objeto que se cae y golpea
+ Constraint (Restriccion) -> Es una cuerda, resorte o clavo que une dos cuerpos, o un cuerpo a un punto fijo
+ MouseConstraint -> Es la herramienta que permite que el usuario pueda manipular el mundo fisico, atraves del cursor puede agarrar, arrastrar y lanzar cuerpos

✍️Replica al menos dos experimentos básicos integrando Matter.js con p5.js    

📎📸Incluye código y capturas o enlaces   

✍️Describe qué tipo de comportamiento físico te interesa explorar en tu palabra    
Luego de pensar varias opciones, el comportamiento final para FRÁGIL es que, si el usuario no tiene cuidado, la fisica lo "castigue"

Quiero intentar que las letras F-R--G-I-L se vean fragmentadas y que tengan un limite de aguante. El usuario debe colocar la letra A en su lugar; si lo hace con demasiada fuerza, velocidad o sin precisión, el golpe contra las otras letras ocasionara que estas se desmoronen por el impacto

La idea es que la garra (MouseConstraint) no se sienta rigida o estable, sino como si la letra estuviera colgando de un hilo inestable. De esta forma, el usuario se ve obligado a moverse con calma y cautela. En resumen, la fisica de esta pieza debe transmitir la sensación constante de estar a punto de romperse

### Actividad 03    
✍️Realiza al menos dos experimentos simples de audio-reactividad   

✍️Explica qué dato estás leyendo del audio    

✍️Explica qué comportamiento visual o físico activa ese dato   

✍️Describe qué tipo de respuesta sonora te serviría más para tu palabra y por qué   
Pense para mayor inmersion, pense en utilizar la amplitud (captada por el microfono) del sonido ambiente como fuente de perturbacion, que sea como una vibracion fisica sobre la letra A

De esta forma si el lugar esta en silencio, el nivel de complejidad para colocarla sera el normal/basico. Pero, si el microfono detecta picos de amplitud (un aplauso, un grito o musica fuerte), esa energia producira un temblor fisico aplicado a la letra

¿Por que este dato?
Porque añade una capa de dificultad a la pieza. El usuario no solo tiene que ser preciso con la mano (mouse), sino que debe guardar silencio o controlar el entorno sonoro para que la letra no vibre demasiado. Si hay mucho ruido, la letra A temblara tanto que sera mas dificil encajarla sin golpear y destruir el resto de la palabra. Quiero dar a entender que la fragilidad no se encuentra solo en el objeto si no en el entorno en el que existe

## Bitácora de aplicación 


## Bitácora de reflexión
