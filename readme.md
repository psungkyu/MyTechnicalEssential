# 강의계획서
Nick의 강의계획서 입니다. 전반적인 내용은 이 강의 수준에 맞는 내용이나 강의를 위해 추가적으로 작성한 부분들이 있습니다. 이는 강의에 깊이를 더하고 풍부하게 준비하기 위한 내용이므로 읽어보셔도 좋고 패스하셔도 됩니다. 기본적으로는 저를 위한 콘텐츠이지만 수강생이 전반적으로 어떤 것을 배울 지 알 수 있기 때문에 공유합니다. 

## 목표
강의를 수강하면 아래의 내용을 알게 된다.
* AWS 서비스를 이용하여 일반적인 아키텍처를 이해할 수 있다.
* 기본적인 서비스의 용도를 이해하고 적용할 수 있다.


## 목차
강의의 형태에 따라 시간이나 기간이 유동적으로 바뀔 수 있음을 알려드립니다.

### 1주차 (2021.03.14. 9:00am - 11:30am)

* AWS에 대한 전반적인 소개(30분)
    * AWS의 경우 최대 클라우드 제공자 중 하나. 거의 모든 지역에 걸쳐 데이터 센터를 구축. 전 세계의 데이터 센터에서 실행되는 시스템에 낮은 지연 시간, 많은 처리량의 연결을 제공하기 위해 고대역 광섬유 네트워크 회선을 사용해 전 세계를 감싼다. (위키북스, 클라우드 네이티브 아키텍처 93p 참고)
    * 리전 - aws가 서비스하는 위치를 의미하며 지리적으로 인프라를 추상화 한 개념, 2개 이상의 가용영역으로 이루어져 있음
        * 리전을 결정할 때 무엇을 고려해야 하는가? 
            * 내가 이용할려고 하는 서비스가 있는 지
            * 가격이 적정한 지
    * 가용영역(Availability Zone, AZ) - 여러 데이터 센터가 클러스터 형태로 구성되어 있는 집합체. 
    * 엣지 로케이션 - Caching을 담당하는 시설물. 인구밀도가 높은 도시에 위치하여 있음. 전세계적으로 200여개 이상.
        * 엣지 로케이션을 이용하는 AWS 서비스 예시
            * CloudFront
            * Route53
            * WAF
            * Shield
            * Lambda
    * 멀티테넌시(Mulltitenancy) - 여러 사용자를 가진 아키텍처. 많은 사람이 같은 기능을 사용하는 웹 메일 서비스가 대표적. 중요한 것은 각 사용자가 독립적으로 이용할 수 있어야 한다. [링크](https://www.itworld.co.kr/news/101255)
    + 화이트보딩(리전과 가용영역 그리고 엣지 로케이션과의 관계)

* AWS의 기본적인 서비스 소개(1시간)
    * EC2 - AWS의 기본적인 컴퓨팅 서비스
        * 인스턴스 vs 서버
        * EC2 라이브 사이클, 가격 정책 모델 숙지([전용호스트와 전용인스턴스의 차이](https://aws-diary.tistory.com/84)), 그 외에도 Savings plan이 있음.
            * 온디맨드
            * 예약 인스턴스 
                * 온디맨드에 비해 75% 정도 저렴
            * 예정된 인스턴스
            * 스팟 인스턴스
                * 온디맨드에 비해 90% 정도 저렴
            * 전용 인스턴스
            * 전용 호스트
            * Savings Plans
        * 유저 데이터, 메타 데이터 설명
        * 인스턴스 유형
            * T2/T3 인스턴스 - 개발 환경
            * C5 인스턴스 - 고성능 웹 서버
            * H1 인스턴스 - 고성능 데이터베이스
            * P3 인스턴스 - 딥 러닝
            * R4/R5 인스턴스 - 분산 파일 시스템
    * Amazon VPC - AWS의 클라우드에서 격리된 프라이빗한 가상 네트워크
        * 서브넷마스크, CIDR 블록 [IP 주소를 묶는 방법, CIDR란?](https://www.youtube.com/watch?v=kYiQGpPVnyI), [cidr.xyz](https://cidr.xyz/)
        + (필요하다면) 서브넷마스크 개념 화이트보딩
        * NAT 게이트웨이 - 내부 내트워크에서는 공인되지 않은 IP 주소를 사용하고, 인터넷으로 나갈 때만 공인 주소(즉 유일한 IP 주소)를 가지고 나가는 방식(IP mascarading). 반드시 EIP(Elastic IP, 고정 IP)를 할당해주어야 함.
        * 보안 액세스 옵션들
            * AWS Site-to-Site VPN
            * AWS Direct Connect
            * AWS Transit Gateway - VPC나 온프레미스 등의 네트워크를 단일 지점으로 연결할 수 있는 라우팅 서비스. 여러 VPC와 여러 온프레미스 환경 간의 네트워크를 게이트웨이를 통해 연결한다.
            * AWS VPN CloudHub
            * 소프트웨어 VPN
    * EBS - 블록 스토리지 서비스
        * 주요 기능
            * EC2의 루트 볼륨 스토리지로 사용
            * EBS에 저장된 데이터는 가용 영역 내에 자동으로 복제
            * EBS 볼륨은 연결된 인스턴스의 워크로드로 투명하게 암호화
        * 여러 EBS 스토리지 타입들 설명
            * SSD - 메모리와 같이 반도체로 만들어졌지만, 전기가 없어도 데이터가 사라지지 않음. 
                * Provisioned IOPS 
                * GP3(새로운 모델), GP2
            * HDD - 장기 저장 목적의 데이터 저장 장소로 사용. 
                * Throughput optimized
                * Cold HDD
    * 인스턴스 스토어 - 호스트 디바이스의 직접 연결되어 있는 로컬 디스크 
        * 일반적인 로컬 디스크에는 아래와 같은 것들이 저장
            * OS의 바이너리 파일
            * OS 메모리 페이징
            * 스왑 영역
    * 데모 1 - [EC2 프로비저닝 해보기](./modules/demo/1.md)
    * S3 - 오브젝트 스토리지 서비스
        * 리전 레벨의 서비스. 여러 가용영역에 복제되어 높은 내구성 보장. 
        * 메타데이터의 의미(바이너리 데이터 + 메타데이터)
        * 버저닝, 정적 웹 호스팅, 미디어 호스팅, 백업 용도로 사용 등
        * 블록 스토리지와 오브젝트 스토리지의 차이점 설명(파일 스토리지에 대해서도 알고 있어야 함)
    * 데모 2 - [S3를 이용하여 정적 웹 호스팅 해보기](./modules/demo/2.md), S3의 리소스 정책 설명
    * 실습 1 - VPC 구축해보기 [링크](./practice/1.md)

### 2주차 (2021.03.21. 9:00am - 11:30am)

* IAM(Identity & Access Management) - 권한 제어 접근 관리 서비스.
    * 보안이 중요한 이유는 우리는 다른 사람들의 자료를 관리하며, 따라서 다른 사람의 자료를 보호할 의무가 있기(법적으로나 도의적으로나) 때문이다. 
    * User - 기본적인 사용 단위. 영구적인 권한 부여하는 방법. 여러 그룹에 속할 수 있음.
    * Role - 사용자나 그룹 그리고 리소스에 부여할 수 있음. 임시적으로 권한을 부여하는 방법.
    * Group - User를 묶을 수 있는 단위. 여러 User를 포함할 수 있음.
    * Policy - 사용자의 권한이 명세되어 있는 JSON 파일. User, Role 그리고 Group에 부여 가능.
        * 명시적 거부, 명시적 허용, 묵시적 거부 설명(내용이 길어질 경우에는 우선순위의 관계 설명을 생략)
    * AWS STS(Security Token Service) -
    + 화이트보딩(전반적인 IAM 서비스를 주체들을 기반으로 관계 설명)
    * 데모 3 - [IAM 사용하기](./modules/demo/3.md)

* 데이터베이스
    * SQL vs NoSQL
    * AWS 관리형 데이터베이스 서비스
        * Amazon DynamoDB
        * Amazon ElastiCache
        * Amazon RDS - MySQL, MongoDB, PostgreSQL 등 다양한 데이터베이스 서버를 호스팅함.
            * (공부하면서 필요한 내용들 적음, '디벨로퍼 에드보킷 테크 에반젤리스트로 산다는 것'의 27p 참조) MongoDB의 경우 소프트웨어도 좋고 일정 비용을 지불하면 전문적인 기술지원이 가능함. 그러나 서버에만 초점이 되어 있다는 점이 아쉬운 점. 웹 브라우저와 같이 로컬 환경에 데이터를 저장해야 한다거나, 다수의 인스턴스들끼리 동기화를 하고 싶어도 마땅한 방법이 없어 오프라인 환경에는 적합하지 않음. 이럴 경우에는 PouchDB(Javascript 기반의 NoSQL 데이터베이스)나 CouchDB(아파치 재단에서 관리하는 NoSQL 데이터베이스)를 알아보는 것이 좋음.
        * Amazon Aurora
        * Amazon Neptune
        * Amazon Redshift
        * Amazon DocumentDB 
    * RDS - 관계형 데이터베이스
        * DB 인스턴스의 개념 - 클라우드에서 실행하는 격리된 데이터베이스 환경. 데이터베이스 엔진을 지원. 
        * DB 인스턴스 스토리지 - 데이터베이스 및 로그 스토리지의 크기 때문에 Amazon EBS를 사용함. Amazon RDS는 필요한 스토리지 용량에 따라 자동으로 데이터를 여러 Amazon EBS 볼륨에 나누어 저장하여 성능을 강화함. [링크](https://docs.aws.amazon.com/ko_kr/AmazonRDS/latest/UserGuide/CHAP_Storage.html)
        * Amazon RDS 백업 작동 방식은 어떻게 이루어지는가?
            * 교차 리전 스냅샷 - RDS의 스냅샷을 다른 리전으로 복사하는 것. DB 인스턴스 차체를 이전할 수 없으므로 스냅샷을 이동시키는 것.
        * RDS 보안
            * SSL(Secure Socket Layer) 연결 사용
            * TDE(Transparent Data Encryption) 사용
        * 데모 4 - [Multi-AZ MySQL 디비 인스턴스 프로비저닝](./modules/demo/4.md)    
    * DynamoDB - 비관계형 데이터베이스
        * 테이블
        * 파티션 키
        * 정렬 키
        * 아이템(항목)
        * 요금 정책
            * 온디맨드 모드 [링크](https://aws.amazon.com/ko/dynamodb/pricing/on-demand/)
                * 쓴 만큼 비용이 나감
                * 트래픽이 발생한 만큼 내는 구조
                * 장비 spec을 설정하지 않는다는 특징이 있음
            * 프로비저닝된 용량 요금 [링크](https://aws.amazon.com/ko/dynamodb/pricing/provisioned/)
                * RCU(읽기 용량 유닛) : 테이블에서 데이터를 읽는 각 API 호출은 읽기 요청. 최대 4KB 크기 항목의 경우 1개의 RCU가 초당 1회의 강력한 일관된 읽기 요청을 수행할 수 있음.
                * WCU(쓰기 용량 유닛) : 데이블에 데이터를 쓰는 각 API 호출은 쓰기 요청. 최대 1KB 크기 항목의 경우 1개의 WCU가 초당 1회의 표준 쓰기 요청을 수행할 수 있음. 1KB보다 큰 항목의 경우 추가 WCU가 필요함. 
    * 실습 2 - 데이터베이스를 프라이빗 서브넷에 Multi-AZ 형태로 구축하고 웹 서버와 연동하기

* 고가용성 아키텍처 및 모니터링 시스템
    * Auto Scaling
        * CloudWatch 알람을 이용하여 Auto Scaling 트리거하는 것. 
        * 예약 오토 스케일링, 동적 오토 스케일링, 기계학습 기반의 오토 스케일링의 차이
    * ELB
        * CLB - EC2-classic에서 운영하던 로드 벨런서. 추가적인 버전이 없음.
        * ALB - L7 영역에서 HTTP/HTTPS 프로토콜이나 URL 기반으로 룰을 셋팅하고 타켓 그룹을 설정할 수 있음.
        * NLB - L4 레벨에서 포트번호를 기반으로 분기 설정 가능. 더 빠른 성능을 보장.
    * CloudWatch - 모니터링 서비스
    * 데모 3 - CloudWatch 기본적인 메트릭 확인하는 법과 대시보드 활용법 [생활코딩 영상 링크](https://www.youtube.com/watch?v=jGryI-hBA38)
        1. Metric에서 EC2 관련된 다양한 메트릭을 보여주기
        2. CPUUtilization을 이용해서 대시모드 만들기
        3. 시간축을 기준으로 얼마만큼의 기간을 확인할 수 있는 지 보여줄 것 - 장기간 데이터를 보고싶은 경우에는 전체 시간 지표를 늘린다
        4. 평균이나 기간값을 늘려서 얼마나 더 자세하게 보고 싶은 지를 설정할 수 있다. [CloudWatch Metrics Retention](https://aws.amazon.com/about-aws/whats-new/2016/11/cloudwatch-extends-metrics-retention-and-new-user-interface/)
        5. 대시보드에 추가해서 저장하는 것 보여주기
        6. 지표화면에서 보기로 들어가서 지표를 다시 마음대로 바꿀 수 있도록 하는 것 보여주기
        7. 위에 지표에서 커스텀 15분으로 메트릭 변형해서 대시보드에 추가하기
    * 실습 3 - 로드밸런서를 이용하여 인스턴스를 자동으로 프로비저닝하는 것 구성하기


## 고객 사례 레퍼런스
1. This is my architecture [링크](https://www.youtube.com/watch?v=K5ww_O4vsxo&list=PLhr1KZpdzukdeX8mQ2qO73bg6UKQHYsHb) - 다양한 고객 사례를 확인할 수 있고 실제로 워크로드에 따라 아키텍처를 어떻게 설계하는 지 확인할 수 있습니다. 
2. AWS 고객 성공 사례 [링크](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc) - 다양한 고객의 마이그레이션에 대한 사례를 확인할 수 있습니다.


## 추가적으로 더 해야 할 일
1. 간단한 CRUD 시스템으로 웹 서버 구축하기
2. CloudFormation으로 실습에 필요한 JSON 파일 만들어보기
3. FAQ
    * S3는 멀티리전을 지원하는가?
    * DynamoDB를 켜놓고 쓰지도 읽지도 않았는데 비용이 나오는 이유는?
        * 데이터를 갱신하는 시스템에서는 트랜잭션 내용을 기록해 둠으로써 데이터 안정성을 높일 수 있다. 트랜잭션을 기반으로 롤백할 지 롤포워드 할 지 결정한다. (그림으로 공부하는 IT 인프라 구조 중 152p)
    * DynamoDB에서 GB당 비용이 발생하는데 0.03GB 사용하면 1GB 사용했을 때 요금이랑 같은가?
    * CloudFormation에서 파라미터는 어떻게 하면 잘 사용할 수 있을까?
    * 전용 호스트랑 전용 인스턴스에 리전 개념이 있는가? 리전에 따라서 가격이 다릅니까?