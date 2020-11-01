# DataBase
디비&서버 입니당! 앞으로 sql문을 업로드 할게용



디비& 서버입니다
중간 부분까지 들어갈 내용은 다음과 같습니다.

기반이 될 데이터베이스 스키마 생성

아래의 ER 다이어 그램을 바탕으로 스키마를 생성했습니다.

<img width="297" alt="20201101_012631" src="https://user-images.githubusercontent.com/60510921/97784391-9ec16c80-1be1-11eb-95bc-9f40f688fff7.png">

스터디 테이블과 패킷 테이블은 서로 약한 엔티티 타입과 강한 엔티티 타입으로 방해한다는 관계를 가집니다.
따라서 약한 엔티티 타입인 패킷 테이블은 스터디 테이블의 날짜 어트리뷰트를 참조하면서 동시에 기본키를 구성합니다.
이 때 디텍트 테이블은 패킷 테이블의 날짜를 외래키로 해서 그 날짜 중 언제 언제 패킷이 감지되었는지를 담고 있습니다.

아래는 스터디 테이블의 sql문입니다.

<img width="299" alt="study 테이블" src="https://user-images.githubusercontent.com/60510921/97783910-3624c080-1bde-11eb-8310-91da7bcbf0ea.png">

스터디 테이블의 어트리뷰트들을 설명하자면
Study_date는 기본키로 날짜별 공부 시간을 구분해줄 어트리뷰트입니다.
Study_time은 각 날짜별 공부량이 어느정도인지 알려주는 어트리뷰트이고
Study_goal은 사용자가 설정할 공부 목표량이며 Study_achieved들의 값을 얻어낼때 도움을 받고자 넣었습니다.
Study_achieved는 사용자가 하루의 목표량을 달성했는지 알려주기 위한 어트리뷰트입니다.

아래는 패킷 테이블의 sql문입니다.

<img width="338" alt="변경된 패킷 sql" src="https://user-images.githubusercontent.com/60510921/97792826-f7672880-1c26-11eb-8a4e-b27f08596db3.png">

패킷 테이블의 어트리뷰트들은
복합키로 기본키를 구성하는 Packet_time과 Packet_date가 있습니다.
Packet_date는 스터디 테이블의 Study_date의 외래키이며 날짜를 나타내고 Packet_time은 하루 중 전체 접속시간이 얼마인지 나타냅니다.
Packet_RSSI는 감지된 패킷의 신호 세기가 얼마인지를 나타냅니다.

마지막으로 디택트 테이블의 sql문입니다.

<img width="377" alt="detect table" src="https://user-images.githubusercontent.com/60510921/97792832-02ba5400-1c27-11eb-867c-edffc7fb2eef.png">

이 테이블은 패킷 테이블에 하루 중 언제 감지가 되었는지를 표현하기엔 무리가 있어서 만들었습니다.
detect_date로 패킷 테이블을 참조하며
detect_time으로 감지된 시간들을 표시합니다.


위의 데이터 베이스를 aws에 구축하기 위해 ec2와 rds를 이용했습니다.

아래는 ec2 접속 사진이고

<img width="412" alt="20201031_234212" src="https://user-images.githubusercontent.com/60510921/97783933-56547f80-1bde-11eb-90f7-50452175f307.png"> 

아래는 rds 구축 사진입니다.

<img width="464" alt="20201101_000106" src="https://user-images.githubusercontent.com/60510921/97783936-5e142400-1bde-11eb-903e-11acf481bb71.png">

