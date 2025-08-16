El juego se llama saltitos es un juego donde tu eres un cubo que va avanzando de manera automatica y tienes que saltar para ir esquivando los obstaculos que llegan a haber en los niveles, puede llegar  a ser eictivo y desesperante al mismo tiempo  

JUGADOR:

extends CharacterBody2D


var SPEED = 15000
const JUMP_VELOCITY = -500
var gravedad = 5000

var coin_counter = 0



func _physics_process(delta: float) -> void:
	#gravedad
	if not is_on_floor():
		velocity += get_gravity() * delta
		$Sprite2D.rotation_degrees += 380 * delta
	else :
		var modulo = int($Sprite2D.rotation_degrees) % 90;
	
		if modulo > 45 :
			$Sprite2D.rotation_degrees += (90 - modulo)
		else :
			$Sprite2D.rotation_degrees -= modulo

	#salto
	if Input.is_action_pressed("salto") and is_on_floor():
		velocity.y = JUMP_VELOCITY

	velocity.x = SPEED * delta

	move_and_slide()

func death():
	SPEED = 0
	$Sprite2D.visible = false
	$Timer.start()
	

func _on_timer_timeout() -> void:
	get_tree().reload_current_scene()



func _on_area_2d_body_entered(body: Node2D) -> void:
	get_tree().change_scene_to_file("res://escenario/NIVEL2.tscn")
	pass # Replace with function body.
	
  Script de personaje (CharacterBody2D)
Controla el movimiento y físicas básicas del jugador
 Aplica gravedad y rota el sprite en el aire, alineándolo al tocar el suelo
 Permite saltar al presionar "salto" estando en el piso
 Se mueve automáticamente hacia la derecha con velocidad constante
extends Area2D


MUERTE:

func _on_body_entered(body):
	if body.is_in_group("kill") :
		$"..".death()
		self.queue_free()

Detector de muerte por cuerpos (body_entered)
Detecta colisión con cuerpos físicos
 Si el cuerpo está en el grupo "kill", llama a death() en el nodo padre
 Se elimina a sí mismo
extends Area2D

MUERTE POR AREA:

func _on_area_entered(area: Area2D) -> void:
	if area.is_in_group("kill") :
		$"..".death()
		self.queue_free()
Detector de muerte por áreas (area_entered)
Detecta colisión con otras áreas (Area2D)
 Si el área está en el grupo "kill", llama a death() en el nodo padre
 Se elimina a sí mismo

 ASSETS DEL JUEGO:
 
<img width="373" height="746" alt="04b0688c0bfbf4609d1d4dd03525503da5ea2a2d" src="https://github.com/user-attachments/assets/794149ff-89e1-4a8c-b5be-82ebc1886737" />

<img width="469" height="321" alt="Captura de pantalla 2025-08-11 041058" src="https://github.com/user-attachments/assets/dbc9e957-4dac-4134-ad43-324f0893dc8c" />

<img width="182" height="182" alt="Captura de pantalla 2025-08-11 041002" src="https://github.com/user-attachments/assets/5142fbc9-00a8-4aae-947d-dc64f2b613da" />

  <img width="288" height="274" alt="Captura de pantalla 2025-08-11 041017" src="https://github.com/user-attachments/assets/580c3988-9756-484b-b00c-a6dad8575b27" />

CAPTURAS DEL JUEGO EN FUNCIONAMIENTO:
<img width="863" height="535" alt="Captura de pantalla 2025-08-15 193100" src="https://github.com/user-attachments/assets/ecd239a2-b2cd-469a-9729-7d67b218a6de" />

<img width="695" height="490" alt="Captura de pantalla 2025-08-15 193008" src="https://github.com/user-attachments/assets/c562c92e-0f65-4651-9eb2-341108474179" />
VIDEOS:


