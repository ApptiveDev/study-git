# 3️⃣️ 협업 중 문제상황

공동 브랜치에 실수로 커밋한 내역을 원격 브랜치에도 올린 상황입니다. 공동으로 작업중인 원격 브랜치는 함부로 `reset` 할 수 없으므로 브랜치 기록을 유지하면서 변경 내역을 되돌려야 합니다.

## 📜️ 진행

- 스터디원은 `step-3-B` 브랜치에서 자신의 브랜치를 생성합니다.
- 스터디원은 `step-3-B` 브랜치에 커밋을 하나 쌓고 push까지 합니다.
- 모든 스터디원이 push를 했으면, 변경사항을 로컬로 가져옵니다.
- 스터디원은 자신의 커밋을 되돌리고 push합니다.
- 스터디원은 되돌린 커밋을 자신의 브랜치로 가져옵니다.


## ✅ 자가확인
- [ ] `step-3-B` 브랜치에는 README.md 파일만 존재한다.
- [ ] 자신의 로컬 브랜치에는 공동 브랜치에 쌓았던 커밋이 존재한다.

## 💻 커맨드
> 스터디원의 연습을 위해 주석은 최소한만 달아주세요.
```bash
git checkout step-3-B
git branch step-3-B-<이름>

echo "실수로 원격 브랜치로 push할 파일" > 실수-<이름>.txt
git add .
git commit -m "실수 커밋-<이름>"
git push

# 커밋 해시 확인 후 복사
git log --oneline --graph   # 또는 git graph 익스텐션 사용
git revert <자신의 커밋 해시>
git push

git checkout step-3-B-<이름>
git cherry-pick <자신의 커밋 해시>
```

## 🚨️ 문제상황

- A. 실수로 공동 브랜치에 commit한 경우 (reset, stash, pop)
- **B. 실수로 공동 브랜치에 commit하고 push까지 한 경우 (cherry-pick, revert)**
- C. commit을 합치고자 하는 경우 (interactive rebase, squash)
- D. commit을 쪼개려는 경우 (interactive rebase, reset mixed)
- E. 충돌 미리 해결하기 (rebase)
- F. 개발 중간에 PR을 올리는 경우 (branch)
- G. 중간에 올린 PR에 변경 요청이 들어온 경우 (rebase)
- H. 중간에 올린 PR을 Squash Merge 할 경우 (interactive rebase)
- I. 실수로 reset --hard 후 push까지 한 경우 (reflog)
- J. 로컬, 원격 브랜치 모두 브랜치명을 변경하고자 할 경우 (push --delete, --set-upstream)

## 실습 코드

### B. 실수로 공동 브랜치에 commit하고 push까지 한 경우 (cherry-pick, revert)

- 이미 push한 경우라면, 로컬에서만 문제를 해결하는 것이 아니라 원격 저장소에서도 처리해야 한다.

##### 공동 브랜치에서 실수한 커밋을 취소하기 (revert):

`git checkout master            # 실수한 커밋이 있는 공동 브랜치로 이동`
`git revert <bad-commit-hash>   # 해당 커밋을 취소하는 새로운 커밋 생성`
`git push                       # 원격 저장소에 변경 사항 반영 `

##### 본인 브랜치로 revert된 커밋을 옮기기 (cherry-pick):

`git checkout step-3-B-nstgic3         # 옮길 대상 본인의 브랜치로 이동`
`git cherry-pick <revert-commit-hash> # revert된 커밋을 현재 브랜치로 복사`

공동 브랜치에서는 실수한 커밋이 취소되고, 본인 브랜치에서는 해당 커밋이 유지가 된다.

메인에 실수로 보낸 커밋이 본인 브랜치에서 필요하면서 공동 브랜치에서는 해당 커밋을 제거해야 할 때 사용할 수 있다.
