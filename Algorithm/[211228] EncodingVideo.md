### Parameter 1: encodings
- integer array containing the encoding progress of the videos to be uploaded
### Parameter 2: speeds
integer array containing the encoding speed of each video
If the encoding speed of a video with a 95% progress rate is 1% per hour, the video upload will take place in 5 hours.
### Output
Your function should return an integer array
### Constraints
Encoding progress is less than 100
Encoding rate is 100 or less
You can upload videos only once per hour
### I/O Example
```js
let encodings = [90, 20, 44];
let speeds = [2, 4, 8];
let output = encodingVideo(encodings, speeds);
console.log(output); // --> [1,2]

encodings = [30, 80, 44, 55, 16, 68, 26];
speeds = [5, 2, 8, 3, 7, 4, 2]; 
output = encodingVideo(encodings, speeds);
console.log(output); // --> [3, 3, 1]
```

- - -
### Solution
```js
function encodingVideo(encodings, speeds) {
    // 업로드 마다 몇 개의 비디오가 업로드 되는지 담아줄 배열 result
    let result = [];
    let hours = 1;
    // 업로드 되는 비디오의 수
    let count = 0;
    // 현재 비디오의 인코딩 진행률
    let encoding = 0;
    
    // 모든 비디오가 다 업로드 될때까지 반복합니다.
    while(encodings[0]){
        encoding = encodings[0] + (speeds[0] * hours);
        // 첫 번째 비디오의 인코딩 진행률이 100이상인 경우
        if(encoding >= 100){
            // 업로드 완료된 비디오의 갯수를 증가 시켜줍니다.
            count++;
            // 업로드가 완료된 비디오는 큐에서 제거합니다.
            encodings.shift();
            // 업로드가 완료된 인코딩 속도는 큐에서 제거합니다.
            speeds.shift();
        }
        // 첫 번째 비디오의 인코딩 진행률이 100 미만일 경우 
        else{
            // 업로드된 비디오가 있다면 result에 push 합니다.
            if(count > 0){
                result.push(count);
            }
            // 업로드 시간이 증가됩니다.
            //(업로드는 한시간에 한번만 가능하기 때문입니다.)
            hours++;
            // 업로드 완료된 비디오의 개수 초기화 
            //(업로드는 한시간에 한번만 가능하기 때문입니다.)
            count = 0;
        }
    }
    // 모든 비디오가 업로드가 되면, 카운트된 업로드 비디오의 개수를 push후 리턴합니다.
    result.push(count);
    
    return result;
}
```
