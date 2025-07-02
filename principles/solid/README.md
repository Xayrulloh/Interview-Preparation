# <center>SOLID</center>

- ## **S:** _Single Responsibility_

  Imagine a baker who is responsible for baking bread. The baker’s role is to
  focus on the task of baking bread, ensuring that the bread is of high quality,
  properly baked, and meets the bakery’s standards.

  ```ts
  // Bad: A class with multiple responsibilities
  class BadUser {
    constructor(
      private name: string,
      private email: string
    ) {}

    saveToDatabase() {
      // Database logic
      console.log(`Saving ${this.name} to database...`)
    }

    sendEmail(subject: string, body: string) {
      // Email logic
      console.log(`Sending email to ${this.email}: ${subject}`)
    }
  }

  // Good: Separate classes for each responsibility
  class User {
    constructor(
      public name: string,
      public email: string
    ) {}
  }

  class UserRepository {
    save(user: User) {
      console.log(`Saving ${user.name} to database...`)
    }
  }

  class EmailService {
    sendEmail(user: User, subject: string, body: string) {
      console.log(`Sending email to ${user.email}: ${subject}`)
    }
  }

  // Usage
  const user = new User('John Doe', 'john@example.com')
  const userRepository = new UserRepository()
  const emailService = new EmailService()

  userRepository.save(user)
  emailService.sendEmail(user, 'Welcome', 'Thanks for signing up!')
  ```

- ## **O:** _Open/Closed_

  This principle states that “**Software entities (classes, modules, functions,
  etc.) should be open for extension, but closed for modification**” which means
  you should be able to extend a class behavior, without modifying it.Imagine
  you have a class called `PaymentProcessor` that processes payments for an
  online store. Initially, the `PaymentProcessor` class only supports processing
  payments using credit cards. However, you want to extend its functionality to
  also support processing payments using PayPal.

  ```ts
  // Bad: Not open for extension
  class BadDiscount {
    giveDiscount(customerType: 'regular' | 'premium', amount: number): number {
      if (customerType === 'regular') {
        return amount * 0.9
      } else if (customerType === 'premium') {
        return amount * 0.7
      }
      return amount
    }
  }

  // Good: Open for extension, closed for modification
  interface Customer {
    getDiscount(): number
  }

  class RegularCustomer implements Customer {
    getDiscount(): number {
      return 0.9
    }
  }

  class PremiumCustomer implements Customer {
    getDiscount(): number {
      return 0.7
    }
  }

  class NewYearCustomer implements Customer {
    getDiscount(): number {
      return 0.5 // Special holiday discount
    }
  }

  class Discount {
    giveDiscount(customer: Customer, amount: number): number {
      return amount * customer.getDiscount()
    }
  }

  // Usage
  const discount = new Discount()
  const regular = new RegularCustomer()
  const premium = new PremiumCustomer()
  const holiday = new NewYearCustomer()

  console.log(discount.giveDiscount(regular, 100)) // 90
  console.log(discount.giveDiscount(premium, 100)) // 70
  console.log(discount.giveDiscount(holiday, 100)) // 50
  ```

- ## **L:** _Liskov’s Substitution_

  The principle was introduced by Barbara Liskov in 1987 and according to this
  principle “**Derived or child classes must be substitutable for their base or
  parent classes**“. One of the classic examples of this principle is a
  rectangle having four sides. A rectangle’s height can be any value and width
  can be any value. A square is a rectangle with equal width and height. So we
  can say that we can extend the properties of the rectangle class into square
  class.

  ```ts
  // Bad: Violates LSP
  class Rectangle {
    protected width: number
    protected height: number

    constructor(width: number, height: number) {
      this.width = width
      this.height = height
    }

    setWidth(width: number) {
      this.width = width
    }

    setHeight(height: number) {
      this.height = height
    }

    getArea(): number {
      return this.width * this.height
    }
  }

  class Square extends Rectangle {
    constructor(size: number) {
      super(size, size)
    }

    setWidth(width: number) {
      this.width = width
      this.height = width
    }

    setHeight(height: number) {
      this.width = height
      this.height = height
    }
  }

  // This function works with Rectangle but breaks with Square
  function increaseRectangleWidth(rectangle: Rectangle) {
    rectangle.setWidth(rectangle.getWidth() + 1)
  }

  // Good: Proper inheritance hierarchy
  interface Shape {
    getArea(): number
  }

  class GoodRectangle implements Shape {
    constructor(
      private width: number,
      private height: number
    ) {}

    getArea(): number {
      return this.width * this.height
    }
  }

  class GoodSquare implements Shape {
    constructor(private size: number) {}

    getArea(): number {
      return this.size * this.size
    }
  }

  function printArea(shape: Shape) {
    console.log(`Area: ${shape.getArea()}`)
  }

  // Usage
  const rect = new GoodRectangle(5, 4)
  const square = new GoodSquare(5)

  printArea(rect) // Area: 20
  printArea(square) // Area: 25
  ```

