# S&D Golden Zone Clean v1.3

## 📖 사용자 가이드 매뉴얼

---

## 목차

1. [개요](#개요)
2. [핵심 개념](#핵심-개념)
3. [설정 옵션](#설정-옵션)
4. [시그널 시스템](#시그널-시스템)
5. [트리거 패턴](#트리거-패턴)
6. [Info Table 해석](#info-table-해석)
7. [추천 설정](#추천-설정)
8. [트레이딩 가이드](#트레이딩-가이드)
9. [버전 히스토리](#버전-히스토리)
10. [FAQ](#faq)

---

## 개요

**S&D Golden Zone Clean v1.3**은 Supply and Demand 기반의 Zone 탐지 인디케이터입니다.

**"자리(Zone) + 트리거(Confirmation) = 진입"**이라는 단순한 철학으로 설계되었습니다.

### 주요 특징

| 기능 | 설명 |
|------|------|
| **Zone 탐지** | BOS/CHOCH 기반 자동 Supply/Demand Zone 식별 |
| **Golden Zone** | 피보나치 50%/61.8%와 Zone 컨플루언스 |
| **실시간 재판정** | 매 캔들마다 골든존 상태 업데이트 |
| **Shape 시그널** | ◆▲● 로 트리거 강도 직관적 표시 |
| **HTF 필터** | 상위 타임프레임 트렌드 정렬 확인 |
| **Risk 평가** | Opposing Zone 자동 감지 |

---

## 핵심 개념

### Supply and Demand Zone

Supply and Demand Zone은 기관 투자자들의 대량 주문이 집행된 가격대입니다.

| 종류 | 정의 | 라벨 |
|------|------|------|
| **Demand Zone** | 상승 임펄스 직전의 마지막 하락 캔들 | D |
| **Supply Zone** | 하락 임펄스 직전의 마지막 상승 캔들 | S |

### BOS vs CHOCH

| 용어 | 의미 | 라벨 표시 |
|------|------|----------|
| **BOS** | Break of Structure - 기존 추세 방향 돌파 | D, S |
| **CHOCH** | Change of Character - 추세 반전 신호 | D•CH, S•CH |

CHOCH는 추세 전환을 의미하므로 더 신뢰도 높은 존입니다.

### Golden Zone

피보나치 되돌림의 핵심 레벨과 Supply/Demand Zone이 겹치는 구간:

| 레벨 | 의미 | 신뢰도 |
|------|------|--------|
| **61.8%** | 가장 강력한 되돌림 레벨 | ⭐⭐⭐ |
| **50.0%** | 중간 되돌림 레벨 | ⭐⭐ |

**Golden Zone 판정 조건** (하나라도 충족 시):
1. 61.8% 레벨이 Zone 안에 있음
2. 50% 레벨이 Zone 안에 있음
3. Zone 중심점이 50%~61.8% 구간 안에 있음

### 실시간 재판정

v1.3의 핵심 기능: **매 캔들마다 모든 Zone의 골든존 여부를 재계산**

```
[상황]
BOS 발생 → 피보나치 업데이트 → 기존 Zone들의 골든존 상태 변경

[결과]
- 이전에 골든존이었던 Zone → 일반존으로 변경될 수 있음
- 이전에 일반존이었던 Zone → 골든존으로 변경될 수 있음
```

이로 인해 항상 **현재 시점에서 유효한 골든존**만 강조 표시됩니다.

---

## 설정 옵션

### Main Settings

| 설정 | 기본값 | 범위 | 설명 |
|------|--------|------|------|
| Swing Length | 5 | 2-20 | 스윙 포인트 감지 민감도 |
| OB Lookback | 10 | 3-20 | Zone 탐색 범위 (캔들 수) |
| OB Extend Bars | 30 | 10-100 | Zone 박스 우측 연장 길이 |
| Signal Cooldown | 5 | 1-20 | 시그널 재발생 방지 기간 |

**Swing Length 가이드:**
- 낮은 값 (2-4): 민감함, 더 많은 Zone 생성
- 높은 값 (6-10): 둔감함, 더 적은 Zone 생성

### HTF Settings

| 설정 | 기본값 | 옵션 | 설명 |
|------|--------|------|------|
| Enable HTF Filter | ON | ON/OFF | 상위 TF 트렌드 필터 사용 |
| HTF Timeframe | 240 | 60/240/D/W | 상위 타임프레임 설정 |

**HTF 설정 가이드:**

| 현재 TF | 권장 HTF |
|---------|----------|
| 1분-5분 | 60 (1시간) |
| 15분-30분 | 240 (4시간) |
| 1시간-4시간 | D (일봉) |
| 일봉 | W (주봉) |

### Fibonacci

| 설정 | 기본값 | 설명 |
|------|--------|------|
| Use 61.8% Level | ON | 61.8% 레벨 사용 |
| Use 50% Level | ON | 50% 레벨 사용 |
| Show Fib Lines | ON | 피보나치 라인 표시 |

### Signal Filter

| 설정 | 기본값 | 설명 |
|------|--------|------|
| Show Weak Signals (DOJI) | OFF | DOJI 트리거 시그널 표시 |
| Show Only Golden Zones | OFF | 골든존만 표시 |
| Max Order Blocks | 20 | 최대 Zone 표시 개수 |
| Show Mitigated Zones | OFF | 무효화된 존 표시 |

### Visual

| 설정 | 기본값 | 설명 |
|------|--------|------|
| Show Info Table | ON | 정보 테이블 표시 |
| Table Size | small | 테이블 크기 (tiny/small/normal) |
| Show Zone Background | ON | 골든존 진입 시 배경색 |

---

## 시그널 시스템

### 시그널 발생 조건

시그널이 발생하려면 **3가지 조건**이 모두 충족되어야 합니다:

| # | 조건 | 설명 |
|---|------|------|
| ① | **Golden Zone** | 가격이 골든존 안에 있어야 함 |
| ② | **Trigger** | 확인 캔들 패턴이 발생해야 함 |
| ③ | **Cooldown** | 이전 시그널 후 N봉 경과 |

### Shape 시그널 표시

**Shape**으로 트리거 강도를 직관적으로 표시:

| Shape | 트리거 | 강도 | 의미 |
|-------|--------|------|------|
| ◆ 다이아몬드 | IBFB | ⭐⭐⭐ | 적극 진입 |
| ▲ 삼각형 | PIN / ENG | ⭐⭐ | 진입 가능 |
| ● 원형 | DOJI | ⭐ | 신중하게 |

### 시그널 색상

| 색상 | 방향 |
|------|------|
| 🟢 녹색 | Long (매수) |
| 🔴 빨간색 | Short (매도) |

### 쿨다운 시스템

시그널 발생 후 설정된 캔들 수 동안 같은 방향 시그널이 재발생하지 않습니다.

```
[예시: Cooldown = 5]

캔들 1: ◆ LONG 시그널 발생
캔들 2-6: 쿨다운 중 (시그널 없음)
캔들 7: 조건 충족 시 새 시그널 가능
```

---

## 트리거 패턴

### ◆ IBFB (Inside Bar False Breakout) - 강도 3

가장 강력한 반전 신호입니다.

**Bullish IBFB:**
```
1. Inside Bar 형성
   → bar[1]의 High < bar[2]의 High
   → bar[1]의 Low > bar[2]의 Low

2. 아래로 False Breakout
   → 현재 Low < bar[1]의 Low

3. 다시 위로 마감
   → Close > bar[1]의 Low
   → Close > Open (양봉)
```

**Bearish IBFB:**
```
1. Inside Bar 형성
2. 위로 False Breakout → High > bar[1]의 High
3. 다시 아래로 마감 → Close < bar[1]의 High, 음봉
```

### ▲ PIN (Pin Bar) - 강도 2

긴 꼬리가 가격 거부를 나타냅니다.

| 방향 | 조건 |
|------|------|
| Bullish | 아래 꼬리 ≥ 캔들 전체 범위의 60% |
| Bearish | 위 꼬리 ≥ 캔들 전체 범위의 60% |

```
Bullish Pin Bar:

    │
    │  ← 짧은 위 꼬리
    ■  ← 작은 바디
    │
    │
    │  ← 긴 아래 꼬리 (60%+)
```

### ▲ ENG (Engulfing) - 강도 2

이전 캔들을 완전히 감싸는 반전 패턴입니다.

| 방향 | 조건 |
|------|------|
| Bullish | 전봉 음봉 + 현봉 양봉이 전봉을 완전히 감쌈 |
| Bearish | 전봉 양봉 + 현봉 음봉이 전봉을 완전히 감쌈 |

```
Bullish Engulfing:

   ■      │
   │      ■
   │  →   ■
          ■
          │
  음봉   양봉(감싸기)
```

### ● DOJI (Doji + Direction) - 강도 1

우유부단 후 방향 결정을 나타냅니다.

| 방향 | 조건 |
|------|------|
| Bullish | 전봉 도지 (바디 < 범위의 10%) + 현봉 양봉 |
| Bearish | 전봉 도지 + 현봉 음봉 |

**참고:** 기본적으로 DOJI 시그널은 숨겨져 있습니다. `Show Weak Signals` 옵션으로 활성화할 수 있습니다.

---

## Info Table 해석

### 테이블 구조

```
┌─────────────────────────────┐
│  S&D Golden    │    v1.3   │  ← 버전 정보
├─────────────────────────────┤
│  Trend:        │    ▲/▲    │  ← LTF/HTF 트렌드
│  Zones:        │ 20(G:1 M:14)│ ← 존 현황
│  In Zone:      │ 🟢 Golden D │ ← 현재 위치
│  Trigger:      │  ◆ IBFB   │  ← 확인 신호
│  Risk:         │   Clean   │  ← 위험도
│  Signal:       │  ◆ LONG   │  ← 최종 판단
├─────────────────────────────┤
│  ◆강 ▲중 ●약  │ Shape 범례 │  ← 참고
└─────────────────────────────┘
```

### 필드별 상세 설명

#### Trend (추세)

| 표시 | 의미 |
|------|------|
| ▲/▲ | LTF 상승 / HTF 상승 |
| ▼/▼ | LTF 하락 / HTF 하락 |
| ▲/▼ | LTF 상승 / HTF 하락 (불일치) |
| ▼/▲ | LTF 하락 / HTF 상승 (불일치) |

| 색상 | 의미 |
|------|------|
| 🟢 녹색 | 정렬됨 (LTF = HTF) |
| 🟠 주황색 | 불일치 (LTF ≠ HTF) |

#### Zones (존 현황)

```
20 (G:1 M:14)
│    │    │
│    │    └── M: Mitigated (무효화된 존)
│    └─────── G: Golden (골든존)
└──────────── 전체 Zone 개수
```

#### In Zone (현재 위치)

| 표시 | 의미 | 행동 |
|------|------|------|
| 🟢 Golden D | 골든 Demand Zone 안 | 롱 준비 |
| 🔴 Golden S | 골든 Supply Zone 안 | 숏 준비 |
| D | 일반 Demand Zone 안 | 관망 |
| S | 일반 Supply Zone 안 | 관망 |
| — | 존 밖 | 대기 |

#### Trigger (확인 신호)

| 표시 | 트리거 | 강도 |
|------|--------|------|
| ◆ IBFB | Inside Bar False Breakout | 강 |
| ▲ PIN/ENG | Pin Bar 또는 Engulfing | 중 |
| ● DOJI | Doji + Direction | 약 |
| 대기중 | 트리거 없음 | - |

#### Risk (위험도)

| 표시 | 의미 | 행동 |
|------|------|------|
| Clean (녹색) | 반대 존 없음 | 풀 사이즈 가능 |
| ⚠️ Opposing (주황) | 근처에 반대 존 있음 | 사이즈 축소 권장 |

**Opposing 판정 기준:** 진입 방향 반대쪽 ATR×3 내에 반대 존 존재

#### Signal (최종 판단)

| 표시 | 의미 | 행동 |
|------|------|------|
| ◆ LONG | 강한 롱 시그널 | 즉시 매수 |
| ▲ LONG | 보통 롱 시그널 | 매수 |
| ● LONG | 약한 롱 시그널 | 신중하게 매수 |
| ◆ SHORT | 강한 숏 시그널 | 즉시 매도 |
| ▲ SHORT | 보통 숏 시그널 | 매도 |
| ● SHORT | 약한 숏 시그널 | 신중하게 매도 |
| ⏳ WAIT L | 롱 대기 | 트리거 기다려 |
| ⏳ WAIT S | 숏 대기 | 트리거 기다려 |
| — | 조건 없음 | 관망 |

---

## 추천 설정

### 스캘핑 (1분 ~ 15분)

```
═══ Main Settings ═══
Swing Length: 3
OB Lookback: 5
Signal Cooldown: 3

═══ HTF Settings ═══
Enable HTF Filter: ON
HTF Timeframe: 60

═══ Signal Filter ═══
Show Weak Signals: OFF
Show Only Golden Zones: ON
Max Order Blocks: 10
```

### 데이트레이딩 (30분 ~ 1시간)

```
═══ Main Settings ═══
Swing Length: 5
OB Lookback: 10
Signal Cooldown: 5

═══ HTF Settings ═══
Enable HTF Filter: ON
HTF Timeframe: 240

═══ Signal Filter ═══
Show Weak Signals: OFF
Show Only Golden Zones: OFF
Max Order Blocks: 15
```

### 스윙 트레이딩 (4시간 ~ 일봉)

```
═══ Main Settings ═══
Swing Length: 8
OB Lookback: 15
Signal Cooldown: 3

═══ HTF Settings ═══
Enable HTF Filter: ON
HTF Timeframe: D

═══ Signal Filter ═══
Show Weak Signals: ON
Show Only Golden Zones: OFF
Max Order Blocks: 20
```

---

## 트레이딩 가이드

### 진입 체크리스트

**Long 진입 조건:**

- [ ] Trend: ▲/▲ (녹색) - 정렬됨
- [ ] In Zone: 🟢 Golden D
- [ ] Trigger: ◆/▲/● 중 하나 발생
- [ ] Signal: ◆/▲/● LONG 표시
- [ ] RR: 최소 2:1 이상

**Short 진입 조건:**

- [ ] Trend: ▼/▼ (녹색) - 정렬됨
- [ ] In Zone: 🔴 Golden S
- [ ] Trigger: ◆/▲/● 중 하나 발생
- [ ] Signal: ◆/▲/● SHORT 표시
- [ ] RR: 최소 2:1 이상

### 손절/익절 가이드

| 포지션 | 손절 | 익절 |
|--------|------|------|
| Long | Golden Zone 하단 아래 | RR 2:1 이상 지점 |
| Short | Golden Zone 상단 위 | RR 2:1 이상 지점 |

### Risk에 따른 사이즈 조절

| Risk 상태 | 권장 사이즈 |
|-----------|-------------|
| Clean | 100% (풀 사이즈) |
| ⚠️ Opposing | 50% (반 사이즈) |

### 분할 익절 전략

```
1차 익절 (50%): RR 1:1 지점
   → 손절을 본절로 이동

2차 익절 (50%): RR 2:1 지점
   → 전체 포지션 청산
```

### 피해야 할 상황

| 상황 | 이유 |
|------|------|
| Trend 불일치 (주황색) | 트렌드 충돌로 변동성 증가 |
| In Zone: — | 존 밖, 자리 아님 |
| Trigger: 대기중 | 확인 없이 진입 = 도박 |
| RR < 2:1 | 기대값 불리 |
| ● DOJI만 발생 | 신호 약함 |

### 시그널 강도별 전략

| 시그널 | 전략 |
|--------|------|
| ◆ (강) | 풀 사이즈, 적극적 진입 |
| ▲ (중) | 적정 사이즈, 일반 진입 |
| ● (약) | 반 사이즈 또는 패스 |

---

## Zone 상태 설명

### Zone 라벨 해석

| 라벨 | 의미 |
|------|------|
| D | Demand Zone (매수 영역) |
| S | Supply Zone (매도 영역) |
| D•CH | Demand + CHOCH (추세 전환) |
| S•CH | Supply + CHOCH (추세 전환) |
| D ★ | Golden Demand Zone |
| S ★ | Golden Supply Zone |
| D ✗ | Mitigated Demand (무효화) |
| S ✗ | Mitigated Supply (무효화) |

### Zone 테두리 스타일

| 스타일 | 의미 |
|--------|------|
| 🟡 금색 실선 (2px) | Golden Zone - 진입 대상 |
| ⚫ 회색 실선 (1px) | 일반 Zone |
| ⚫ 회색 점선 (1px) | Mitigated Zone (무효화) |

### Mitigation (무효화)

| Zone 종류 | 무효화 조건 |
|-----------|-------------|
| Demand | 종가가 Zone 하단 아래로 마감 |
| Supply | 종가가 Zone 상단 위로 마감 |

무효화된 존은 더 이상 유효하지 않으며, 설정에 따라 숨기거나 흐리게 표시됩니다.

---

## 버전 히스토리

### v1.3 (Current)

- ✅ Table Size 옵션 추가 (tiny/small/normal)
- ✅ Show Mitigated Zones 옵션 추가
- ✅ 설정 그룹 정리

### v1.2

- ✅ Shape로 트리거 강도 표시 (◆▲●)
- ✅ 라벨 제거로 차트 깔끔하게
- ✅ Mitigated Zone 삭제 대신 유지
- ✅ Show Weak Signals 옵션 추가

### v1.1

- ✅ 매 캔들마다 골든존 상태 업데이트
- ✅ 피보나치와 동기화된 존 스타일링
- ✅ 정확한 골든존 표시

### v1.0

- ✅ Supply and Demand Zone 탐지
- ✅ Golden Zone 필터
- ✅ GO/WAIT 이진 시스템
- ✅ IBFB 트리거 추가
- ✅ Opposing Zone 리스크 평가

---

## FAQ

### Q: 시그널이 발생하지 않아요

**A:** 다음을 확인하세요:
1. **In Zone**이 "🟢 Golden D" 또는 "🔴 Golden S"인지
2. **Trigger**가 "대기중"이 아닌지
3. 쿨다운 기간이 지났는지 (이전 시그널 후 N봉)

### Q: 골든존이 자꾸 바뀌어요

**A:** 정상입니다. v1.3은 **실시간 재판정** 기능이 있어서:
- 새로운 BOS/CHOCH 발생 → 피보나치 업데이트
- 피보나치 변경 → 골든존 상태 재계산
- 항상 현재 시점에서 유효한 골든존만 강조

### Q: Mitigated 존이 너무 많아요

**A:** 다음 설정을 조정하세요:
1. `Show Mitigated Zones: OFF` (기본값)
2. `Max Order Blocks` 값 줄이기

### Q: 어떤 트리거가 가장 좋나요?

**A:** 강도 순서:
1. **◆ IBFB** - 가장 신뢰도 높음, 적극 진입
2. **▲ PIN/ENG** - 좋음, 일반 진입
3. **● DOJI** - 약함, 신중하게 또는 패스

### Q: HTF 필터를 꺼도 되나요?

**A:** 가능하지만 권장하지 않습니다.
- HTF 필터 ON: 트렌드 정렬된 고품질 시그널만
- HTF 필터 OFF: 더 많은 시그널, 하지만 품질 저하

### Q: RR은 어떻게 계산하나요?

**A:**
```
RR = 리워드 ÷ 리스크

리스크 = |진입가 - 손절가|
리워드 = |진입가 - 익절가|

예시:
진입: 1.740
손절: 1.781 → 리스크 = 0.041
익절: 1.658 → 리워드 = 0.082
RR = 0.082 ÷ 0.041 = 2:1 ✅
```

---

## 알림 (Alerts)

### 사용 가능한 알림 조건

| 알림 | 조건 |
|------|------|
| ◆ GO Long (IBFB) | Golden Demand + IBFB 트리거 |
| ▲ GO Long (PIN/ENG) | Golden Demand + PIN/ENG 트리거 |
| ◆ GO Short (IBFB) | Golden Supply + IBFB 트리거 |
| ▲ GO Short (PIN/ENG) | Golden Supply + PIN/ENG 트리거 |
| ⏳ WAIT Long | Golden Demand 진입, 트리거 대기 |
| ⏳ WAIT Short | Golden Supply 진입, 트리거 대기 |

### 알림 설정 방법

1. TradingView 알림 패널 열기
2. 조건: S&D Golden Zone Clean v1.3 선택
3. 원하는 알림 조건 선택
4. 알림 방식 설정 (앱, 이메일, 웹훅 등)

---

## 요약

### 핵심 철학

```
자리 (Golden Zone) + 트리거 (◆▲●) = 진입
```

### 빠른 체크리스트

진입 전 확인:

- [ ] Trend 녹색 (정렬됨)
- [ ] In Zone = Golden D/S
- [ ] Trigger ≠ 대기중
- [ ] Signal = ◆/▲/● LONG/SHORT
- [ ] RR ≥ 2:1

**모두 ✅ → 진입!**

---

*Last Updated: 2025-01-13*
*Version: 1.3*
