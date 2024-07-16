![](Pasted%20image%2020240716094012.png)

각각인자마다 최장 증가수열을 찾음
그다음 인자를 더할때는 이전 최장증가수열중 마지막 값(사실 각각이 다 마지막 인덱스임)이 자기보다 작은것중 가장 긴것을 선택한후 1을 더하고 자기자신을 추가함
https://namu.wiki/w/%EC%B5%9C%EC%9E%A5%20%EC%A6%9D%EA%B0%80%20%EB%B6%80%EB%B6%84%20%EC%88%98%EC%97%B4

각각 인덱스의 최장 증가수열 구할때 순서
1) 이전것중 깃것부터 찾음
2) 그중 자기보다 작은 값이면 그값 +1 이 길이

### DP 이용
```
void LIS_DP() {
    for (int i = 0; i < n; i++) {
        dp[i] = 1;            //해당 원소에서 끝나는 LIS 길이의 최솟값. 즉, 자기 자신
        for (int j = 0; j < i; j++) {
            //i번째 이전의 모든 원소에 대해, 그 원소에서 끝나는 LIS의 길이를 확인한다.
            if (arr[i] > arr[j]) {
                //단, 이는 현재 수가 그 원소보다 클 때만 확인한다.
                dp[i] = max(dp[i], dp[j] + 1);        //dp[j] + 1 : 이전 원소에서 끝나는 LIS에 현재 수를 붙인 새 LIS 길이
            }
        }
    }
}
```

### 이분탐색
```
int binary_search(vector<int> lis, int start, int end, int element) {
    //이분 탐색으로 lis 벡터 내에서 element의 위치를 반환
    //lis 벡터의 start - end 구간에서만 확인
    while (start < end) {
        int mid = (start + end) / 2;
        if (element > lis[mid]) start = mid + 1;
        else end = mid;
    }
    return end;
}

int LIS_BS() {
    int ret = 0;
    vector<int> lis;
    lis.push_back(arr[0]);
    for (int i = 1; i < n; i++) {
        //만약 lis 벡터의 마지막 수보다 i번째 수가 크다면, 그냥 뒤에 붙인다.
        if (arr[i] > lis.back()) {
            lis.push_back(arr[i]);
            ret = lis.size() - 1;
        }

        //i번째 수에 대해, lis 벡터 내에서 그 수의 위치를 찾는다.

        int pos = binary_search(lis, 0, ret, arr[i]);

        lis[pos] = arr[i];

    }

    return ret + 1;

}
```