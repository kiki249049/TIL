'{name : 'Lotto', params : {luckyNums:6}}'

이름과 router설정.

![image-20220510130612236](C:\Users\kiki2\AppData\Roaming\Typora\typora-user-images\image-20220510130612236.png)



part - snippet

q - query

type - video

### Youtube 불러오기 흐름

App.vue - selectBar.vue연동 - VideoList.vue 연동 - VideoList와 VideoListItem.vue 연동 - videoListItem에서 selected된 video를 VideoList로 올림 - VideoList에서 App으로 selectedvideo를 올림 - 다시 Selectedvideo정보를 - videoDetail로 보냄





1. SearchBar에서 쓰고 fetch-videos를 app에 넘겨준다. -> 검색한 url의 비디오 묶음 videos를 app에게 emit함.
2. 그 videos를 videoList가 바인딩으로 받는다.
3. 바인딩 받는 videos를 v-for문으로 돌리면서 videoListItem에 li로 하나씩 넘겨줌
4. videoListItem 각각 개체는 선택을 당하면 select됐다는 것이므로 emit으로 다시 videoList에 넘겨줌
5. videoList는 넘겨진 selectvideo를 App에 전달.
6. App은 selectvideo를 VideoDetail로 넘겨서 화면 가운데에 송출.