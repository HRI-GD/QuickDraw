# QuickDraw

**신호를 기다렸다가 상대보다 빠르게 검을 뽑는 2D 반응속도 대결 게임**입니다.

Unreal Engine 5.6과 Blueprint를 사용한 Udemy 강의 기반 학습 프로젝트입니다. 짧은 결투를 구현하면서 게임 단계 관리, 플레이어와 NPC의 역할 분리, 이벤트 기반 통신, 스프라이트 연출을 학습했습니다.

## 프로젝트 개요

- **장르:** 2D 반응속도 / 결투
- **엔진:** Unreal Engine 5.6
- **게임플레이 구현:** Blueprint
- **2D 표현:** Paper2D 스프라이트
- **입력 처리:** Enhanced Input
- **플레이 방식:** 플레이어와 NPC의 대결
- **기본 맵:** `MAP_Duel`

## 플레이 방법

1. 결투가 시작되면 공격 신호를 기다립니다.
2. 느낌표 신호가 나타나면 **Space Bar**를 눌러 공격합니다.
3. 공격 결과에 따라 캐릭터의 공격·패배 연출이 진행됩니다.

입력은 `IA_Attack` 액션과 `IMC_Duel` 매핑 컨텍스트로 구성되어 있습니다.

## 주요 구현 요소

### 게임 단계와 라운드 흐름

`GM_Duel`과 `E_Phase`를 사용해 결투의 진행 단계를 관리합니다.

```text
Intro → Wait → Draw → Finished
등장     대기    공격     종료
```

- 시작 지연과 무작위 대기 시간을 이용한 공격 신호 타이밍 구성
- 현재 단계에 따른 공격 처리
- 라운드 종료 후 재시작 흐름 구성

### 플레이어와 NPC의 역할 분리

- `BP_Samurai`: 캐릭터의 공통 공격·패배 동작과 연출
- `BP_Samurai_Player`: Enhanced Input을 통한 플레이어 입력 처리
- `BP_Samurai_NPC`: 공격 신호에 반응하는 NPC 동작과 공격 지연 처리

공통 동작과 입력 주체별 처리를 나누어 Blueprint 상속 구조를 학습했습니다.

### 이벤트 기반 통신

`GM_Duel`의 `DrawPhaseStarted` 이벤트 디스패처를 통해 공격 단계의 시작을 알리고, NPC가 해당 신호에 반응하도록 구성했습니다.

### 스프라이트와 사운드 연출

- 대기·공격·패배 상태별 캐릭터 스프라이트
- Timeline을 활용한 공격 동작 연출
- `BP_Exclamation`을 이용한 시각적 공격 신호
- 발도 사운드를 통한 공격 피드백

## 실행 방법

**Unreal Engine 5.6**이 필요합니다.

1. 저장소를 내려받습니다.

   ```bash
   git clone https://github.com/HRI-GD/QuickDraw.git
   ```

2. `QuickDraw.uproject`를 Unreal Editor로 엽니다.
3. 기본 맵 `Content/Maps/MAP_Duel`이 열리는지 확인합니다.
4. 에디터의 **Play** 버튼을 누릅니다.
5. 게임 화면을 클릭해 입력 포커스를 준 뒤 **Space Bar**로 공격합니다.

## 프로젝트 구조

```text
QuickDraw/
├── QuickDraw.uproject
├── Config/                       프로젝트 및 입력 설정
├── Content/
│   ├── Blueprints/
│   │   ├── Enums/E_Phase         결투 진행 단계
│   │   ├── GM_Duel              게임 규칙과 라운드 관리
│   │   ├── BP_Samurai           캐릭터 공통 동작
│   │   ├── BP_Samurai_Player    플레이어 입력
│   │   ├── BP_Samurai_NPC       NPC 동작
│   │   └── BP_Exclamation       공격 신호
│   ├── Input/                   입력 액션과 매핑 컨텍스트
│   ├── Maps/                    결투 맵
│   └── PaperAssets/             배경·캐릭터·효과음 리소스
└── Build/Windows/               애플리케이션 아이콘
```

## 학습 포인트

- Enum으로 게임 흐름을 명시적으로 구분하기
- GameMode에서 라운드 규칙을 관리하고 캐릭터 동작과 분리하기
- Blueprint 상속으로 공통 동작을 공유하기
- 이벤트 디스패처로 게임 단계 변경을 전달하기
- Enhanced Input의 액션과 키 매핑을 연결하기
- 시각·청각 피드백으로 입력 결과를 전달하기

## 학습 출처

이 저장소는 **Udemy 강의를 기반으로 구현한 프로젝트의 학습 기록**입니다. 포트폴리오에서는 위 구현 구조와 학습 내용을 중심으로 소개합니다.

캐시, 중간 빌드 파일, 로그, 패키징된 실행 파일은 저장소에서 제외했습니다. 실행은 Unreal Editor에서 프로젝트를 여는 방식을 기준으로 합니다.
