## 관련 링크

[관련 링크](https://cornswrold.tistory.com/308)

## 공부한 내용

### supplier에 대해 알게 되었다.

java Optional method에 대해 공부하던 중 .orElseGet()에 대해 알게 되었다.

내부 코드를 보니 인자로 supplier를 받는 것을 볼 수 있었다.
관련 코드는 다음과 같다.

```java
    public T orElseGet(Supplier<? extends T> supplier) {
        return this.value != null ? this.value : supplier.get();
    }

    public <X extends Throwable> T orElseThrow(Supplier<? extends X> exceptionSupplier) throws X {
        if (this.value != null) {
            return this.value;
        } else {
            throw (Throwable)exceptionSupplier.get();
        }
    }
```

내부 코드에서는 제네릭을 활용해 상속받은 모든 것들을 활용할 수 있게 만들어보인다.

여기서 Supplier는 인자없는 함수코드를 실행해준다. 또한 함수형이기에 lazy연산도 가능하다.
