# Variable
```swift
var number: Int = 5
print(number)

number = 10
print(number)
```
```swift
var message: String = "Hello"
var message = "Hello"
message.append("123") //Mutating
```
# Constants
```swift
let number: Int = 5
```

# Function
func
```swift
func add(x: Int, y: Int) -> Int {
    let result: Int = x + y
    return result
    //以下不會再執行
}
```
OuterName
```swift
func add(outerX innerX: Int, y: Int) -> Int 
    let result: Int = innerX + y
    return result
    //以下不會再執行
}

let result: Int = add(outerX: 3, y:5)
print(result)
```
Void
```swift
func sayHello() -> Void{
    print("Hello")

    //return Void()
    //return ()
}
sayHello() 

func sayHi() -> Void{
    print("Hi")
}
sayHi() 
```

# Boolean
```swift
let bool: Bool = true

if bool {print("This value is true.")}
else {print("The value is false.")}
```
```swift
let result1: Bool = 1 > 3
print(result1)

let nums = 1...5
let result2: Bool = nums.cotains(3)
print(result2)
```

# Optional
像是一個盒子
```swift
struct Cake{ }

let chocolateCake: Cake = Cake()

var cakeBox: Cake?

cakeBox = chocolateCake

print(cakeBox)  //Optional(__lldb_expr_93.Cake())


//開箱蛋糕盒子 - 1
func unwrapBox(_ cakeBox: Cake?){
    if let unwrappedCake: Cake = cakeBox{
        print(unwrappedCake)
        //Cake()
    }
    else{
        print("No cake in the box.")
    }
}

unwrapBox(cakeBox)


//開箱蛋糕盒子 - 2
func unwrapBox(_ cakeBox: Cake?){
    guard
        let unwrappedCake: Cake = cakeBox
    else{
        print("No cake in the box.")
        return
    }
}
unwrapBox(cakeBox)

```
```swift
var numberBox: Int?
numberBox = 10
let number: Int = numberBox ?? 5 //Box如果沒有值就用??後面的那個
print(number)
```
```swift
var numberBox: Int?
numberBox = 10
let number: Int = numberBox! //直接假設盒子中有東西，暴力開啟，Box沒東西的話程式會直接crash
print(number)
```
Optional != Variable
```swift
let optionalName: String? = "Roy"

let name: String = "Roy"

print(optionalName)  //Optional("Roy")
print(name)          //Roy

let sayHello: String = "Hi, \(optionalName)"
print(sayHello)
```
Option 就是 Enum
```swift
let chocolateCake: Cake = Cake()
//var cakeBox: Cake?
var cakeBox: Optional<Cake>

cakeBox = chocolateCake

switch cakeBox{
    case .none: print("No cake.")

    case .some(let unwrappedCake):print(unwrappedCake)
}
```
總結Optional
```
If let / Guard let / ??
! < Never Use This
```
# Struct
Value Type
```swift

struct Coordinate{
    let latitude: Double
    let longitude: Double

    //可以省略，會自動產生
    init(latitude:Double, longitude:Double){
        self.latitude = latitude
        self.longitude = longitude
    }
}

enum Cuisine{
    case american
    case italian
    case japanese
    case taiwanese
}

struct Resturant{
    let name: String

    let cuisine: Cuisine

    let coordinate: Coordinate

    init(name: String){ self.name = name }

    func open(){
        print("\(name) is now open.")
    }
    func close(){
    print("\(name) is now close.")
}

}
let dinTaiFung = Restaurant(
    name: "鼎泰豐"
    cuisine: .taiwanese,
    coordinate: Coordinate(
        latitude:25.03 
        longitude:121.5
    )
)
print(dinTaiFung.name)
dinTaiFung.open()
dinTaiFung.close()

```
# Class
```swift
class User{
    let name: String

    init(name: String){ self.name = name }

    func sayHi(){
        print("Hi, my name is \(name)")
    }
}
```
繼承
```swift
class Animal{
    let numberOfLegs: Int
    init(numberOfLegs: Int){
        self.numberOfLegs = numberOfLegs
    }

    func makeSounds(){print("Hmmm...")}
}

let unknowAnimal = Animal(numberOfLegs: 2)
print(unknowAnimal.numberOfLegs)
unknowAnimal.makeSounds()


//Cat繼承Anmail
class Cat: Animal{
    //新屬性
    let color: String
    init(color: String){
        self.color = color
        //Animal
        super.init(numberOfLegs: 4)
    }

    //Override
    override func makeSound(){print("Meow...")}

}
//let cat = Cat(numberOfLegs: 4)
let cat = Cat(color: "white")
print(cat.color)
print(cat.numberOfLegs)
cat.makeSounds()
```
# Enum(Enumeration)
```swift
enum TrafficLight{
    case red
    case yellow
    case green
}
let trafficLight: TrafficLight = TrafficLight.red
print(trafficLight)

switch trafficLight{
    case TrafficLight.red   : print("stop.")
    case TrafficLight.yellow: print("slow.")
    case TrafficLight.green : print("Go.")

    //case .red   : print("stop.")
    //case .yellow: print("slow.")
    //case .green : print("Go.")
}

```
```swift
enum Planet{
    case mercury, venus, earth, mars,jupiter, saturn, uranus, neptune
}
let planet: Planet = Planet.earth
//let planet: Planet = .earth
if planet == Planet.mars{
    print("Mars.")
}
else{
    print("Not Mars.")
}

```
Enum RawValue
```swift
//外在來源(JSON、DataBase)拿到資料後swift不能直接用Enum的狀況

//"red"    -> TrafficLight.red
//"yellow" -> TrafficLight.yellow
//"green"  -> TrafficLight.green

enum TrafficLight: String{
    //String -> Enum
    case red, yellow, green

    //自動加上的 字串轉
    init?(rawValue: String)
}

print("Red's rawValue:", TrafficLight.red.rawValue)
print("Yellow's rawValue:", TrafficLight.yellow.rawValue)
print("Green's rawValue:", TrafficLight.green.rawValue)

//Optional
let trafficLight1: TrafficLight? = TrafficLight(rawValue: "red")
print(trafficLight1)
//Optional(__lldb_expr_169.TrafficLight.red)

let trafficLight2: TrafficLight? = TrafficLight
(rawValue: "black")
print(trafficLight2)
//nil
```
```swift

// 1 -> Planet.mercury
// 2 -> Planet.venus
// 3 -> Planet.earth

enum Planet: Int{
    //0 , 1, 2,....
    case mercury=1, venus, earth, mars,jupiter,
saturn, uranus, neptune
}

print("mercury's rawValue:", Planet.mercury.rawValue)

//Optional
let planet1: Planet? = Planet(rawValue: 2)
print(planet1)
//Optional(__lldb_expr_183.Planet.venus)

let planet2: Planet? = Planet(rawValue: 100)
print(planet2)
//nil
```
Associated Value 
```swift
//不同Case有不同對應的值的時候
enum Shape{
    //radius
    case circle(radius: Double)


    //width, height
    case rectngle(
        width: Double,
        height: Double
    )
}


let circle: Shape = .circle(radius: 10.0)
let rectangle: Shape = .rectangle(width: 10.0,height: 20.0)


func calculateArea(of shape: Shape) -> Double{
    switch shape{
        case .circle(let raduis):
            return radius * radius * .pi
        case .rectangle(let width,let height):
            return width * height
    }
}

let areaOfCircle = calculateArea(of: circle)
print(areaOfCircle)

let areaOfRectangle = calculateArea(of: rectangle)
print(areaOfRectangle)
```