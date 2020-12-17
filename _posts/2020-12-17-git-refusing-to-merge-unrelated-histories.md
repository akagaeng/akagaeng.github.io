---
excerpt: >-
  git 으로 소스코드 관리를 하다보면 가끔 fatal: refusing to merge unrelated histories 와 같은 메시지를 볼 수 있습니다. 이러한 경우에 할 수 있는 간단한 해결책을 알아보겠습니다. 
thumb_img_path: ''
content_img_path: ''
layout: post
---

> git 으로 소스코드 관리를 하다보면 가끔 fatal: refusing to merge unrelated histories 와 같은 메시지를 볼 수 있습니다. 
  이러한 경우에 할 수 있는 간단한 해결책을 알아보겠습니다. 

## Problem

우선 저는 `git pull` 과 `git push` 둘다에 대해서 제대로 수행이 되지 않았습니다.

그 원인은 2개의 다른 환경(pc) 에서 별도의 작업을 진행하였고, 그 중 하나에서 history 를 삭제하는 등의 작업을 하였고 나머지 하나에서 sync를 위해 push/pull을 시도하는 경우입니다.  
   
해결을 위해 다음 에러 메시지를 살펴보겠습니다.

### git push

```bash
$ git push
To https://github.com/akagaeng/your-project-name.git
 ! [rejected]        main -> main (non-fast-forward)
error: failed to push some refs to 'https://github.com/akagaeng/your-project-name.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Integrate the remote changes (e.g.
hint: 'git pull ...') before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

위 에러 메시지를 확인해보면 `hint`를 찾을 수 있습니다.
* `git pull` 등을 이용해서 코드를 합쳐라.
  * 일부가 원격 저장소보다 더 오래된 버전이다(behind) 라고 하는 것 같습니다.
* `git push --help` 에서 `fast-forwards` 부분을 참고해라.

아래에서 한번 확인해 보겠습니다.

### git pull

```bash
$ git pull
fatal: refusing to merge unrelated histories
```

여기서는 위 사례처럼 에러 메시지에서 가이드가 없으므로, 에러 메시지로 [구글](https://www.google.com/search?sxsrf=ALeKk035nOYcEwo4kuKO11f0ZD4qui7abQ%3A1608172459511&source=hp&ei=q8PaX5iaHfTRmAXpj7nwDA&q=fatal%3A+refusing+to+merge+unrelated+histories&oq=fatal%3A+refusing+to+merge+unrelated+histories&gs_lcp=CgZwc3ktYWIQAzIECCMQJzIHCAAQFBCHAjICCAAyAggAMgQIABAeMgQIABAeMgQIABAeMgQIABAeMgQIABAeMgQIABAeOgcIIxDqAhAnUL09WL09YNtBaAFwAHgAgAHfA4gB3wOSAQM0LTGYAQCgAQKgAQGqAQdnd3Mtd2l6sAEK&sclient=psy-ab&ved=0ahUKEwjYm72h_dPtAhX0KKYKHelHDs4Q4dUDCAc&uact=5), [stack overflow](https://stackoverflow.com/search?q=fatal%3A+refusing+to+merge+unrelated+histories) 등에서 검색해볼 수 있겠습니다.

## Solution

위 문제분석을 통해 제가 찾아낸 해결책은 다음과 같습니다. 본인의 상황에 맞도록 활용하시면 좋겠습니다.

### 현재 작업하는 버전을 살리고 싶은 경우
다른건 모르겠고 현재 작업중인 환경(pc)을 살리고 싶은 경우입니다.

```bash
git push origin master --force
```

이렇게 하면, 원격지의 버전을 현재 버전으로 덮어쓰게 됩니다. (overwrite)

### 원격에 push 되어있는 버전을 살리고 싶은 경우

```bash
git pull --rebase

# or
git pull --allow-unrelated-histories
```

위 두개 중에 하나를 실행시키시면 원격지의 버전을 로컬 환경에 반영하게 됩니다.