- ## **I:** _Interface Segregation_

  This principle is the first principle that applies to Interfaces instead of
  classes in SOLID and it is similar to the single responsibility principle. It
  states that “**do not force any client to implement an interface which is
  irrelevant to them**“.Suppose if you enter a restaurant and you are a pure
  vegetarian. The waiter in that restaurant gave you the menu card which
  includes vegetarian items, non-vegetarian items, drinks, and sweets. In this
  case, as a customer, you should have a menu card which includes only
  vegetarian items, not everything which you don’t eat in your food. Here the
  menu should be different for different types of customers.

  ```ts
  // Bad: One large interface
  interface Worker {
    work(): void
    eat(): void
    sleep(): void
  }

  class HumanWorker implements Worker {
    work() {
      console.log('Human working')
    }
    eat() {
      console.log('Human eating')
    }
    sleep() {
      console.log('Human sleeping')
    }
  }

  class RobotWorker implements Worker {
    work() {
      console.log('Robot working')
    }
    eat() {
      throw new Error("Robot doesn't eat")
    }
    sleep() {
      throw new Error("Robot doesn't sleep")
    }
  }

  // Good: Segregated interfaces
  interface Workable {
    work(): void
  }

  interface Eatable {
    eat(): void
  }

  interface Sleepable {
    sleep(): void
  }

  class GoodHumanWorker implements Workable, Eatable, Sleepable {
    work() {
      console.log('Human working')
    }
    eat() {
      console.log('Human eating')
    }
    sleep() {
      console.log('Human sleeping')
    }
  }

  class GoodRobotWorker implements Workable {
    work() {
      console.log('Robot working')
    }
  }

  // Usage
  const human: Workable & Eatable & Sleepable = new GoodHumanWorker()
  const robot: Workable = new GoodRobotWorker()

  human.work()
  human.eat()
  human.sleep()

  robot.work()
  ```

- ## **D:** _Dependency Inversion_

  The Dependency Inversion Principle (DIP) is a principle in object-oriented
  design that states that “**High-level modules should not depend on low-level
  modules. Both should depend on abstractions**“. Let’s understand the
  Dependency Inversion Principle using an example: In a software development
  team, developers depend on an abstract version control system (e.g., Git) to
  manage and track changes to the codebase. They don’t depend on specific
  details of how Git works internally.

  ```ts
  // Bad: High-level module depends on low-level module
  class BadLightBulb {
    turnOn() {
      console.log('Light bulb turned on')
    }

    turnOff() {
      console.log('Light bulb turned off')
    }
  }

  class BadSwitch {
    private bulb: BadLightBulb

    constructor() {
      this.bulb = new BadLightBulb()
    }

    operate(isOn: boolean) {
      if (isOn) {
        this.bulb.turnOn()
      } else {
        this.bulb.turnOff()
      }
    }
  }

  // Good: Both depend on abstraction
  interface Switchable {
    turnOn(): void
    turnOff(): void
  }

  class LightBulb implements Switchable {
    turnOn() {
      console.log('Light bulb turned on')
    }

    turnOff() {
      console.log('Light bulb turned off')
    }
  }

  class Fan implements Switchable {
    turnOn() {
      console.log('Fan turned on')
    }

    turnOff() {
      console.log('Fan turned off')
    }
  }

  class Switch {
    constructor(private device: Switchable) {}

    operate(isOn: boolean) {
      if (isOn) {
        this.device.turnOn()
      } else {
        this.device.turnOff()
      }
    }
  }

  // Usage
  const bulb = new LightBulb()
  const fan = new Fan()

  const bulbSwitch = new Switch(bulb)
  const fanSwitch = new Switch(fan)

  bulbSwitch.operate(true) // Light bulb turned on
  fanSwitch.operate(false) // Fan turned off
  ```
