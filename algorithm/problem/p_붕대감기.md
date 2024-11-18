[구현](../theory/구현.md)
### 문제
https://school.programmers.co.kr/learn/courses/30/lessons/250137
체력회복 : t초 * x
t초연속 붕대감기 성공시 +y추가 회복
최대 체력이 존재함
공격 당하면 기술과 체력회복이 취소당함
공격시 정해진 피해량만큼 체력줄어듬
if 체력 0이하 >  캐릭터주금
### 답
공격과 공겨사이 기간동안  추가회복이 한번만이뤄지는게아니라 여러번 이뤄질 수 있다는 것을 유의해야한다
```js
function solution(bandage, health, attacks) {
    let prevTime = 0;
    let curHealth = health;
    for(let a of attacks){
        let [at,ad] = a;
        let remainTime = at- prevTime-1;
        curHealth = getRecovery(remainTime,curHealth,bandage,health);
        // console.log(remainTime,"초 회복후",curHealth)
        curHealth -= ad;
        // console.log("공격후",curHealth)
        // console.log('-----',at)
        prevTime = at;
        if(curHealth<=0) return -1
    }
    
    return curHealth;
}

function getRecovery(time,curHealth,bandage,health){
    let [bTime, bRecover, bAddRecover]=bandage;
    curHealth += time * bRecover
    if(time>=bTime){
        curHealth += bAddRecover *parseInt(time/bTime);
    }
    if(curHealth>=health) return health;
    return curHealth;
}
```