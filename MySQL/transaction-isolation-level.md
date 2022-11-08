### Transaction Isolation Level (트랜잭션 격리 수준)

1. READ UNCOMMITTED
2. READ COMMITTED
3. REPEATABLE READ
4. SERIALIZABLE

|                      | <center>DIRTY READ</center> | <center>NON - REPEATABLE READ</center> | <center>PHANTOM READ</center> |
| :------------------- | :-------------------------: | :------------------------------------: | :---------------------------: |
| **READ UNCOMMITTED** |              O              |                   O                    |               O               |
| **READ COMMITTED**   |              X              |                   O                    |               O               |
| **REPEATABLE READ**  |              X              |                   X                    |      O (InnoDB는 발생 X)      |
| **SERIALIZABLE**     |              X              |                   X                    |               X               |

- **DIRTY READ** : 어떤 트랜잭션에서 처리한 작업이 완료되지 않았는데도 다른 트랜잭션에서 볼 수 있게 되는 현상
- **NON - REPEATABLE READ** : 하나의 트랜잭션 내에서 똑같은 SELECT 쿼리를 실행했을 때는 항상 같은 결과를 가져야하는데 (이를 REPEATABLE READ 정합성 이라 함) 이 정합성이 깨지는 것을 뜻 함
- **PHANTOM READ** : 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상
