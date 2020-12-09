---
excerpt: >-
  여러 개의 github profile을 이용하는 등으로 author 정보가 잘못 원격 저장소에 올라간 경우 이에 대한 조치 방법입니다. 
thumb_img_path: '' # images/9.jpg
content_img_path: '' # images/9.jpg
layout: post
---

## Summary

### 이전 커밋의 author 변경

변경할 커밋의 `바로 직전` commit hash 확인

```
$ git log

commit c3ec0cb2d55f69b82d08621a6174b7b1bfdee4a9 (HEAD -> main)
Author: akagaeng <akagaeng@gmail.com>
Date:   Wed Dec 9 20:13:21 2020 +0900

    feat: add 3

commit d1ae535d9ec31150d18d1d0e5da3e8199168669a
Author: wrong <wrong_email@gmail.com>
Date:   Wed Dec 9 20:13:11 2020 +0900

    feat: add 2

commit 3b08f22adcd5955c8e5b5b30cf5d8b4d111f3ddb
Author: akagaeng <akagaeng@gmail.com>
Date:   Wed Dec 9 20:12:50 2020 +0900

    feat: add 1

```

이 경우에는 시간 순서상 add 1 -> add 2 -> add 3 순으로 커밋이 되었는데,
add 2의 커밋에서의 author가 잘못 입력되어있습니다.
따라서 변경할 add 2커밋의 `바로 직전` 즉, add 3의 commit hash를 확인해야 합니다.
이 경우에는 add 1의 commit hash는 `3b08f22adcd5955c8e5b5b30cf5d8b4d111f3ddb`가 됩니다.
 

### rebase

```
git rebase -i -p 3b08f22adcd5955c8e5b5b30cf5d8b4d111f3ddb
```

### 커밋 수정
* 수정할 커밋 앞에 pick이라고 적힌 것을 edit으로 수정하고 저장 `wq`
* 수정할 커밋부터 과거로부터 현재까지의 순서로 수정 진행 (오래된 것부터)

* 첫번째 커밋 수정하기
```
git commit --amend --author="작성자명 <email주소>"
# git commit --amend --author="akagaeng <akagaeng@gmail.com>"
```

* 수정 후 다음 커밋으로 이동
```
git rebase --continue
```

* 계속 진행 ...
  * 커밋당 수정이므로 동일한 작업이라도 반복적으로 진행해야 합니다.



* 수정이 다 끝나면 다음과 같이 Success 메시지가 나옵니다.
```
$ git rebase --continue
Successfully rebased and updated refs/heads/feature/fix_jobs_controller.
```

### 수정사항 반영

```
git pull
git push
```

## Reference
* [https://madplay.github.io/post/change-git-author-name](https://madplay.github.io/post/change-git-author-name)