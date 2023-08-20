```C
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class NewBehaviourScript : MonoBehaviour
{
    int health;
    string title = "전설의";
    int level = 5;
    float Strength = 15.5f;
    string playerName = "나검사";
    bool isFullLevel = false;
    int exp = 1500;

    void Start()
    {
        //1. 변수
        int level = 5;
        float Strength = 15.5f;
        string playerName = "나검사";
        bool isFullLevel = false;

        Debug.Log("용사의 이름은 ?");
        Debug.Log(playerName);
        Debug.Log("용사의 레벨은?");
        Debug.Log(level);
        Debug.Log("용사의 힘은?");
        Debug.Log(Strength);
        Debug.Log("용사는 만렙인가?");
        Debug.Log(isFullLevel);

        //2. 그룹형 변수
        string[] monsters = { "슬라임", "사막뱀", "악마" };

        Debug.Log("맵에 존재하는 몬스터");
        Debug.Log(monsters[0]);
        Debug.Log(monsters[1]);
        Debug.Log(monsters[2]);

        int[] monsterLevel = new int[3];
        monsterLevel[0] = 1;
        monsterLevel[1] = 6;
        monsterLevel[2] = 20;

        Debug.Log("맵에 존재하는 몬스터의 레벨은?");
        Debug.Log(monsterLevel[0]);
        Debug.Log(monsterLevel[1]);
        Debug.Log(monsterLevel[2]);

        List<string> items = new List<string>();
        items.Add("생명물약 30");
        items.Add("마나물약 30");

        items.RemoveAt(0);

        //3. 연산자
        int exp = 1500;

        exp = 1500 + 320;
        exp = exp - 10;
        level = exp / 300;
        Strength = level * 3.1f;

        Debug.Log("용사의 총 경험치는?");
        Debug.Log(exp);
        Debug.Log("용사의 레벨은?");
        Debug.Log(level);
        Debug.Log("용사의 힘은?");
        Debug.Log(Strength);

        int nextexp = 300 - (exp % 300);
        Debug.Log("다음 레벨을 위한 남은 경험치는?");
        Debug.Log(nextexp);

        string title = "전설의";
        Debug.Log("용사의 이름은?");
        Debug.Log(title + " " + playerName);

        int fullLevel = 99;
        isFullLevel = level == fullLevel;
        Debug.Log("용사는 만렙입니까?" + isFullLevel);

        bool isEndTutorial = level > 10;
        Debug.Log("튜토리얼이 끝난 용사입니까?" + isEndTutorial);

        int health = 30;
        int mana = 25;
        bool isBadCondition = health <= 50 || mana <= 20;
        Debug.Log("용사의 상태가 나쁩니까?" + isBadCondition);

        string condition = isBadCondition ? "나쁨" : "좋음";
        Debug.Log("용사의 상태가 나쁩니까?" + condition);

        //4. 키워드
        //int float string bool new List

        //5. 조건문
        if (condition == "나쁨")
        {
            Debug.Log("플레이어 상태가 나쁘니 물약을 사용하세요.");
        }
        else
        {
            Debug.Log("플레이어 상태가 좋습니다.");
        }

        if (isBadCondition && items[0] == "생명물약30")
        {
            items.RemoveAt(0);
            health += 30;
            Debug.Log("생명물약30을 사용하였습니다.");
        }
        else if (isBadCondition && items[0] == "마나물약30")
        {
            items.RemoveAt(0);
            mana += 30;
            Debug.Log("마나물약30을 사용하였습니다.");
        }

        switch (monsters[1])
        {
            case "슬라임":
            case "사막뱀":
                items.RemoveAt(0);
                health += 30;
                Debug.Log("소형 몬스터 출현!");
                break;
            case "악마":
                Debug.Log("중형 몬스터 출현!");
                break;
            case "골렘":
                Debug.Log("대형 몬스터 출현!");
                break;
            default:
                Debug.Log("??? 몬스터 출현!");
                break;
        }

        //6. 반복문
        while (health > 0)
        {
            health--;
            if (health > 0)
                Debug.Log("독 데미지를 입었습니다." + health);
            else
                Debug.Log("사망하였습니다.");
        }

        for (int count = 0;  count < 10; count++)
        {
            health++;
            Debug.Log("붕대로 치료 중..." + health);
        }

        for (int index = 0; index < monsters.Length; index++)
        {
            Debug.Log("이 지역에 있는 몬스터 : " + monsters[index]);
        }

        foreach (string monster in monsters)
        {
            //Debug.Log("이 지역에 있는 몬스터 : " + monster);
        }

        Heal();

        for (int index = 0; index < monsters.Length; index++)
        {
            Debug.Log("용사는" + monsters[index] + "에게" +
                Battle(monsterLevel[index]));
        }
    }

    //7. 함수 (메소드)
    void Heal()
    {
        health += 10;
        Debug.Log("힐을 받았습니다. " + health);
    }

    string Battle(int monsterLevel)
    {
        string result;
        if (level >= monsterLevel)
            result = "이겼습니다.";
        else
            result = "졌습니다.";

        return result;
    }
}
```

```C
//8. 클래스 : 상속의 개념을 이용해 부모의 메서드를 자식이 사용 가능.
        Player player = new Player();
        player.id = 0;
        player.name = "나법사";
        player.title = "현명한";
        player.strength = 2.4f;
        player.weapon = "나무 지팡이";

        Debug.Log(player.Talk());
        Debug.Log(player.HasWeapon());

        player.LevelUp();
        Debug.Log(player.name + "의 레벨은" + player.level + "입니다.");

        Debug.Log(player.move());

		using System.Collections;
		using System.Collections.Generic;
		using UnityEngine;
		
		public class Player : Actor
		{
		   public string move()
		    {
		        return "플레이어는 움직입니다.";
		    }
		}

```
### LifeCycle
전반적인 게임 프레임의 과정을 코드로 구현한 예시

```C
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class LifeCycle : MonoBehaviour
{
    // 게임 프레임 순서 : 초기화 -> 물리 ->게임로직 -> 해체

    // 밑 함수 두개가 초기화 영역
    private void Awake()
    {
        Debug.Log("플레이어 데이터가 준비되었습니다.");
    }

    // 게임 오브젝트가 활성화 되었을 때
    private void OnEnable()
    {
        Debug.Log("플레이어가 로그인했습니다.");   
    }

    private void Start()
    {
        Debug.Log("사냥 장비를 챙겼습니다.");
    }

    // 물리 연산 업데이트 : 고정된 실행 주기로 CPU 다사용 (초당 50회정도)
    private void FixedUpdate()
    {
        Debug.Log("이동");
    }

    // 게임 로직 업데이트
    private void Update()
    {
        Debug.Log("몬스터 사냥!!");
    }

    // 모든 업데이트 종료 후
    private void LateUpdate()
    {
        Debug.Log("경험치 획득!");
    }

    // 게임이 비활성화 될 때
    private void OnDisable()
    {
        Debug.Log("플레이어가 로그아웃했습니다.");
    }
    // 게임 오브젝트가 삭제될 때
    private void OnDestroy()
    {
        Debug.Log("플레이어 데이터를 해체하였습니다.");
    }
}
```

