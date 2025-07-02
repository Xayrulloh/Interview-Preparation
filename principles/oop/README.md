# <center>OOP</center>

Object-oriented programming (OOP) is a programming paradigm that structures
software design around objects, rather than functions and logic. It organizes
code into reusable modules called classes that encapsulate data (attributes) and
methods (functions) that operate on that data.

- ## **Encapsulation:**
  - **private** (accessible only within class)
  - **protected** (accessible within or subclass)
  - **public** (accessible anywhere)

  ```ts
  class BankAccount {
    private _balance: number
    private readonly accountNumber: string

    constructor(accountNumber: string, initialBalance: number = 0) {
      this.accountNumber = accountNumber
      this._balance = initialBalance
    }

    // Getter for read-only access
    get balance(): number {
      return this._balance
    }

    // Method to deposit money
    deposit(amount: number): void {
      if (amount <= 0) {
        throw new Error('Deposit amount must be positive')
      }
      this._balance += amount
      console.log(`Deposited $${amount}. New balance: $${this._balance}`)
    }

    // Method to withdraw money
    withdraw(amount: number): boolean {
      if (amount <= 0) {
        throw new Error('Withdrawal amount must be positive')
      }
      if (amount > this._balance) {
        console.log('Insufficient funds')
        return false
      }
      this._balance -= amount
      console.log(`Withdrew $${amount}. New balance: $${this._balance}`)
      return true
    }

    // Private method for internal use
    private logTransaction(type: string, amount: number): void {
      console.log(`Account ${this.accountNumber}: ${type} $${amount}`)
    }
  }

  // Usage
  const account = new BankAccount('123456789', 1000)
  account.deposit(500) // Deposited $500. New balance: $1500
  account.withdraw(200) // Withdrew $200. New balance: $1300
  console.log(account.balance) // 1300
  // account._balance = 10000; // Error: Property '_balance' is private
  ```

<br>

- ## **Abstraction:**

  Like interface and other classes which are implementing don’t need to know
  what’s going on inside it. (Do you really know what happens when you press on
  button to switch on your TV)

  ```ts
  // Interface
  interface PaymentProcessor {
    processPayment(amount: number): boolean
    refundPayment(amount: number): boolean
  }

  // Abstract class
  abstract class PaymentGateway {
    constructor(protected apiKey: string) {}

    abstract authenticate(): boolean

    protected logTransaction(transactionId: string): void {
      console.log(`Transaction logged: ${transactionId}`)
    }
  }

  // Concrete implementation
  class StripeProcessor extends PaymentGateway implements PaymentProcessor {
    authenticate(): boolean {
      console.log(
        `Authenticating with Stripe using key: ${this.apiKey.substring(
          0,
          5
        )}...`
      )
      return true
    }

    processPayment(amount: number): boolean {
      if (!this.authenticate()) return false

      console.log(`Processing Stripe payment of $${amount}`)
      const transactionId = `stripe_${Math.random()
        .toString(36)
        .substring(2, 11)}`
      this.logTransaction(transactionId)
      return true
    }

    refundPayment(amount: number): boolean {
      if (!this.authenticate()) return false

      console.log(`Processing Stripe refund of $${amount}`)
      const transactionId = `stripe_refund_${Math.random()
        .toString(36)
        .substring(2, 11)}`
      this.logTransaction(transactionId)
      return true
    }
  }

  // Another concrete implementation
  class PayPalProcessor implements PaymentProcessor {
    processPayment(amount: number): boolean {
      console.log(`Processing PayPal payment of $${amount}`)
      return true
    }

    refundPayment(amount: number): boolean {
      console.log(`Processing PayPal refund of $${amount}`)
      return true
    }
  }

  // Usage
  const stripe = new StripeProcessor('sk_test_12345')
  stripe.processPayment(100)
  /*
  Authenticating with Stripe using key: sk_te...
  Processing Stripe payment of $100
  Transaction logged: stripe_4n5x7yv2d
  */

  const paypal = new PayPalProcessor()
  paypal.refundPayment(50)
  // Processing PayPal refund of $50

  // Function demonstrating interface usage
  function handlePayment(processor: PaymentProcessor, amount: number): void {
    if (processor.processPayment(amount)) {
      console.log('Payment successful')
    } else {
      console.log('Payment failed')
    }
  }

  handlePayment(stripe, 75)
  handlePayment(paypal, 125)
  ```

