## Question
A parking lot has some parking spaces. Whenever a car arrives at the parking lot, the parking lot staff checks whether there are any parking spaces available. If parking spaces are full, cars are going out in specific order. If more cars arrive while some car is waiting, they all line up in a queue in the order in which they arrived. Then, when a parking space becomes available, the first car in the queue that arrived the earliest is parked there.

The cost of parking in dollars is the weight of the car in kilograms multiplied by the specific rate of its parking space.

The parking lot operator knows car's arrivalOrder with weights and departureOrder with specific space order. Parking spaces are given spaceOrder with specific price rate. Help him calculate how many dollars his total revenue is going to be today.

### Input
Parameter 1: spaceOrder
Array type spaceOrder with specific price rate for multiplication
Parameter 2: arrivalOrder
Array type arrivalOrder with car's weight
Parameter 3: departureOrder
Array type departureOrder with specific space order
### Output
Number should be returned.
### Constraints
spaceOrder: 1 <= spaceOrder[element] <= 10
spaceOrder: 1 <= spaceOrder.length <=100
arrivalOrder: 200 <= arrivalOrder[element] <= 1000
arrivalOrder: 1 <= arrivalOrder.length <= 2000
departureOrder: 1 <= departureOrder[element] <= 100
departureOrder: 1 <= departureOrder.length <= 2000
### I/O Example
```js
const spaceOrder = [2, 3, 5, 4];
const arrivalOrder = [400, 400, 300, 200, 400, 300, 200, 400];
const departureOrder = [3, 2, 4, 1, 3, 4, 1, 2];

const output = test2(spaceOrder, arrivalOrder, departureOrder);
console.log(output); // 8800
```

- - - 

### SOLUTION
```js
// que 로 
function test2(spaceOrder, arrivalOrder, departureOrder){
  let totalRevenue = 0;
  let count = 0;

  while(arrivalOrder.length > 0){
    const head = arrivalOrder[0];

    //When the first car is parked, the parking spaces are all empty.
    //So cars should be parked in order according to the number of parking spaces.
    if(count < spaceOrder.length){
      totalRevenue = totalRevenue + head * spaceOrder[count];
    }else{
      const departureIdx = count - spaceOrder.length;
      const parkIdx = departureOrder[departureIdx]-1;
      totalRevenue = totalRevenue + head * spaceOrder[parkIdx]
    }
     arrivalOrder.shift();
     count++;
  }
  return totalRevenue;
}

```
