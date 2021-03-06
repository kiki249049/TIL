## [1] Foreign Key

### (1) **개념**

- 외래 키(외부 키)
- 관계형 데이터베이스에서 한 테이블이 다른 테이블의 행을 식별할 수 있도록 하는 키입니다.
- 참조하는 테이블에서 1개의 키(속성 또는 속성의 집합)에 해당하고, 이는 참조되는 측 테이블의 기본 키(Primary Key)를 가리킴
- 참조하는 테이블(N)의 행 1개의 값은, 참조되는 측 테이블의 행 값에 대응됨
  - 이 때문에 참조하는 테이블의 행에는, 참조되는 테이블에 나타나지 않는 값을 포함할 수 없음
- 참조하는 테이블의 행 여러 개가, 참조되는 테이블의 동일한 행을 참조할 수 있음

### (2) **특징**

- 키를 사용하여 부모 테이블의 유일한 값을 참조 (참조 무결성)
- 외래 키의 값이 반드시 부모 테이블의 기본 키 일 필요는 없지만 유일해야 함
- [참고] 참조 무결성
  - 데이터베이스 관계 모델에서 관련된 2개의 테이블 간의 일관성을 말함
  - 외래 키가 선언된 테이블의 외래 키 속성(열)의 값은 그 테이블의 부모가 되는 테이블의 기본 키 값으로 존재해야 함

### (3) ForeignKey model field

- A many-to-one relationship

- 2개의 필수 위치 인자가 필요

  1. 참조하는 model class

  2. on_delete 옵션

     - 외래 키가 참조하는 객체가 사라졌을 때 외래 키를 가진 객체를 어떻게 처리할 지를 정의

     - Database Integrity(데이터 무결성)을 위해서 매우 중요한 설정

     - on_delete 옵션에 사용 가능한 값들

       - `CASCADE` : **부모 객체(참조 된 객체)가 삭제 됐을 때 이를 참조하는 객체도 삭제**

       - `PROTECT` : 참조가 되어 있는 경우 오류 발생

       - `SET_NULL` : 부모객체가 삭제 됐을 때 모든 값을 NULL로 치환 (NOT NULL 조건시 불가능)

       - ```
         SET_DEFAULT
         ```

          : 모든 값이 DEFAULT 값으로 치환

         - DEFAULT 설정 있어야 하며 DB에서는 보통 default가 없으면 null로 잡기도 함. 장고는 아님.

       - `SET()` : 특정 함수 호출

       - ```
         DO_NOTHING
         ```

          : 아무것도 하지 않음.

         - 다만, 데이터베이스 필드에 대한 SQL `ON DELETE` 제한 조건을 설정해야 함

       - ```
         RESTRICT
         ```

          (new in 3.1)

         - RestrictedError를 발생시켜 참조 된 객체의 삭제를 방지

  - 데이터 무결성