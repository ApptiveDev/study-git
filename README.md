# 3️⃣️ 협업 중 문제상황

커밋에 너무 많은 내용이 들어가 있으면 히스토리를 관리하기 힘들어 집니다. 해당 커밋이 문제를 일으킨 경우 reset이나 revert를 해야 하는데, 전체를 되돌리면 불필요한 부분까지 되돌려지기 때문입니다. 이곳에 있는 커밋 1개를 2개로 쪼개보세요.

## 📜️ 진행 (로컬)

- 스터디원은 '쪼갤커밋'을 되돌립니다.
- 스터디원은 다음 2개로 다시 커밋합니다.
  - 커밋 1: dev1.txt 만 담습니다.
  - 커밋 2: dev2.txt 만 담습니다.

## 🚨️ 문제상황

- A. 실수로 공동 브랜치에 commit한 경우 (reset, stash, pop)
- B. 실수로 공동 브랜치에 commit하고 push까지 한 경우 (cherry-pick, revert)
- C. commit을 합치고자 하는 경우 (interactive rebase, squash)
- **D. commit을 쪼개려는 경우 (interactive rebase, reset mixed)**
- E. 충돌 미리 해결하기 (rebase)
- F. 개발 중간에 PR을 올리는 경우 (branch)
- G. 중간에 올린 PR에 변경 요청이 들어온 경우 (rebase)
- H. 중간에 올린 PR을 Squash Merge 할 경우 (interactive rebase)
- I. 실수로 reset --hard 후 push까지 한 경우 (reflog)
- J. 로컬, 원격 브랜치 모두 브랜치명을 변경하고자 할 경우 (push --delete, --set-upstream)

## 실습 코드

### D. commit을 쪼개려는 경우 (interactive rebase, reset mixed)

크게 두가지 방식을 소개하려고한다.

1. rebase를 이용해서 쪼개려하는 커밋의 범위를 지정
2. reset mixed 사용해서 특정 커밋 상태로 브랜치를 되돌리는 방식

#### 1. interactive rebase 사용하기

쪼개고자 하는 커밋의 범위를 지정하여 interactive rebase를 시작한다.

- <commit-hash>: 쪼개고자 하는 커밋의 해시

`git rebase -i <commit-hash>`

##### 커밋을 편집하기 위해 "edit" 사용

- 편집기에서 쪼개고자 하는 커밋 앞의 단어를 pick에서 edit으로 변경한다.

```
pick a1d2e3f Second change
-> edit a1d2e3f Second change
```

##### 변경 사항을 unstage 상태로 변경

- 변경 사항을 unstage 상태로 만든다.

`git reset HEAD`

##### 변경 사항을 새로운 커밋으로 분할

- 원하는 대로 변경 사항을 나누고 각각을 새로운 커밋으로 만든다.

```
git add <file-part-1>
git commit -m "First part of split commit"
git add <file-part-2>
git commit -m "Second part of split commit"
```

##### rebase 마무리

`git rebase --continue`

#### 2. reset mixed 사용하기

##### 해당 커밋까지 브랜치를 되돌리기

- <commit-hash>: 브랜치 상태를 되돌리려는 커밋의 해시

`git reset --mixed <commit-hash>`

##### 변경 사항을 여러 커밋으로 나누기

- 변경 사항은 unstaged 상태이므로 원하는 대로 파일을 나누어 커밋이 가능

```
git add <file-part-1>
git commit -m "First part of split commit"
git add <file-part-2>
git commit -m "Second part of split commit"
```

이제 복잡한 변경 사항을 더 세밀하게 관리하고, 각 커밋의 목적을 명확하게 할 수 있게 되었습니다!
