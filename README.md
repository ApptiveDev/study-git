# 3️⃣️ 협업 중 문제상황
 중간에 올린 PR이 Squash Merge로 병합된다면 자식 브랜치는 항상 충돌을 해결해야 합니다. 같은 내용의 커밋이더라도 커밋 해시가 바뀌면서 병합되기 때문입니다. 이를 충돌을 피하면서 해결해봅시다.

## 📜️ 진행
- 스터디원은 `step-3-H-parent` 브랜치로부터 개인 브랜치를 만듭니다.
- 스터디원은 개인 브랜치에 새 파일을 만들고 커밋합니다.
- 스터디장은 `step-3-H-parent`를 `step-3-H`에 squash merge합니다.
- 스터디원은 본인의 브랜치를 `step-3-H`에 rebase 합니다.
- 스터디원은 충돌을 확인하고, 충돌 없이 해결할 방법을 찾아봅니다.

## 커맨드
> 연습을 위해 주석은 최소한만 달아주세요.
```bash
git checkout step-3-H-parent
git branch step-3-H-<이름>
git add . && git commit -m "새로운 커밋"

# 스터디장은 step-3-H-parent PR 및 Squash Merge

git checkout step-3-H-<이름>
git rebase step-3-H

git rebase --abort
git rebase -i step-3-H~5
```

## 🚨️ 문제상황
- A. 실수로 공동 브랜치에 commit한 경우 (reset, stash, pop)
- B. 실수로 공동 브랜치에 commit하고 push까지 한 경우 (cherry-pick, revert)
- C. commit을 합치고자 하는 경우 (interactive rebase, squash)
- D. commit을 쪼개려는 경우 (interactive rebase, reset mixed)
- E. 충돌 미리 해결하기 (rebase)
- F. 개발 중간에 PR을 올리는 경우 (branch)
- G. 중간에 올린 PR에 변경 요청이 들어온 경우 (rebase)
- **H. 중간에 올린 PR을 Squash Merge 할 경우 (interactive rebase)**
- I. 실수로 reset --hard 후 push까지 한 경우 (reflog)
- J. 로컬, 원격 브랜치 모두 브랜치명을 변경하고자 할 경우 (push --delete, --set-upstream)