<br>

- ## **Inheritance:**

  Inherit other classes (Person \-\> Father, Person \-\> Mather, Son \-\>
  Father, Mother)

  ```ts
  // Base class
  class Animal {
    constructor(
      public name: string,
      protected age: number
    ) {}

    makeSound(): void {
      console.log('Some generic animal sound')
    }

    move(distance: number = 0): void {
      console.log(`${this.name} moved ${distance}m`)
    }

    protected getAge(): number {
      return this.age
    }
  }

  // Derived class
  class Dog extends Animal {
    private breed: string

    constructor(name: string, age: number, breed: string) {
      super(name, age)
      this.breed = breed
    }

    // Method overriding
    makeSound(): void {
      console.log('Woof! Woof!')
    }

    // New method specific to Dog
    fetch(item: string): void {
      console.log(`${this.name} (${this.breed}) fetched the ${item}`)
    }

    // Using protected member from parent
    getDogInfo(): string {
      return `${this.name} is a ${this.breed}, ${this.getAge()} years old`
    }
  }

  // Usage
  const genericAnimal = new Animal('Generic', 3)
  genericAnimal.makeSound() // Some generic animal sound

  const myDog = new Dog('Buddy', 5, 'Golden Retriever')
  myDog.makeSound() // Woof! Woof!
  myDog.fetch('ball') // Buddy (Golden Retriever) fetched the ball
  console.log(myDog.getDogInfo()) // Buddy is a Golden Retriever, 5 years old
  myDog.move(10) // Buddy moved 10m
  ```

<br>

- ## **Polymorphism:**

_Poly_ \=\> Multiple, _Morphism_ \=\> Form \===\> Multiple Form  
 _Person_ \=\> Father, Mother, Child, Worker, President, etc..  
 _OOP_

- Parent class (sound \=\> ‘parent’)
- Child class inherited Parent class (sound \=\> ‘child’)

```ts
// Abstract base class
abstract class Shape {
  constructor(public color: string) {}

  abstract getArea(): number
  abstract draw(): void

  displayInfo(): void {
    console.log(`This is a ${this.color} shape with area ${this.getArea()}`)
  }
}

// Concrete implementations
class Circle extends Shape {
  constructor(
    color: string,
    private radius: number
  ) {
    super(color)
  }

  getArea(): number {
    return Math.PI * this.radius ** 2
  }

  draw(): void {
    console.log(`Drawing a ${this.color} circle with radius ${this.radius}`)
  }
}

class Rectangle extends Shape {
  constructor(
    color: string,
    private width: number,
    private height: number
  ) {
    super(color)
  }

  getArea(): number {
    return this.width * this.height
  }

  draw(): void {
    console.log(
      `Drawing a ${this.color} rectangle ${this.width}x${this.height}`
    )
  }
}

// Function demonstrating polymorphism
function processShapes(shapes: Shape[]): void {
  shapes.forEach(shape => {
    shape.draw()
    shape.displayInfo()
    console.log('---')
  })
}

// Usage
const shapes: Shape[] = [
  new Circle('red', 5),
  new Rectangle('blue', 4, 6),
  new Circle('green', 3)
]

processShapes(shapes)
/*
 Drawing a red circle with radius 5
 This is a red shape with area 78.53981633974483
 ---
 Drawing a blue rectangle 4x6
 This is a blue shape with area 24
 ---
 Drawing a green circle with radius 3
 This is a green shape with area 28.274333882308138
 ---
 */
```
