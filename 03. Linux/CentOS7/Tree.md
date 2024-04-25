###Linux tree 명령어 사용법
tree 는 폴더의 하위 구조를 계층적으로 표시해 주는 유틸리티로 전체 구조를 대략적으로 파악할 때 유용합니다.

##depth 제한
-L(Level) 옵션뒤에 depth 인 2를 주고 실행

$ tree -L 2 -N /


###directory 만 표시
-d 옵션 사용

$ tree -L 2 -d -N /

###no indentation + full path
depth 에 따른 들여쓰기를 하지 않을 경우 -i 옵션 추가하고 파일의 전체 경로를 표시할 경우 -f 옵션 사용.

$ tree -L 2 -d -fi -N /


###2 depth, 특정 폴더 제외
특정 폴더를 제외할 경우 -I(대문자 I) 뒤에 제외할 패턴을 입력. 아래는 tests와 node_moduels 폴더 제외하고 tree 구조 표시

$ tree -N -L 2 -d -I "node_modules|tests"

#주요 옵션
-d	
디렉터리만 표시
-f	
파일의 전체 경로 표시
-i	
 Makes tree not print the indentation lines, useful when used in conjunction with the -f option.
-I	pattern	
Do not list those files that match the wild-card pattern.

-P	pattern	List  only  those files that match the wild-card pattern. 
-L	level	
-N	
tree는 ascii 가 아닌 문자는 \332 같이 8진수가 인코딩해서 표시하므로 한글이 깨져 보임.

-N 옵션을 추가하면 한글이 제대로 표시됨.

Ref
https://github.com/tldr-pages/tldr/blob/master/pages/linux/tree.md
https://www.computerhope.com/unix/tree.htm
https://unix.stackexchange.com/questions/47805/how-do-we-specify-multiple-ignore-patterns-for-tree-command
