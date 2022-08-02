### Array와 fill을 이용한 map사용

```react
<div className='product_rating'>
            {
                Array(rating)
                    .fill()
                    .map(() => (
                        <p><StarIcon style={ {color : "orange"} }></StarIcon></p>
                    ))
            }


</div>
```

rating의 크기만큼 Array가 생성되고 안에 fill()으로 인해 undefined로 채워진다(fill안에 인자가 없기 때문). 그 후 undefined를 map함수를 이용해 staricon으로 채워준다. 

### atom, selector

```react
import { atom } from 'recoil'

export const textState = () => {
    key : 'textState',
    default : ''
}
```



### Recoil-persist

```react
npm install persist-recoil
```

