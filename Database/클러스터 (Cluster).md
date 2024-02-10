### 클러스터 (Cluster)

- 각기 다른 것들을 하나로 묶어서 하나의 시스템같이 동작하게 함으로써, 클라이언트들에게 고가용성의 서비스를 제공하는 것이다.
- 클러스터로 묶인 한 시스템에 장애가 발생하면, 정보의 제공 포인트는 클러스터로 묶인 다른 정상적인 것으로 이동한다.

### 클러스터링(Clustering)

- DB 분산 기법 중 하나로 DB 서버를 여러 개를 두어 서버 한 대가 죽었을 때 대비할 수 있는 기법

### Active-Active Clustering

- DB 서버를 여러개 구성하는데 각 서버를 Active 상태로 둔다.
    - (+) 서버 하나가 죽더라도 다른 서버가 역할을 바로 수행하므로 서비스 중단이 없다.
    - (+) CPU와 메모리 이용률을 올릴 수 있다.
    - (-) 저장소 하나를 공유하게 되면 병목현상이 발생할 수 있다.
    - (-) 서버를 여러대 한꺼번에 운영하므로 비용이 더 발생한다.

### Active-Standby Clustering

- 서버를 하나만 운영하고 나머지 서버는 Standby 상태로 둔다. ⇒ 운영하고 있는 서버가 다운되었을 시에 Standby 상태의 서버를 Active 상태로 전환한다.
    - (+) Active-Avtice 클러스터링에 비해 적은 비용이 든다.
    - (-) 서버가 다운되었을 때 Standby 상태의 서버를 Active 상태로 전환 시 시간이 든다.

### 💡 Reference

- https://allpartner.tistory.com/11
- [https://dheldh77.tistory.com/entry/데이터베이스-클러스터링Clustering](https://dheldh77.tistory.com/entry/%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B2%A0%EC%9D%B4%EC%8A%A4-%ED%81%B4%EB%9F%AC%EC%8A%A4%ED%84%B0%EB%A7%81Clustering)
- [https://rastalion.me/mariadb-galera를-이용한-다중화-구성/](https://rastalion.me/mariadb-galera%EB%A5%BC-%EC%9D%B4%EC%9A%A9%ED%95%9C-%EB%8B%A4%EC%A4%91%ED%99%94-%EA%B5%AC%EC%84%B1/)
- https://sarc.io/index.php/mariadb/599-mysql-replication-galera-cluster
- https://m.blog.naver.com/youngchanmm/221922599192