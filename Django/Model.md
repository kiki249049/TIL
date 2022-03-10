장고 복습.

Model을 이용해 게시판을 만들기

### CREATE

Model makemigrations-migrate를 사용해서 DB를 만든다. DB에 등록하는 형식은 Article이라는 class를 model에 만들었다고 하면 article=Ariticle()이런식으로 인스턴스를 만든 후 article.title="first"로 입력하고 article.save()로 등록을 하거나article=Article(title="하이", content="내용")후 article.save()로 넣거나바로 Article.objects.create(title='하이', content='내용') 이런 3가지 방법으로 추가 할 수 있다.

model class의 작성의 예시

```python
from django.db import models

# Create your models here.
class Article(models.Model) :
    title = models.CharField(max_length=10)
    content = models.TextField()
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)

    def __str__(self) :
        return f'{self.pk}번 게시글 - {self.title}'
```

### READ

READ의 명령어

1. all()
2. get() - 주어진 매개변수와 일치하는 객체를 반환.
3. filter() ex) Article.objects.filter(content="django") - "django" 제목을 가진 데이터를 반환.



### UPDATE

article=article.objects.get(pk=1)로 pk=1에 해당하는 개체를 받고 다시 그 객체를 article.title='새 제목' 같이 제목을 새로 갱신해주는 방식으로 update를 진행

### DELETE

article=article.objects.get(pk=1)로 pk=1에 해당하는 개체를 받고 article.delete()로 삭제 진행.



Article index게시판 뼈대를 만든다. - 그다음 new - create post형식으로 form을 넘김-detail를 이용해 내용 자세히 보게 해줌(create를 detail로 redirect해줌+article.pk와 함께)-delete-edit-update(edit에서 바뀐 내용을 post로 update에 전달하고 detail페이지 redirect)순