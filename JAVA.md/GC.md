# GC(Garbage Collector)


##  Garbage Collector란?
> 
 JVM의 메모리 여역 내에 heap 영역에서 사용하지 않는 메모리들을 회수하는 역할을 수행한다.
일회성 객체들을 주기적으로 비워줌으로써 한정된 메모리를 효율적으로 사용할 수 있게 해준다.

---
## Heap 영역이란?
>
객체를 저장하는 메모리 공간으로 클래스 내에 선언되는 모든 객체들이 저장된다.
Heap 영역은 2가지를 전제로 설계된다. 

1. 대부분 객체는 접근 불가능 상태(Unreachable)이 된다.
   
2.  오래된 객체에서 새로운 객체로 참조는 아주 적다.

   위에 두 가지 전제를 토대로 Heap 영역은 참조되는 시간이 적다는 것을 알 수 있고 이로 인해 Heap 영역에 저장되는 객체들은 대부분 일회성 객체라는 것을 알 수 있다.

 Heap 영역은 3가지로 나눌 수 있다.
 Young, Old, MetaSpace가 있다.

 JDK 7까지 있던 Permanent 영역이 사라지고 JDK 8부터는 MetaSpace라는 MetaData를 담는 영역이 생겨났다.

### Minor GC
> Young 영역에서 일어나는 GC이다. Young 영역도 두 개의 내부 영역을 가지고 있다. 하나는 Eden 영역, 다른 하나는 survivor 영역으로 구성된다.
> 새롭게 생겨난 객체는 Eden 영역으로 이동하게 된다. Eden 영역이 객체로 차게 되면 Minor GC가 발생한다. Minor GC가 발생해 Eden 영역에 있는 객체들은 다음 영역인 survivor 영역으로 이동하게 된다. survivor 영역 또한 2개로 나누어지기 때문에 첫 번째 survivor 영역이 차게 되면 Minor GC를 실행해 두 번째 survivor 영역으로 이동하게 한다.


### Full GC
> Old 영역에서 일어나는 GC이다. Young 영역의 모든 내부 영역이 차서 Minor GC가 일어나 Old 영역으로 넘어오게 된다. Full GC의 범위는 모든 Heap 영역 전체이기 때문에 Minor GC의 실행 시간보다 약 10배가 더 걸린다. GC가 일어날 때에는 stop-the-world 라는 것이 발생한다. GC가 발생할 때에는 애플리케이션의 일시적인 중단이 발생한다는 것이다.
