lostTIL(구 TIL) 레포지토리에 JSP 이론을 정리 하는 폴더가 있었는데 프로젝트 연습한 폴더도 lostTIL폴더에 있으면 좋겠다고 생각해
JSP 폴더 밑에 pratice 폴더를 새로 만들어 이쪽에 프로젝트 연습한 내용을 push 하려고 했다. 
git bash에 sparsecheckout을 true로 하고 세부 디렉토리를 추가해서 push를 하려고 했는데 error: failed to push some refs to 에러로 잘 되지 않았다 
그래서 pratice 폴더를 pull 한 다음 다시 push 하려고 했느데 계속 error: failed to push some refs to push --force로 강제로 push 했더니
기존에 이론 정리하던 원격 히스토리가 완벽한 dangling commit이 되어버려 복구하지 못하게 되버렸다.(프로젝트랑 처음 연결한 것이기도 하여 local commit 기록에도 남아 있는게 없음)
