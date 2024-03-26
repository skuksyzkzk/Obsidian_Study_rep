ssh -p 1398 s21315626@swji.skku.edu

 ssh u20213156@sslab.skku.edu -p2221


패스워드 둘다 u2021315626


# 생각 
서브젝트가 클라이언트의 권한을 사용해야하는 경우에 실수로 자기 자신의 권한으로 수행했을 때 발생한다 

그게 confused deputy 

ACL을 사용한다 보통은 이건 근데 유저가 어떤 권한 가지고 있는지만 체크
소프트웨어 자체를 검사하진 않는다 이걸 이용하면 되지 않나 

password 프로그램을 통해서 자신의 암호파일을 고치는데
여기서 buffer overflow를 발생시키거나 그렇게 해서 암호검사 우회해서 권한을 획득해야하나 어떻게 해야하나 

서버프로그램이 UID 가지고 있으면 해당 UID 권한으로 프로세스가 수행되니까 
서버에 서비스를 요청해야하나 


# 결론

결국 confused deputy 파일을 실행시키면 id에 입력하면 id입력한 값으로 파일이 생성된다
그래서 그걸이용해서 passwd 이름으로 프로그램 파일을 덮어씌운것 

그래서 vi 이걸로 읽기는 됨 
처음 들가면 어처피 해쉬값이라 읽어봐도 무의미 

lpESBNdjFkRYFTtObKfeVaAFpmpAKQkwWjZdhLayKKeMrapoLmtZggeMRPlvhSlv

flag값 