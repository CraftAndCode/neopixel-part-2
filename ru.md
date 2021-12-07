# Neopixel: Часть 2

```package
core
radio
microphone
neopixel=github:microsoft/pxt-neopixel
```

```template
basic.forever(function () {
strip = neopixel.create(DigitalPin.P0, 10, NeoPixelMode.RGB)
})
```

```blocks
basic.forever(function () {
})
```


## Step 0 @showDialog
Привет! Сегодня мы продолжим открывать новые возможности светодиодной подсветки.

Перед тем, как начать, убедись, что Micro:bit подключен к светодиодной ленте так, как показано на схеме.
![](https://raw.githubusercontent.com/CraftAndCode/neopixel-extension/master/strip.png)
 
## Step 1 @showDialog
### Самая полезная команда
В предыдущем уроке каждая команда, которую мы добавляли в программу, мгновенно меняла цвет светодиодной ленты целиком. Но в этот раз, мы будем менять цвета каждого светодиода по отдельности.
  
Расширение Neopixel даёт возможность сначала изменить состояния светодиодов с помощью списка инструкций, а затем использовать отдельную команду, чтобы применить все эти изменения одновременно. Это команда ``||neopixel.show||``.
```block
let strip: neopixel.Strip = null
strip.show()
```
Команда ``||neopixel.show||`` отправляет на светодиодную ленту все инструкции, которые были записаны с момента выполнения предыдущей команды ``||neopixel.show||``. Без неё все изменения попросту не будут отображены.

## Step 2 @showDialog
### Управляем светодиодами
Команда ``||neopixel.set pixel color||`` задаёт цвет из списка выбранному светодиоду.
  
`Важно: компьютеры начинают счёт не с единицы, а с нуля. Поэтому в ленте из 10 светодиодов первому будет присвоен номер 0, а последнему - номер 9.`
```block
let strip: neopixel.Strip = null
strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
```
  

Команда ``||neopixel.rotate pixels||`` сдвигает все зажжённые светодиоды на выбранное количество позиций. При этом, цвета, которые были в конце, сдвигаются в начало.
```block
let strip: neopixel.Strip = null
strip.rotate(1)
```
  

Команда ``||neopixel.set brightness||`` регулирует яркость всех зажженных светодиодов. Максимально возможная яркость - 255.
```block
let strip: neopixel.Strip = null
strip.setBrightness(255)
```

Ещё раз напомним, что каждая из этих команд не обновляет цвета ленты мгновенно, а лишь подготавливает инструкции, которые будут выполнены с командой ``neopixel.show``.
## Step 3 @showDialog
### Проверим на практике
Чтобы лучше понять, как пользоваться новыми командами, давай соберём примеры программ с использованием новых блоков кода!

## Step 3.5 @showHint
### Пример 1: Бегущий огонь
В этом примере, красный огонёк перемещается по светодиодной ленте по нажатию кнопок.

```blocks
input.onButtonPressed(Button.A, function () {
    strip.rotate(-1)
    strip.show()
})
input.onButtonPressed(Button.B, function () {
    strip.rotate(1)
    strip.show()
})
let strip: neopixel.Strip = null
strip = neopixel.create(DigitalPin.P0, 10, NeoPixelMode.RGB)
strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Red))
strip.show()
```
## Step 4 @showHint
### Пример 2: Полицейская мигалка
В этом примере подсветка показывает вращающийся сине-красный свет. При желании, можешь добавить в программу звуки полицейской сирены!
```blocks
let strip = neopixel.create(DigitalPin.P0, 10, NeoPixelMode.RGB)
strip.showColor(neopixel.colors(NeoPixelColors.Blue))
strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Red))
strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Red))
strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Red))
strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Red))
basic.forever(function () {
    strip.rotate(1)
    strip.show()
    basic.pause(50)
})

```
## Step 5 @showHint
### Пример 3: Индикатор громкости
В этом примере положение красного огонька на ленте зависит от уровня громкости.
```blocks
let strip = neopixel.create(DigitalPin.P0, 10, NeoPixelMode.RGB)
basic.forever(function () {
    strip.showColor(neopixel.colors(NeoPixelColors.Blue))
    strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
    strip.rotate(Math.map(input.soundLevel(), 0, 255, 0, 9))
    strip.show()
})
```

## Step 6
### Теперь твой черёд!
Давай проверим, как мы научились управлять светодиодами. Напиши программу, которая покажет на светодиодной ленте радугу. В этом уроке команда ``||neopixel.show rainbow||`` отключена, поэтому для того, чтобы это сделать, необходимо задать цвет для каждого светодиода вручную.
## Step 7 @showDialog
### Больше цветов!
Дисплеи, светодиоды и экраны мониторов для кодирования цветов используют так называемую RGB-модель цвета. Она описывает цвет как сумму трёх основных цветов: красного(R), зелёного(G) и синего (B). 
  
RGB-модель работает не так, как привычное нам смешивание красок на палитре. Сочетание разных цветов даёт нам другие результаты, а при максимальном сочетании всех цветов сразу получается белый цвет. 
  
![](https://raw.githubusercontent.com/CraftAndCode/neopixel-extension/master/rgb.png)
  
Задать цвет в таком формате можно с помощью блока ``||neopixel.red green blue||``, которым можно заменить стандартный список цветов. Выбирая количество каждого цвета от 0 до 255, возможно отобразить до 16581375 разных цветов!

```block
let strip: neopixel.Strip = null
strip.setPixelColor(0, neopixel.rgb(255, 255, 255))
```

## Step 8 @showHint
### Больше цветов!
Попробуй отобразить на светодиодной ленте следующие цвета. Отличаются ли они от тех, которые мы видели раньше?
```block
let strip: neopixel.Strip = null
strip.setPixelColor(0, neopixel.rgb(0, 255, 255))
```
```block
let strip: neopixel.Strip = null
strip.setPixelColor(0, neopixel.rgb(255, 0, 255))
```
```block
let strip: neopixel.Strip = null
strip.setPixelColor(0, neopixel.rgb(255, 255, 0))
```

## Step 9 @showHint
### Градиент
Градиентом называется плавный переход между двумя цветами. 
У нас есть задание для тебя. Используя блок ``||neopixel.red green blue||``, чтобы точно задавать количество каждого из основных цветов в финальном цвете, покажи на ленте плавный переход из одного цвета в другой.
```hint
```
![](https://raw.githubusercontent.com/CraftAndCode/neopixel-extension/master/gradient.png)
## Step 10 @showDialog
### Ответы: Теперь твой черёд!
```blocks
let strip = neopixel.create(DigitalPin.P0, 10, NeoPixelMode.RGB)
strip.setPixelColor(0, neopixel.colors(NeoPixelColors.Red))
strip.setPixelColor(1, neopixel.colors(NeoPixelColors.Orange))
strip.setPixelColor(2, neopixel.colors(NeoPixelColors.Yellow))
strip.setPixelColor(3, neopixel.colors(NeoPixelColors.Green))
strip.setPixelColor(4, neopixel.colors(NeoPixelColors.Blue))
strip.setPixelColor(5, neopixel.colors(NeoPixelColors.Indigo))
strip.setPixelColor(6, neopixel.colors(NeoPixelColors.Purple))
strip.show()
```
  
### Ответы: Градиент
Так может выглядеть плавный переход между зелёным и красным цветами.
```blocks
let strip = neopixel.create(DigitalPin.P0, 10, NeoPixelMode.RGB)
strip.setPixelColor(0, neopixel.rgb(0, 225, 0))
strip.setPixelColor(1, neopixel.rgb(25, 200, 0))
strip.setPixelColor(2, neopixel.rgb(50, 175, 0))
strip.setPixelColor(3, neopixel.rgb(100, 150, 0))
strip.setPixelColor(4, neopixel.rgb(125, 125, 0))
strip.setPixelColor(5, neopixel.rgb(150, 100, 0))
strip.setPixelColor(6, neopixel.rgb(175, 75, 0))
strip.setPixelColor(7, neopixel.rgb(200, 50, 0))
strip.setPixelColor(8, neopixel.rgb(225, 25, 0))
strip.setPixelColor(9, neopixel.rgb(255, 0, 0))
strip.show()
```
## Step 9
Задания выполнены! Теперь ты знаешь, как показать любой цвет с помощью светодиодной ленты. Если для твоего проекта понадобится расширение Neopixel, ты сможешь активировать его в списке `|Расширенные|` - `|Расширения|`.
