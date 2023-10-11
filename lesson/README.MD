# Clase de prueba en la dirección "Desarrollo de juegos"
## Al iniciar RobloxStudio, selecciona la plantilla "Classic Beseplate".
<img src = "img/RobloxStudio1.jpg">

## Se abre el área de trabajo principal
<img src = "img/RobloxStudio2.jpg">

## Seleccionamos la opción Parte y la subopción Block
<img src = "img/RobloxStudio3.jpg">

## Se creará un block rectangular 
<img src = "img/RobloxStudio4.jpg">

## En el block del menú Explorer, haz clic en el signo de más (+)
<img src = "img/RobloxStudio5.jpg">

## Y seleccionaremos la opción Script
<img src = "img/script.jpg">

## Pulsamos sobre el elemento Script creado y eliminamos el código print("Hello world!")

<img src = "img/RobloxStudio7.jpg">

## Peguemos el código y ejecutemos el código

```lua
element = script.Parent
element.BrickColor = BrickColor.new("Dark blue")
```
<img src = "img/RobloxStudio8.jpg">

## Veremos el resultado: el block se vuelve de color azul oscuro después de la ejecución 

<img src = "img/RobloxStudio9.jpg">

## Agregaremos un efecto de fuego al block "fire"
Para hacerlo, presionamos el signo '+' junto al nombre del block (Part).
<img src = "img/RobloxStudio10.jpg">

Y mediante la búsqueda, encontraremos el efecto de fuego (fire)
<img src = "img/RobloxStudio11.jpg">

El fuego, como propiedad, aparecerá en el block seleccionado
<img src = "img/RobloxStudio12.jpg">

## Añadiremos código que cambiará dinámicamente el efecto
```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
end

wait(10)
stopFire()
```
<img src = "img/RobloxStudio13.jpg">
Este código cambiará el efecto del block de 'fuego' (fire) a 'emisor de partículas' (ParticleEmitter) después de 10 segundos desde su inicio
<img src = "img/change_property.gif">  

## Añadiremos la implementación de la desaparición del block
Para hacer esto, crearemos la función destroyBlock y la llamaremos después de 5 segundos de la desaparición del efecto "emisor de partículas"
```lua
local element = script.Parent

local function stopFire()
	element.Fire:Destroy()
	local spark = Instance.new("ParticleEmitter")
	spark.Parent = element
end
local function destroyBlock()
	element:Destroy()
end


wait(10)
stopFire()
wait(5)
destroyBlock()
```  
<img src = "img/RobloxStudio14.jpg">
obtendremos el resultado:
<img src = "img/effects.gif">

## Añadiremos una característica al block: un cambio cíclico de color
```lua
while true do
	element.BrickColor = BrickColor.new(0.9,0.6,0.2)
	wait(3)
	element.BrickColor = BrickColor.new(0.2,0.6,0.2)
	wait(3)
end

```
<img src = "img/RobloxStudio15.jpg">
Obtendremos el resultado  
<img src = "img/change_color.gif">

## Додамо функціональність балів
Junto al punto 'Workspace', haremos clic en "+"
<img src = "img/RobloxStudio16.jpg">  
Elegiremos la opción Script
<img src = "img/RobloxStudio17.jpg">

En el nuevo block Script, eliminaremos el código `print("Hello world!")` (que está allí por defecto) y agregaremos el código para generar puntos

```lua
local function onPlayerJoin(player)
	local leaderstats = Instance.new("Folder")
	leaderstats.Name = "leaderstats"
	leaderstats.Parent = player

	local points = Instance.new("IntValue")
	points.Name = "Points"
	points.Value = 0
	points.Parent = leaderstats

end

game.Players.PlayerAdded:Connect(onPlayerJoin)
```
<img src = "img/RobloxStudio18.jpg">
## Añadiremos un nuevo block
Seleccionamos el botón Block (1) en la barra de herramientas. En la lista desplegable, elegimos Part (2). Se creará un nuevo block (3)

<img src = "img/RobloxStudio19.jpg">
En el block Explorer, junto al elemento de menú Part que corresponde al block creado, haremos clic en el símbolo '+'
<img src = "img/RobloxStudio20.jpg">
En el menú que aparecerá, seleccionaremos el punto Script

<img src = "img/RobloxStudio21.jpg">

En lugar del código que está en este block por defecto (`print("Hello world!")`), agregaremos un código para obtener puntos según el color del block
```lua
local pointPart = script.Parent

local blue = Color3.fromRGB(0, 0, 255)
local green = Color3.fromRGB(0, 255, 0)
local red = Color3.fromRGB(255 ,0, 0)

local smallPoints = 10
local largePoints = 50
local losePoints = 100

local Players = game:GetService("Players")

local function givePoints(player)
	local currentColor = pointPart.Color

	local playerStats = player:WaitForChild("leaderstats")
	local playerPoints = playerStats:WaitForChild("Points")

	if currentColor == blue then
		playerPoints.Value = playerPoints.Value + smallPoints
	elseif currentColor == green then
		playerPoints.Value = playerPoints.Value + largePoints
	else
		playerPoints.Value = playerPoints.Value - losePoints
	end

	pointPart:Destroy()

	local playerCharacter = player.Character
	local particle = Instance.new("ParticleEmitter")
	particle.Color = ColorSequence.new(currentColor)
	particle.Parent = playerCharacter:WaitForChild("Head")
	wait(1)
	particle:Destroy()
end

local function partTouched(otherPart)
	local player = game.Players:GetPlayerFromCharacter(otherPart.Parent)

	if player then
		givePoints(player)
	end
end

pointPart.Touched:Connect(partTouched)

while true do
	pointPart.Color = blue
	wait(4)
	pointPart.Color = green
	wait(3)
	pointPart.Color = red
	wait(2)
end
```
<img src = "img/RobloxStudio22.jpg">
Duplique el block (haciendo clic con el botón derecho del ratón y seleccionando 'Duplicate')
<img src = "img/RobloxStudio23.jpg">
Mueva el block duplicado 
<img src = "img/duplicate.gif">
Repite tres veces

## Ejecuta el código para obtener el resultado 
<img src = "img/result.gif">
