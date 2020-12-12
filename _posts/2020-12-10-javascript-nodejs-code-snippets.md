---
excerpt: >-
  평소에 개발할 때라거나 코딩 테스트를 한다거나 할 때 필요한 javascript/node 코드 스니펫입니다. 필요한게 생길때마다 계속 업데이트 하고 있습니다. :)
thumb_img_path: ''
content_img_path: ''
layout: post
---

> 이 포스트는 계속 업데이트 예정입니다.

### 중복 값 제거하여 집합(set)으로 만들기

```javascript
function getUniqueArray(arr) {
  return arr.filter((v, i, t) => t.indexOf(v) === i)
}

# const set = getUniqueArray([1,2,3,3,3])
# console.log(set) # [1, 2, 3]
```

### 값이 모두 같은지 비교

```javascript
function compareArray(arr, arrToCompare) {
  if (arr.length !== arrToCompare.length) {
    return false
  }

  const arrSort = arr.sort()
  const arrToCompareSort = arrToCompare.sort()
  return arrSort.every((v, i) => v === arrToCompareSort[i])
}
```

**주의사항**
* `arr.sort()` 는 알파벳 정렬만 해주기 때문에 숫자 등의 경우에는 별도로 정렬하는 코드를 넣어야 한다.

### 배열 중 일부분만 잘라내서 활용하기

```javascript
const slicedArr = arr.slice(start, end)
# arr = [ 0, 1, 2, 3]
# start= 1, end=2 인 경우 결과는 1
# start <= result < end
```

