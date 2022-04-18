### 1. 일대 다 관계(1:N) => ForginKey를 부여

reporter(유저)

articles_article(게시글)

### 2. 다대다 관계(N:M)

ex) 예약시스템. 의사와 환자 진료를 예약하는 시스템을 생각해보자.

의사

환자

2개의 table을 어떻게 관리할까?(의사와 환자의 관계)

만약 1:N 처럼 FK 넣으면 환자가 의사를 2명 만나거나 변경 시 수정이 불가능하다.

따라서 별도의 table을 만드는 것이 핵심이다. 그리고 별도의 table에 추가가 발생하면 아래 부분에 추가 해 주면 된다.

Reservation

추가 예약이 발생하면 아래에 행을 추가시켜서 넣어준다.

이제부터 위의 내용을 모델링을 해보자.

### 2-1. 단순 직관적 모델링

위의 내용을 그대로 models.py에 적어보자

```python
classDoctor(models.Model):
    name = models.CharField(max_length=10)

classPatient(models.Model):
    name = models.CharField(max_length=10)

classReservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```

doctor.reservation_set.all()

patient.reservation_set.all()

### 2-2 중개 모델 활용

의사-환자들 /환자-의사들로 직접 접근을 하기 위해서는 ManyToManyField를 사용한다.

through 를 이용하고 reservation을 통해서, Doctor에 접근. 위와 단순 직관적 모델링과 같은데 ORM 조작만 차이가 난다.

```python
classDoctor(models.Model):
    name = models.CharField(max_length=10)

classPatient(models.Model):
    name = models.CharField(max_length=10)
    doctors = models.ManyToManyField(doctor,
                                    through='Reservation')

classReservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```

doctor.patient_set

patients.doctors

중개 모델 중 반드시 역참조를 써야하는 상황

유저와 게시글, 좋아요누른 사람과 게시글의 관계를 설정시 게시글 클래스에 related_name 없이 정의를 하게 되면 역참조 이슈를 발생한다.

```python
classDoctor(models.Model):
    name = models.CharField(max_length=10)

classPatient(models.Model):
    name = models.CharField(max_length=10)
    doctors = models.ManyToManyField(doctor,
                                    through='Reservation',
                                    related_name='patients')

classReservation(models.Model):
    doctor = models.ForeignKey(Doctor, on_delete=models.CASCADE)
    patient = models.ForeignKey(Patient, on_delete=models.CASCADE)
```

doctor.patients

patients.doctors

**코드해석**(ManyToManyField)

ManyToManyField를 적으면 자연스럽게 table을 하나 더 만들어 준다.

doctor        - 의사와 연결을 시키고 patient는 doctor을 참조한다.

through       - Reservation을 통해 탐색한다

related_name   - 이걸 적으면 보통 through를 지운다. 역참조로 중개 클래스도 삭제해준다. 그 부분이 아래 코드. 그러나 중개 table이 필요한 경우도 있다. 예약날짜 같은 추가 정보가 필요하다면 table을 위 처럼 넣어준다.

2-3. 중개 모델 없이 설정

일반적으로 추가 필드 필요없이 id 값만 존재하는 경우는 아래와 같이 선언한다.

```python
classDoctor(models.Model):
    name = models.CharField(max_length=10)

classPatient(models.Model):
    name = models.CharField(max_length=10)
    doctors = models.ManyToManyField(doctor,
                                    related_name='patients')
```

정리

중개모델이 필요 없는 경우는 특정 Class에 ManyToManyField 선언하자.

중개모델이 필요한 경우에는 중개 모델을 정의 후에 특정 class에 ManyToManyField에 through 옵션을 통해 조작하자.

그리고 ManyToMany에서는 복수형의 포현으로 반드시 related_name을 선언하자.