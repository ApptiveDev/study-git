# 3️⃣️ 협업 중 문제상황
 아직 코드리뷰 중인 부모 브랜치를 수정해야 한다면, 수정 후 자식 브랜치에도 이 수정사항을 반영해야 합니다.  
 `step-3-G-parent`와 `step-3-G-child` 브랜치가 있고, `step-3-G-parent`는 현재 코드리뷰 중임을 가정합니다.  

## 📜️ 진행 (로컬)
- `step-3-G-parent` 브랜치의 `/playground`에 새로운 텍스트 파일을 만들고 커밋합니다.
- 부모 브랜치의 변경 사항을 자식 브랜치에도 반영해봅니다.

## 🚨️ 문제상황
- A. 실수로 공동 브랜치에 commit한 경우 (reset, stash, pop)
- B. 실수로 공동 브랜치에 commit하고 push까지 한 경우 (cherry-pick, revert)
- C. commit을 합치고자 하는 경우 (interactive rebase, squash)
- D. commit을 쪼개려는 경우 (interactive rebase, reset mixed)
- E. 충돌 미리 해결하기 (rebase)
- F. 개발 중간에 PR을 올리는 경우 (branch)
- **G. 중간에 올린 PR에 변경 요청이 들어온 경우 (rebase)**
- H. 중간에 올린 PR을 Squash Merge 할 경우 (interactive rebase)
- I. 실수로 reset --hard 후 push까지 한 경우 (reflog)
- J. 로컬, 원격 브랜치 모두 브랜치명을 변경하고자 할 경우 (push --delete, --set-upstream)