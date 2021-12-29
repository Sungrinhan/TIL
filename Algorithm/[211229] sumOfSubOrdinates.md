## sumOfSubOrdinates
### Question
There is a company in which the relationships of employees are hierarchical.
For example, If there is a subordinate B whose boss is A, then B's subordinate C is also a subordinate of A. A HR staff wants to know the total number of subordinates for a specific employee in the company. Complete a function that returns the sum of subordinates of employee from hierarchcy.

### Input
Parameter 1: hierarchy
Object type with employees with subordinates
Parameter 2: employee
String type
### Output
Number should be returned.
the total number of subordinates including employee should be returned.
### Constraints
Each employee cannot be duplicated.
### I/O Example
```js
const hierarchy = {
  A: ["B", "C"],
  B: ["D", "E"],
  C: ["F"],
  D: ["G", "H", "I"],
  E: ["J", "K"],
  F: ["L", "M"],
  G: ["N", "O", "P"],
  H: ["Q", "R"],
  J: ["S"],
  L: ["T", "U", "V"],
};
const employee = 'B';

const output = sumOfSubOrdinates(hierarchy, employee);
console.log(output); // 14
```

- - -
### Solution
```js
function sumOfSubOrdinates(hierarchy, employee) {
  // 재귀함수로 진행한다.
  // employee value 에 있는 값들을 조회해서
  


   // start로 특정직원을 넣어준다. 
 let result = [employee];
	//호출할 재귀 aux
  const aux = function (hierarchy, node) {
		//base case 더 이상 부하직원이 없을 때,
    if (hierarchy[node] === undefined) return;
		//recursive case 탐색할 부하직원이 있을 때,
    else {
      const needChecked = hierarchy[node];
      for (let i = 0; i < needChecked.length; i++) {
        //확인된 부하직원은 result에 계속 넣어준다.
        result.push(needChecked[i]);
        aux(hierarchy, needChecked[i]);
      }
    }
  };
  aux(hierarchy, employee);
  return result.length;
}
```
