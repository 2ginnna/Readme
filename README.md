# Read Me  
### Verifiable Agent-to-Agent Social Protocol on Avalanche

---

## 1. Project Definition

Read Me는 단순한 소개팅 앱이 아닙니다.

이 프로젝트는 다음을 구현합니다:

AI가 인간을 대신해 협상하고  
그 합의 과정을 온체인에 기록하는  
Verifiable Agent-to-Agent Social Protocol

데이트는 첫 번째 유스케이스일 뿐입니다.

이 프로토콜은 다음 영역으로 확장 가능합니다:

- Recruiting
- Co-founder Matching
- Business Partner Discovery
- High-trust Social Coordination

핵심은 다음입니다:

AI가 나를 대신해 상대방을 검증하고  
그 검증 기록이 온체인에 남는다.

Swipe가 아니라 Consensus입니다.

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

사용자는 자신의 AI 에이전트와 대화합니다.

AI는 대화를 분석하여 Persona State(성향 요약본)를 생성합니다.

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

AI 협상은 한 번의 매칭에도 수십~수백 개의 트랜잭션을 발생시킵니다.

이를 C-Chain에서 처리하면 가스비가 비효율적입니다.

Read Me는 전용 L1을 구축하여:

- 고빈도 트랜잭션 처리
- 비용 최소화
- App-specific Blockspace 확보

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

프라이버시를 유지하면서도 상태 무결성을 증명합니다.

---

### Step 2 — On-Chain Agent Negotiation

1. Agent A와 Agent B가 스마트 컨트랙트 내에서 협상 시작
2. 가치관 정렬도 계산
3. 리스크 분석
4. Compatibility Score 산출

모든 협상 로그는 Subnet에 기록됩니다.

이는 사후 검증이 가능한 구조입니다.

---

### Step 3 — Teleporter State Transition

AI들이 합의에 도달하면:

Negotiation Subnet  
→ Teleporter  
→ C-Chain

협상 결과가 메인 체인으로 전달됩니다.

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
- 일정 기간 대화 유지 → 보증금 반환 + 토큰 보상

실패:
- Ghosting / 비매너 → Slashing

가벼운 참여는 비용을 지불하게 됩니다.
진지한 참여는 보상을 받습니다.

---

### 2. Agent Upgrade Economy (NFT 기반)

에이전트 기능 확장은 NFT 장착 형태로 구현됩니다.

예:

- Multi-Thread Core NFT → 동시 협상 5명
- Deep Scan Lens NFT → 분석 정확도 상승

유저는 기능을 소비하는 것이 아니라  
에이전트를 자산화합니다.

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

2. Proof of Sincerity  
   Staking은 스마트 컨트랙트로 자동 집행됩니다.

3. Data Sovereignty  
   원본 데이터는 오프체인에 보관하고,
   검증 가능한 상태만 온체인에 기록합니다.

4. Composability  
   온체인 에이전트는 다른 Avalanche 기반 앱에서도 활동 가능합니다.

---

## 6. Why Avalanche

### 1. App-Specific L1 (Subnet)

- 고빈도 AI 협상 처리
- Gas-less UX 구현
- 독립적 블록스페이스 확보

### 2. ACP-77 기반 유연한 체인 운영

- 낮아진 검증자 진입 장벽
- 스타트업 친화적 구조

### 3. Teleporter 기반 상태 전이

- 협상 → 자산화의 즉각적 연결
- 브릿지 없이 체인 간 메시지 전송

### 4. Sub-second Finality

- 1초 미만 확정성
- 실시간 AI 협상 UX 구현 가능

---

## 7. MVP Demo Focus

데모는 다음 3장면에 집중합니다:

1. Agent Setup  
   Persona Minted on Subnet

2. Agent Negotiation  
   실시간 협상 로그 시각화

3. Teleport & Mint  
   Relationship NFT가 C-Chain에서 민팅되는 장면

---

## 8. Vision

Read Me는 앱이 아닙니다.

우리는 수백만 개의 AI 에이전트가  
동시에 협상하고 신뢰를 구축하는

Mass-Scale Consensus Network를 구축합니다.

Swipe를 제거합니다.  
Consensus로 연결합니다.
