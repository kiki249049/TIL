git branch : 브랜치 목록 확인

git branch 브랜치이름 : 새로운 브랜치 생성

git branch -d 브랜치이름 : 병합된 특정 브랜치 삭제

git branch -D 브랜치이름 : 강제 삭제

git switch 브랜치 이름 : 다른 브랜치로 이동

git switch -c 브랜치 이름 : 브랜치를 새로 생성과 동시에 이동

m1 - m2 - m3 에따라 HEAD 이동

git log --onelne

git log --online --all

git log --oneline --all --graph

### merge(병합)

git merge 병합할 브랜치이름

* merge하기 전에 일단 다른 브랜치를 합치려고 하는 메인 브랜치로 switch해야함 A,B와 A가 메인이면 A로 이동해야함.

### 1. fast-forward

### 2. 3-way merge(merge commit)

새로운 버젼이 생김.

### 3. merge conflict

* merge하는 두 브랜치에서 같은 파일의 같은 부분을 동시에 수정하고 merge하면 git은 해당부분을 자동으로 merge해주지 못함.

* 반면 동일 파일이더라도 서로 다른 부분을 수정했다면 conflict없이 자동으로 merge commit 된다.

-> vim(옛날 cmd)에디터가 나옴 당황no

