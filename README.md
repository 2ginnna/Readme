# SAGE Protocol  
### Verifiable Agent-to-Agent Social Protocol on Avalanche

---

## 1. Project Definition

SAGE Protocol은 단순한 소개팅 앱이 아닙니다.

이 프로젝트는 다음을 구현합니다:

> AI가 인간을 대신해 협상하고,  
> 그 합의 과정을 온체인에 기록하는  
> Verifiable Agent-to-Agent Social Protocol

데이트는 첫 번째 유스케이스일 뿐입니다.

이 프로토콜은 다음 영역으로 확장 가능합니다:

- Recruiting (채용)
- Co-founder Matching (공동 창업자 탐색)
- Business Partner Discovery
- High-trust Social Coordination

핵심 개념은 다음입니다:

AI가 나를 대신해 상대방을 검증하고  
그 검증 기록이 온체인에 남는다.

---

## 2. System Architecture

### Layer 1 — User & Private Layer

역할:
- 사용자 민감 데이터 처리
- 개인 AI 학습
- Persona State 생성

기술:
- Vector DB (Pinecone / Milvus)
- LLM (Local or API)
- Client-side encryption

동작:

사용자와 AI의 대화는 오프체인에서 처리됩니다.

AI는 대화를 요약하여 "Persona State"를 생성합니다.

온체인에는 원본 데이터가 아닌,
요약 상태의 해시(Hash) 또는 암호화된 상태만 기록됩니다.

목적:
- 데이터 무결성 증명
- 프라이버시 보호

---

### Layer 2 — Negotiation Subnet (Custom Avalanche L1)

역할:
- AI Agent 간 고빈도 협상 처리
- 협상 로그 기록
- Gas-less 환경 구성

기술:
- Avalanche Subnet (Custom EVM)
- Custom Gas Policy (0 Gas or Custom Gas Token)

왜 Subnet인가:

AI 협상은 수십~수백 개의 트랜잭션을 발생시킵니다.

이를 C-Chain에서 처리하면 가스비가 비효율적입니다.

SAGE는 전용 L1을 구축하여:

- 고빈도 트랜잭션 처리
- 비용 최소화
- App-specific blockspace 확보

이것이 Avalanche 선택의 핵심 근거입니다.

---

### Layer 3 — Settlement Layer (Avalanche C-Chain)

역할:
- 최종 매칭 결과 자산화
- NFT 발행
- Staking / Escrow 실행

기술:
- Avalanche C-Chain
- Teleporter (AWM 기반 메시징)
- ERC-721 / ERC-1155

---

## 3. Detailed Data Flow

### Step 1 — Persona Commit

1. 사용자가 AI와 대화
2. AI가 Persona State 생성
3. Persona Hash를 Subnet에 기록

목적:
- 프라이버시 유지
- 상태 무결성 보장

---

### Step 2 — On-Chain Agent Negotiation

1. Agent A와 Agent B가 스마트 컨트랙트 내에서 대화
2. 가치관 정렬도 계산
3. 리스크 분석
4. Compatibility Score 산출

모든 협상 로그는 Subnet에 기록됩니다.

이 로그는 추후 "왜 매칭되었는가?"에 대한 검증 근거가 됩니다.

---

### Step 3 — Teleporter State Transition

AI들이 합의에 도달하면:

Negotiation Subnet → Teleporter → C-Chain

"Match Confirmed" 메시지가 전송됩니다.

Teleporter는 단순 자산 이동이 아니라

협상 데이터에서 자산화된 관계로의 상태 전이를 담당합니다.

---

### Step 4 — Relationship NFT Minting

C-Chain에서:

- Relationship NFT 발행
- 조건부 메타데이터 포함
- Staking 조건 명시

예:

- 3일간 대화 유지 시 보증금 반환
- 조건 미달성 시 Slashing

관계의 진정성을 코드로 집행합니다.

---

## 4. Crypto-Native Economic Model (Trust-Fi)

### 1. Proof of Sincerity — Staking

매칭 요청 시 AVAX를 예치합니다.

스마트 컨트랙트 규칙:

성공:
- 일정 기간 대화 유지 → 100% 반환 + 보상 토큰

실패:
- Ghosting / 비매너 → Slashing

효과:
- 가벼운 매칭 방지
- 진지한 참여 유도

---

### 2. Agent Upgrade Economy (NFT 기반)

에이전트 기능 확장은 NFT 장착 형태로 구현됩니다.

예:

- Multi-Thread Core NFT → 동시 협상 5명
- Deep Scan Lens NFT → 분석 정확도 상승

유저는 비용을 소비하는 것이 아니라  
에이전트를 업그레이드하는 자산을 보유합니다.

---

### 3. Lounge Signal Economy

- Megaphone NFT → 라운지 상단 노출
- Direct Intervene Ticket → AI 협상 중 인간 개입

수익 모델:
- NFT 판매
- 2차 거래 수수료
- Slashing 수익
- Staking Yield

---

## 5. Why On-Chain

1. Algorithm Transparency  
   AI 판단 근거가 온체인에 기록됩니다.

2.
