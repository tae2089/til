```
#!/usr/bin/env sh
#. "$(dirname -- "$0")/_/husky.sh"


COMMIT_MSG_FILE=$1
COMMIT_SOURCE=$2
SHA1=$3

if [ -z "$BRANCHES_TO_SKIP" ]; then
    BRANCHES_TO_SKIP=(master develop release hotfix)
fi

BRANCH_NAME=$(git symbolic-ref --short HEAD)
BRANCH_NAME="${BRANCH_NAME##*/}"
JIRA_ID=`echo $BRANCH_NAME | egrep -o 'B.-[0-9]+'`
COMMIT_SUBJECT=$(cat $1 |head -1)
COMMIT_SUBJECT_NEW=$(printf "%s (#%s)" "${COMMIT_SUBJECT}" "${JIRA_ID}")

{
    BRANCH_EXCLUDED=$(printf "%s\n" "${BRANCHES_TO_SKIP[@]}" | grep -c "^$BRANCH_NAME$")
} ||
{
    BRANCH_EXCLUDED=0
}

{
    BRANCH_IN_COMMIT=$(grep -c "$JIRA_ID" $1)
} ||
{
    BRANCH_IN_COMMIT=0
}

if [ -n $JIRA_ID ] && ! [[ $BRANCH_EXCLUDED -eq 1 ]] && ! [[ $BRANCH_IN_COMMIT -ge 1 ]]; then
    sed -i.bak -e "1s/.*/$COMMIT_SUBJECT_NEW /" $1
fi
```

git에는 hook이라는게 존재한다. 이걸 활용하면 git을 사용할 때 추가적인
작업을 자동으로 해줄 수 있다.

나는 jira issue를 커밋메시지에 자동으로 붙이고 싶어 prepare-commit-msg를 사용했다.

맨위에 있는 스크립트는 jira issue 번호를 자동으로 붙여주는 코드이다.
저기서 주위할 점은 JIRA_ID 부분인데 자신의 티켓번호를 보면 TEST-01이런식으로 나오게 된다. 여기서 TEST를 잘 기억해서 egrep -o 'A.-[0-9]+'`에서 "TEST"면 "TES." 으로 입력해주고 ROK이면 "RO." 으로 입력해주기만 하면 된다.

마지막으로 스크립트를 사용하려면 .git/hooks/prepare-commit-msg.sample파일을 .git/hooks/prepare-commit-msg로 카피나 변경해준 다음
맨 위에 있는 코드를 prepare-commit-msg에 추가해주기만 하면 된다.
