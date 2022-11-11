# Amazon Athena란 무엇인가요?
- Amazon Athena는 표준 SQL을 사용하여 Amazon S3(Amazon Simple Storage Service)에 있는 데
이터를 직접 간편하게 분석할 수 있는 대화형 쿼리 서비스
- AWS Management Console에서 몇 가지 작업을 수행하면 Athena에서 Amazon S3에 저장된 데이터를 지정하고 표준 SQL을 사용하여 임시 쿼리를
실행하여 몇 초 안에 결과를 얻을 수 있음
- Athena는 서버리스 서비스이므로 설정하거나 관리할 인프라가 없으며 실행한 쿼리에 대해서만 비용을 지불
함 
- Athena는 자동으로 확장되어 쿼리를 병렬로 실행하여 대규모 데이터 집합과 복잡한 쿼리에서
도 빠르게 결과를 얻을 수 있습니다.

# Athena는 언제 사용해야 하나요?
Amazon Athena와 같은 쿼리 서비스, Amazon Redshift와 같은 데이터 웨어하우스, Amazon EMR과 같은 정
교한 데이터 처리 프레임워크
## Amazon Athena
- Athena는 Amazon S3에 저장된 비정형, 반정형 및 정형 데이터를 분석하는 데 도움을 줌
  - 예를 들면 CSV, JSON 또는 컬럼 방식 데이터 형식(예: Apache Parquet 및 Apache ORC)이 해당
  - Athena를 사용하면 데이터를 집계하거나 Athena로 로드할 필요 없이 ANSI SQL을 사용한 임의 쿼리를 실행 가능
- Athena는 간편한 데이터 시각화를 위해 Amazon QuickSight와 통합
  - Athena를 사용하여 보고서를 생성하거나 JDBC 또는 ODBC 드라이버를 통해 연결된 비즈니스 인텔리전스 도구 또는 SQL 클라이언트
로 데이터를 탐색 가능
- Athena는 Amazon S3에서 데이터에 대한 지속적 메타데이터 스토어를 제공하는 AWS Glue Data Catalog와
통합
  - 이렇게 하면 Amazon Web Services 계정 전체에서 사용할 수 있는 중앙 메타데이터 스토어를
기반으로 Athena에서 테이블과 쿼리 데이터를 생성하고 AWS Glue의 ETL 및 데이터 검색 기능을 통합할 수
있음
- Amazon Athena를 사용하면 데이터를 포맷하거나 인프라를 관리할 필요 없이 Amazon S3 직접 데이터에 대
해 대화형 쿼리를 쉽게 실행 가능 
- Athena는 웹 로그에서 빠른 쿼리를 실행하여 사이트의 성능 문제를 해결하려는 경우에 유용
- 데이터에 대한 테이블을 정의하고 표준 SQL을 사용하여 쿼리를 시작하기만 하면 됨
- 인프라 또는 클러스터를 관리할 필요 없이 Amazon S3의 데이터에 대해 대화형 임시 SQL 쿼리를 실행하려
면 Amazon Athena를 사용
- Amazon Athena는 서버를 설정하거나 관리할 필요 없이 Amazon S3데이터에 대한 임시 쿼리를 실행할 수 있는 가장 쉬운 방법을 제공

## Amazon EMR
- Amazon EMR을 사용하면 온프레미스 배포와 비교할 때 Hadoop, Spark 및 Presto와 같이 고도로 분산된 처
리 프레임워크를 간단하고 비용 효율적으로 실행할
- Amazon EMR은 유연
- 사용자 지정애플리케이션과 코드를 실행하고 특정 컴퓨팅, 메모리, 스토리지 및 애플리케이션 파라미터를 정의하여 분석
요구 사항을 최적화할 수 있음
- Amazon EMR은 SQL 쿼리를 실행하는 것 외에도 기계 학습, 그래프 분석, 데이터 변환, 데이터 스트리밍 및
사실상 코딩 가능한 거의 모든 업무의 애플리케이션을 위한 다양한 확장 데이터 처리 작업을 실행
- 사용자 지정 코드를 사용하여 Spark, Hadoop, Presto 또는 Hbase 등의 최신 빅 데이터 처리 프레임워
크를 사용하여 매우 큰 데이터 세트를 처리하고 분석하는 경우 Amazon EMR을 사용 
- Amazon EMR을 사용하면 클러스터와 클러스터에 설치된 소프트웨어의 구성을 완벽하게 제어할 수 있음
- Amazon Athena를 사용하면 Amazon EMR을 사용하여 처리하는 데이터를 쿼리할 수 있음
- Amazon Athena는 Amazon EMR과 동일한 여러 데이터 형식을 지원
- Athena의 데이터 카탈로그는 Hive 메타스토어와 호환
- EMR을 사용하고 이미 Hive 메타스토어가 있는 경우, Amazon Athena에서 DDL 문을 실행하고 Amazon EMR 작업에 영향을 주지 않고 즉시 데이터를 쿼리

## Amazon Redshift
- Amazon Redshift와 같은 데이터 웨어하우스는 인벤토리 시스템, 금융 시스템, 소매 판매 시스템 등 다양한
소스의 데이터를 공통 형식으로 가져와서 장기간 저장해야 할 때 가장 좋은 선택
- 과거 데이터에서 정교한 비즈니스 보고서를 작성하려는 경우 Amazon Redshift와 같은 데이터 웨어하우스가 최상의 선택
- Amazon Redshift의 쿼리 엔진은 다수의 매우 큰 데이터베이스 테이블을 조인하는 복잡한 쿼리를 실행할 때 특히 효과적으로 수행되도록 최적화
- 다수의 매우 큰 테이블의 조인이 필요한 고도로 구조화된 데이터에 대해 쿼리를 실행해야 하는 경우
